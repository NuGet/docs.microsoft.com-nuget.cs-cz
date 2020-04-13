---
title: Instalace a použití balíčku NuGet v sadě Visual Studio
description: Návod k procesu instalace a používání balíčku NuGet v projektu sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147484"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="16b2f-103">Úvodní příručka: Instalace a použití balíčku v sadě Visual Studio (jenom pro Windows)</span><span class="sxs-lookup"><span data-stu-id="16b2f-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="16b2f-104">Balíčky NuGet obsahují opakovaně použitelný kód, který vám ostatní vývojáři zpřístupní pro použití ve vašich projektech.</span><span class="sxs-lookup"><span data-stu-id="16b2f-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="16b2f-105">Podívejte se [na co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="16b2f-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="16b2f-106">Balíčky jsou nainstalovány do projektu sady Visual Studio pomocí Správce balíčků NuGet, [Konzola správce balíčků](../consume-packages/install-use-packages-powershell)nebo [rozhraní SE kontinuu dotnet .](install-and-use-a-package-using-the-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="16b2f-106">Packages are installed into a Visual Studio project using the NuGet Package Manager, the [Package Manager Console](../consume-packages/install-use-packages-powershell), or the [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md).</span></span> <span data-ttu-id="16b2f-107">Tento článek ukazuje proces pomocí populární [newtonsoft.json](https://www.nuget.org/packages/Newtonsoft.Json/) balíček a Windows Presentation Foundation (WPF) projekt.</span><span class="sxs-lookup"><span data-stu-id="16b2f-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="16b2f-108">Stejný proces platí pro všechny ostatní projekty .NET nebo .NET Core.</span><span class="sxs-lookup"><span data-stu-id="16b2f-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="16b2f-109">Po instalaci, odkazovat na `using <namespace>` balíček v kódu s kde \<obor názvů\> je specifické pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="16b2f-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="16b2f-110">Jakmile je odkaz, můžete volat balíček prostřednictvím jeho rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="16b2f-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="16b2f-111">**Začněte s nuget.org**: Procházení *nuget.org* je způsob, jakým vývojáři rozhraní .NET obvykle vyhledávají součásti, které mohou znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="16b2f-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="16b2f-112">Můžete hledat *nuget.org* přímo nebo najít a nainstalovat balíčky v rámci sady Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="16b2f-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="16b2f-113">Obecné informace naleznete v [tématu Hledání a vyhodnocení balíčků NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="16b2f-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16b2f-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="16b2f-114">Prerequisites</span></span>

- <span data-ttu-id="16b2f-115">Visual Studio 2019 s úlohou vývoje plochy .NET.</span><span class="sxs-lookup"><span data-stu-id="16b2f-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="16b2f-116">Můžete nainstalovat edici Community 2019 zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.</span><span class="sxs-lookup"><span data-stu-id="16b2f-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="16b2f-117">Pokud používáte Visual Studio pro Mac, přečtěte si informace [o instalaci a použití balíčku ve Visual Studiu for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="16b2f-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="16b2f-118">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="16b2f-118">Create a project</span></span>

<span data-ttu-id="16b2f-119">Balíčky NuGet lze nainstalovat do libovolného projektu .NET za předpokladu, že balíček podporuje stejný cílový rámec jako projekt.</span><span class="sxs-lookup"><span data-stu-id="16b2f-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="16b2f-120">Pro tento návod použijte jednoduchou aplikaci WPF.</span><span class="sxs-lookup"><span data-stu-id="16b2f-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="16b2f-121">Vytvořte projekt v sadě Visual Studio pomocí**nového projektu** **souboru** > , zadejte **rozhraní .NET** do vyhledávacího pole a pak vyberte **aplikaci WPF (.NET Framework).**</span><span class="sxs-lookup"><span data-stu-id="16b2f-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="16b2f-122">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="16b2f-122">Click **Next**.</span></span> <span data-ttu-id="16b2f-123">Přijímejte výchozí hodnoty pro **rozhraní Framework** po zobrazení výzvy.</span><span class="sxs-lookup"><span data-stu-id="16b2f-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="16b2f-124">Visual Studio vytvoří projekt, který se otevře v Průzkumníku řešení.</span><span class="sxs-lookup"><span data-stu-id="16b2f-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="16b2f-125">Přidat balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="16b2f-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="16b2f-126">Chcete-li nainstalovat balíček, můžete použít buď Správce balíčků NuGet nebo konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="16b2f-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="16b2f-127">Při instalaci balíčku NuGet zaznamenává závislost v souboru projektu `packages.config` nebo souboru (v závislosti na formátu projektu).</span><span class="sxs-lookup"><span data-stu-id="16b2f-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="16b2f-128">Další informace naleznete v [tématu Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="16b2f-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="16b2f-129">Správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="16b2f-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="16b2f-130">V Průzkumníku řešení klepněte pravým **tlačítkem** myši na reference a zvolte **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="16b2f-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="16b2f-132">Jako **zdroj balíčku**zvolte "nuget.org", vyberte kartu **Procházet,** vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte **Instalovat**:</span><span class="sxs-lookup"><span data-stu-id="16b2f-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Lokalizace newtonsoft.json balíčku](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="16b2f-134">Pokud chcete další informace o Správci balíčků NuGet, přečtěte si informace [o instalaci a správě balíčků pomocí sady Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="16b2f-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="16b2f-135">Přijměte všechny výzvy k licenci.</span><span class="sxs-lookup"><span data-stu-id="16b2f-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="16b2f-136">(Pouze Visual Studio 2017) Pokud se zobrazí výzva k výběru formátu správy balíčků, vyberte **v souboru projektu položku PackageReference**:</span><span class="sxs-lookup"><span data-stu-id="16b2f-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Výběr formátu správy balíčků](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="16b2f-138">Pokud se zobrazí výzva ke kontrole změn, vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="16b2f-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="16b2f-139">Konzola Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="16b2f-139">Package Manager Console</span></span>

1. <span data-ttu-id="16b2f-140">Vyberte příkaz příkaz **konzoly** > Správce > **balíčků** Správce balíčků Nástroje**NuGet.**</span><span class="sxs-lookup"><span data-stu-id="16b2f-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="16b2f-141">Po otevření konzoly zkontrolujte, zda se v rozevíracím seznamu **Výchozí projekt** zobrazuje projekt, do kterého chcete balíček nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="16b2f-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="16b2f-142">Pokud máte v řešení jeden projekt, je již vybrán.</span><span class="sxs-lookup"><span data-stu-id="16b2f-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Lokalizace newtonsoft.json balíčku](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="16b2f-144">Zadejte `Install-Package Newtonsoft.Json` příkaz (viz [Instalační balíček](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="16b2f-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="16b2f-145">Okno konzoly zobrazuje výstup příkazu.</span><span class="sxs-lookup"><span data-stu-id="16b2f-145">The console window shows output for the command.</span></span> <span data-ttu-id="16b2f-146">Chyby obvykle označují, že balíček není kompatibilní s cílovým rámcem projektu.</span><span class="sxs-lookup"><span data-stu-id="16b2f-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="16b2f-147">Chcete-li získat další informace o konzoli Správce balíčků, přečtěte si informace [o instalaci a správě balíčků pomocí konzoly Správce balíčků](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="16b2f-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="16b2f-148">Použití rozhraní Newtonsoft.Json API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="16b2f-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="16b2f-149">S newtonsoft.Json balíček v projektu, `JsonConvert.SerializeObject` můžete volat jeho metodu převést objekt na člověka čitelný řetězec.</span><span class="sxs-lookup"><span data-stu-id="16b2f-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="16b2f-150">Otevřete `MainWindow.xaml` a `Grid` nahraďte existující prvek následujícím:</span><span class="sxs-lookup"><span data-stu-id="16b2f-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="16b2f-151">Otevřete `MainWindow.xaml.cs` soubor (umístěný v `MainWindow.xaml` Průzkumníku řešení pod uzlovým) a do `MainWindow` třídy vložte následující kód:</span><span class="sxs-lookup"><span data-stu-id="16b2f-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="16b2f-152">I když jste do projektu přidali balíček Newtonsoft.Json, `JsonConvert` zobrazí se `using` pod ním červené vlnovky, protože potřebujete prohlášení v horní části souboru kódu:</span><span class="sxs-lookup"><span data-stu-id="16b2f-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="16b2f-153">Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **možnosti Ladění** > **ladění startování**:</span><span class="sxs-lookup"><span data-stu-id="16b2f-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Počáteční výstup aplikace WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="16b2f-155">Výběrem na tlačítku zobrazíte obsah textového bloku nahrazený nějakým textem JSON:</span><span class="sxs-lookup"><span data-stu-id="16b2f-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Výstup aplikace WPF po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="16b2f-157">Související video</span><span class="sxs-lookup"><span data-stu-id="16b2f-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="16b2f-158">Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="16b2f-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16b2f-159">Další kroky</span><span class="sxs-lookup"><span data-stu-id="16b2f-159">Next steps</span></span>

<span data-ttu-id="16b2f-160">Gratulujeme k instalaci a používání vašeho prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="16b2f-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="16b2f-161">Instalace a správa balíčků pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16b2f-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="16b2f-162">Instalace a správa balíčků pomocí konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="16b2f-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="16b2f-163">Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.</span><span class="sxs-lookup"><span data-stu-id="16b2f-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="16b2f-164">Přehled a pracovní postup spotřeby balíků</span><span class="sxs-lookup"><span data-stu-id="16b2f-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="16b2f-165">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="16b2f-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="16b2f-166">Odkazy na balíčky v souborech projektů</span><span class="sxs-lookup"><span data-stu-id="16b2f-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
