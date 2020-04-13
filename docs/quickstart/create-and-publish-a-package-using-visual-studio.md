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
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="63d18-103">Úvodní příručka: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (Standard.NET, jenom windows)</span><span class="sxs-lookup"><span data-stu-id="63d18-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="63d18-104">Je to jednoduchý proces k vytvoření balíčku NuGet z knihovny tříd .NET Standard v sadě Visual Studio v systému Windows a potom publikovat do nuget.org pomocí nástroje rozhraní rozhraní se kšak obc.</span><span class="sxs-lookup"><span data-stu-id="63d18-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="63d18-105">Pokud používáte Visual Studio for Mac, podívejte se na [tyto informace](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) o vytvoření balíčku NuGet nebo použijte [nástroje dotnet CLI](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="63d18-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63d18-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="63d18-106">Prerequisites</span></span>

1. <span data-ttu-id="63d18-107">Nainstalujte libovolnou edici Visual Studia 2019 z [visualstudio.com](https://www.visualstudio.com/) s úlohou související s jádrem .NET.</span><span class="sxs-lookup"><span data-stu-id="63d18-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="63d18-108">Pokud ještě není nainstalován, nainstalujte cli. `dotnet`</span><span class="sxs-lookup"><span data-stu-id="63d18-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="63d18-109">Pro `dotnet` rozhraní se konkretním rozhraním, počínaje Visual Studio 2017, `dotnet` rozhraní se automaticky nainstaluje s libovolnými úlohami souvisejícími s jádrem .NET Core.</span><span class="sxs-lookup"><span data-stu-id="63d18-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="63d18-110">V opačném případě nainstalujte sadu [.NET Core SDK,](https://www.microsoft.com/net/download/) abyste získali rozhraní se konzumního `dotnet` rozhraní.</span><span class="sxs-lookup"><span data-stu-id="63d18-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="63d18-111">Rozhraní `dotnet` příkazového příkazu je vyžadováno pro projekty .NET Standard, které používají [formát ve stylu sady SDK](../resources/check-project-format.md) (atribut SDK).</span><span class="sxs-lookup"><span data-stu-id="63d18-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="63d18-112">Výchozí šablona knihovny tříd .NET Standard v sadě Visual Studio 2017 a vyšší, která se používá v tomto článku, používá atribut SDK.</span><span class="sxs-lookup"><span data-stu-id="63d18-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="63d18-113">Pokud pracujete s projektem, který není ve stylu sady SDK, postupujte podle postupů v [části Vytvoření a publikování balíčku rozhraní .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) a vytvořte a publikujte balíček.</span><span class="sxs-lookup"><span data-stu-id="63d18-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="63d18-114">Pro tento článek `dotnet` je doporučeno zaokreslování.</span><span class="sxs-lookup"><span data-stu-id="63d18-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="63d18-115">I když můžete publikovat libovolný `nuget.exe` balíček NuGet pomocí rozhraní se konstatování, některé kroky v tomto článku jsou specifické pro projekty ve stylu sady SDK a rozhraní se konstatování dotnet.</span><span class="sxs-lookup"><span data-stu-id="63d18-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="63d18-116">Rozhraní CLI nuget.exe se používá pro [projekty, které nejsou ve stylu sady SDK](../resources/check-project-format.md) (obvykle rozhraní .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="63d18-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="63d18-117">[Zaregistrujte se zdarma účet na nuget.org,](../nuget-org/individual-accounts.md#add-a-new-individual-account) pokud nemáte ještě jeden.</span><span class="sxs-lookup"><span data-stu-id="63d18-117">[Register for a free account on nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="63d18-118">Vytvoření nového účtu odešle potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="63d18-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="63d18-119">Před nahráním balíčku musíte účet potvrdit.</span><span class="sxs-lookup"><span data-stu-id="63d18-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="63d18-120">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="63d18-120">Create a class library project</span></span>

<span data-ttu-id="63d18-121">Pro kód, který chcete zabalit, můžete použít existující projekt knihovny standardní třídy .NET nebo vytvořit jednoduchý:</span><span class="sxs-lookup"><span data-stu-id="63d18-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="63d18-122">V sadě Visual Studio zvolte **Soubor > Nový > Project**, rozbalte uzel Visual **C# > .NET Standard,** vyberte šablonu "Knihovna tříd (.NET Standard)", pojmenujte projekt AppLogger a klepněte na **tlačítko OK**.</span><span class="sxs-lookup"><span data-stu-id="63d18-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

   > [!Tip]
   > <span data-ttu-id="63d18-123">Pokud nemáte důvod zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.</span><span class="sxs-lookup"><span data-stu-id="63d18-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="63d18-124">Klikněte pravým tlačítkem myši na výsledný soubor projektu a vyberte **sestavení,** abyste se ujistili, že byl projekt vytvořen správně.</span><span class="sxs-lookup"><span data-stu-id="63d18-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="63d18-125">DLL se nachází ve složce Ladění (nebo verze, pokud vytvoříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="63d18-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="63d18-126">V rámci skutečného balíčku NuGet samozřejmě implementovat mnoho užitečných funkcí, s nimiž ostatní mohou vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="63d18-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="63d18-127">Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostatečná k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="63d18-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="63d18-128">Přesto, pokud chcete nějaký funkční kód pro balíček, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="63d18-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="63d18-129">Konfigurace vlastností balíčku</span><span class="sxs-lookup"><span data-stu-id="63d18-129">Configure package properties</span></span>

1. <span data-ttu-id="63d18-130">Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a zvolte Příkaz nabídky **Vlastnosti** a pak vyberte kartu **Balíček.**</span><span class="sxs-lookup"><span data-stu-id="63d18-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="63d18-131">Karta **Balíček** se zobrazí pouze pro projekty ve stylu sady SDK v sadě Visual Studio, obvykle .NET Standard nebo .NET Core projekty knihovny tříd; Pokud cílíte na projekt stylu sady SDK (obvykle rozhraní .NET Framework), [migrujte projekt](../consume-packages/migrate-packages-config-to-package-reference.md) nebo se podívejte [na tlačítko Vytvořit a publikovat balíček rozhraní .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.</span><span class="sxs-lookup"><span data-stu-id="63d18-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Vlastnosti balíčku NuGet v projektu sady Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="63d18-133">U balíčků vytvořených pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **Tags,** protože značky pomáhají ostatním najít váš balíček a pochopit, co dělá.</span><span class="sxs-lookup"><span data-stu-id="63d18-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="63d18-134">Podejte svému balíčku jedinečný identifikátor a vyplňte všechny ostatní požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="63d18-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="63d18-135">Mapování vlastností MSBuild (projekt ve stylu sady SDK) na vlastnosti v *souboru .nuspec*naleznete v [tématu cíle balíčku](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="63d18-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec*, see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="63d18-136">Popis vlastností naleznete v [odkazu na soubor .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="63d18-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="63d18-137">Všechny vlastnosti zde přejde do manifestu, `.nuspec` který vytvoří visual studio pro projekt.</span><span class="sxs-lookup"><span data-stu-id="63d18-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="63d18-138">Balíček je nutné poskytnout identifikátor, který je jedinečný v celé nuget.org nebo libovolného hostitele, který používáte.</span><span class="sxs-lookup"><span data-stu-id="63d18-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="63d18-139">Pro tento návod doporučujeme zahrnout "Ukázka" nebo "Test" v názvu jako pozdější krok publikování dělá balíček veřejně viditelné (i když je nepravděpodobné, že někdo bude skutečně používat).</span><span class="sxs-lookup"><span data-stu-id="63d18-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="63d18-140">Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="63d18-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="63d18-141">(Nepovinné) Chcete-li zobrazit vlastnosti přímo v souboru projektu, klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte **příkaz Upravit soubor AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="63d18-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="63d18-142">Tato možnost je k dispozici pouze od visual studia 2017 pro projekty, které používají atribut stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="63d18-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="63d18-143">V opačném případě klepněte pravým tlačítkem myši na projekt a zvolte **Uvolnit projekt**.</span><span class="sxs-lookup"><span data-stu-id="63d18-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="63d18-144">Potom klepněte pravým tlačítkem myši na nezatížený projekt a zvolte **Upravit AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="63d18-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="63d18-145">Spuštění příkazu pack</span><span class="sxs-lookup"><span data-stu-id="63d18-145">Run the pack command</span></span>

1. <span data-ttu-id="63d18-146">Nastavte konfiguraci na **Release**.</span><span class="sxs-lookup"><span data-stu-id="63d18-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="63d18-147">Klikněte pravým tlačítkem myši na projekt v **Průzkumníku řešení** a vyberte příkaz **Pack:**</span><span class="sxs-lookup"><span data-stu-id="63d18-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Příkaz NuGet pack v kontextové nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="63d18-149">Pokud nevidíte **pack** příkaz, váš projekt pravděpodobně není projekt ve stylu SDK `nuget.exe` a je třeba použít příkaz příkazového příkazového příkazu.</span><span class="sxs-lookup"><span data-stu-id="63d18-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="63d18-150">Buď [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) `dotnet` projekt a použijte rozhraní příkazového příkazového příkazu, nebo najdete [v tématu Vytvoření a publikování balíčku rozhraní .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) pro podrobné pokyny.</span><span class="sxs-lookup"><span data-stu-id="63d18-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="63d18-151">Visual Studio vytvoří projekt a `.nupkg` vytvoří soubor.</span><span class="sxs-lookup"><span data-stu-id="63d18-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="63d18-152">Zkontrolujte **okno Výstup** pro podrobnosti (podobně jako následující), který obsahuje cestu k souboru balíčku.</span><span class="sxs-lookup"><span data-stu-id="63d18-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="63d18-153">Všimněte si také, `bin\Release\netstandard2.0` že sestavené sestavení je v, jak se sluší na cíl .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="63d18-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="63d18-154">(Nepovinné) Generovat balíček při sestavení</span><span class="sxs-lookup"><span data-stu-id="63d18-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="63d18-155">Visual Studio můžete nakonfigurovat tak, aby automaticky generovalo balíček NuGet při vytváření projektu.</span><span class="sxs-lookup"><span data-stu-id="63d18-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="63d18-156">V Průzkumníku řešení klepněte pravým tlačítkem myši na projekt a zvolte **Vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="63d18-156">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="63d18-157">Na kartě **Balíček** vyberte **Generovat balíček NuGet při sestavení**.</span><span class="sxs-lookup"><span data-stu-id="63d18-157">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![Automaticky generovat balíček při sestavení](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="63d18-159">Při automatickém generování balíčku čas balení zvyšuje dobu sestavení pro váš projekt.</span><span class="sxs-lookup"><span data-stu-id="63d18-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="63d18-160">(Volitelné) balení s MSBuild</span><span class="sxs-lookup"><span data-stu-id="63d18-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="63d18-161">Jako alternativu k použití příkazu nabídky **Pack** NuGet 4.x+ a MSBuild 15.1+ podporuje `pack` cíl, když projekt obsahuje potřebná data balíčku.</span><span class="sxs-lookup"><span data-stu-id="63d18-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="63d18-162">Otevřete příkazový řádek, přejděte do složky projektu a spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="63d18-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="63d18-163">(Obvykle chcete spustit "Příkazový řádek pro vývojáře pro Visual Studio" z nabídky Start, protože bude nakonfigurován se všemi potřebnými cestami pro MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="63d18-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="63d18-164">Další informace naleznete [v tématu Vytvoření balíčku pomocí msbuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="63d18-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="63d18-165">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="63d18-165">Publish the package</span></span>

<span data-ttu-id="63d18-166">Jakmile máte `.nupkg` soubor, publikujete jej nuget.org `nuget.exe` pomocí rozhraní `dotnet.exe` se kli nebo rozhraní se klisy spolu s klíčem rozhraní API získaného z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="63d18-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="63d18-167">Získání klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="63d18-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="63d18-168">Publikovat pomocí rozhraní SE koncli dotnet nebo nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="63d18-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="63d18-169">Vyberte kartu pro nástroj příkazového příkazového příkazového příkazu, buď **rozhraní .NET Core CLI** (dotnet CLI) nebo **NuGet** (nuget.exe CLI).</span><span class="sxs-lookup"><span data-stu-id="63d18-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-cli"></a>[<span data-ttu-id="63d18-170">Rozhraní příkazového řádku .NET Core</span><span class="sxs-lookup"><span data-stu-id="63d18-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="63d18-171">Tento krok je doporučenou `nuget.exe`alternativou k použití .</span><span class="sxs-lookup"><span data-stu-id="63d18-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="63d18-172">Před publikováním balíčku je nutné nejprve otevřít příkazový řádek.</span><span class="sxs-lookup"><span data-stu-id="63d18-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[<span data-ttu-id="63d18-173">NuGet</span><span class="sxs-lookup"><span data-stu-id="63d18-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="63d18-174">Tento krok je alternativou k použití `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="63d18-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="63d18-175">Otevřete příkazový řádek a změňte `.nupkg` na složku obsahující soubor.</span><span class="sxs-lookup"><span data-stu-id="63d18-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="63d18-176">Spusťte následující příkaz, zadejte název balíčku (jedinečné ID balíčku) a nahraďte hodnotu klíče klíčem rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="63d18-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="63d18-177">nuget.exe zobrazí výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="63d18-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="63d18-178">Viz [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="63d18-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="63d18-179">Chyby publikování</span><span class="sxs-lookup"><span data-stu-id="63d18-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="63d18-180">Správa publikovaného balíčku</span><span class="sxs-lookup"><span data-stu-id="63d18-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="63d18-181">Přidání souboru readme a dalších souborů</span><span class="sxs-lookup"><span data-stu-id="63d18-181">Adding a readme and other files</span></span>

<span data-ttu-id="63d18-182">Chcete-li přímo určit soubory, které mají být `content` zahrnuty do balíčku, upravte soubor projektu a použijte vlastnost:</span><span class="sxs-lookup"><span data-stu-id="63d18-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="63d18-183">To bude obsahovat `readme.txt` soubor pojmenovaný v kořenovém adresáři balíčku.</span><span class="sxs-lookup"><span data-stu-id="63d18-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="63d18-184">Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="63d18-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="63d18-185">(Soubory Readme se nezobrazují pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="63d18-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="63d18-186">Například zde je návod, jak se zobrazí readme pro balíček HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="63d18-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazení souboru readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="63d18-188">Pouhé přidání souboru readme.txt v kořenovém adresáři projektu nepovede k jeho zahrnutí do výsledného balíčku.</span><span class="sxs-lookup"><span data-stu-id="63d18-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-video"></a><span data-ttu-id="63d18-189">Související video</span><span class="sxs-lookup"><span data-stu-id="63d18-189">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

<span data-ttu-id="63d18-190">Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="63d18-190">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="related-topics"></a><span data-ttu-id="63d18-191">Související témata</span><span class="sxs-lookup"><span data-stu-id="63d18-191">Related topics</span></span>

- [<span data-ttu-id="63d18-192">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="63d18-192">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="63d18-193">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="63d18-193">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="63d18-194">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="63d18-194">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="63d18-195">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="63d18-195">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="63d18-196">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="63d18-196">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="63d18-197">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="63d18-197">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="63d18-198">Dokumentace standardní knihovny .NET</span><span class="sxs-lookup"><span data-stu-id="63d18-198">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="63d18-199">Přenesení na jádro .NET z rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="63d18-199">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
