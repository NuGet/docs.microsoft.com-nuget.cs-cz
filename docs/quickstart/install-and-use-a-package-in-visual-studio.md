---
title: Úvodní příručka k pomocí balíčků NuGet v sadě Visual Studio
description: Kurz návod týkající se procesu instalace a použití balíčku NuGet v projektu sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 014b316ea03b45584406c313d46b96ad36340124
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426222"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="abc39-103">Rychlý start: Nainstalovat a používat balíčky v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abc39-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="abc39-104">Balíčky NuGet obsahují opakovaně použitelný kód, který jinými vývojáři zpřístupnit je pro použití ve vašich projektech.</span><span class="sxs-lookup"><span data-stu-id="abc39-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="abc39-105">Zobrazit [co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="abc39-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="abc39-106">Balíčky se nainstalují do projektu sady Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="abc39-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="abc39-107">Tento článek popisuje proces pomocí Oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku a projekt univerzální platformy Windows (UPW).</span><span class="sxs-lookup"><span data-stu-id="abc39-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="abc39-108">Stejný postup platí pro libovolný jiný projekt .NET nebo .NET Core.</span><span class="sxs-lookup"><span data-stu-id="abc39-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="abc39-109">Po instalaci se odkazovat na balíček v kódu s `using <namespace>` kde \<obor názvů\> je specifický pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="abc39-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="abc39-110">Jakmile se odkazuje, můžete volat balíček prostřednictvím jejího rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="abc39-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="abc39-111">**Začněte s nuget.org**: Procházení nuget.org je, jak vývojáři na platformě .NET obvykle najdete součásti můžete znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="abc39-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="abc39-112">Můžete vyhledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="abc39-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abc39-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="abc39-113">Prerequisites</span></span>

- <span data-ttu-id="abc39-114">Visual Studio 2017 s úlohou vývoj univerzální platformy Windows, nebo</span><span class="sxs-lookup"><span data-stu-id="abc39-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="abc39-115">Visual Studio 2015 Update 3 s Tools for Universal Windows Apps.</span><span class="sxs-lookup"><span data-stu-id="abc39-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="abc39-116">Edice Community 2017 můžete nainstalovat zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použijte edice Professional nebo Enterprise.</span><span class="sxs-lookup"><span data-stu-id="abc39-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="abc39-117">Pokud používáte Visual Studio pro Mac, najdete v článku [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="abc39-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="abc39-118">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="abc39-118">Create a project</span></span>

<span data-ttu-id="abc39-119">Balíčky NuGet můžete nainstalovat do jakéhokoli projektu .NET, za předpokladu, že balíček podporuje stejnou cílovou architekturu jako projekt.</span><span class="sxs-lookup"><span data-stu-id="abc39-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="abc39-120">V tomto návodu použijte jednoduché aplikace pro Universal Windows (UPW).</span><span class="sxs-lookup"><span data-stu-id="abc39-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="abc39-121">Vytvoření projektu v sadě Visual Studio pomocí **soubor > Nový projekt...**  a vyberete **Windows Universal > prázdná aplikace (Universal Windows)** .</span><span class="sxs-lookup"><span data-stu-id="abc39-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="abc39-122">Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.</span><span class="sxs-lookup"><span data-stu-id="abc39-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="abc39-123">Přidejte balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="abc39-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="abc39-124">Chcete-li nainstalovat balíček, můžete použít uživatelské rozhraní Správce balíčků nebo konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="abc39-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="abc39-125">Při instalaci balíčku NuGet zaznamenává závislost v jednom souboru projektu nebo `packages.config` souboru.</span><span class="sxs-lookup"><span data-stu-id="abc39-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="abc39-126">Další informace najdete v tématu [balíček spotřeby přehled a pracovní postup](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="abc39-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="abc39-127">Uživatelské rozhraní Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="abc39-127">Package Manager UI</span></span>

1. <span data-ttu-id="abc39-128">V Průzkumníku řešení klikněte pravým tlačítkem na **odkazy** a zvolte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="abc39-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Spravovat balíčky NuGet příkaz pro projektové odkazy](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="abc39-130">Zvolte možnost "nuget.org" jako **zdroj balíčku**, vyberte **Procházet** kartu, vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte  **Nainstalujte**:</span><span class="sxs-lookup"><span data-stu-id="abc39-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Vyhledání balíček Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="abc39-132">Přijměte případné výzvy licence.</span><span class="sxs-lookup"><span data-stu-id="abc39-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="abc39-133">(Visual Studio 2017) Pokud se zobrazí výzva k výběru formát správy balíčků, vyberte **PackageReference v souboru projektu**:</span><span class="sxs-lookup"><span data-stu-id="abc39-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Vyberte formát správy balíčků](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="abc39-135">Pokud budete vyzváni ke zkontrolování změn, vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="abc39-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="abc39-136">Konzola Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="abc39-136">Package Manager Console</span></span>

1. <span data-ttu-id="abc39-137">Vyberte **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="abc39-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="abc39-138">Jakmile se otevře se konzola, zkontrolujte, že **výchozí projekt** rozevíracím seznamu zobrazí projektu, do kterého chcete balíček nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="abc39-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="abc39-139">Pokud máte jeden projekt v řešení, je už vybraná.</span><span class="sxs-lookup"><span data-stu-id="abc39-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Vyhledání balíček Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="abc39-141">Zadejte příkaz `Install-Package Newtonsoft.Json` (viz [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="abc39-141">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="abc39-142">V okně konzoly se zobrazí výstup příkazu.</span><span class="sxs-lookup"><span data-stu-id="abc39-142">The console window shows output for the command.</span></span> <span data-ttu-id="abc39-143">Chyby obvykle signalizují, že balíček není kompatibilní s cílovou architekturu projektu.</span><span class="sxs-lookup"><span data-stu-id="abc39-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="abc39-144">Použít Newtonsoft.Json rozhraní API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="abc39-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="abc39-145">S balíčkem Newtonsoft.Json v projektu, můžete volat jeho `JsonConvert.SerializeObject` způsobů, jak převést objekt na řetězec čitelný.</span><span class="sxs-lookup"><span data-stu-id="abc39-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="abc39-146">Otevřít `MainPage.xaml` a nahraďte existující `Grid` element následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="abc39-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="abc39-147">Otevřít `MainPage.xaml.cs` souboru (umístěné v Průzkumníkovi řešení pod `MainPage.xaml` uzlu) a vložte následující kód `MainPage` konstruktor:</span><span class="sxs-lookup"><span data-stu-id="abc39-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="abc39-148">I když jste přidali do projektu balíček Newtonsoft.Json, červenou vlnovkou se zobrazí v části `JsonConvert` vzhledem k tomu, že je nutné `using` příkazu v horní části souboru kódu:</span><span class="sxs-lookup"><span data-stu-id="abc39-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="abc39-149">Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **ladit > Spustit ladění**:</span><span class="sxs-lookup"><span data-stu-id="abc39-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Výstup počáteční aplikace pro UPW](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="abc39-151">Vyberte na tlačítko Zobrazit obsah TextBlock nahradit JSON text:</span><span class="sxs-lookup"><span data-stu-id="abc39-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Výstup aplikace UPW po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="abc39-153">Související články</span><span class="sxs-lookup"><span data-stu-id="abc39-153">Related articles</span></span>

- [<span data-ttu-id="abc39-154">Přehled a pracovní postup využití balíčků</span><span class="sxs-lookup"><span data-stu-id="abc39-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="abc39-155">Instalace a Správa balíčků s využitím sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abc39-155">Install and manage packages using Visual Studio</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="abc39-156">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="abc39-156">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="abc39-157">Obvyklé konfigurace NuGet</span><span class="sxs-lookup"><span data-stu-id="abc39-157">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
