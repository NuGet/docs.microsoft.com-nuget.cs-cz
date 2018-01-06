---
title: "Úvodní příručka o vytváření a publikování balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "Návod kurz týkající se vytváření a publikování balíčku NuGet pomocí rozhraní příkazového řádku nuget.exe a Visual Studio."
keywords: "Vytvoření balíčku NuGet, publikování, balíček NuGet kurzu NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b33344c3b3dd782fc4668d2a1674b9501fadcc03
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="create-and-publish-a-package"></a>Vytvoření a publikování balíčku

Je jednoduchý proces vytvoření balíčku NuGet z knihovny tříd rozhraní .NET a publikujete ho v nuget.org. Následující kroky vás provedou procesem, pomocí rozhraní NuGet příkazového řádku (CLI) a Visual Studio:

- [Předpoklady](#install-pre-requisites)
- [Vytvoření souboru manifestu balíčku příponou .nuspec](#create-the-nuspec-package-manifest-file)
- [Spusťte příkaz pack](#run-the-pack-command)
- [Umožňuje publikovat balíček](#publish-the-package)

## <a name="pre-requisites"></a>Předpoklady

1. Nainstalujte všechny edice Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/).

1. Nainstalujte nástroj příkazového řádku NuGet `nuget.exe`, stáhněte nejnovější verzi `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads)a uložit `.exe` do umístění v CESTĚ. Všimněte si, že stahování *je* nástroj sám, není instalační program.

1. Vytvoření vhodného knihovna tříd rozhraní .NET projektu pro kód, který chcete balíček. Pokud ještě nemáte projektu, můžete vytvořit jednoduchý následujícím způsobem:
    1. V sadě Visual Studio, vyberte **soubor > Nový > projekt**, rozbalte **Visual C# > Windows** uzlu, vyberte šablonu "Knihovna tříd", název projektu AppLogger a klikněte na tlačítko **OK**.
    1. Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** a ujistěte se, vytvoření projektu správně. Knihovny DLL nachází v rámci ladění složky (nebo verze, pokud vytváříte tuto konfiguraci místo).

    V rámci skutečné balíčku NuGet samozřejmě budete implementovat mnoho užitečných funkcí, o kterých ostatní mohou vytvářet aplikace. V tomto návodu však nebude napsat další kód, protože knihovny tříd ze šablony, stačí vytvořit balíček.

## <a name="create-the-nuspec-package-manifest-file"></a>Vytvoření souboru manifestu balíčku příponou .nuspec

Každý balíček NuGet musí manifestu&mdash; `.nuspec` soubor&mdash;k popisu její obsah a jeho závislosti. `nuget spec` Příkaz vytvoří tento soubor pro vás, která pak přizpůsobit. V tomto příkladu vytvoříte `.nuspec` ze souboru projektu; můžete také vytvořit manifest jinými způsoby jak je popsáno na [vytvořit balíček](../create-packages/creating-a-package.md).

1. Otevřete příkazový řádek a přejděte ke složce obsahující soubor projektu (`.csproj`).

1. Spuštění rozhraní příkazového řádku NuGet `spec` příkaz pro generování manifestu, který se nazývá po projektu, například `AppLogger.nuspec`:

    ```
    nuget spec
    ```

1. Otevřete soubor v textovém editoru. Manifest je podobný kódu níže, kde tokeny ve formátu  *$ `<token>` $*  nahrazená při vytváření balíčku hodnotami z Properties/AssemblyInfo.cs projektu soubor. Další informace o tokeny v [vytváření soubor s příponou .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. Vyberte ID balíčku, který je jedinečný v rámci nuget.org. Doporučujeme používat se zásadami vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Nezapomeňte aktualizovat autora a popis značky nebo dojde k chybě v dalším kroku. Tady je aktualizované `.nuspec` souboru jako příklad:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost `<tags>` elementu, jako jsou tyto značky ostatní najít váš balíček a co provádí.

## <a name="run-the-pack-command"></a>Spusťte příkaz pack

K vytvoření balíčku NuGet ( `.nupkg` souboru) z projektu, spusťte `pack` příkaz:

```
nuget pack AppLogger.csproj
```

Tento příkaz vytvoří `AppLogger.1.0.0.0.nupkg` pomocí číslo název a verze balíčku z `.nuspec` souboru. Příkaz vydá upozornění, pokud jste neprovedli aktualizaci různých polí v `.nuspec` soubor z výchozí hodnoty.

## <a name="publish-the-package"></a>Umožňuje publikovat balíček

Jakmile máte `.nupkg` souboru ji publikujete pomocí nuget.org `push` příkaz. (Alternativně můžete použít [pracovní postup publikování nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).

> [!Warning]
> Balíčky, které publikujete nuget.org jsou veřejně viditelné pro ostatní vývojáři. K hostování balíčků soukromě, najdete v části [hostování balíčků](../hosting-packages/overview.md).

1. Vytvořit bezplatný účet na [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), nebo se přihlásit, pokud již účet máte. Vytvoření nového účtu odešle e-mail s potvrzením. Účet je potřeba zkontrolovat, než můžete nahrát balíček.

1. Po přihlášení, vyberte jméno uživatele (v pravém horním rohu) a pak vyberte **klíče rozhraní API**.

1. Vyberte **vytvořit**, zadejte název klíče, vyberte **vyberte obory > Push**pod **klíč rozhraní API**, zadejte * pro **Glob vzor**, pak Vyberte **vytvořit**.

1. Po vytvoření klíče, vyberte **kopie** načíst přístup klíčů budete potřebovat v rozhraní příkazového řádku:

    ![Klíč rozhraní API kopírování do schránky.](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Váš klíč uložit na bezpečném místě a udržování je tajný klíč. Pokud váš klíč se omylem zjistí, můžete ho obnovit vždy kdykoli. Klíč rozhraní API můžete také odebrat, pokud již nechcete push balíčky prostřednictvím rozhraní příkazového řádku.

1. Na příkazovém řádku spusťte následující příkaz zadáte název balíčku a klíč nahraďte hodnotou zkopírovali v kroku 4:

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe zobrazuje výsledky procesu publikování:

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. Váš profil na nuget.org vyberte **spravovat balíčky** zobrazíte ten právě publikovaný. Také obdržíte e-mail s potvrzením. Všimněte si, že může trvat nějakou dobu vašeho balíčku indexovat a zobrazit ve výsledcích hledání tam, kde ostatní můžete najít. Během této doby stránku balíčku zobrazuje následující zpráva:

    ![Tento balíček nebyl nebyly indexovány. To se zobrazí ve výsledcích hledání a bude k dispozici pro instalaci nebo obnovení po dokončení indexování.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Viry**: všechny balíčky nahrán do nuget.org jsou zkontrolovat viry a odmítnuta, pokud nejsou nalezeny žádné viry. Všechny balíčky uvedené v nuget.org také jsou pravidelně kontrolovány.

A je to! Právě jste publikovali vaše první balíček NuGet, abyste [nuget.org](https://www.nuget.org/), který ostatní vývojáři mohou použít ve svých vlastních projektů.

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../create-packages/publish-a-package.md)
- [Podpora více cílové rozhraní](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčku](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
