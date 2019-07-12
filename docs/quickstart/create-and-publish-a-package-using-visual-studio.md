---
title: Vytvoření a publikování balíčku .NET Standard ve Windows pomocí sady Visual Studio
description: Kurz návod týkající se vytváření a publikování balíčku .NET Standard NuGet pomocí sady Visual Studio na Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: d9eccfa373a5a283542fd158e76ba74b1872f3d6
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842152"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="4518c-103">Rychlý start: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (.NET Standard, jenom Windows)</span><span class="sxs-lookup"><span data-stu-id="4518c-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="4518c-104">Je jednoduchý proces vytvoření balíčku NuGet z knihovny .NET Standard třídy v sadě Visual Studio ve Windows a potom ji publikovat na nuget.org pomocí nástroje příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="4518c-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="4518c-105">Pokud používáte Visual Studio pro Mac, podívejte se na [tyto informace](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) vytvoření balíčku NuGet, nebo použít [nástroje rozhraní příkazového řádku dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4518c-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4518c-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4518c-106">Prerequisites</span></span>

1. <span data-ttu-id="4518c-107">Instalaci libovolné edice sady Visual Studio 2017 nebo novější z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy.</span><span class="sxs-lookup"><span data-stu-id="4518c-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="4518c-108">Visual Studio 2017 a vyšší automaticky zahrnují možnosti NuGet, když je nainstalovaná úloha .NET.</span><span class="sxs-lookup"><span data-stu-id="4518c-108">Visual Studio 2017 and higher automatically include NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="4518c-109">Nainstalujte `dotnet` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="4518c-109">Install the `dotnet` CLI.</span></span>

   <span data-ttu-id="4518c-110">Pro `dotnet` rozhraní příkazového řádku, spouští se v sadě Visual Studio 2017 `dotnet` rozhraní příkazového řádku je automaticky nainstalován se sadou jakékoli .NET Core související úlohy.</span><span class="sxs-lookup"><span data-stu-id="4518c-110">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="4518c-111">V opačném případě nainstalovat [.NET Core SDK](https://www.microsoft.com/net/download/) zobrazíte `dotnet` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="4518c-111">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="4518c-112">`dotnet` Je vyžadován pro .NET Standard projekty, které používají rozhraní příkazového řádku [SDK – vizuální styl formátu](../resources/check-project-format.md) (atribut SDK).</span><span class="sxs-lookup"><span data-stu-id="4518c-112">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="4518c-113">Výchozí šablona knihovny tříd v sadě Visual Studio 2017 a novější, který se používá v tomto článku, používá atribut SDK.</span><span class="sxs-lookup"><span data-stu-id="4518c-113">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="4518c-114">Pro účely tohoto článku `dotnet` se doporučuje rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="4518c-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="4518c-115">I když můžete publikovat jakékoli pomocí balíčku NuGet `nuget.exe` rozhraní příkazového řádku, některé kroky v tomto článku jsou specifické pro projekty založenými na sadě SDK a rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="4518c-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="4518c-116">Nuget.exe rozhraní příkazového řádku se používá pro [SDK styl projekty](../resources/check-project-format.md) (obvykle rozhraní .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="4518c-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="4518c-117">Pokud pracujete s projektem sada SDK styl, postupujte podle pokynů v [vytvoření a publikování balíčku .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) vytvoření a publikování balíčku.</span><span class="sxs-lookup"><span data-stu-id="4518c-117">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="4518c-118">[Zaregistrujte si bezplatný účet na nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="4518c-118">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="4518c-119">Vytvoření nového účtu se odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="4518c-119">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="4518c-120">Účet musí ověřit dříve, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="4518c-120">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="4518c-121">Vytvořte projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="4518c-121">Create a class library project</span></span>

<span data-ttu-id="4518c-122">Můžete použít existující projekt knihovna tříd rozhraní .NET Standard pro kód, který chcete balíček nebo vytvořit jednoduchý následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="4518c-122">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="4518c-123">V sadě Visual Studio, zvolte **soubor > Nový > projekt**, rozbalte **Visual C# > .NET Standard** uzlu, vyberte šablonu "Knihovna tříd (.NET Standard)", pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="4518c-123">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="4518c-124">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** k Ujistěte se, že projekt je vytvořený řádně.</span><span class="sxs-lookup"><span data-stu-id="4518c-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="4518c-125">Knihovny DLL se nachází složka pro ladění (nebo vydání, pokud vytváříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="4518c-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="4518c-126">V rámci skutečné balíčku NuGet samozřejmě, můžete implementovat mnoho užitečných funkcí, se kterými ostatní můžete vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="4518c-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="4518c-127">V tomto návodu ale nebude napíšete žádný další kód vzhledem k tomu, že knihovna tříd z této šablony je dostatečná pro vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="4518c-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="4518c-128">Pokud chcete některé funkční kód pro balíček, stále, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="4518c-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="4518c-129">Pokud nemáte důvod nerozhodnete jinak, .NET Standard je upřednostňovaným cílem, pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projektů.</span><span class="sxs-lookup"><span data-stu-id="4518c-129">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="4518c-130">Konfigurace vlastností balíčku</span><span class="sxs-lookup"><span data-stu-id="4518c-130">Configure package properties</span></span>

1. <span data-ttu-id="4518c-131">Klikněte pravým tlačítkem na projekt v Průzkumníku řešení a zvolte **vlastnosti** nabídce příkaz a pak vyberte **balíčku** kartu.</span><span class="sxs-lookup"><span data-stu-id="4518c-131">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="4518c-132">**Balíčku** kartě se zobrazí pouze pro projekty založenými na sadě SDK v sadě Visual Studio, obvykle .NET Standard nebo projekty knihovny tříd .NET Core, pokud cílíte na styl projektu – sada SDK (obvykle rozhraní .NET Framework), buď [ Projekt migrovat,](../reference/migrate-packages-config-to-package-reference.md) a používat `dotnet` rozhraní příkazového řádku, nebo naleznete v tématu [vytvoření a publikování balíčku .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) nebo naleznete v tématu [vytvoření a publikování balíčku .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) místo toho pro podrobné pokyny.</span><span class="sxs-lookup"><span data-stu-id="4518c-132">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Vlastnosti balíčku NuGet v projektu sady Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="4518c-134">Balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost **značky** vlastnost, protože značky pomoci ostatním najít váš balíček a pochopit jeho význam.</span><span class="sxs-lookup"><span data-stu-id="4518c-134">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="4518c-135">Zadejte jedinečný identifikátor balíčku a vyplňte všechny požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="4518c-135">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="4518c-136">Popis různých vlastností najdete v tématu [odkaz na soubor souboru .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="4518c-136">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="4518c-137">Všechny vlastnosti zde pohledu `.nuspec` manifestu, který sada Visual Studio vytvoří pro projekt.</span><span class="sxs-lookup"><span data-stu-id="4518c-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="4518c-138">Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo cokoli, co můžete hostovat používáte.</span><span class="sxs-lookup"><span data-stu-id="4518c-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="4518c-139">Pro Tento názorný postup doporučujeme, abyste pozdějším kroku publikování provádění balíček veřejně viditelné (i když nepravděpodobné, že kdo bude ve skutečnosti použít) včetně "Ukázkový" nebo "Test" v názvu.</span><span class="sxs-lookup"><span data-stu-id="4518c-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="4518c-140">Při pokusu publikovat balíček s názvem, který již existuje, se zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="4518c-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="4518c-141">Volitelné: Pokud chcete zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **upravit AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="4518c-141">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="4518c-142">Tato možnost je pouze k dispozici pro projekty, které používají atribut SDK – vizuální styl od v sadě Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4518c-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="4518c-143">V opačném případě klikněte pravým tlačítkem na projekt a zvolte **uvolnit projekt**.</span><span class="sxs-lookup"><span data-stu-id="4518c-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="4518c-144">Klikněte pravým tlačítkem na projekt uvolněn a zvolte **upravit AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="4518c-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="4518c-145">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="4518c-145">Run the pack command</span></span>

1. <span data-ttu-id="4518c-146">Nastavení konfigurace **vydání**.</span><span class="sxs-lookup"><span data-stu-id="4518c-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="4518c-147">Klikněte pravým tlačítkem myši na projekt v **Průzkumníka řešení** a vyberte **Pack** příkaz:</span><span class="sxs-lookup"><span data-stu-id="4518c-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Příkaz balíčku NuGet v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="4518c-149">Pokud se nezobrazí **Pack** projektu není pravděpodobně SDK styl projektu a budete muset použít příkaz `nuget.exe` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="4518c-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="4518c-150">Buď [projekt migrovat,](../reference/migrate-packages-config-to-package-reference.md) a použít `dotnet` rozhraní příkazového řádku, nebo se podívejte [vytvoření a publikování balíčku .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) místo pro podrobné pokyny.</span><span class="sxs-lookup"><span data-stu-id="4518c-150">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="4518c-151">Visual Studio vytvoří projekt a vytvoří `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="4518c-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="4518c-152">Zkontrolujte **výstup** okna podrobnosti (podobně jako následující), který obsahuje cestu k souboru balíčku.</span><span class="sxs-lookup"><span data-stu-id="4518c-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="4518c-153">Všimněte si také, že sestavení je v `bin\Release\netstandard2.0` befits jako cílové rozhraní .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="4518c-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="4518c-154">Alternativní možnost: balíček pomocí nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="4518c-154">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="4518c-155">Jako alternativu k použití **Pack** příkaz nabídky, NuGet 4.x+ a podporuje MSBuild 15.1 + `pack` cílit při projekt obsahuje data potřebný balíček.</span><span class="sxs-lookup"><span data-stu-id="4518c-155">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="4518c-156">Otevřete příkazový řádek, přejděte do složky vašeho projektu a spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="4518c-156">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="4518c-157">(Obvykle chcete spustit "Pro vývojáře příkazového řádku pro Visual Studio" z nabídky Start, jak bude nakonfigurován s všechny nezbytné cesty pro MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="4518c-157">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="4518c-158">Balíček pak najdete v `bin\Release` složky.</span><span class="sxs-lookup"><span data-stu-id="4518c-158">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="4518c-159">Další možnosti s `msbuild -t:pack`, naleznete v tématu [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="4518c-159">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="4518c-160">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="4518c-160">Publish the package</span></span>

<span data-ttu-id="4518c-161">Jakmile budete mít `.nupkg` souboru, ji publikujete do nuget.org buď pomocí `nuget.exe` rozhraní příkazového řádku nebo `dotnet.exe` rozhraní příkazového řádku spolu s klíčem rozhraní API získaných z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4518c-161">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="4518c-162">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="4518c-162">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="4518c-163">Publikování pomocí nasdílení změn nuget dotnet (rozhraní příkazového řádku dotnet)</span><span class="sxs-lookup"><span data-stu-id="4518c-163">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="4518c-164">Tento krok je doporučenou alternativou k použití `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="4518c-164">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="4518c-165">Před publikováním balíčku, je nutné otevřít příkazový řádek.</span><span class="sxs-lookup"><span data-stu-id="4518c-165">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="4518c-166">Publikování pomocí nasdílení změn nuget (nuget.exe rozhraní příkazového řádku)</span><span class="sxs-lookup"><span data-stu-id="4518c-166">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="4518c-167">Tento krok je alternativou k používání `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="4518c-167">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="4518c-168">Otevřete příkazový řádek a změňte na složku obsahující `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="4518c-168">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="4518c-169">Spusťte následující příkaz, zadávání názvu balíčku (ID balíčku jedinečný) a nahraďte hodnotu klíče svůj klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="4518c-169">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="4518c-170">nuget.exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="4518c-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="4518c-171">Zobrazit [nuget nabízených](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="4518c-171">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="4518c-172">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="4518c-172">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="4518c-173">Správa publikované balíčku</span><span class="sxs-lookup"><span data-stu-id="4518c-173">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="4518c-174">Přidání souboru readme a další soubory</span><span class="sxs-lookup"><span data-stu-id="4518c-174">Adding a readme and other files</span></span>

<span data-ttu-id="4518c-175">Přímo zadat soubory, které chcete zahrnout do balíčku, upravte soubor projektu a použít `content` vlastnost:</span><span class="sxs-lookup"><span data-stu-id="4518c-175">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="4518c-176">Tato možnost zahrne soubor s názvem `readme.txt` v kořenovém adresáři balíčku.</span><span class="sxs-lookup"><span data-stu-id="4518c-176">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="4518c-177">Visual Studio zobrazí okamžitě po instalaci balíčku přímo obsah tohoto souboru jako prostý text.</span><span class="sxs-lookup"><span data-stu-id="4518c-177">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="4518c-178">(Soubory Readme nejsou zobrazeny pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="4518c-178">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="4518c-179">Tady je například jak se zobrazí v souboru readme HtmlAgilityPack balíčku:</span><span class="sxs-lookup"><span data-stu-id="4518c-179">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazit soubor readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="4518c-181">V něm nebudou zahrnuty do výsledný balíček nebude výsledkem pouze přidání readme.txt v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="4518c-181">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="4518c-182">Související témata</span><span class="sxs-lookup"><span data-stu-id="4518c-182">Related topics</span></span>

- [<span data-ttu-id="4518c-183">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="4518c-183">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="4518c-184">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="4518c-184">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="4518c-185">Balíčky v předběžné verzi</span><span class="sxs-lookup"><span data-stu-id="4518c-185">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="4518c-186">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="4518c-186">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4518c-187">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="4518c-187">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4518c-188">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="4518c-188">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="4518c-189">Dokumentace ke službě knihovna .NET standard</span><span class="sxs-lookup"><span data-stu-id="4518c-189">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="4518c-190">Portování do .NET Core v rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4518c-190">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
