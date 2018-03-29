---
title: Balíčky NuGet ve šablony sady Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/03/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Pokyny včetně balíčků NuGet v rámci šablon projektů a položek v sadě Visual Studio.
keywords: NuGet v sadě Visual Studio, šablony projektů Visual Studio, položka šablony sady Visual Studio, balíčky v projektu šablony, balíčky v šablonách položek
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 8c1751ba9caf5e71ace7a81575e4e5448b1e4185
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="packages-in-visual-studio-templates"></a>Balíčky v šablony sady Visual Studio

Projektů a položek šablony sady Visual Studio se často potřebují k zajištění, že některé balíčky byly nainstalovány při vytváření projektu nebo položky. Například šablony ASP.NET MVC 3 nainstaluje jQuery, Modernizr a dalších balíčků.

Za tímto účelem šablony autorům určit, aby NuGet k instalaci potřebné balíčky, nikoli jednotlivých knihoven. Vývojáři tedy můžete snadno aktualizovat tyto balíčky kdykoli později.

Další informace o vytváření šablon sami, najdete v tématu [postupy: vytvoření šablony projektů](/visualstudio/ide/how-to-create-project-templates) nebo [vytváření vlastních projektů a šablon položek](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Zbývající část Tato část popisuje konkrétní kroky pro zajištění správně zahrnout balíčků NuGet při vytváření šablony.

- [Přidávání balíčků do šablony](#adding-packages-to-a-template)
- [Doporučené postupy](#best-practices)

Příklad, naleznete v části [NuGetInVsTemplates ukázka](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Přidávání balíčků do šablony

Při vytváření instance šablony [Průvodce šablonou](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) je vyvolána k načíst seznam balíčků, které mají nainstalovat společně s informacemi o tom, kde najít tyto balíčky. Balíčky mohou být vložených ve VSIX, vložené v šabloně nebo umístěné na místním pevném disku v takovém případě pomocí klíče registru tak, aby odkazovaly cesta k souboru. Podrobnosti o těchto umístění jsou uvedeny později v této části.

Předinstalované balíčky pomocí fungovalo [průvodců pro šablony](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Speciální Průvodce volán získá vytvoření instance šablony. Průvodce načte seznam balíčků, které je potřeba nainstalovat a předá tyto informace k rozhraním API odpovídající NuGet.

Postup do šablony zahrnout balíčky:

1. Ve vaší `vstemplate` soubor, přidejte odkaz na Průvodce šablonou NuGet přidáním [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` je sestavení obsahující pouze `TemplateWizard` třídy, která představuje jednoduchý obálku, který volá do skutečné implementace v `NuGet.VisualStudio.dll`. Verze sestavení se nikdy změnit tak, aby šablon projektu nebo položek pokračovat v práci s novými verzemi nástroje NuGet.

1. Přidáte seznam balíčků pro instalaci v projektu:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Průvodce podporuje více `<package>` elementy pro podporu více zdrojů balíčků. Jak `id` a `version` atributy jsou požadovány, což znamená, že konkrétní verze balíčku se nainstalují i v případě, že je k dispozici novější verze. Aktualizace balíčků zabrání nejnovější šablony, a rozhodnout pro daný balíček aktualizovat vývojáře pomocí šablony.

1. Zadejte úložiště NuGet kde najdete balíčky, jak je popsáno v následujících částech.

### <a name="vsix-package-repository"></a>Úložiště balíčku VSIX

Doporučené nasazení přístup pro šablony sady Visual Studio nebo položka projektu je [VSIX rozšíření](/visualstudio/extensibility/shipping-visual-studio-extensions) protože umožňuje sbalit několik šablon projektu/položky společně a umožňuje vývojářům snadno zjistit vaše šablony pomocí Správce rozšíření VS nebo Galerii Visual Studia. Aktualizace pro rozšíření jsou také snadno nasadit pomocí [mechanizmus automatických aktualizací Visual Studio rozšíření Manager](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

VSIX samotné může sloužit jako zdroj pro balíčky vyžadované šablonou:

1. Změnit `<packages>` element v `.vstemplate` následujícím způsobem:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` Atribut určuje typ úložiště jako `extension` při `repositoryId` je jedinečný identifikátor VSIX samotné (to je hodnota `ID` atribut v rozšíření `vsixmanifest` souborů najdete v tématu [ Referenční dokumentace schématu 2.0 rozšíření VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Místní vaše `nupkg` soubory ve složce nazývají `Packages` ve VSIX.

1. Přidat soubory potřebný balíček jako `<Asset>` ve vaší `vsixmanifest` souboru (v tématu [VSIX rozšíření schéma 2.0 – referenční informace](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Poznámka: abyste mohli zajistit balíčků ve stejné VSIX jako šablony projektu nebo můžete je umístit do samostatné VSIX to další pro váš scénář. Neodkazujte však žádné VSIX, přes který nemáte ovládací prvek, protože změny tohoto rozšíření by mohlo způsobit narušení vaší šablony.

### <a name="template-package-repository"></a>Úložiště balíčků šablony

Pokud je distribuován pouze jednu projektu nebo položku šablonu a nemusíte balíček několik šablon společně, můžete použít jednodušší, i když omezenější přístup, který obsahuje balíčky přímo v souboru ZIP šablony projektu/položky:

1. Změnit `<packages>` element v `.vstemplate` následujícím způsobem:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` Atribut má hodnotu `template` a `repositoryId` atribut se nevyžaduje.

1. Umístěte balíčky v kořenové složce soubor ZIP šablony projektu/položky.

Všimněte si, že použití tohoto přístupu v VSIX, který obsahuje několik šablon vede k tomu nepotřebné když jeden nebo více balíčků, které jsou společné pro šablony. V takových případech použít [VSIX jako úložiště](#vsix-package-repository) jak je popsáno v předchozí části.

### <a name="registry-specified-folder-path"></a>Cesta ke složce zadat registru

Sady SDK, které se instalují pomocí souboru MSI mohou instalovat balíčky NuGet přímo na počítači pro vývojáře. Tato díky je k dispozici při šablonu projektu nebo položky se používá, namísto nutnosti extrahovat je během této doby. Tuto metodu použijte šablony ASP.NET.

1. Máte MSI instalovat balíčky do počítače. Můžete nainstalovat pouze `.nupkg` soubory, nebo můžete nainstalovat těch, které společně s rozšířené obsah, který uloží na další krok, pokud šablony. V takovém případě postupujte podle NuGet standardní struktuře složek ve kterém `.nupkg` jsou soubory v kořenové složce a potom každý balíček obsahuje podsložky dvojice id a verzi jako název podsložky.

1. Zapsat klíč registru pro určení umístění balíčku:

    - Klíč umístění: buď úrovni celého `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` nebo pokud je nainstalována na uživatele šablony a balíčky, případně použít. `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Název klíče: použijte název, který je jedinečný pro vás. Například šablony ASP.NET MVC 4 pro sadu VS 2012 použití `AspNetMvc4VS11`.
    - Hodnoty: úplná cesta ke složce balíčků.

1. V `<packages>` element v `.vstemplate` soubor, přidejte atribut `repository="registry"` a zadejte název klíče v registru `keyName` atribut.

    - Pokud máte předem unzipped vlastních balíčků, použijte `isPreunzipped="true"` atribut.
    - *(NuGet 3.2 +)*  Pokud chcete vynutit sestavení návrhu na konci instalace balíčku, přidejte `forceDesignTimeBuild="true"` atribut.
    - Jako optimalizace, přidejte `skipAssemblyReferences="true"` protože samotné šablony již obsahuje odkazy na nezbytné.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Doporučené postupy

1. Závislost na NuGet VSIX deklarujte přidáním odkazu k němu v manifestu VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Vyžadovat šablon projektu nebo položek uložit na vytváření zahrnutím [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) v `.vstemplate` souboru.

1. Šablony neobsahují `packages.config` souboru a nezahrnují nebo žádné odkazy nebo obsah, který by byl přidán, když se instalují balíčky NuGet.
