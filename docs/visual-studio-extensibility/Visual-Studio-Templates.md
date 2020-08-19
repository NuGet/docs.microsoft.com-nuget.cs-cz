---
title: Balíčky NuGet v šablonách sady Visual Studio
description: Pokyny, jak zahrnout balíčky NuGet jako součást šablon projektů a položek sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 2dfbd793eee05169f051d9c8943bc065945b92da
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622639"
---
# <a name="packages-in-visual-studio-templates"></a>Balíčky v šablonách sady Visual Studio

Šablony projektů a položek sady Visual Studio často potřebují zajistit, aby při vytvoření projektu nebo položky byly nainstalovány určité balíčky. Například šablona ASP.NET MVC 3 nainstaluje jQuery, modernizr a další balíčky.

Pro podporu tohoto nástroje můžou autoři šablon dát pokyn NuGet k instalaci potřebných balíčků místo jednotlivých knihoven. Vývojáři pak tyto balíčky můžou později snadno aktualizovat.

Další informace o vytváření vlastních šablon najdete v tématu [Postupy: vytváření šablon projektů](/visualstudio/ide/how-to-create-project-templates) nebo [vytváření vlastních šablon projektů a položek](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Zbývající část této části popisuje konkrétní kroky, které je potřeba provést při vytváření šablony pro správné zahrnutí balíčků NuGet.

- [Přidání balíčků do šablony](#adding-packages-to-a-template)
- [Osvědčené postupy](#best-practices)

Příklad najdete v [ukázce NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Přidání balíčků do šablony

Při vytvoření instance šablony se vyvolá [Průvodce šablonou](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) , který načte seznam balíčků k instalaci společně s informacemi o tom, kde tyto balíčky najít. Balíčky mohou být vloženy do VSIX, vloženy do šablony nebo umístěny na místním pevném disku. v takovém případě použijete klíč registru pro odkazování na cestu k souboru. Podrobnosti o těchto umístěních jsou uvedené dále v této části.

Předinstalované balíčky fungují pomocí [průvodců šablonou](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Speciální průvodce, který se vyvolá při vytváření instance šablony. Průvodce načte seznam balíčků, které je potřeba nainstalovat, a předá tyto informace do příslušných rozhraní API NuGet.

Postup zahrnutí balíčků do šablony:

1. Do `vstemplate` souboru přidejte odkaz na Průvodce šablonou NuGet přidáním [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) elementu:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` je sestavení, které obsahuje pouze `TemplateWizard` třídu, což je jednoduchá obálka, která volá do samotné implementace v `NuGet.VisualStudio.dll` . Verze sestavení se nikdy nezmění, aby šablony projektů a položek pokračovaly v práci s novými verzemi NuGet.

1. Přidat seznam balíčků k instalaci v projektu:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Průvodce podporuje více `<package>` prvků pro podporu více zdrojů balíčků. `id` `version` Atributy i jsou povinné, což znamená, že se nainstaluje konkrétní verze balíčku i v případě, že je k dispozici novější verze. Tím zabráníte tomu, aby se aktualizace balíčků přerušujíy v šabloně, takže se možnost aktualizace balíčku aktualizuje na vývojáře pomocí šablony.

1. Zadejte úložiště, ve kterém může NuGet najít balíčky, jak je popsáno v následujících částech.

### <a name="vsix-package-repository"></a>Úložiště balíčků VSIX

Doporučený přístup k nasazení šablon projektů a položek sady Visual Studio je [rozšíření VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) , protože umožňuje zabalit více šablon projektů a položek dohromady a umožňuje vývojářům snadno vyhledat šablony pomocí Správce rozšíření vs nebo galerie sady Visual Studio. Aktualizace rozšíření je také snadné nasadit pomocí [mechanismu automatických aktualizací správce rozšíření sady Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

Samotný VSIX může sloužit jako zdroj pro balíčky, které šablona vyžaduje:

1. Upravte `<packages>` prvek v souboru následujícím `.vstemplate` způsobem:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository`Atribut určuje typ úložiště, jako by `extension` byl ale `repositoryId` jedinečný identifikátor samotného VSIX (Jedná se o hodnotu `ID` atributu v `vsixmanifest` souboru rozšíření, viz [Referenční dokumentace schématu rozšíření VSIX 2,0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Umístěte `nupkg` soubory do složky pojmenované v `Packages` rámci VSIX.

1. Přidejte potřebné soubory balíčku jako `<Asset>` v `vsixmanifest` souboru (viz Referenční dokumentace [schématu rozšíření VSIX 2,0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Všimněte si, že můžete doručovat balíčky na stejném VSIX jako šablony projektu nebo je můžete umístit do samostatného souboru VSIX, pokud to pro váš scénář bude smysluplnější. Ale neodkazujte na žádný VSIX, přes který nemáte kontrolu, protože změny tohoto rozšíření by mohly přerušit vaši šablonu.

### <a name="template-package-repository"></a>Úložiště balíčků šablon

Pokud distribuujete pouze jednu šablonu projektu nebo položky a nepotřebujete zabalit více šablon dohromady, můžete použít jednodušší, ale omezený přístup, který obsahuje balíčky přímo v souboru ZIP šablony projektu nebo položky:

1. Upravte `<packages>` prvek v souboru následujícím `.vstemplate` způsobem:

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    `repository`Atribut má hodnotu `template` a `repositoryId` atribut není požadován.

1. Umístěte balíčky do kořenové složky souboru ZIP šablony projektu nebo položky.

Všimněte si, že použití tohoto přístupu v souboru VSIX, který obsahuje více šablon, vede k zbytečným dispozici determinističtějšíům, pokud je jeden nebo více balíčků běžné pro šablony. V takových případech použijte [VSIX jako úložiště](#vsix-package-repository) , jak je popsáno v předchozí části.

### <a name="registry-specified-folder-path"></a>Cesta ke složce zadané v registru

Sady SDK, které jsou nainstalované pomocí MSI, můžou instalovat balíčky NuGet přímo v počítači vývojáře. Díky tomu jsou okamžitě k dispozici při použití šablony projektu nebo položky, nikoli při jejich extrakci během této doby. Tento přístup používají šablony ASP.NET.

1. Instalační balíčky MSI nainstalujte do počítače. Můžete instalovat pouze `.nupkg` soubory, nebo je můžete nainstalovat spolu s rozbaleným obsahem, který při použití šablony uloží další krok. V takovém případě postupujte podle standardní struktury složek NuGet `.nupkg` , kde jsou soubory v kořenové složce, a pak každý balíček má jako název podsložky podsložku s identifikátorem ID/verze.

1. Zadejte klíč registru pro identifikaci umístění balíčku:

    - Umístění klíče: buď na úrovni počítače `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` , nebo pokud je to pro jednotlivé uživatele nainstalované šablony a balíčky, případně použít `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Název klíče: použijte název, který je pro vás jedinečný. Například šablony ASP.NET MVC 4 pro VS 2012 use `AspNetMvc4VS11` .
    - Hodnoty: úplná cesta ke složce Packages.

1. V `<packages>` elementu v `.vstemplate` souboru přidejte atribut `repository="registry"` a v atributu zadejte název klíče registru `keyName` .

    - Pokud máte předběžné rozbalení balíčků, použijte `isPreunzipped="true"` atribut.
    - *(NuGet 3.2 +)* Pokud chcete vynutit sestavení během návrhu na konci instalace balíčku, přidejte `forceDesignTimeBuild="true"` atribut.
    - Jako optimalizaci přidejte, `skipAssemblyReferences="true"` protože již vlastní šablona obsahuje nezbytné odkazy.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Osvědčené postupy

1. Deklarace závislosti na VSIX NuGet přidáním odkazu do manifestu VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Vyžadovat, aby byly šablony projektů a položek uloženy při vytváření, včetně [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) v `.vstemplate` souboru.

1. Šablony neobsahují soubor a neobsahují `packages.config` ani žádné odkazy nebo obsah, které by se přidaly při instalaci balíčků NuGet.
