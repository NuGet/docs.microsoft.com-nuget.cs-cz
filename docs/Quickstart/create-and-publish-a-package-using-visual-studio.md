---
title: "Úvodní příručka k vytváření a publikování .NET standardní balíčku NuGet pomocí sady Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/18/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Návod kurz týkající se vytváření a publikování balíčku NuGet pro standardní rozhraní .NET pomocí Visual Studio 2017."
keywords: "Balíček NuGet vytvoření, publikování balíčku NuGet, kurzu NuGet sady Visual Studio vytvořit balíček NuGet, aktualizací Service pack nástroje msbuild"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 733fee616601e1d15d8fb5814b5bfb7905ff4a33
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-standard"></a><span data-ttu-id="c6348-104">Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)</span><span class="sxs-lookup"><span data-stu-id="c6348-104">Create and publish a package using Visual Studio (.NET Standard)</span></span>

<span data-ttu-id="c6348-105">Je jednoduchý proces vytvoření balíčku NuGet z knihovny .NET standardní třídy v sadě Visual Studio, a potom jej publikujte do nuget.org pomocí rozhraní příkazového řádku nástroje.</span><span class="sxs-lookup"><span data-stu-id="c6348-105">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6348-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c6348-106">Prerequisites</span></span>

1. <span data-ttu-id="c6348-107">Nainstalujte všechny edice Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy.</span><span class="sxs-lookup"><span data-stu-id="c6348-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="c6348-108">Visual Studio 2017 automaticky zahrnuje NuGet možností při instalaci rozhraní .NET zatížení.</span><span class="sxs-lookup"><span data-stu-id="c6348-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="c6348-109">Nainstalujte `nuget.exe` CLI stažením z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, `.exe` souboru do složky vhodný, a přidáním této složce do vaší proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="c6348-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="c6348-110">Případně pokud máte [.NET Core SDK](https://www.microsoft.com/net/download/) nainstalován, můžete použít `dotnet` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="c6348-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="c6348-111">[Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="c6348-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="c6348-112">Vytvoření nového účtu odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="c6348-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="c6348-113">Účet je potřeba zkontrolovat, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="c6348-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="c6348-114">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="c6348-114">Create a class library project</span></span>

<span data-ttu-id="c6348-115">Můžete použít existující projekt standardní knihovna tříd rozhraní .NET pro kód, který chcete balíček nebo vytvořit jednoduchý takto:</span><span class="sxs-lookup"><span data-stu-id="c6348-115">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="c6348-116">V sadě Visual Studio, vyberte **soubor > Nový > projekt**, rozbalte **Visual C# > .NET Standard** uzlu, vyberte šablonu, "Knihovny tříd (.NET Standard)", název projektu AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6348-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="c6348-117">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** a ujistěte se, vytvoření projektu správně.</span><span class="sxs-lookup"><span data-stu-id="c6348-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="c6348-118">Knihovny DLL nachází v rámci ladění složky (nebo verze, pokud vytváříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="c6348-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="c6348-119">V rámci skutečné balíčku NuGet samozřejmě můžete implementovat řadu užitečných funkcí, se kterými ostatní mohou vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="c6348-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="c6348-120">V tomto návodu však nebude napsat další kód, protože knihovny tříd ze šablony, stačí vytvořit balíček.</span><span class="sxs-lookup"><span data-stu-id="c6348-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="c6348-121">Pokud chcete některé funkční kód pro balíček, stále, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="c6348-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="c6348-122">Pokud nemáte důvod, proč zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projekty.</span><span class="sxs-lookup"><span data-stu-id="c6348-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="c6348-123">Konfigurovat vlastnosti balíčku</span><span class="sxs-lookup"><span data-stu-id="c6348-123">Configure package properties</span></span>

1. <span data-ttu-id="c6348-124">Vyberte **Projekt > vlastnosti** nabídky příkazu a pak vyberte **balíček** kartě. ( **Balíček** karta se zobrazí pouze u projektů knihovny tříd rozhraní .NET standardní; Pokud cílíte na rozhraní .NET Framework, přečtěte si téma [vytvořit a publikovat balíček pro rozhraní .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) místo.)</span><span class="sxs-lookup"><span data-stu-id="c6348-124">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.)</span></span>

    ![Vlastnosti balíčku NuGet v projektu sady Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="c6348-126">Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **značky** vlastnosti, jako jsou značky ostatní najít váš balíček a co provádí.</span><span class="sxs-lookup"><span data-stu-id="c6348-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="c6348-127">Zadejte jedinečný identifikátor vašeho balíčku a vyplňte další požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="c6348-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="c6348-128">Popis různé vlastnosti najdete v tématu [odkaz na soubor příponou .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="c6348-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="c6348-129">Všechny vlastnosti sem přejděte do `.nuspec` manifestu, který vytvoří sada Visual Studio pro projekt.</span><span class="sxs-lookup"><span data-stu-id="c6348-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="c6348-130">Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte.</span><span class="sxs-lookup"><span data-stu-id="c6348-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="c6348-131">Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).</span><span class="sxs-lookup"><span data-stu-id="c6348-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="c6348-132">Pokud se pokusíte o publikování balíčku s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="c6348-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="c6348-133">Volitelné: Pokud chcete zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **upravit AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="c6348-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="c6348-134">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="c6348-134">Run the pack command</span></span>

1. <span data-ttu-id="c6348-135">Nastavte konfiguraci na **verze**.</span><span class="sxs-lookup"><span data-stu-id="c6348-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="c6348-136">Klikněte pravým tlačítkem na projekt v **Průzkumníku řešení** a vyberte **Pack** příkaz:</span><span class="sxs-lookup"><span data-stu-id="c6348-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Příkaz pack NuGet v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="c6348-138">Visual Studio vytvoří projekt a vytvoří `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="c6348-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="c6348-139">Zkontrolujte **výstup** okno Podrobnosti (podobně jako následující), který obsahuje cestu k souboru balíčku.</span><span class="sxs-lookup"><span data-stu-id="c6348-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="c6348-140">Všimněte si také, že integrované sestavení je v `bin\Release\netstandard2.0` jako befits cíl standardní rozhraní .NET 2.0.</span><span class="sxs-lookup"><span data-stu-id="c6348-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="c6348-141">Alternativní možnost: pack pomocí nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="c6348-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="c6348-142">Jako náhradní pomocí **Pack** příkaz nabídky, NuGet 4.x+ a podporuje MSBuild 15.1 + `pack` cíle Pokud projekt obsahuje data nezbytná balíčku.</span><span class="sxs-lookup"><span data-stu-id="c6348-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="c6348-143">Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="c6348-143">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="c6348-144">(Obvykle chcete spustit "Vývojáře příkazového řádku pro sady Visual Studio" z nabídky Start, jak bude nakonfigurován s všechny nezbytné cesty pro MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="c6348-144">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="c6348-145">Balíček pak lze nalézt v `bin\Release` složky.</span><span class="sxs-lookup"><span data-stu-id="c6348-145">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="c6348-146">Další možnosti s `msbuild /t:pack`, najdete v části [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="c6348-146">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="c6348-147">Umožňuje publikovat balíček</span><span class="sxs-lookup"><span data-stu-id="c6348-147">Publish the package</span></span>

<span data-ttu-id="c6348-148">Až budete mít `.nupkg` souboru ji publikujete do nuget.org buď pomocí `nuget.exe` rozhraní příkazového řádku nebo `dotnet.exe` rozhraní příkazového řádku spolu s klíčem rozhraní API získali z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c6348-148">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="c6348-149">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c6348-149">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="c6348-150">Publikování pomocí nabízených nuget</span><span class="sxs-lookup"><span data-stu-id="c6348-150">Publish with nuget push</span></span>

<span data-ttu-id="c6348-151">Tento krok je alternativu k použití `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="c6348-151">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="c6348-152">Změnit na složku, která obsahuje `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="c6348-152">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="c6348-153">Spusťte následující příkaz, zadáte název balíčku a nahraďte hodnotu klíče klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="c6348-153">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="c6348-154">nuget.exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="c6348-154">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="c6348-155">V tématu [nuget nabízené](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="c6348-155">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="c6348-156">Publikování pomocí nabízených nuget dotnet.</span><span class="sxs-lookup"><span data-stu-id="c6348-156">Publish with dotnet nuget push</span></span>

<span data-ttu-id="c6348-157">Tento krok je alternativu k použití `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="c6348-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="c6348-158">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="c6348-158">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="c6348-159">Spravovat zveřejněný balíček</span><span class="sxs-lookup"><span data-stu-id="c6348-159">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="c6348-160">Související témata</span><span class="sxs-lookup"><span data-stu-id="c6348-160">Related topics</span></span>

- [<span data-ttu-id="c6348-161">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="c6348-161">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="c6348-162">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="c6348-162">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="c6348-163">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="c6348-163">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="c6348-164">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="c6348-164">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="c6348-165">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="c6348-165">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="c6348-166">Standardní knihovny .NET dokumentaci</span><span class="sxs-lookup"><span data-stu-id="c6348-166">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="c6348-167">Portování do .NET Core z rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c6348-167">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)