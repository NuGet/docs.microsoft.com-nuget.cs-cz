---
title: Vytvoření a publikování balíčku .NET Standard NuGet – Visual Studio v systému Windows
description: Návod k vytvoření a publikování balíčku .NET Standard NuGet pomocí sady Visual Studio v systému Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429029"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Úvodní příručka: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (Standard.NET, jenom windows)

Je to jednoduchý proces k vytvoření balíčku NuGet z knihovny tříd .NET Standard v sadě Visual Studio v systému Windows a potom publikovat do nuget.org pomocí nástroje rozhraní rozhraní se kšak obc.

> [!Note]
> Pokud používáte Visual Studio for Mac, podívejte se na [tyto informace](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) o vytvoření balíčku NuGet nebo použijte [nástroje dotnet CLI](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte libovolnou edici Visual Studia 2019 z [visualstudio.com](https://www.visualstudio.com/) s úlohou související s jádrem .NET.

1. Pokud ještě není nainstalován, nainstalujte cli. `dotnet`

   Pro `dotnet` rozhraní se konkretním rozhraním, počínaje Visual Studio 2017, `dotnet` rozhraní se automaticky nainstaluje s libovolnými úlohami souvisejícími s jádrem .NET Core. V opačném případě nainstalujte sadu [.NET Core SDK,](https://www.microsoft.com/net/download/) abyste získali rozhraní se konzumního `dotnet` rozhraní. Rozhraní `dotnet` příkazového příkazu je vyžadováno pro projekty .NET Standard, které používají [formát ve stylu sady SDK](../resources/check-project-format.md) (atribut SDK). Výchozí šablona knihovny tříd .NET Standard v sadě Visual Studio 2017 a vyšší, která se používá v tomto článku, používá atribut SDK.
   
   > [!Important]
   > Pokud pracujete s projektem, který není ve stylu sady SDK, postupujte podle postupů v [části Vytvoření a publikování balíčku rozhraní .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) a vytvořte a publikujte balíček. Pro tento článek `dotnet` je doporučeno zaokreslování. I když můžete publikovat libovolný `nuget.exe` balíček NuGet pomocí rozhraní se konstatování, některé kroky v tomto článku jsou specifické pro projekty ve stylu sady SDK a rozhraní se konstatování dotnet. Rozhraní CLI nuget.exe se používá pro [projekty, které nejsou ve stylu sady SDK](../resources/check-project-format.md) (obvykle rozhraní .NET Framework).

1. [Zaregistrujte se zdarma účet na nuget.org,](../nuget-org/individual-accounts.md#add-a-new-individual-account) pokud nemáte ještě jeden. Vytvoření nového účtu odešle potvrzovací e-mail. Před nahráním balíčku musíte účet potvrdit.

## <a name="create-a-class-library-project"></a>Vytvoření projektu knihovny tříd

Pro kód, který chcete zabalit, můžete použít existující projekt knihovny standardní třídy .NET nebo vytvořit jednoduchý:

1. V sadě Visual Studio zvolte **Soubor > Nový > Project**, rozbalte uzel Visual **C# > .NET Standard,** vyberte šablonu "Knihovna tříd (.NET Standard)", pojmenujte projekt AppLogger a klepněte na **tlačítko OK**.

   > [!Tip]
   > Pokud nemáte důvod zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.

1. Klikněte pravým tlačítkem myši na výsledný soubor projektu a vyberte **sestavení,** abyste se ujistili, že byl projekt vytvořen správně. DLL se nachází ve složce Ladění (nebo verze, pokud vytvoříte tuto konfiguraci místo).

V rámci skutečného balíčku NuGet samozřejmě implementovat mnoho užitečných funkcí, s nimiž ostatní mohou vytvářet aplikace. Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostatečná k vytvoření balíčku. Přesto, pokud chcete nějaký funkční kód pro balíček, použijte následující:

```cs
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

## <a name="configure-package-properties"></a>Konfigurace vlastností balíčku

1. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a zvolte Příkaz nabídky **Vlastnosti** a pak vyberte kartu **Balíček.**

   Karta **Balíček** se zobrazí pouze pro projekty ve stylu sady SDK v sadě Visual Studio, obvykle .NET Standard nebo .NET Core projekty knihovny tříd; Pokud cílíte na projekt stylu sady SDK (obvykle rozhraní .NET Framework), [migrujte projekt](../consume-packages/migrate-packages-config-to-package-reference.md) nebo se podívejte [na tlačítko Vytvořit a publikovat balíček rozhraní .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.

    ![Vlastnosti balíčku NuGet v projektu sady Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > U balíčků vytvořených pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **Tags,** protože značky pomáhají ostatním najít váš balíček a pochopit, co dělá.

1. Podejte svému balíčku jedinečný identifikátor a vyplňte všechny ostatní požadované vlastnosti. Mapování vlastností MSBuild (projekt ve stylu sady SDK) na vlastnosti v *souboru .nuspec*naleznete v [tématu cíle balíčku](../reference/msbuild-targets.md#pack-target). Popis vlastností naleznete v [odkazu na soubor .nuspec](../reference/nuspec.md). Všechny vlastnosti zde přejde do manifestu, `.nuspec` který vytvoří visual studio pro projekt.

    > [!Important]
    > Balíček je nutné poskytnout identifikátor, který je jedinečný v celé nuget.org nebo libovolného hostitele, který používáte. Pro tento návod doporučujeme zahrnout "Ukázka" nebo "Test" v názvu jako pozdější krok publikování dělá balíček veřejně viditelné (i když je nepravděpodobné, že někdo bude skutečně používat).
    >
    > Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.

1. (Nepovinné) Chcete-li zobrazit vlastnosti přímo v souboru projektu, klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte **příkaz Upravit soubor AppLogger.csproj**.

   Tato možnost je k dispozici pouze od visual studia 2017 pro projekty, které používají atribut stylu sady SDK. V opačném případě klepněte pravým tlačítkem myši na projekt a zvolte **Uvolnit projekt**. Potom klepněte pravým tlačítkem myši na nezatížený projekt a zvolte **Upravit AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Spuštění příkazu pack

1. Nastavte konfiguraci na **Release**.

1. Klikněte pravým tlačítkem myši na projekt v **Průzkumníku řešení** a vyberte příkaz **Pack:**

    ![Příkaz NuGet pack v kontextové nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

    Pokud nevidíte **pack** příkaz, váš projekt pravděpodobně není projekt ve stylu SDK `nuget.exe` a je třeba použít příkaz příkazového příkazového příkazu. Buď [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) `dotnet` projekt a použijte rozhraní příkazového příkazového příkazu, nebo najdete [v tématu Vytvoření a publikování balíčku rozhraní .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.

1. Visual Studio vytvoří projekt a `.nupkg` vytvoří soubor. Zkontrolujte **okno Výstup** pro podrobnosti (podobně jako následující), který obsahuje cestu k souboru balíčku. Všimněte si také, `bin\Release\netstandard2.0` že sestavené sestavení je v, jak se sluší na cíl .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(Nepovinné) Generovat balíček při sestavení

Visual Studio můžete nakonfigurovat tak, aby automaticky generovalo balíček NuGet při vytváření projektu.

1. V Průzkumníku řešení klepněte pravým tlačítkem myši na projekt a zvolte **Vlastnosti**.

2. Na kartě **Balíček** vyberte **Generovat balíček NuGet při sestavení**.

   ![Automaticky generovat balíček při sestavení](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Při automatickém generování balíčku čas balení zvyšuje dobu sestavení pro váš projekt.

### <a name="optional-pack-with-msbuild"></a>(Volitelné) balení s MSBuild

Jako alternativu k použití příkazu nabídky **Pack** NuGet 4.x+ a MSBuild 15.1+ podporuje `pack` cíl, když projekt obsahuje potřebná data balíčku. Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz. (Obvykle chcete spustit "Příkazový řádek pro vývojáře pro Visual Studio" z nabídky Start, protože bude nakonfigurován se všemi potřebnými cestami pro MSBuild.)

Další informace naleznete [v tématu Vytvoření balíčku pomocí msbuild](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile máte `.nupkg` soubor, publikujete jej nuget.org `nuget.exe` pomocí rozhraní `dotnet.exe` se kli nebo rozhraní se klisy spolu s klíčem rozhraní API získaného z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>Publikovat pomocí rozhraní SE koncli dotnet nebo nuget.exe CLI

Vyberte kartu pro nástroj příkazového příkazového příkazového příkazu, buď **rozhraní .NET Core CLI** (dotnet CLI) nebo **NuGet** (nuget.exe CLI).

# <a name="net-core-cli"></a>[Rozhraní příkazového řádku .NET Core](#tab/netcore-cli)

Tento krok je doporučenou `nuget.exe`alternativou k použití .

Před publikováním balíčku je nutné nejprve otevřít příkazový řádek.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[NuGet](#tab/nuget)

Tento krok je alternativou k použití `dotnet.exe`.

1. Otevřete příkazový řádek a změňte `.nupkg` na složku obsahující soubor.

1. Spusťte následující příkaz, zadejte název balíčku (jedinečné ID balíčku) a nahraďte hodnotu klíče klíčem rozhraní API:

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

---

### <a name="publish-errors"></a>Chyby publikování

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikovaného balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Přidání souboru readme a dalších souborů

Chcete-li přímo určit soubory, které mají být `content` zahrnuty do balíčku, upravte soubor projektu a použijte vlastnost:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

To bude obsahovat `readme.txt` soubor pojmenovaný v kořenovém adresáři balíčku. Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo. (Soubory Readme se nezobrazují pro balíčky nainstalované jako závislosti). Například zde je návod, jak se zobrazí readme pro balíček HtmlAgilityPack:

![Zobrazení souboru readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Pouhé přidání souboru readme.txt v kořenovém adresáři projektu nepovede k jeho zahrnutí do výsledného balíčku.

## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package-dotnet-cli.md)
- [Publikování balíčku](../nuget-org/publish-a-package.md)
- [Předběžné verze balíčků](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Dokumentace standardní knihovny .NET](/dotnet/articles/standard/library)
- [Přenesení na jádro .NET z rozhraní .NET Framework](/dotnet/articles/core/porting/index)
