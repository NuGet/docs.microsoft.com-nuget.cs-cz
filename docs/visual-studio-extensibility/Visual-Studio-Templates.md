---
title: Balíčky NuGet v šablonách sady Visual Studio
description: Pokyny pro zahrnutí balíčků NuGet jako součást projektu Visual Studio a šablony položek.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498236"
---
# <a name="packages-in-visual-studio-templates"></a>Balíčky v šablonách Sady Visual Studio

Šablony projektů a položek sady Visual Studio často potřebují zajistit, aby byly při vytvoření projektu nebo položky nainstalovány určité balíčky. Například šablona ASP.NET MVC 3 nainstaluje jQuery, Modernizr a další balíčky.

Chcete-li to podporovat, autoři šablony můžete pokyn NuGet nainstalovat potřebné balíčky, nikoli jednotlivé knihovny. Vývojáři pak mohou tyto balíčky kdykoli později snadno aktualizovat.

Další informace o vytváření šablon naleznete v článku [Postup: Vytvoření šablon projektů](/visualstudio/ide/how-to-create-project-templates) nebo [Vytvoření vlastních šablon projektů a položek](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Zbývající část této části popisuje konkrétní kroky, které je třeba provést při vytváření šablony správně zahrnout balíčky NuGet.

- [Přidání balíčků do šablony](#adding-packages-to-a-template)
- [Osvědčené postupy](#best-practices)

Příklad naleznete v [nugetinvstemplates ukázka](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Přidání balíčků do šablony

Při vytvoření instance šablony je vyvolán [průvodce šablonou](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) k načtení seznamu balíčků k instalaci spolu s informacemi o tom, kde tyto balíčky najít. Balíčky mohou být vloženy do vsix, vložené do šablony nebo umístěny na místním pevném disku, v takovém případě použijete klíč registru k odkazování na cestu k souboru. Podrobnosti o těchto místech jsou uvedeny dále v této části.

Předinstalované balíčky fungují pomocí [průvodců šablonami](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Zvláštní průvodce získá vyvolána při vytvoření instance šablony. Průvodce načte seznam balíčků, které je třeba nainstalovat, a předá tyto informace příslušným rozhraním API NuGet.

Postup zahrnutí balíčků do šablony:

1. Do `vstemplate` souboru přidejte odkaz na Průvodce šablonou [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) NuGet přidáním prvku:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll`je sestavení, které `TemplateWizard` obsahuje pouze třídu, což je jednoduchý obálka, která volá do skutečné implementace v aplikaci `NuGet.VisualStudio.dll`. Verze sestavení se nikdy nezmění tak, aby šablony projektu nebo položky nadále pracovat s novými verzemi NuGet.

1. Přidejte seznam balíčků, které chcete nainstalovat do projektu:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Průvodce podporuje `<package>` více prvků pro podporu více zdrojů balíčků. Atributy `id` `version` a jsou povinné, což znamená, že konkrétní verze balíčku bude nainstalována i v případě, že je k dispozici novější verze. Tím zabráníte aktualizace balíčku z porušení šablony, takže možnost aktualizovat balíček pro vývojáře pomocí šablony.

1. Zadejte úložiště, kde NuGet můžete najít balíčky, jak je popsáno v následujících částech.

### <a name="vsix-package-repository"></a>Úložiště balíčků VSIX

Doporučený přístup nasazení pro šablony projektu a položek sady Visual Studio je [rozšíření VSIX,](/visualstudio/extensibility/shipping-visual-studio-extensions) protože umožňuje sbalit více šablon projektu nebo položek dohromady a umožňuje vývojářům snadno zjistit šablony pomocí Správce rozšíření VS nebo Galerie Visual Studio. Aktualizace rozšíření se také snadno nasazují pomocí [mechanismu automatické aktualizace Správce rozšíření sady Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

VSIX sám může sloužit jako zdroj pro balíčky vyžadované šablonou:

1. Upravte `<packages>` prvek `.vstemplate` v souboru takto:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    Atribut `repository` určuje typ úložiště, protože `extension` `repositoryId` zatímco je jedinečný identifikátor VSIX sám (Toto `ID` je hodnota atributu v `vsixmanifest` souboru rozšíření, viz [VSIX Rozšíření Schéma 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Umístěte `nupkg` soubory do složky volané `Packages` v rámci VSIX.

1. Přidejte potřebné soubory `<Asset>` balíčků `vsixmanifest` jako do souboru (viz [Odkaz na rozšíření VSIX 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Všimněte si, že můžete doručit balíčky ve stejném VSIX jako šablony projektu nebo je můžete umístit do samostatného VSIX, pokud to dává větší smysl pro váš scénář. Však neodkazují žádné VSIX, nad kterými nemáte kontrolu, protože změny tohoto rozšíření může přerušit šablonu.

### <a name="template-package-repository"></a>Úložiště balíčků šablon

Pokud distribuujete pouze jednu šablonu projektu/položky a nepotřebujete sbalit více šablon dohromady, můžete použít jednodušší, ale omezenější přístup, který zahrnuje balíčky přímo v souboru ZIP šablony projektu/položky:

1. Upravte `<packages>` prvek `.vstemplate` v souboru takto:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    Atribut `repository` má hodnotu `template` `repositoryId` a atribut není vyžadován.

1. Umístěte balíčky do kořenové složky souboru ZIP šablony projektu/položky.

Všimněte si, že pomocí tohoto přístupu v VSIX, který obsahuje více šablon vede ke zbytečnému nafouknutí, když jeden nebo více balíčků jsou společné šablony. V takových případech použijte [VSIX jako úložiště,](#vsix-package-repository) jak je popsáno v předchozí části.

### <a name="registry-specified-folder-path"></a>Cesta ke složce zadané registrem

Sady SDK, které jsou nainstalovány pomocí MSI můžete nainstalovat balíčky NuGet přímo v počítači vývojáře. Díky tomu je okamžitě k dispozici při projektu nebo šablony položky, spíše než muset extrahovat během této doby. ASP.NET šablony používají tento přístup.

1. Mít msi instalační balíčky do počítače. Můžete nainstalovat pouze `.nupkg` soubory, nebo můžete nainstalovat ty spolu s rozbaleným obsahem, který šetří další krok při použití šablony. V tomto případě postupujte NuGet standardní strukturu `.nupkg` složek, kde jsou soubory v kořenové složce a pak každý balíček má podsložku s id/version pair jako název podsložky.

1. Napište klíč registru k identifikaci umístění balíčku:

    - Umístění klíče: Buď v `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` celém počítači, nebo pokud je to per-user nainstalovány šablony a balíčky, případně použít`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Název klíče: použijte název, který je pro vás jedinečný. Například ASP.NET šablony MVC 4 pro VS 2012 použití `AspNetMvc4VS11`.
    - Hodnoty: úplná cesta ke složce packages.

1. Do `<packages>` prvku v `.vstemplate` souboru přidejte atribut `repository="registry"` a zadejte `keyName` název klíče registru v atributu.

    - Pokud jste balíčky předem rozbalili, `isPreunzipped="true"` použijte atribut.
    - *(NuGet 3,2+)* Pokud chcete vynutit sestavení návrhu na konci instalace `forceDesignTimeBuild="true"` balíčku, přidejte atribut.
    - Jako optimalizaci `skipAssemblyReferences="true"` přidejte, protože samotná šablona již obsahuje potřebné odkazy.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Osvědčené postupy

1. Deklarovat závislost na NuGet VSIX přidáním odkazu na něj v manifestu VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Vyžadovat, aby byly šablony projektů/položek [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) uloženy `.vstemplate` při vytváření, zahrnutím do souboru.

1. Šablony neobsahují `packages.config` soubor a nezahrnují ani žádné odkazy nebo obsah, který by byl přidán při instalaci balíčků NuGet.
