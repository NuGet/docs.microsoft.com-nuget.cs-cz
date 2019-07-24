---
title: Vytvoření a publikování .NET Framework balíčku NuGet pomocí sady Visual Studio ve Windows
description: Návod k vytvoření a publikování .NET Framework balíčku NuGet pomocí sady Visual Studio ve Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 75160bf2b01f6d4707162e019a6263ddc64a6f5e
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342522"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Rychlý start: Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Framework, Windows)

Vytvoření balíčku NuGet z knihovny tříd .NET Framework zahrnuje vytvoření knihovny DLL v aplikaci Visual Studio ve Windows a následné vytvoření a publikování balíčku pomocí nástroje příkazového řádku NuGet. exe.

> [!Note]
> Tento rychlý Start se týká jenom sady Visual Studio 2017 pro Windows. Visual Studio pro Mac nezahrnuje funkce popsané tady. Místo toho použijte [nástroje DOTNET CLI](create-and-publish-a-package-using-the-dotnet-cli.md) .

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte jakoukoli edici sady Visual Studio 2017 z [VisualStudio.com](https://www.visualstudio.com/) s libovolným. Zatížení související s NET. Pokud je nainstalovaná úloha .NET, Visual Studio 2017 automaticky zahrnuje funkce NuGet.

1. Nainstalujte rozhraní `nuget.exe` příkazového řádku stažením z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), uložte tento `.exe` soubor do vhodné složky a přidejte tuto složku do proměnné prostředí PATH.

1. [Zaregistrujte si bezplatný účet na NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) , pokud ho ještě nemáte. Když se vytvoří nový účet, pošle se potvrzovací e-mail. Než budete moct nahrát balíček, musíte účet potvrdit.

## <a name="create-a-class-library-project"></a>Vytvořit projekt knihovny tříd

Můžete použít existující .NET Framework projekt knihovny tříd pro kód, který chcete zabalit, nebo vytvořit jednoduchý, a to následujícím způsobem:

1. V aplikaci Visual Studio zvolte **soubor > Nový > projekt**, vyberte uzel **vizuálů C#**  , vyberte šablonu knihovny tříd (.NET Framework), pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.

1. Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavit** , abyste se ujistili, že se projekt vytvořil správně. Knihovna DLL se nachází ve složce ladění (nebo v případě, že tuto konfiguraci sestavíte místo toho).

V rámci skutečného balíčku NuGet samozřejmě implementujete spoustu užitečných funkcí, se kterými můžou sestavovat aplikace i ostatní. Můžete také nastavit cílové architektury, například. Podívejte se například na příručky pro [UWP](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).

Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostačující k vytvoření balíčku. I když chcete pro balíček použít nějaký funkční kód, použijte následující:

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> Pokud nemáte důvod vybrat jinak, .NET Standard je upřednostňovaným cílem pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů. Přečtěte si téma [Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Konfigurovat vlastnosti projektu pro balíček

Balíček NuGet obsahuje manifest ( `.nuspec` soubor), který obsahuje relevantní metadata, jako je například identifikátor balíčku, číslo verze, popis a další. Některé z nich lze vykreslit přímo z vlastností projektu a zabránit tak jejich samostatné aktualizaci v projektu i v manifestu. V této části se dozvíte, kde můžete nastavit příslušné vlastnosti.

1. Vyberte příkaz nabídky **Vlastnosti projektu >** a pak vyberte kartu **aplikace** .

1. V poli **název sestavení** poskytněte balíčku jedinečný identifikátor.

    > [!Important]
    > Balíčku musíte dát identifikátor, který je jedinečný v rámci nuget.org nebo libovolného hostitele, který používáte. Pro tento návod doporučujeme, abyste v názvu jako pozdější krok publikování použili "Sample" nebo "test", aby byl balíček veřejně viditelný (i když je to nepravděpodobné, že ho kdokoli bude používat).
    >
    > Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.

1. Vyberte tlačítko **informace o sestavení...** , které zobrazí dialogové okno, ve kterém můžete zadat další vlastnosti, které se přenesou do manifestu (viz [soubor. nuspec – náhradní tokeny reference](../reference/nuspec.md#replacement-tokens)). Nejčastěji používaná pole jsou **název**, **Popis**, **Společnost**, **Copyright**a **verze sestavení**. Tyto vlastnosti se nakonec zobrazí s vaším balíčkem na hostiteli, jako je nuget.org, a ujistěte se, že jsou plně popisné.

    ![Informace o sestavení v projektu .NET Framework v aplikaci Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Volitelné: Chcete-li zobrazit a upravit vlastnosti přímo, otevřete `Properties/AssemblyInfo.cs` soubor v projektu.

1. Po nastavení vlastností nastavte konfiguraci projektu na vydaná a znovu  Sestavte projekt, aby se vygenerovala Aktualizovaná knihovna DLL.

## <a name="generate-the-initial-manifest"></a>Generování počátečního manifestu

Když je knihovna DLL v rukou a nastavené vlastnosti projektu, můžete nyní `nuget spec` použít příkaz k vygenerování `.nuspec` počátečního souboru z projektu. Tento krok zahrnuje relevantní náhradní tokeny k vykreslování informací ze souboru projektu.

Pro vygenerování počátečního manifestu se spustí `nuget spec` jenom jednou. Při aktualizaci balíčku můžete buď změnit hodnoty v projektu, nebo přímo upravit manifest.

1. Otevřete příkazový řádek a přejděte do složky projektu obsahující `AppLogger.csproj` soubor.

1. Spusťte následující příkaz: `nuget spec AppLogger.csproj`. Když zadáte projekt, NuGet vytvoří v tomto případě `AppLogger.nuspec`manifest, který se shoduje s názvem projektu. Obsahuje také náhradní tokeny v manifestu.

1. Otevřete `AppLogger.nuspec` v textovém editoru, abyste prozkoumali jeho obsah, který by měl vypadat takto:

    ```xml
    <?xml version="1.0"?>
    <package >
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
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Upravit manifest

1. NuGet vyvolá chybu, pokud se pokusíte vytvořit balíček s výchozími hodnotami v `.nuspec` souboru, takže před pokračováním musíte upravit následující pole. Viz [odkaz na soubor. nuspec – volitelné prvky metadat](../reference/nuspec.md#optional-metadata-elements) pro popis způsobu jejich použití.

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - značky

1. Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **značek** , protože značky můžou ostatním uživatelům najít balíček na zdrojích, jako je NuGet.org, a pochopit, co dělá.

1. V tomto okamžiku můžete také přidat další prvky do manifestu, jak je popsáno v [souboru. nuspec reference](../reference/nuspec.md).

1. Než budete pokračovat, soubor uložte.

## <a name="run-the-pack-command"></a>Spuštění příkazu Pack

1. Z příkazového řádku ve složce, která obsahuje `.nuspec` váš soubor, spusťte příkaz `nuget pack`.

1. NuGet vygeneruje `.nupkg` soubor ve formě identifikátoru *Version. nupkg*, který najdete v aktuální složce.

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile budete mít `.nupkg` soubor, publikujete ho pro NuGet.org pomocí `nuget.exe` klíče rozhraní API získaného z NuGet.org. Pro NuGet.org musíte použít `nuget.exe` 4.1.0 nebo vyšší.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikování s nabízeným oznámením NuGet

1. Otevřete příkazový řádek a přejděte do složky, která obsahuje `.nupkg` soubor.

1. Spusťte následující příkaz, zadáním názvu balíčku a nahrazením hodnoty klíče vaším klíčem rozhraní API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. NuGet. exe zobrazuje výsledky procesu publikování:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Viz [push NuGet](../reference/cli-reference/cli-ref-push.md).

### <a name="publish-errors"></a>Chyby publikování

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikovaného balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Další kroky

Blahopřejeme k vytvoření prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Vytvoření balíčku](../create-packages/creating-a-package.md)

Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.

- [Publikování balíčku](../nuget-org/publish-a-package.md)
- [Předběžné verze balíčků](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových architektur](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
