---
title: Vytvoření a publikování .NET Standard balíčku NuGet – Visual Studio ve Windows
description: Návod k vytvoření a publikování .NET Standard balíčku NuGet pomocí sady Visual Studio ve Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231289"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="ae25e-103">Rychlý Start: vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (.NET Standard, pouze Windows)</span><span class="sxs-lookup"><span data-stu-id="ae25e-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="ae25e-104">Je to jednoduchý proces vytvoření balíčku NuGet z knihovny tříd .NET Standard v aplikaci Visual Studio ve Windows a jeho následné publikování na nuget.org pomocí nástroje CLI.</span><span class="sxs-lookup"><span data-stu-id="ae25e-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="ae25e-105">Pokud používáte Visual Studio pro Mac, přečtěte si [tyto informace](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) o vytvoření balíčku NuGet nebo použijte [nástroje dotnet CLI](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ae25e-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae25e-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ae25e-106">Prerequisites</span></span>

1. <span data-ttu-id="ae25e-107">Nainstalujte jakoukoli edici sady Visual Studio 2019 z [VisualStudio.com](https://www.visualstudio.com/) s využitím úlohy související s .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ae25e-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="ae25e-108">Pokud ještě není nainstalovaná, nainstalujte `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="ae25e-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="ae25e-109">Pro `dotnet` CLI počínaje sadou Visual Studio 2017 se `dotnet` CLI automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ae25e-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="ae25e-110">V opačném případě nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/) pro získání `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="ae25e-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="ae25e-111">`dotnet` CLI je vyžadován pro .NET Standard projekty, které používají [Formát sady SDK](../resources/check-project-format.md) (atribut sady SDK).</span><span class="sxs-lookup"><span data-stu-id="ae25e-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="ae25e-112">Výchozí .NET Standard šablona knihovny tříd v sadě Visual Studio 2017 a vyšší, která se používá v tomto článku, používá atribut SDK.</span><span class="sxs-lookup"><span data-stu-id="ae25e-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="ae25e-113">Pokud pracujete s projektem, který není typu SDK, postupujte podle pokynů v části [Vytvoření a publikování .NET Frameworkho balíčku (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) pro vytvoření a publikování balíčku.</span><span class="sxs-lookup"><span data-stu-id="ae25e-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="ae25e-114">V tomto článku se doporučuje `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="ae25e-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="ae25e-115">I když můžete publikovat libovolný balíček NuGet pomocí `nuget.exe` CLI, některé kroky v tomto článku jsou specifické pro projekty ve stylu sady SDK a rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="ae25e-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="ae25e-116">Rozhraní příkazového řádku NuGet. exe se používá pro [projekty, které nejsou ve stylu sady SDK](../resources/check-project-format.md) (obvykle .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="ae25e-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="ae25e-117">[Zaregistrujte si bezplatný účet na NuGet.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) , pokud ho ještě nemáte.</span><span class="sxs-lookup"><span data-stu-id="ae25e-117">[Register for a free account on nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="ae25e-118">Když se vytvoří nový účet, pošle se potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="ae25e-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="ae25e-119">Než budete moct nahrát balíček, musíte účet potvrdit.</span><span class="sxs-lookup"><span data-stu-id="ae25e-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="ae25e-120">Vytvořit projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="ae25e-120">Create a class library project</span></span>

<span data-ttu-id="ae25e-121">Můžete použít existující .NET Standard projekt knihovny tříd pro kód, který chcete zabalit, nebo vytvořit jednoduchý, a to následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="ae25e-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="ae25e-122">V aplikaci Visual Studio zvolte **soubor > nový > projekt**, rozbalte uzel **Visual C# > .NET Standard** , vyberte šablonu knihovny tříd (.NET Standard), pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae25e-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

   > [!Tip]
   > <span data-ttu-id="ae25e-123">Pokud nemáte důvod vybrat jinak, .NET Standard je upřednostňovaným cílem pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.</span><span class="sxs-lookup"><span data-stu-id="ae25e-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="ae25e-124">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavit** , abyste se ujistili, že se projekt vytvořil správně.</span><span class="sxs-lookup"><span data-stu-id="ae25e-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="ae25e-125">Knihovna DLL se nachází ve složce ladění (nebo v případě, že tuto konfiguraci sestavíte místo toho).</span><span class="sxs-lookup"><span data-stu-id="ae25e-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="ae25e-126">V rámci skutečného balíčku NuGet samozřejmě implementujete spoustu užitečných funkcí, se kterými můžou sestavovat aplikace i ostatní.</span><span class="sxs-lookup"><span data-stu-id="ae25e-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="ae25e-127">Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostačující k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="ae25e-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="ae25e-128">I když chcete pro balíček použít nějaký funkční kód, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="ae25e-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="ae25e-129">Konfigurovat vlastnosti balíčku</span><span class="sxs-lookup"><span data-stu-id="ae25e-129">Configure package properties</span></span>

1. <span data-ttu-id="ae25e-130">Klikněte pravým tlačítkem na projekt v Průzkumník řešení a zvolte příkaz nabídky **vlastnosti** a pak vyberte kartu **balíček** .</span><span class="sxs-lookup"><span data-stu-id="ae25e-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="ae25e-131">Karta **balíček** se zobrazí pouze pro projekty ve stylu sady SDK v aplikaci Visual Studio, obvykle .NET Standard nebo .NET Core Class projektů; Pokud cílíte na jiný projekt než sadu SDK (obvykle .NET Framework), buď [migrujte projekt](../consume-packages/migrate-packages-config-to-package-reference.md) , nebo si přečtěte téma [vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.</span><span class="sxs-lookup"><span data-stu-id="ae25e-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Vlastnosti balíčku NuGet v projektu Visual studia](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="ae25e-133">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **značek** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.</span><span class="sxs-lookup"><span data-stu-id="ae25e-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="ae25e-134">Dejte balíčku jedinečný identifikátor a vyplňte všechny požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="ae25e-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="ae25e-135">Mapování vlastností MSBuild (projekt ve stylu sady SDK) na vlastnosti v *. nuspec*naleznete v tématu [cíle balíčku](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="ae25e-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec*, see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="ae25e-136">Popisy vlastností naleznete v [souboru. nuspec reference](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ae25e-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="ae25e-137">Všechny vlastnosti zde přejdou do `.nuspec` manifestu, který Visual Studio vytvoří pro projekt.</span><span class="sxs-lookup"><span data-stu-id="ae25e-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="ae25e-138">Balíčku musíte dát identifikátor, který je jedinečný v rámci nuget.org nebo libovolného hostitele, který používáte.</span><span class="sxs-lookup"><span data-stu-id="ae25e-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="ae25e-139">Pro tento návod doporučujeme, abyste v názvu jako pozdější krok publikování použili "Sample" nebo "test", aby byl balíček veřejně viditelný (i když je to nepravděpodobné, že ho kdokoli bude používat).</span><span class="sxs-lookup"><span data-stu-id="ae25e-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="ae25e-140">Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="ae25e-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="ae25e-141">Volitelné Chcete-li zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem myši na projekt v Průzkumník řešení a vyberte **Upravit AppLogger. csproj**.</span><span class="sxs-lookup"><span data-stu-id="ae25e-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="ae25e-142">Tato možnost je k dispozici pouze od začátku v sadě Visual Studio 2017 pro projekty, které používají atribut Style sady SDK.</span><span class="sxs-lookup"><span data-stu-id="ae25e-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="ae25e-143">V opačném případě klikněte pravým tlačítkem myši na projekt a vyberte **Uvolnit projekt**.</span><span class="sxs-lookup"><span data-stu-id="ae25e-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="ae25e-144">Pak klikněte pravým tlačítkem na uvolněný projekt a zvolte **Upravit AppLogger. csproj**.</span><span class="sxs-lookup"><span data-stu-id="ae25e-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="ae25e-145">Spuštění příkazu Pack</span><span class="sxs-lookup"><span data-stu-id="ae25e-145">Run the pack command</span></span>

1. <span data-ttu-id="ae25e-146">Nastavte konfiguraci na **release**.</span><span class="sxs-lookup"><span data-stu-id="ae25e-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="ae25e-147">Klikněte pravým tlačítkem na projekt v **Průzkumník řešení** a vyberte příkaz **Pack** :</span><span class="sxs-lookup"><span data-stu-id="ae25e-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Příkaz NuGet Pack v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="ae25e-149">Pokud nevidíte příkaz **Pack** , projekt pravděpodobně není projekt ve stylu sady SDK a je nutné použít `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="ae25e-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="ae25e-150">Buď [migrujte projekt](../consume-packages/migrate-packages-config-to-package-reference.md) a použijte `dotnet` CLI, nebo si přečtěte článek [vytvoření a publikování .NET Framework balíčku](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.</span><span class="sxs-lookup"><span data-stu-id="ae25e-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="ae25e-151">Visual Studio vytvoří projekt a vytvoří soubor `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ae25e-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="ae25e-152">Projděte si podrobnosti v okně **výstup** (podobně jako v následujícím příkladu), který obsahuje cestu k souboru balíčku.</span><span class="sxs-lookup"><span data-stu-id="ae25e-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="ae25e-153">Všimněte si také, že sestavené sestavení je v `bin\Release\netstandard2.0` jako befits na cíl .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="ae25e-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="ae25e-154">Volitelné Generovat balíček při sestavení</span><span class="sxs-lookup"><span data-stu-id="ae25e-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="ae25e-155">Sadu Visual Studio můžete nakonfigurovat tak, aby automaticky generovala balíček NuGet při sestavování projektu.</span><span class="sxs-lookup"><span data-stu-id="ae25e-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="ae25e-156">V Průzkumník řešení klikněte pravým tlačítkem na projekt a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="ae25e-156">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="ae25e-157">Na kartě **balíček** vyberte při **sestavování vytvořit balíček NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ae25e-157">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![Automaticky generovat balíček při sestavení](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="ae25e-159">Když balíček automaticky vygenerujete, čas k zabalení zvýší čas sestavení pro váš projekt.</span><span class="sxs-lookup"><span data-stu-id="ae25e-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="ae25e-160">(Nepovinný) Pack s nástrojem MSBuild</span><span class="sxs-lookup"><span data-stu-id="ae25e-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="ae25e-161">Jako alternativu k použití příkazu nabídky **Pack** , NuGet 4. x + a MSBuild 15.1 + podporuje cíl `pack`, když projekt obsahuje potřebná data balíčku.</span><span class="sxs-lookup"><span data-stu-id="ae25e-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="ae25e-162">Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="ae25e-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="ae25e-163">(Obvykle chcete spustit "Developer Command Prompt pro Visual Studio" z nabídky Start, protože se nakonfiguruje se všemi nezbytnými cestami pro MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="ae25e-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="ae25e-164">Další informace najdete v tématu [Vytvoření balíčku pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="ae25e-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="ae25e-165">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="ae25e-165">Publish the package</span></span>

<span data-ttu-id="ae25e-166">Jakmile budete mít soubor `.nupkg`, publikujete ho nuget.org pomocí `nuget.exe` CLI nebo rozhraní příkazového řádku `dotnet.exe` spolu s klíčem rozhraní API získaným z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ae25e-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="ae25e-167">Získání klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="ae25e-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="ae25e-168">Publikování pomocí rozhraní příkazového řádku dotnet nebo NuGet. exe CLI</span><span class="sxs-lookup"><span data-stu-id="ae25e-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="ae25e-169">Vyberte kartu pro nástroj CLI, buď **.NET Core CLI** (dotnet CLI), nebo **NuGet** (NuGet. exe CLI).</span><span class="sxs-lookup"><span data-stu-id="ae25e-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-cli"></a>[<span data-ttu-id="ae25e-170">Rozhraní příkazového řádku .NET Core</span><span class="sxs-lookup"><span data-stu-id="ae25e-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="ae25e-171">Tento krok je doporučenou alternativou použití `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ae25e-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="ae25e-172">Než budete moct balíček publikovat, musíte nejdřív otevřít příkazový řádek.</span><span class="sxs-lookup"><span data-stu-id="ae25e-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[<span data-ttu-id="ae25e-173">NuGet</span><span class="sxs-lookup"><span data-stu-id="ae25e-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="ae25e-174">Tento krok je alternativou k použití `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="ae25e-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="ae25e-175">Otevřete příkazový řádek a přejděte do složky, která obsahuje soubor `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ae25e-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="ae25e-176">Spusťte následující příkaz, zadáním názvu balíčku (jedinečné ID balíčku) a nahrazením hodnoty klíče klíčem rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="ae25e-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="ae25e-177">NuGet. exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="ae25e-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="ae25e-178">Viz [push NuGet](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="ae25e-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="ae25e-179">Chyby publikování</span><span class="sxs-lookup"><span data-stu-id="ae25e-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="ae25e-180">Správa publikovaného balíčku</span><span class="sxs-lookup"><span data-stu-id="ae25e-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="ae25e-181">Přidání souboru Readme a dalších souborů</span><span class="sxs-lookup"><span data-stu-id="ae25e-181">Adding a readme and other files</span></span>

<span data-ttu-id="ae25e-182">Chcete-li přímo určit soubory, které mají být zahrnuty do balíčku, upravte soubor projektu a použijte vlastnost `content`:</span><span class="sxs-lookup"><span data-stu-id="ae25e-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="ae25e-183">Tato akce zahrne do kořenového adresáře balíčku soubor s názvem `readme.txt`.</span><span class="sxs-lookup"><span data-stu-id="ae25e-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="ae25e-184">Sada Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="ae25e-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="ae25e-185">(Soubory Readme se nezobrazí pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="ae25e-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="ae25e-186">Tady je příklad, jak se zobrazí soubor Readme pro balíček HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="ae25e-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazení souboru Readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="ae25e-188">Pouze přidání souboru Readme. txt v kořenu projektu nebude mít za následek zahrnutí do výsledného balíčku.</span><span class="sxs-lookup"><span data-stu-id="ae25e-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-video"></a><span data-ttu-id="ae25e-189">Související video</span><span class="sxs-lookup"><span data-stu-id="ae25e-189">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

<span data-ttu-id="ae25e-190">Další videa k NuGetu najdete na webu [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="ae25e-190">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="related-topics"></a><span data-ttu-id="ae25e-191">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="ae25e-191">Related topics</span></span>

- [<span data-ttu-id="ae25e-192">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="ae25e-192">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="ae25e-193">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="ae25e-193">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="ae25e-194">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="ae25e-194">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="ae25e-195">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="ae25e-195">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="ae25e-196">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="ae25e-196">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="ae25e-197">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="ae25e-197">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ae25e-198">Dokumentace ke knihovně .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ae25e-198">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="ae25e-199">Přenos do .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ae25e-199">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
