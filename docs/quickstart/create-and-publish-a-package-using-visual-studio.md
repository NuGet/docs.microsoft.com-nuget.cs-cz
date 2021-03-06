---
title: Vytvoření a publikování .NET Standard balíčku NuGet – Visual Studio ve Windows
description: Návod k vytvoření a publikování .NET Standard balíčku NuGet pomocí sady Visual Studio ve Windows.
author: JonDouglas
ms.author: jodou
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 53f54f6723ad10fca2ed6f75290ba3829dfb9a5e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775681"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Rychlý Start: vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (.NET Standard, pouze Windows)

Je to jednoduchý proces vytvoření balíčku NuGet z knihovny tříd .NET Standard v aplikaci Visual Studio ve Windows a jeho následné publikování na nuget.org pomocí nástroje CLI.

> [!Note]
> Pokud používáte Visual Studio pro Mac, přečtěte si [tyto informace](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) o vytvoření balíčku NuGet nebo použijte [nástroje dotnet CLI](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte jakoukoli edici sady Visual Studio 2019 z [VisualStudio.com](https://www.visualstudio.com/) s využitím úlohy související s .NET Core.

1. Pokud ještě není nainstalovaný, nainstalujte rozhraní příkazového `dotnet` řádku.

   Pro rozhraní `dotnet` příkazového řádku, počínaje sadou Visual Studio 2017, se rozhraní příkazového `dotnet` řádku automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core. V opačném případě nainstalujte rozhraní příkazového řádku, abyste získali [.NET Core SDK](https://www.microsoft.com/net/download/) `dotnet` . Rozhraní příkazového `dotnet` řádku je vyžadováno pro .NET Standard projekty, které používají [Formát sady SDK](../resources/check-project-format.md) (atribut sady SDK). Výchozí .NET Standard šablona knihovny tříd v sadě Visual Studio 2017 a vyšší, která se používá v tomto článku, používá atribut SDK.
   
   > [!Important]
   > Pokud pracujete s projektem, který není typu SDK, postupujte podle pokynů v části [Vytvoření a publikování .NET Frameworkho balíčku (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) pro vytvoření a publikování balíčku. V tomto článku se doporučuje používat rozhraní příkazového `dotnet` řádku. I když můžete publikovat libovolný balíček NuGet pomocí rozhraní `nuget.exe` příkazového řádku, některé kroky v tomto článku jsou specifické pro projekty ve stylu sady SDK a rozhraní příkazového řádku dotnet. nuget.exe CLI se používá pro [projekty, které nejsou ve stylu sady SDK](../resources/check-project-format.md) (obvykle .NET Framework).

1. [Zaregistrujte si bezplatný účet na NuGet.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) , pokud ho ještě nemáte. Když se vytvoří nový účet, pošle se potvrzovací e-mail. Než budete moct nahrát balíček, musíte účet potvrdit.

## <a name="create-a-class-library-project"></a>Vytvořit projekt knihovny tříd

Můžete použít existující .NET Standard projekt knihovny tříd pro kód, který chcete zabalit, nebo vytvořit jednoduchý, a to následujícím způsobem:

1. V aplikaci Visual Studio zvolte **soubor > nový > projekt**, rozbalte uzel **Visual C# > .NET Standard** , vyberte šablonu knihovny tříd (.NET Standard), pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.

   > [!Tip]
   > Pokud nemáte důvod vybrat jinak, .NET Standard je upřednostňovaným cílem pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.

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

## <a name="configure-package-properties"></a>Konfigurace vlastností balíčku

1. Klikněte pravým tlačítkem na projekt v Průzkumník řešení a zvolte příkaz nabídky **vlastnosti** a pak vyberte kartu **balíček** .

   Karta **balíček** se zobrazí pouze pro projekty ve stylu sady SDK v aplikaci Visual Studio, obvykle .NET Standard nebo .NET Core Class projektů; Pokud cílíte na jiný projekt než sadu SDK (obvykle .NET Framework), buď [migrujte projekt](../consume-packages/migrate-packages-config-to-package-reference.md) , nebo si přečtěte téma [vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.

    ![Vlastnosti balíčku NuGet v projektu Visual studia](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **značek** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.

1. Dejte balíčku jedinečný identifikátor a vyplňte všechny požadované vlastnosti. Mapování vlastností MSBuild (projekt ve stylu sady SDK) na vlastnosti v *. nuspec* naleznete v tématu [cíle balíčku](../reference/msbuild-targets.md#pack-target). Popisy vlastností naleznete v [souboru. nuspec reference](../reference/nuspec.md). Všechny vlastnosti zde přejdou do `.nuspec` manifestu, který Visual Studio vytvoří pro projekt.

    > [!Important]
    > Balíčku musíte dát identifikátor, který je jedinečný v rámci nuget.org nebo libovolného hostitele, který používáte. Pro tento návod doporučujeme, abyste v názvu jako pozdější krok publikování použili "Sample" nebo "test", aby byl balíček veřejně viditelný (i když je to nepravděpodobné, že ho kdokoli bude používat).
    >
    > Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.

1. Volitelné Chcete-li zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem myši na projekt v Průzkumník řešení a vyberte **Upravit AppLogger. csproj**.

   Tato možnost je k dispozici pouze od začátku v sadě Visual Studio 2017 pro projekty, které používají atribut Style sady SDK. V opačném případě klikněte pravým tlačítkem myši na projekt a vyberte **Uvolnit projekt**. Pak klikněte pravým tlačítkem na uvolněný projekt a zvolte **Upravit AppLogger. csproj**.

## <a name="run-the-pack-command"></a>Spuštění příkazu Pack

1. Nastavte konfiguraci na **release**.

1. Klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a vyberte příkaz **Pack** :

    ![Příkaz NuGet Pack v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

    Pokud nevidíte příkaz **Pack** , projekt pravděpodobně není projekt ve stylu sady SDK a je nutné použít rozhraní příkazového `nuget.exe` řádku. Buď [migrujte projekt](../consume-packages/migrate-packages-config-to-package-reference.md) a použijte rozhraní `dotnet` příkazového řádku, nebo si přečtěte článek [Vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.

1. Visual Studio vytvoří projekt a vytvoří `.nupkg` soubor. Projděte si podrobnosti v okně **výstup** (podobně jako v následujícím příkladu), který obsahuje cestu k souboru balíčku. Všimněte si také, že sestavené sestavení je v `bin\Release\netstandard2.0` podobě befits na cíl .NET Standard 2,0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>Volitelné Generovat balíček při sestavení

Sadu Visual Studio můžete nakonfigurovat tak, aby automaticky generovala balíček NuGet při sestavování projektu.

1. V Průzkumník řešení klikněte pravým tlačítkem na projekt a vyberte **vlastnosti**.

2. Na kartě **balíček** vyberte při **sestavování vytvořit balíček NuGet**.

   ![Automaticky generovat balíček při sestavení](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Když balíček automaticky vygenerujete, čas k zabalení zvýší čas sestavení pro váš projekt.

### <a name="optional-pack-with-msbuild"></a>(Nepovinný) Pack s nástrojem MSBuild

Jako alternativu k použití příkazu nabídky **Pack** , NuGet 4. x + a MSBuild 15.1 + podporuje cíl, `pack` když projekt obsahuje potřebná data balíčku. Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz. (Obvykle chcete spustit "Developer Command Prompt pro Visual Studio" z nabídky Start, protože se nakonfiguruje se všemi nezbytnými cestami pro MSBuild.)

Další informace najdete v tématu [Vytvoření balíčku pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile budete mít `.nupkg` soubor, publikujete ho v NuGet.org pomocí rozhraní příkazového `nuget.exe` řádku nebo rozhraní příkazového `dotnet.exe` řádku spolu s klíčem rozhraní API získaným z NuGet.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>Publikování pomocí rozhraní příkazového řádku dotnet nebo nuget.exe CLI

Vyberte kartu pro nástroj rozhraní příkazového řádku, buď **.NET Core CLI** (dotnet CLI), nebo **NUGET** (nuget.exe CLI).

# <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

Tento krok je doporučenou alternativou použití nástroje `nuget.exe` .

Než budete moct balíček publikovat, musíte nejdřív otevřít příkazový řádek.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[NuGet](#tab/nuget)

Tento krok je alternativou k použití `dotnet.exe` .

1. Otevřete příkazový řádek a přejděte do složky, která obsahuje `.nupkg` soubor.

1. Spusťte následující příkaz, zadáním názvu balíčku (jedinečné ID balíčku) a nahrazením hodnoty klíče klíčem rozhraní API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe zobrazuje výsledky procesu publikování:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Viz [push NuGet](../reference/cli-reference/cli-ref-push.md).

---

### <a name="publish-errors"></a>Chyby publikování

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikovaného balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Přidání souboru Readme a dalších souborů

Chcete-li přímo určit soubory, které mají být zahrnuty do balíčku, upravte soubor projektu a použijte `content` vlastnost:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Tato akce bude obsahovat soubor s názvem `readme.txt` v kořenovém adresáři balíčku. Sada Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo. (Soubory Readme se nezobrazí pro balíčky nainstalované jako závislosti). Tady je příklad, jak se zobrazí soubor Readme pro balíček HtmlAgilityPack:

![Zobrazení souboru Readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Pouze přidání readme.txt v kořenu projektu nebude mít za následek zahrnutí do výsledného balíčku.

## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

Další videa k NuGetu najdete na webu [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package-dotnet-cli.md)
- [Publikování balíčku](../nuget-org/publish-a-package.md)
- [Předběžné verze balíčků](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Správa verzí balíčků](../concepts/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Dokumentace ke knihovně .NET Standard](/dotnet/articles/standard/library)
- [Přenos do .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
