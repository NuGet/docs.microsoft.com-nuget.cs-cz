---
title: Balíčky NuGet ve šablony sady Visual Studio
description: Pokyny, včetně balíčků NuGet jako součást šablony projektů a položek aplikace Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550507"
---
# <a name="packages-in-visual-studio-templates"></a>Balíčky v šablony sady Visual Studio

Šablony projektů a položek aplikace Visual Studio je často potřeba zajistit, že některé balíčky se nainstalují při vytvoření projektu nebo položky. Například šablony ASP.NET MVC 3 nainstalovat, jQuery, Modernizr a další balíčky.

Z toho důvodu autoři šablon můžete dát pokyn NuGet k instalaci potřebné balíčky, nikoli jednotlivých knihoven. Vývojáři tedy můžete snadno aktualizovat tyto balíčky kdykoli později.

Další informace o vytváření samotné šablony, najdete v tématu [postupy: vytváření šablon projektu](/visualstudio/ide/how-to-create-project-templates) nebo [vytváření vlastních šablon projektů a položek](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Zbytek tohoto oddílu popisuje zvláštní postup provést, když šablonu správně zahrnout balíčky NuGet.

- [Přidávají se balíčky do šablony](#adding-packages-to-a-template)
- [Osvědčené postupy](#best-practices)

Příklad najdete v tématu [NuGetInVsTemplates ukázka](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Přidávají se balíčky do šablony

Při vytváření instance šablony [Průvodce šablonou](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) se vyvolá k načtení seznamu balíčků, které mají nainstalovat společně s informacemi o tom, kde najít tyto balíčky. Balíčky může být vložen do VSIX, vložené v šabloně nebo umístěný na místní pevný disk v takovém případě odkazují na cestu k souboru pomocí klíče registru. Podrobnosti na tato místa jsou uvedeny dále v této části.

Předinstalované balíčky pracovat pomocí [průvodců pro šablony](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Speciální průvodce získá vyvolat získává vytvoření instance šablony. Průvodce načte seznam balíčků, které je potřeba nainstalovat a předá tyto informace do příslušné NuGet rozhraní API.

Postup do šablony zahrnout balíčky:

1. Ve vaší `vstemplate` přidejte odkaz na Průvodce šablonou NuGet tak, že přidáte [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` je sestavení, který obsahuje pouze `TemplateWizard` třídu, která představuje jednoduchou obálku, která volá aktuální implementaci v `NuGet.VisualStudio.dll`. Verze sestavení se nikdy nezmění tak, že šablony projektu/položky pokračovat v práci s novými verzemi nástroje NuGet.

1. Přidáte seznam balíčků pro instalaci v projektu:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Průvodce podporuje více `<package>` prvky pro podporu více zdroje balíčků. Jak `id` a `version` atributy jsou požadovány, což znamená, že konkrétní verzi balíčku se nainstaluje i v případě, že je k dispozici novější verze. Aktualizace balíčků zabrání dopadem na dřívější kód šablony byste museli opustit možnost Aktualizovat balíček pro vývojáře pomocí šablony.

1. Zadáním úložiště NuGet kde najdete balíčky, jak je popsáno v následujících částech.

### <a name="vsix-package-repository"></a>Úložiště balíčků VSIX

Doporučené nasazení přístup pro šablony sady Visual Studio projekt/položka je [rozšíření VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) protože umožňuje zabalit více šablon projektu/položky společně a umožňuje vývojářům snadné nalezení šablony Použití Správce rozšíření VS nebo Galerie sady Visual Studio. Aktualizace rozšíření jsou také snadno nasadit pomocí [mechanizmus automatických aktualizací Správce rozšíření pro Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

VSIX sám může sloužit jako zdroj pro balíčky vyžadované šablonou:

1. Upravit `<packages>` prvek `.vstemplate` to následujícím způsobem:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` Atribut určuje typ úložiště jako `extension` při `repositoryId` je jedinečný identifikátor souboru VSIX, samotný (jedná se o hodnotu z `ID` atribut do rozšíření `vsixmanifest` souborů naleznete v tématu [ VSIX Extension Schema 2.0 – referenční informace](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Místo vaše `nupkg` soubory ve složce volá `Packages` ve VSIX.

1. Přidání souborů potřebný balíček jako `<Asset>` ve vaší `vsixmanifest` souboru (naleznete v tématu [VSIX Extension Schema 2.0 referenční informace](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Všimněte si, že můžete doručujte balíčky do stejného VSIX jako projekt šablony nebo je můžete umístit do samostatného souboru VSIX a pokud se díky tomu větší smysl pro váš scénář. Neodkazovat však žádné VSIX nad tím, které nemají ovládací prvek, protože změny tohoto rozšíření může poškodit šablony.

### <a name="template-package-repository"></a>Úložiště balíčků šablony

Pokud je distribuován pouze jeden projekt/položka šablony a nemusíte balíček více šablon najednou, můžete použít jednodušší, ale více omezený přístup, který obsahuje balíčky přímo v souboru ZIP šablony projektu/položky:

1. Upravit `<packages>` prvek `.vstemplate` to následujícím způsobem:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` Atribut má hodnotu `template` a `repositoryId` atribut se nevyžaduje.

1. Umístěte balíčky v kořenové složce soubor ZIP šablony projektu/položky.

Všimněte si, že použití tohoto přístupu v rozšíření VSIX, který obsahuje více šablon vede ke zbytečné determinističtější když jeden nebo více balíčků, které jsou společné pro šablony. V takovém případě použijte [VSIX jako úložiště](#vsix-package-repository) jak je popsáno v předchozí části.

### <a name="registry-specified-folder-path"></a>Cesta ke složce zadat registru

Sady SDK, které se instalují pomocí MSI můžete nainstalovat balíčky NuGet přímo na počítači pro vývojáře. Toto usnadňuje je k dispozici při šablonu projektu nebo položky se používá, namísto nutnosti jejich extrakci během této doby. Šablony ASP.NET pomocí tohoto postupu.

1. Máte MSI nainstalujte balíčky do počítače. Můžete nainstalovat pouze `.nupkg` soubory, nebo můžete nainstalovat ty spolu s rozšířené obsah, který uloží na další krok při použití této šablony. V tomto případě mají následující strukturu složky standardní Nugetu ve které `.nupkg` jsou soubory v kořenové složce a potom každý balíček obsahuje podsložku s pár id a verzi jako název podsložky.

1. Zapsat klíč registru pro určení umístění balíčku:

    - Klíč umístění: buď celý počítač `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` nebo pokud je nainstalována na uživatele šablony a balíčky, případně použít. `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Název klíče: použijte název, který je jedinečný pro vás. Například šablony ASP.NET MVC 4 pro sadu VS 2012 použití `AspNetMvc4VS11`.
    - Hodnoty: úplná cesta ke složce balíčků.

1. V `<packages>` prvek `.vstemplate` přidejte atribut `repository="registry"` a zadejte název klíče registru v `keyName` atribut.

    - Pokud jste předem odblokujte balíčků, použijte `isPreunzipped="true"` atribut.
    - *(NuGet 3.2 +)*  Pokud chcete vynutit sestavení doby návrhu na konci instalace balíčku, přidejte `forceDesignTimeBuild="true"` atribut.
    - Optimalizace, přidejte `skipAssemblyReferences="true"` protože samotné šablony již obsahuje potřebné odkazy.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Doporučené postupy

1. Deklaruje závislost na NuGet VSIX tak, že přidáte na ni odkaz v manifestu VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Vyžadují šablony projektu/položky mají být uloženy vytváření zahrnutím [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) v `.vstemplate` souboru.

1. Šablony nejsou zahrnuté `packages.config` souborů a nezahrnuje nebo odkazy nebo obsah, který se přidá při instalaci balíčků NuGet.
