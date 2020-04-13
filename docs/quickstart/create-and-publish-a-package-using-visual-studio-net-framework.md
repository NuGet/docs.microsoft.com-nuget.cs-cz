---
title: Vytvoření a publikování balíčku .NET Framework NuGet pomocí sady Visual Studio v systému Windows
description: Návod k vytvoření a publikování balíčku .NET Framework NuGet pomocí sady Visual Studio v systému Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380648"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Úvodní příručka: Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Framework, Windows)

Vytvoření balíčku NuGet z knihovny tříd rozhraní .NET Framework zahrnuje vytvoření knihovny DLL v sadě Visual Studio v systému Windows a následné vytvoření a publikování balíčku pomocí nástroje příkazového řádku nuget.exe.

> [!Note]
> Tento úvodní příručka se vztahuje pouze na visual studio 2017 a vyšší verze pro Windows. Visual Studio pro Mac neobsahuje zde popsané funkce. Místo toho použijte [nástroje rozhraní SE kontinua dotnet.](create-and-publish-a-package-using-the-dotnet-cli.md)

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte libovolnou edici Visual Studia 2017 nebo vyšší z [visualstudio.com](https://www.visualstudio.com/) s libovolným . NET související s úlohou. Visual Studio 2017 automaticky zahrnuje funkce NuGet při instalaci úlohy .NET.

1. Nainstalujte `nuget.exe` rozhraní se konstatování pomocí `.exe` nuget.org [,](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)uložíte jej do vhodné složky a přidáte tuto složku do proměnné prostředí PATH.

1. [Zaregistrujte se zdarma účet na nuget.org,](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) pokud nemáte ještě jeden. Vytvoření nového účtu odešle potvrzovací e-mail. Před nahráním balíčku musíte účet potvrdit.

## <a name="create-a-class-library-project"></a>Vytvoření projektu knihovny tříd

Můžete použít existující projekt knihovny tříd rozhraní .NET Framework pro kód, který chcete zabalit, nebo vytvořit jednoduchý následující:

1. V sadě Visual Studio zvolte **Soubor > Nový > project**, vyberte uzel Visual **C#,** vyberte šablonu "Knihovna tříd (.NET Framework)", pojmenujte projekt AppLogger a klepněte na tlačítko **OK**.

1. Klikněte pravým tlačítkem myši na výsledný soubor projektu a vyberte **sestavení,** abyste se ujistili, že byl projekt vytvořen správně. DLL se nachází ve složce Ladění (nebo verze, pokud vytvoříte tuto konfiguraci místo).

V rámci skutečného balíčku NuGet samozřejmě implementovat mnoho užitečných funkcí, s nimiž ostatní mohou vytvářet aplikace. Můžete také nastavit cílové architektury, jak se vám líbí. Například naleznete v průvodcích pro [UPW](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).

Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostatečná k vytvoření balíčku. Přesto, pokud chcete nějaký funkční kód pro balíček, použijte následující:

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
> Pokud nemáte důvod zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů. Viz [Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard).](create-and-publish-a-package-using-visual-studio.md)

## <a name="configure-project-properties-for-the-package"></a>Konfigurace vlastností projektu pro balíček

Balíček NuGet obsahuje manifest `.nuspec` (soubor), který obsahuje relevantní metadata, jako je například identifikátor balíčku, číslo verze, popis a další. Některé z nich lze vyvodit z vlastností projektu přímo, což zabraňuje nutnosti samostatně aktualizovat v projektu i manifestu. Tato část popisuje, kde nastavit příslušné vlastnosti.

1. Vyberte příkaz Nabídky **Vlastnosti projektu >** a pak vyberte kartu **Aplikace.**

1. V poli **Název sestavení** pojmenujte balíček jedinečným identifikátorem.

    > [!Important]
    > Balíček je nutné poskytnout identifikátor, který je jedinečný v celé nuget.org nebo libovolného hostitele, který používáte. Pro tento návod doporučujeme zahrnout "Ukázka" nebo "Test" v názvu jako pozdější krok publikování dělá balíček veřejně viditelné (i když je nepravděpodobné, že někdo bude skutečně používat).
    >
    > Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.

1. Vyberte tlačítko **Informace o sestavení...** tlačítko, ve kterém se zobrazí dialogové okno, ve kterém můžete zadat další vlastnosti, které se přenášejí do manifestu (viz [.nuspec odkaz na soubor - náhradní tokeny](../reference/nuspec.md#replacement-tokens)). Nejčastěji používanými poli jsou **verze Název**, **Popis**, **Společnost**, **Autorská práva**a **Sestava**. Tyto vlastnosti se nakonec zobrazí s balíčkem na hostiteli, jako je nuget.org, takže se ujistěte, že jsou plně popisné.

    ![Informace o sestavení v projektu rozhraní .NET Framework v sadě Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Volitelné: chcete-li vlastnosti zobrazit `Properties/AssemblyInfo.cs` a upravit přímo, otevřete soubor v projektu.

1. Když jsou vlastnosti nastaveny, nastavte konfiguraci projektu na **Release** a znovu vytvořte projekt, abyste vygenerovali aktualizovanou dll.

## <a name="generate-the-initial-manifest"></a>Generovat počáteční manifest

Se sadou vlastností DLL a vlastností `nuget spec` projektu nyní `.nuspec` pomocí příkazu vygenerujete počáteční soubor z projektu. Tento krok zahrnuje příslušné náhradní tokeny pro kreslení informací ze souboru projektu.

Spuštění `nuget spec` pouze jednou generovat počáteční manifest. Při aktualizaci balíčku můžete buď změnit hodnoty v projektu, nebo přímo upravit manifest.

1. Otevřete příkazový řádek a přejděte `AppLogger.csproj` do složky projektu obsahující soubor.

1. Spusťte následující `nuget spec AppLogger.csproj`příkaz: . Zadáním projektu, NuGet vytvoří manifest, který odpovídá názvu projektu, `AppLogger.nuspec`v tomto případě . Zahrnuje také náhradní tokeny v manifestu.

1. Otevřete `AppLogger.nuspec` v textovém editoru a prohlédněte si jeho obsah, který by se měl zobrazit takto:

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Úprava manifestu

1. NuGet vytvoří chybu, pokud se pokusíte vytvořit balíček s výchozí hodnoty v `.nuspec` souboru, takže je nutné upravit následující pole před pokračováním. Viz [.nuspec odkaz na soubor - volitelné prvky metadat](../reference/nuspec.md#optional-metadata-elements) pro popis, jak jsou použity.

    - licenseUrl
    - projektUrl
    - iconUrl
    - releaseNotes
    - tags

1. U balíčků vytvořených pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **Tags,** protože značky pomáhají ostatním najít váš balíček na zdrojích, jako je nuget.org a pochopit, co dělá.

1. V tuto chvíli můžete také přidat do manifestu další prvky, jak je popsáno [v odkazu na soubor .nuspec](../reference/nuspec.md).

1. Před pokračováním soubor uložte.

## <a name="run-the-pack-command"></a>Spuštění příkazu pack

1. Z příkazového řádku ve složce obsahující `.nuspec` soubor `nuget pack`spusťte příkaz .

1. NuGet generuje `.nupkg` soubor ve formě *identifier-version.nupkg*, který najdete v aktuální složce.

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile máte `.nupkg` soubor, publikujete jej `nuget.exe` nuget.org pomocí klíče rozhraní API získaného z nuget.org. Pro nuget.org musíte `nuget.exe` použít 4.1.0 nebo vyšší.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikovat pomocí nuget push

1. Otevřete příkazový řádek a změňte `.nupkg` na složku obsahující soubor.

1. Spusťte následující příkaz, zadejte název balíčku a nahraďte hodnotu klíče klíčem rozhraní API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe zobrazí výsledky procesu publikování:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Viz [nuget push](../reference/cli-reference/cli-ref-push.md).

### <a name="publish-errors"></a>Chyby publikování

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikovaného balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Další kroky

Gratulujeme k vytvoření prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Vytvoření balíčku](../create-packages/creating-a-package.md)

Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.

- [Publikování balíčku](../nuget-org/publish-a-package.md)
- [Předběžné verze balíčků](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových architektur](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
