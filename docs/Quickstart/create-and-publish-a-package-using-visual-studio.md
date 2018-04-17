---
title: Úvodní příručka k vytváření a publikování .NET standardní balíčku NuGet pomocí sady Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/18/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Návod kurz týkající se vytváření a publikování balíčku NuGet pro standardní rozhraní .NET pomocí Visual Studio 2017.
keywords: Balíček NuGet vytvoření, publikování balíčku NuGet, kurzu NuGet sady Visual Studio vytvořit balíček NuGet, aktualizací Service pack nástroje msbuild
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7c5fb7911edcbbd3413a8836d20e7f108751f79
ms.sourcegitcommit: 55433d3bda7684d978f26d559f801878223675fa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/16/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-standard"></a>Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)

Je jednoduchý proces vytvoření balíčku NuGet z knihovny .NET standardní třídy v sadě Visual Studio, a potom jej publikujte do nuget.org pomocí rozhraní příkazového řádku nástroje.

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte všechny edice Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy. Visual Studio 2017 automaticky zahrnuje NuGet možností při instalaci rozhraní .NET zatížení.

1. Nainstalujte `nuget.exe` CLI stažením z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, `.exe` souboru do složky vhodný, a přidáním této složce do vaší proměnné prostředí PATH.

    Případně pokud máte [.NET Core SDK](https://www.microsoft.com/net/download/) nainstalován, můžete použít `dotnet` rozhraní příkazového řádku.

1. [Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte. Vytvoření nového účtu odešle e-mail s potvrzením. Účet je potřeba zkontrolovat, než můžete nahrát balíček.

## <a name="create-a-class-library-project"></a>Vytvoření projektu knihovny tříd

Můžete použít existující projekt standardní knihovna tříd rozhraní .NET pro kód, který chcete balíček nebo vytvořit jednoduchý takto:

1. V sadě Visual Studio, vyberte **soubor > Nový > projekt**, rozbalte **Visual C# > .NET Standard** uzlu, vyberte šablonu, "Knihovny tříd (.NET Standard)", název projektu AppLogger a klikněte na tlačítko **OK**.

1. Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** a ujistěte se, vytvoření projektu správně. Knihovny DLL nachází v rámci ladění složky (nebo verze, pokud vytváříte tuto konfiguraci místo).

V rámci skutečné balíčku NuGet samozřejmě můžete implementovat řadu užitečných funkcí, se kterými ostatní mohou vytvářet aplikace. V tomto návodu však nebude napsat další kód, protože knihovny tříd ze šablony, stačí vytvořit balíček. Pokud chcete některé funkční kód pro balíček, stále, použijte tento příkaz:

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
> Pokud nemáte důvod, proč zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projekty.

## <a name="configure-package-properties"></a>Konfigurovat vlastnosti balíčku

1. Vyberte **Projekt > vlastnosti** nabídky příkazu a pak vyberte **balíček** kartě. ( **Balíček** karta se zobrazí pouze u projektů knihovny tříd rozhraní .NET standardní; Pokud cílíte na rozhraní .NET Framework, přečtěte si téma [vytvořit a publikovat balíček pro rozhraní .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) místo. Pokud se nezobrazí pro .NET Standard projekt, musíte aktualizovat na nejnovější verzi Visual Studio 2017.)

    ![Vlastnosti balíčku NuGet v projektu sady Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **značky** vlastnosti, jako jsou značky ostatní najít váš balíček a co provádí.

1. Zadejte jedinečný identifikátor vašeho balíčku a vyplňte další požadované vlastnosti. Popis různé vlastnosti najdete v tématu [odkaz na soubor příponou .nuspec](../reference/nuspec.md). Všechny vlastnosti sem přejděte do `.nuspec` manifestu, který vytvoří sada Visual Studio pro projekt.

    > [!Important]
    > Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte. Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).
    >
    > Pokud se pokusíte o publikování balíčku s názvem, který již existuje, zobrazí se chyba.

1. Volitelné: Pokud chcete zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **upravit AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Spusťte příkaz pack

1. Nastavte konfiguraci na **verze**.

1. Klikněte pravým tlačítkem na projekt v **Průzkumníku řešení** a vyberte **Pack** příkaz:

    ![Příkaz pack NuGet v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

1. Visual Studio vytvoří projekt a vytvoří `.nupkg` souboru. Zkontrolujte **výstup** okno Podrobnosti (podobně jako následující), který obsahuje cestu k souboru balíčku. Všimněte si také, že integrované sestavení je v `bin\Release\netstandard2.0` jako befits cíl standardní rozhraní .NET 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Alternativní možnost: pack pomocí nástroje MSBuild

Jako náhradní pomocí **Pack** příkaz nabídky, NuGet 4.x+ a podporuje MSBuild 15.1 + `pack` cíle Pokud projekt obsahuje data nezbytná balíčku. Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz. (Obvykle chcete spustit "Vývojáře příkazového řádku pro sady Visual Studio" z nabídky Start, jak bude nakonfigurován s všechny nezbytné cesty pro MSBuild.)

```cli
msbuild /t:pack /p:Configuration=Release
```

Balíček pak lze nalézt v `bin\Release` složky.

Další možnosti s `msbuild /t:pack`, najdete v části [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Umožňuje publikovat balíček

Až budete mít `.nupkg` souboru ji publikujete do nuget.org buď pomocí `nuget.exe` rozhraní příkazového řádku nebo `dotnet.exe` rozhraní příkazového řádku spolu s klíčem rozhraní API získali z nuget.org.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získat klíč rozhraní API

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikování pomocí nabízených nuget

Tento krok je alternativu k použití `dotnet.exe`.

1. Změnit na složku, která obsahuje `.nupkg` souboru.

1. Spusťte následující příkaz, zadáte název balíčku a nahraďte hodnotu klíče klíč rozhraní API:

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

V tématu [nuget nabízené](../tools/cli-ref-push.md).

### <a name="publish-with-dotnet-nuget-push"></a>Publikování pomocí nabízených nuget dotnet.

Tento krok je alternativu k použití `nuget.exe`.

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikování chyby

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Spravovat zveřejněný balíček

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../create-packages/publish-a-package.md)
- [Podpora více cílové rozhraní](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Standardní knihovny .NET dokumentaci](/dotnet/articles/standard/library)
- [Portování do .NET Core z rozhraní .NET Framework](/dotnet/articles/core/porting/index)