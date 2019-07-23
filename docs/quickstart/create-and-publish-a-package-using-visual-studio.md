---
title: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio ve Windows
description: Návod k vytvoření a publikování .NET Standard balíčku NuGet pomocí sady Visual Studio ve Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 949c49d77ef088f802bdbd9c681f7df41d9a4c67
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342556"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="927f4-103">Rychlý start: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (.NET Standard, pouze Windows)</span><span class="sxs-lookup"><span data-stu-id="927f4-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="927f4-104">Je to jednoduchý proces vytvoření balíčku NuGet z knihovny tříd .NET Standard v aplikaci Visual Studio ve Windows a jeho následné publikování na nuget.org pomocí nástroje CLI.</span><span class="sxs-lookup"><span data-stu-id="927f4-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="927f4-105">Pokud používáte Visual Studio pro Mac, přečtěte si [tyto informace](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) o vytvoření balíčku NuGet nebo použijte [nástroje dotnet CLI](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="927f4-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="927f4-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="927f4-106">Prerequisites</span></span>

1. <span data-ttu-id="927f4-107">Nainstalujte jakoukoli edici sady Visual Studio 2017 nebo novější z [VisualStudio.com](https://www.visualstudio.com/) s libovolným. Zatížení související s NET.</span><span class="sxs-lookup"><span data-stu-id="927f4-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="927f4-108">Visual Studio 2017 a vyšší automaticky zahrnují funkce NuGet při instalaci úlohy .NET.</span><span class="sxs-lookup"><span data-stu-id="927f4-108">Visual Studio 2017 and higher automatically include NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="927f4-109">Nainstalujte rozhraní `dotnet` příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="927f4-109">Install the `dotnet` CLI.</span></span>

   <span data-ttu-id="927f4-110">Pro rozhraní `dotnet` příkazového řádku, počínaje sadou Visual Studio 2017 `dotnet` , se rozhraní příkazového řádku automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.</span><span class="sxs-lookup"><span data-stu-id="927f4-110">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="927f4-111">V opačném případě nainstalujte rozhraní příkazového `dotnet` řádku, abyste získali [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="927f4-111">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="927f4-112">Rozhraní `dotnet` příkazového řádku je vyžadováno pro .NET Standard projekty, které používají [Formát sady SDK](../resources/check-project-format.md) (atribut sady SDK).</span><span class="sxs-lookup"><span data-stu-id="927f4-112">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="927f4-113">Výchozí šablona knihovny tříd v sadě Visual Studio 2017 a vyšší, která se používá v tomto článku, používá atribut SDK.</span><span class="sxs-lookup"><span data-stu-id="927f4-113">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="927f4-114">V tomto článku se doporučuje `dotnet` používat rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="927f4-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="927f4-115">I když můžete publikovat libovolný balíček NuGet pomocí rozhraní `nuget.exe` příkazového řádku, některé kroky v tomto článku jsou specifické pro projekty ve stylu sady SDK a rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="927f4-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="927f4-116">Rozhraní příkazového řádku NuGet. exe se používá pro [projekty, které nejsou ve stylu sady SDK](../resources/check-project-format.md) (obvykle .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="927f4-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="927f4-117">Pokud pracujete s projektem, který není typu SDK, postupujte podle pokynů v části [Vytvoření a publikování .NET Framework balíčku (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) pro vytvoření a publikování balíčku.</span><span class="sxs-lookup"><span data-stu-id="927f4-117">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="927f4-118">[Zaregistrujte si bezplatný účet na NuGet.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) , pokud ho ještě nemáte.</span><span class="sxs-lookup"><span data-stu-id="927f4-118">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="927f4-119">Když se vytvoří nový účet, pošle se potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="927f4-119">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="927f4-120">Než budete moct nahrát balíček, musíte účet potvrdit.</span><span class="sxs-lookup"><span data-stu-id="927f4-120">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="927f4-121">Vytvořit projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="927f4-121">Create a class library project</span></span>

<span data-ttu-id="927f4-122">Můžete použít existující .NET Standard projekt knihovny tříd pro kód, který chcete zabalit, nebo vytvořit jednoduchý, a to následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="927f4-122">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="927f4-123">V aplikaci Visual Studio zvolte **soubor > nový > projekt**, rozbalte uzel **Visual C# > .NET Standard** , vyberte šablonu knihovny tříd (.NET Standard), pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="927f4-123">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="927f4-124">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavit** , abyste se ujistili, že se projekt vytvořil správně.</span><span class="sxs-lookup"><span data-stu-id="927f4-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="927f4-125">Knihovna DLL se nachází ve složce ladění (nebo v případě, že tuto konfiguraci sestavíte místo toho).</span><span class="sxs-lookup"><span data-stu-id="927f4-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="927f4-126">V rámci skutečného balíčku NuGet samozřejmě implementujete spoustu užitečných funkcí, se kterými můžou sestavovat aplikace i ostatní.</span><span class="sxs-lookup"><span data-stu-id="927f4-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="927f4-127">Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostačující k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="927f4-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="927f4-128">I když chcete pro balíček použít nějaký funkční kód, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="927f4-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="927f4-129">Pokud nemáte důvod vybrat jinak, .NET Standard je upřednostňovaným cílem pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.</span><span class="sxs-lookup"><span data-stu-id="927f4-129">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="927f4-130">Konfigurovat vlastnosti balíčku</span><span class="sxs-lookup"><span data-stu-id="927f4-130">Configure package properties</span></span>

1. <span data-ttu-id="927f4-131">Klikněte pravým tlačítkem na projekt v Průzkumník řešení a zvolte příkaz nabídky **vlastnosti** a pak vyberte kartu **balíček** .</span><span class="sxs-lookup"><span data-stu-id="927f4-131">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="927f4-132">Karta **balíček** se zobrazí pouze pro projekty ve stylu sady SDK v aplikaci Visual Studio, obvykle .NET Standard nebo .NET Core Class projektů; Pokud cílíte na projekt bez sady SDK (obvykle .NET Framework), buď migrujte [projekt](../reference/migrate-packages-config-to-package-reference.md) a použijte `dotnet` rozhraní příkazového řádku, nebo si přečtěte téma [Vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) nebo téma [Vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) . místo toho, abyste mohli postupovat podle pokynů.</span><span class="sxs-lookup"><span data-stu-id="927f4-132">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Vlastnosti balíčku NuGet v projektu Visual studia](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="927f4-134">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **značek** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.</span><span class="sxs-lookup"><span data-stu-id="927f4-134">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="927f4-135">Dejte balíčku jedinečný identifikátor a vyplňte všechny požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="927f4-135">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="927f4-136">Popis různých vlastností naleznete v tématu [Reference k souboru. nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="927f4-136">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="927f4-137">Všechny vlastnosti zde přejdou do `.nuspec` manifestu, který Visual Studio vytvoří pro projekt.</span><span class="sxs-lookup"><span data-stu-id="927f4-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="927f4-138">Balíčku musíte dát identifikátor, který je jedinečný v rámci nuget.org nebo libovolného hostitele, který používáte.</span><span class="sxs-lookup"><span data-stu-id="927f4-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="927f4-139">Pro tento návod doporučujeme, abyste v názvu jako pozdější krok publikování použili "Sample" nebo "test", aby byl balíček veřejně viditelný (i když je to nepravděpodobné, že ho kdokoli bude používat).</span><span class="sxs-lookup"><span data-stu-id="927f4-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="927f4-140">Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="927f4-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="927f4-141">Volitelné: Chcete-li zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem myši na projekt v Průzkumník řešení a vyberte **Upravit AppLogger. csproj**.</span><span class="sxs-lookup"><span data-stu-id="927f4-141">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="927f4-142">Tato možnost je k dispozici pouze od začátku v sadě Visual Studio 2017 pro projekty, které používají atribut Style sady SDK.</span><span class="sxs-lookup"><span data-stu-id="927f4-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="927f4-143">V opačném případě klikněte pravým tlačítkem myši na projekt a vyberte **Uvolnit projekt**.</span><span class="sxs-lookup"><span data-stu-id="927f4-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="927f4-144">Pak klikněte pravým tlačítkem na uvolněný projekt a zvolte **Upravit AppLogger. csproj**.</span><span class="sxs-lookup"><span data-stu-id="927f4-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="927f4-145">Spuštění příkazu Pack</span><span class="sxs-lookup"><span data-stu-id="927f4-145">Run the pack command</span></span>

1. <span data-ttu-id="927f4-146">Nastavte konfiguraci na **release**.</span><span class="sxs-lookup"><span data-stu-id="927f4-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="927f4-147">Klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a vyberte příkaz **Pack** :</span><span class="sxs-lookup"><span data-stu-id="927f4-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Příkaz NuGet Pack v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="927f4-149">Pokud nevidíte příkaz **Pack** , projekt pravděpodobně není projekt ve stylu sady SDK a je nutné použít rozhraní `nuget.exe` příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="927f4-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="927f4-150">Buď [migrujte projekt](../reference/migrate-packages-config-to-package-reference.md) a použijte `dotnet` rozhraní příkazového řádku, nebo si přečtěte článek [Vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.</span><span class="sxs-lookup"><span data-stu-id="927f4-150">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="927f4-151">Visual Studio vytvoří projekt a vytvoří `.nupkg` soubor.</span><span class="sxs-lookup"><span data-stu-id="927f4-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="927f4-152">Projděte si podrobnosti v okně **výstup** (podobně jako v následujícím příkladu), který obsahuje cestu k souboru balíčku.</span><span class="sxs-lookup"><span data-stu-id="927f4-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="927f4-153">Všimněte si také, že sestavené sestavení `bin\Release\netstandard2.0` je v podobě befits na cíl .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="927f4-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="927f4-154">Alternativní možnost: sada s MSBuild</span><span class="sxs-lookup"><span data-stu-id="927f4-154">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="927f4-155">Jako alternativu k použití příkazu nabídky **Pack** , NuGet 4. x + a MSBuild 15.1 + podporuje `pack` cíl, když projekt obsahuje potřebná data balíčku.</span><span class="sxs-lookup"><span data-stu-id="927f4-155">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="927f4-156">Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="927f4-156">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="927f4-157">(Obvykle chcete spustit "Developer Command Prompt pro Visual Studio" z nabídky Start, protože se nakonfiguruje se všemi nezbytnými cestami pro MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="927f4-157">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="927f4-158">Balíček se pak dá najít ve `bin\Release` složce.</span><span class="sxs-lookup"><span data-stu-id="927f4-158">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="927f4-159">Další možnosti s `msbuild -t:pack`najdete v tématu [sada NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="927f4-159">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="927f4-160">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="927f4-160">Publish the package</span></span>

<span data-ttu-id="927f4-161">Jakmile budete mít `.nupkg` soubor, publikujete ho v NuGet.org pomocí rozhraní `nuget.exe` příkazového řádku nebo `dotnet.exe` rozhraní příkazového řádku spolu s klíčem rozhraní API získaným z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="927f4-161">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="927f4-162">Získání klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="927f4-162">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="927f4-163">Publikování pomocí příkazu dotnet NuGet push (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="927f4-163">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="927f4-164">Tento krok je doporučenou alternativou použití `nuget.exe`nástroje.</span><span class="sxs-lookup"><span data-stu-id="927f4-164">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="927f4-165">Než budete moct balíček publikovat, musíte nejdřív otevřít příkazový řádek.</span><span class="sxs-lookup"><span data-stu-id="927f4-165">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="927f4-166">Publikování pomocí Push NuGet (NuGet. exe CLI)</span><span class="sxs-lookup"><span data-stu-id="927f4-166">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="927f4-167">Tento krok je alternativou k použití `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="927f4-167">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="927f4-168">Otevřete příkazový řádek a přejděte do složky, která obsahuje `.nupkg` soubor.</span><span class="sxs-lookup"><span data-stu-id="927f4-168">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="927f4-169">Spusťte následující příkaz, zadáním názvu balíčku (jedinečné ID balíčku) a nahrazením hodnoty klíče klíčem rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="927f4-169">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="927f4-170">NuGet. exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="927f4-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="927f4-171">Viz [push NuGet](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="927f4-171">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="927f4-172">Chyby publikování</span><span class="sxs-lookup"><span data-stu-id="927f4-172">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="927f4-173">Správa publikovaného balíčku</span><span class="sxs-lookup"><span data-stu-id="927f4-173">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="927f4-174">Přidání souboru Readme a dalších souborů</span><span class="sxs-lookup"><span data-stu-id="927f4-174">Adding a readme and other files</span></span>

<span data-ttu-id="927f4-175">Chcete-li přímo určit soubory, které mají být zahrnuty do balíčku, upravte soubor projektu `content` a použijte vlastnost:</span><span class="sxs-lookup"><span data-stu-id="927f4-175">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="927f4-176">Tato akce bude obsahovat soubor s `readme.txt` názvem v kořenovém adresáři balíčku.</span><span class="sxs-lookup"><span data-stu-id="927f4-176">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="927f4-177">Sada Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="927f4-177">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="927f4-178">(Soubory Readme se nezobrazí pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="927f4-178">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="927f4-179">Tady je příklad, jak se zobrazí soubor Readme pro balíček HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="927f4-179">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazení souboru Readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="927f4-181">Pouze přidání souboru Readme. txt v kořenu projektu nebude mít za následek zahrnutí do výsledného balíčku.</span><span class="sxs-lookup"><span data-stu-id="927f4-181">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="927f4-182">Související témata</span><span class="sxs-lookup"><span data-stu-id="927f4-182">Related topics</span></span>

- [<span data-ttu-id="927f4-183">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="927f4-183">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="927f4-184">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="927f4-184">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="927f4-185">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="927f4-185">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="927f4-186">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="927f4-186">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="927f4-187">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="927f4-187">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="927f4-188">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="927f4-188">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="927f4-189">Dokumentace ke knihovně .NET Standard</span><span class="sxs-lookup"><span data-stu-id="927f4-189">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="927f4-190">Přenos do .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="927f4-190">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
