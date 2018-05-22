---
title: Vytvoření a publikování .NET Standard balíček pomocí sady Visual Studio v systému Windows
description: Návod kurz týkající se vytváření a publikování balíčku NuGet pro rozhraní .NET standardní pomocí Visual Studio 2017 v systému Windows.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: f4e6473d307f2f71016f6926abbcdb1295abc7b5
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="f46da-103">Rychlý úvod: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (.NET Standard, pouze v systému Windows)</span><span class="sxs-lookup"><span data-stu-id="f46da-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="f46da-104">Je jednoduchý proces vytvoření balíčku NuGet z knihovny .NET standardní třídy v sadě Visual Studio v systému Windows, a potom jej publikujte do nuget.org pomocí rozhraní příkazového řádku nástroje.</span><span class="sxs-lookup"><span data-stu-id="f46da-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="f46da-105">Tento rychlý start platí pro Visual Studio 2017 pro systém Windows jenom.</span><span class="sxs-lookup"><span data-stu-id="f46da-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="f46da-106">Visual Studio pro Mac nezahrnuje možnosti popsané v tomto poli.</span><span class="sxs-lookup"><span data-stu-id="f46da-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="f46da-107">Použití [nástrojů příkazového řádku dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) místo.</span><span class="sxs-lookup"><span data-stu-id="f46da-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f46da-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f46da-108">Prerequisites</span></span>

1. <span data-ttu-id="f46da-109">Nainstalujte všechny edice Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy.</span><span class="sxs-lookup"><span data-stu-id="f46da-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="f46da-110">Visual Studio 2017 automaticky zahrnuje NuGet možností při instalaci rozhraní .NET zatížení.</span><span class="sxs-lookup"><span data-stu-id="f46da-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="f46da-111">Nainstalujte `nuget.exe` CLI stažením z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, `.exe` souboru do složky vhodný, a přidáním této složce do vaší proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="f46da-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="f46da-112">Případně pokud máte [.NET Core SDK](https://www.microsoft.com/net/download/) nainstalován, můžete použít `dotnet` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="f46da-112">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="f46da-113">[Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="f46da-113">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="f46da-114">Vytvoření nového účtu odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="f46da-114">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="f46da-115">Účet je potřeba zkontrolovat, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="f46da-115">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="f46da-116">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="f46da-116">Create a class library project</span></span>

<span data-ttu-id="f46da-117">Můžete použít existující projekt standardní knihovna tříd rozhraní .NET pro kód, který chcete balíček nebo vytvořit jednoduchý takto:</span><span class="sxs-lookup"><span data-stu-id="f46da-117">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="f46da-118">V sadě Visual Studio, vyberte **soubor > Nový > projekt**, rozbalte **Visual C# > .NET Standard** uzlu, vyberte šablonu, "Knihovny tříd (.NET Standard)", název projektu AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="f46da-118">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="f46da-119">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** a ujistěte se, vytvoření projektu správně.</span><span class="sxs-lookup"><span data-stu-id="f46da-119">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="f46da-120">Knihovny DLL nachází v rámci ladění složky (nebo verze, pokud vytváříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="f46da-120">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="f46da-121">V rámci skutečné balíčku NuGet samozřejmě můžete implementovat řadu užitečných funkcí, se kterými ostatní mohou vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="f46da-121">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="f46da-122">V tomto návodu však nebude napsat další kód, protože knihovny tříd ze šablony, stačí vytvořit balíček.</span><span class="sxs-lookup"><span data-stu-id="f46da-122">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="f46da-123">Pokud chcete některé funkční kód pro balíček, stále, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="f46da-123">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="f46da-124">Pokud nemáte důvod, proč zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projekty.</span><span class="sxs-lookup"><span data-stu-id="f46da-124">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="f46da-125">Konfigurovat vlastnosti balíčku</span><span class="sxs-lookup"><span data-stu-id="f46da-125">Configure package properties</span></span>

1. <span data-ttu-id="f46da-126">Vyberte **Projekt > vlastnosti** nabídky příkazu a pak vyberte **balíček** kartě. ( **Balíček** karta se zobrazí pouze u projektů knihovny tříd rozhraní .NET standardní; Pokud cílíte na rozhraní .NET Framework, přečtěte si téma [vytvořit a publikovat balíček pro rozhraní .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) místo.</span><span class="sxs-lookup"><span data-stu-id="f46da-126">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="f46da-127">Pokud se nezobrazí pro .NET Standard projekt, musíte aktualizovat na nejnovější verzi Visual Studio 2017.)</span><span class="sxs-lookup"><span data-stu-id="f46da-127">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Vlastnosti balíčku NuGet v projektu sady Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="f46da-129">Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **značky** vlastnosti, jako jsou značky ostatní najít váš balíček a co provádí.</span><span class="sxs-lookup"><span data-stu-id="f46da-129">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="f46da-130">Zadejte jedinečný identifikátor vašeho balíčku a vyplňte další požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="f46da-130">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="f46da-131">Popis různé vlastnosti najdete v tématu [odkaz na soubor příponou .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f46da-131">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="f46da-132">Všechny vlastnosti sem přejděte do `.nuspec` manifestu, který vytvoří sada Visual Studio pro projekt.</span><span class="sxs-lookup"><span data-stu-id="f46da-132">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="f46da-133">Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte.</span><span class="sxs-lookup"><span data-stu-id="f46da-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="f46da-134">Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).</span><span class="sxs-lookup"><span data-stu-id="f46da-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="f46da-135">Pokud se pokusíte o publikování balíčku s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="f46da-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="f46da-136">Volitelné: Pokud chcete zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **upravit AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="f46da-136">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="f46da-137">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="f46da-137">Run the pack command</span></span>

1. <span data-ttu-id="f46da-138">Nastavte konfiguraci na **verze**.</span><span class="sxs-lookup"><span data-stu-id="f46da-138">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="f46da-139">Klikněte pravým tlačítkem na projekt v **Průzkumníku řešení** a vyberte **Pack** příkaz:</span><span class="sxs-lookup"><span data-stu-id="f46da-139">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Příkaz pack NuGet v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="f46da-141">Visual Studio vytvoří projekt a vytvoří `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="f46da-141">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="f46da-142">Zkontrolujte **výstup** okno Podrobnosti (podobně jako následující), který obsahuje cestu k souboru balíčku.</span><span class="sxs-lookup"><span data-stu-id="f46da-142">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="f46da-143">Všimněte si také, že integrované sestavení je v `bin\Release\netstandard2.0` jako befits cíl standardní rozhraní .NET 2.0.</span><span class="sxs-lookup"><span data-stu-id="f46da-143">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="f46da-144">Alternativní možnost: pack pomocí nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="f46da-144">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="f46da-145">Jako náhradní pomocí **Pack** příkaz nabídky, NuGet 4.x+ a podporuje MSBuild 15.1 + `pack` cíle Pokud projekt obsahuje data nezbytná balíčku.</span><span class="sxs-lookup"><span data-stu-id="f46da-145">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="f46da-146">Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="f46da-146">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="f46da-147">(Obvykle chcete spustit "Vývojáře příkazového řádku pro sady Visual Studio" z nabídky Start, jak bude nakonfigurován s všechny nezbytné cesty pro MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="f46da-147">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="f46da-148">Balíček pak lze nalézt v `bin\Release` složky.</span><span class="sxs-lookup"><span data-stu-id="f46da-148">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="f46da-149">Další možnosti s `msbuild /t:pack`, najdete v části [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="f46da-149">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f46da-150">Umožňuje publikovat balíček</span><span class="sxs-lookup"><span data-stu-id="f46da-150">Publish the package</span></span>

<span data-ttu-id="f46da-151">Až budete mít `.nupkg` souboru ji publikujete do nuget.org buď pomocí `nuget.exe` rozhraní příkazového řádku nebo `dotnet.exe` rozhraní příkazového řádku spolu s klíčem rozhraní API získali z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f46da-151">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="f46da-152">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="f46da-152">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="f46da-153">Publikování pomocí nabízených nuget</span><span class="sxs-lookup"><span data-stu-id="f46da-153">Publish with nuget push</span></span>

<span data-ttu-id="f46da-154">Tento krok je alternativu k použití `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="f46da-154">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="f46da-155">Změnit na složku, která obsahuje `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="f46da-155">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="f46da-156">Spusťte následující příkaz, zadáte název balíčku a nahraďte hodnotu klíče klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="f46da-156">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="f46da-157">nuget.exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="f46da-157">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="f46da-158">V tématu [nuget nabízené](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="f46da-158">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="f46da-159">Publikování pomocí nabízených nuget dotnet.</span><span class="sxs-lookup"><span data-stu-id="f46da-159">Publish with dotnet nuget push</span></span>

<span data-ttu-id="f46da-160">Tento krok je alternativu k použití `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="f46da-160">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="f46da-161">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="f46da-161">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="f46da-162">Spravovat zveřejněný balíček</span><span class="sxs-lookup"><span data-stu-id="f46da-162">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="f46da-163">Související témata</span><span class="sxs-lookup"><span data-stu-id="f46da-163">Related topics</span></span>

- [<span data-ttu-id="f46da-164">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="f46da-164">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="f46da-165">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="f46da-165">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="f46da-166">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="f46da-166">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="f46da-167">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="f46da-167">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f46da-168">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="f46da-168">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f46da-169">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="f46da-169">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="f46da-170">Standardní knihovny .NET dokumentaci</span><span class="sxs-lookup"><span data-stu-id="f46da-170">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="f46da-171">Portování do .NET Core z rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f46da-171">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
