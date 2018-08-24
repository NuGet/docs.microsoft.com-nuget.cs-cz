---
title: Vytvoření a publikování balíčku .NET Standard ve Windows pomocí sady Visual Studio
description: Kurz návod týkající se vytváření a publikování balíčku .NET Standard NuGet pomocí sady Visual Studio 2017 na Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: af6e6e015f2e4adccd99171abb37e7291551351c
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794096"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Rychlý start: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (.NET Standard, jenom Windows)

Je jednoduchý proces vytvoření balíčku NuGet z knihovny .NET Standard třídy v sadě Visual Studio ve Windows a potom ji publikovat na nuget.org pomocí nástroje příkazového řádku.

> [!Note]
> V tomto rychlém startu platí pro Visual Studio 2017 pro Windows pouze. Visual Studio pro Mac nezahrnuje možnosti popsané tady. Použití [nástroje rozhraní příkazového řádku dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) místo.

## <a name="prerequisites"></a>Požadavky

1. Instalaci libovolné edice sady Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy. Visual Studio 2017 automaticky zahrnuje NuGet možnosti, když je nainstalovaná úloha .NET.

1. Nainstalujte `nuget.exe` rozhraní příkazového řádku, stáhněte si ji z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, který `.exe` soubor vhodný složky a přidání složky do proměnné prostředí PATH.

    Případně pokud máte [.NET Core SDK](https://www.microsoft.com/net/download/) nainstalované, můžete použít `dotnet` rozhraní příkazového řádku.

1. [Zaregistrujte si bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte. Vytvoření nového účtu se odešle e-mail s potvrzením. Účet musí ověřit dříve, než můžete nahrát balíček.

## <a name="create-a-class-library-project"></a>Vytvořte projekt knihovny tříd

Můžete použít existující projekt knihovna tříd rozhraní .NET Standard pro kód, který chcete balíček nebo vytvořit jednoduchý následujícím způsobem:

1. V sadě Visual Studio, zvolte **soubor > Nový > projekt**, rozbalte **Visual C# > .NET Standard** uzlu, vyberte šablonu "Knihovna tříd (.NET Standard)", pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.

1. Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** k Ujistěte se, že projekt je vytvořený řádně. Knihovny DLL se nachází složka pro ladění (nebo vydání, pokud vytváříte tuto konfiguraci místo).

V rámci skutečné balíčku NuGet samozřejmě, můžete implementovat mnoho užitečných funkcí, se kterými ostatní můžete vytvářet aplikace. V tomto návodu ale nebude napíšete žádný další kód vzhledem k tomu, že knihovna tříd z této šablony je dostatečná pro vytvoření balíčku. Pokud chcete některé funkční kód pro balíček, stále, použijte následující:

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
> Pokud nemáte důvod nerozhodnete jinak, .NET Standard je upřednostňovaným cílem, pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projektů.

## <a name="configure-package-properties"></a>Konfigurace vlastností balíčku

1. Vyberte **projektu > vlastnosti** nabídce příkaz a pak vyberte **balíčku** kartu. ( **Balíčku** kartě se zobrazí pouze pro projekty knihovny tříd .NET Standard; Pokud se zaměřujete na rozhraní .NET Framework, přečtěte si téma [vytvoření a publikování balíčku .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) místo. Pokud se nezobrazí pro projekt .NET Standard, budete muset aktualizovat na nejnovější verzi sady Visual Studio 2017.)

    ![Vlastnosti balíčku NuGet v projektu sady Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost **značky** vlastnost, protože značky pomoci ostatním najít váš balíček a pochopit jeho význam.

1. Zadejte jedinečný identifikátor balíčku a vyplňte všechny požadované vlastnosti. Popis různých vlastností najdete v tématu [odkaz na soubor souboru .nuspec](../reference/nuspec.md). Všechny vlastnosti zde pohledu `.nuspec` manifestu, který sada Visual Studio vytvoří pro projekt.

    > [!Important]
    > Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo cokoli, co můžete hostovat používáte. Pro Tento názorný postup doporučujeme, abyste pozdějším kroku publikování provádění balíček veřejně viditelné (i když nepravděpodobné, že kdo bude ve skutečnosti použít) včetně "Ukázkový" nebo "Test" v názvu.
    >
    > Při pokusu publikovat balíček s názvem, který již existuje, se zobrazí chyba.

1. Volitelné: Pokud chcete zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **upravit AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Spusťte příkaz pack

1. Nastavení konfigurace **vydání**.

1. Klikněte pravým tlačítkem myši na projekt v **Průzkumníka řešení** a vyberte **Pack** příkaz:

    ![Příkaz balíčku NuGet v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

1. Visual Studio vytvoří projekt a vytvoří `.nupkg` souboru. Zkontrolujte **výstup** okna podrobnosti (podobně jako následující), který obsahuje cestu k souboru balíčku. Všimněte si také, že sestavení je v `bin\Release\netstandard2.0` befits jako cílové rozhraní .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Alternativní možnost: balíček pomocí nástroje MSBuild

Jako alternativu k použití **Pack** příkaz nabídky, NuGet 4.x+ a podporuje MSBuild 15.1 + `pack` cílit při projekt obsahuje data potřebný balíček. Otevřete příkazový řádek, přejděte do složky vašeho projektu a spusťte následující příkaz. (Obvykle chcete spustit "Pro vývojáře příkazového řádku pro Visual Studio" z nabídky Start, jak bude nakonfigurován s všechny nezbytné cesty pro MSBuild.)

```cli
msbuild /t:pack /p:Configuration=Release
```

Balíček pak najdete v `bin\Release` složky.

Další možnosti s `msbuild /t:pack`, naleznete v tématu [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile budete mít `.nupkg` souboru, ji publikujete do nuget.org buď pomocí `nuget.exe` rozhraní příkazového řádku nebo `dotnet.exe` rozhraní příkazového řádku spolu s klíčem rozhraní API získaných z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získat klíč rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikování pomocí nuget nasdílení změn

Tento krok je alternativou k používání `dotnet.exe`.

1. Změnit na složku obsahující `.nupkg` souboru.

1. Spusťte následující příkaz, zadávání názvu balíčku a nahraďte hodnotu klíče svůj klíč rozhraní API:

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

Zobrazit [nuget nabízených](../tools/cli-ref-push.md).

### <a name="publish-with-dotnet-nuget-push"></a>Publikování pomocí nuget dotnet nasdílení změn

Tento krok je alternativou k používání `nuget.exe`.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikování chyby

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikované balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Přidání souboru readme a další soubory

Přímo zadat soubory, které chcete zahrnout do balíčku, upravte soubor projektu a použít `content` vlastnost:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Tato možnost zahrne soubor s názvem `readme.txt` v kořenovém adresáři balíčku. Visual Studio zobrazí okamžitě po instalaci balíčku přímo obsah tohoto souboru jako prostý text. (Soubory Readme nejsou zobrazeny pro balíčky nainstalované jako závislosti). Tady je například jak se zobrazí v souboru readme HtmlAgilityPack balíčku:

![Zobrazit soubor readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> V něm nebudou zahrnuty do výsledný balíček nebude výsledkem pouze přidání readme.txt v kořenovém adresáři projektu.

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../create-packages/publish-a-package.md)
- [Balíčky v předběžné verzi](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových platforem](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Dokumentace ke službě knihovna .NET standard](/dotnet/articles/standard/library)
- [Portování do .NET Core v rozhraní .NET Framework](/dotnet/articles/core/porting/index)
