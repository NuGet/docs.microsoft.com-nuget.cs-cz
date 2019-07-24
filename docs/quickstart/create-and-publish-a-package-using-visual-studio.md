---
title: Vytvoření a publikování .NET Standard balíčku NuGet pomocí sady Visual Studio ve Windows
description: Návod k vytvoření a publikování .NET Standard balíčku NuGet pomocí sady Visual Studio ve Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419918"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Rychlý start: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (.NET Standard, pouze Windows)

Je to jednoduchý proces vytvoření balíčku NuGet z knihovny tříd .NET Standard v aplikaci Visual Studio ve Windows a jeho následné publikování na nuget.org pomocí nástroje CLI.

> [!Note]
> Pokud používáte Visual Studio pro Mac, přečtěte si [tyto informace](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) o vytvoření balíčku NuGet nebo použijte [nástroje dotnet CLI](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte jakoukoli edici sady Visual Studio 2017 nebo vyšší z [VisualStudio.com](https://www.visualstudio.com/) s využitím úlohy související s .NET Core.

1. Pokud ještě není nainstalovaný, nainstalujte rozhraní `dotnet` příkazového řádku.

   Pro rozhraní `dotnet` příkazového řádku, počínaje sadou Visual Studio 2017 `dotnet` , se rozhraní příkazového řádku automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core. V opačném případě nainstalujte rozhraní příkazového `dotnet` řádku, abyste získali [.NET Core SDK](https://www.microsoft.com/net/download/). Rozhraní `dotnet` příkazového řádku je vyžadováno pro .NET Standard projekty, které používají [Formát sady SDK](../resources/check-project-format.md) (atribut sady SDK). Výchozí šablona knihovny tříd v sadě Visual Studio 2017 a vyšší, která se používá v tomto článku, používá atribut SDK.
   
   > [!Important]
   > V tomto článku se doporučuje `dotnet` používat rozhraní příkazového řádku. I když můžete publikovat libovolný balíček NuGet pomocí rozhraní `nuget.exe` příkazového řádku, některé kroky v tomto článku jsou specifické pro projekty ve stylu sady SDK a rozhraní příkazového řádku dotnet. Rozhraní příkazového řádku NuGet. exe se používá pro [projekty, které nejsou ve stylu sady SDK](../resources/check-project-format.md) (obvykle .NET Framework). Pokud pracujete s projektem, který není typu SDK, postupujte podle pokynů v části [Vytvoření a publikování .NET Framework balíčku (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) pro vytvoření a publikování balíčku.

1. [Zaregistrujte si bezplatný účet na NuGet.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) , pokud ho ještě nemáte. Když se vytvoří nový účet, pošle se potvrzovací e-mail. Než budete moct nahrát balíček, musíte účet potvrdit.

## <a name="create-a-class-library-project"></a>Vytvořit projekt knihovny tříd

Můžete použít existující .NET Standard projekt knihovny tříd pro kód, který chcete zabalit, nebo vytvořit jednoduchý, a to následujícím způsobem:

1. V aplikaci Visual Studio zvolte **soubor > nový > projekt**, rozbalte uzel **Visual C# > .NET Standard** , vyberte šablonu knihovny tříd (.NET Standard), pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.

1. Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavit** , abyste se ujistili, že se projekt vytvořil správně. Knihovna DLL se nachází ve složce ladění (nebo v případě, že tuto konfiguraci sestavíte místo toho).

V rámci skutečného balíčku NuGet samozřejmě implementujete spoustu užitečných funkcí, se kterými můžou sestavovat aplikace i ostatní. Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostačující k vytvoření balíčku. I když chcete pro balíček použít nějaký funkční kód, použijte následující:

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

> [!Tip]
> Pokud nemáte důvod vybrat jinak, .NET Standard je upřednostňovaným cílem pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.

## <a name="configure-package-properties"></a>Konfigurovat vlastnosti balíčku

1. Klikněte pravým tlačítkem na projekt v Průzkumník řešení a zvolte příkaz nabídky **vlastnosti** a pak vyberte kartu **balíček** .

   Karta **balíček** se zobrazí pouze pro projekty ve stylu sady SDK v aplikaci Visual Studio, obvykle .NET Standard nebo .NET Core Class projektů; Pokud cílíte na projekt bez sady SDK (obvykle .NET Framework), buď migrujte [projekt](../reference/migrate-packages-config-to-package-reference.md) a použijte `dotnet` rozhraní příkazového řádku, nebo si přečtěte téma [Vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) nebo téma [Vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) . místo toho, abyste mohli postupovat podle pokynů.

    ![Vlastnosti balíčku NuGet v projektu Visual studia](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **značek** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.

1. Dejte balíčku jedinečný identifikátor a vyplňte všechny požadované vlastnosti. Popis různých vlastností naleznete v tématu [Reference k souboru. nuspec](../reference/nuspec.md). Všechny vlastnosti zde přejdou do `.nuspec` manifestu, který Visual Studio vytvoří pro projekt.

    > [!Important]
    > Balíčku musíte dát identifikátor, který je jedinečný v rámci nuget.org nebo libovolného hostitele, který používáte. Pro tento návod doporučujeme, abyste v názvu jako pozdější krok publikování použili "Sample" nebo "test", aby byl balíček veřejně viditelný (i když je to nepravděpodobné, že ho kdokoli bude používat).
    >
    > Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.

1. Volitelné: Chcete-li zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem myši na projekt v Průzkumník řešení a vyberte **Upravit AppLogger. csproj**.

   Tato možnost je k dispozici pouze od začátku v sadě Visual Studio 2017 pro projekty, které používají atribut Style sady SDK. V opačném případě klikněte pravým tlačítkem myši na projekt a vyberte **Uvolnit projekt**. Pak klikněte pravým tlačítkem na uvolněný projekt a zvolte **Upravit AppLogger. csproj**.

## <a name="run-the-pack-command"></a>Spuštění příkazu Pack

1. Nastavte konfiguraci na **release**.

1. Klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a vyberte příkaz **Pack** :

    ![Příkaz NuGet Pack v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

    Pokud nevidíte příkaz **Pack** , projekt pravděpodobně není projekt ve stylu sady SDK a je nutné použít rozhraní `nuget.exe` příkazového řádku. Buď [migrujte projekt](../reference/migrate-packages-config-to-package-reference.md) a použijte `dotnet` rozhraní příkazového řádku, nebo si přečtěte článek [Vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.

1. Visual Studio vytvoří projekt a vytvoří `.nupkg` soubor. Projděte si podrobnosti v okně **výstup** (podobně jako v následujícím příkladu), který obsahuje cestu k souboru balíčku. Všimněte si také, že sestavené sestavení `bin\Release\netstandard2.0` je v podobě befits na cíl .NET Standard 2,0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Alternativní možnost: sada s MSBuild

Jako alternativu k použití příkazu nabídky **Pack** , NuGet 4. x + a MSBuild 15.1 + podporuje `pack` cíl, když projekt obsahuje potřebná data balíčku. Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz. (Obvykle chcete spustit "Developer Command Prompt pro Visual Studio" z nabídky Start, protože se nakonfiguruje se všemi nezbytnými cestami pro MSBuild.)

```cli
msbuild -t:pack -p:Configuration=Release
```

Balíček se pak dá najít ve `bin\Release` složce.

Další možnosti s `msbuild -t:pack`najdete v tématu [sada NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile budete mít `.nupkg` soubor, publikujete ho v NuGet.org pomocí rozhraní `nuget.exe` příkazového řádku nebo `dotnet.exe` rozhraní příkazového řádku spolu s klíčem rozhraní API získaným z NuGet.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a>Publikování pomocí příkazu dotnet NuGet push (dotnet CLI)

Tento krok je doporučenou alternativou použití `nuget.exe`nástroje.

Než budete moct balíček publikovat, musíte nejdřív otevřít příkazový řádek.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Publikování pomocí Push NuGet (NuGet. exe CLI)

Tento krok je alternativou k použití `dotnet.exe`.

1. Otevřete příkazový řádek a přejděte do složky, která obsahuje `.nupkg` soubor.

1. Spusťte následující příkaz, zadáním názvu balíčku (jedinečné ID balíčku) a nahrazením hodnoty klíče klíčem rozhraní API:

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

## <a name="adding-a-readme-and-other-files"></a>Přidání souboru Readme a dalších souborů

Chcete-li přímo určit soubory, které mají být zahrnuty do balíčku, upravte soubor projektu `content` a použijte vlastnost:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Tato akce bude obsahovat soubor s `readme.txt` názvem v kořenovém adresáři balíčku. Sada Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo. (Soubory Readme se nezobrazí pro balíčky nainstalované jako závislosti). Tady je příklad, jak se zobrazí soubor Readme pro balíček HtmlAgilityPack:

![Zobrazení souboru Readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Pouze přidání souboru Readme. txt v kořenu projektu nebude mít za následek zahrnutí do výsledného balíčku.

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../nuget-org/publish-a-package.md)
- [Předběžné verze balíčků](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Dokumentace ke knihovně .NET Standard](/dotnet/articles/standard/library)
- [Přenos do .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
