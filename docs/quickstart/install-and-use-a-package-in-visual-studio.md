---
title: Instalace a použití balíčku NuGet v aplikaci Visual Studio
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 05fd30a9d9d51c81b89d83a16b2fb08a55875e47
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419995"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="a11e1-103">Rychlý start: Instalace a použití balíčku v aplikaci Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a11e1-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="a11e1-104">Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři.</span><span class="sxs-lookup"><span data-stu-id="a11e1-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="a11e1-105">Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="a11e1-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="a11e1-106">Balíčky jsou nainstalovány do projektu aplikace Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="a11e1-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="a11e1-107">Tento článek popisuje proces použití oblíbeného balíčku [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) a projektu univerzální platforma Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="a11e1-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="a11e1-108">Stejný postup platí pro všechny ostatní projekty .NET nebo .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a11e1-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="a11e1-109">Po instalaci se podívejte na balíček v kódu `using <namespace>` , kde \<obor názvů\> je specifický pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="a11e1-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="a11e1-110">Po provedení odkazu můžete balíček volat prostřednictvím jeho rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a11e1-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="a11e1-111">**Začínáme s NuGet.org**: Procházení nuget.org je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="a11e1-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="a11e1-112">Můžete vyhledat nuget.org přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="a11e1-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a11e1-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a11e1-113">Prerequisites</span></span>

- <span data-ttu-id="a11e1-114">Visual Studio 2017 s úlohou vývoje Univerzální platforma Windows nebo</span><span class="sxs-lookup"><span data-stu-id="a11e1-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="a11e1-115">Visual Studio 2015 Update 3 s nástroji pro univerzální aplikace pro Windows</span><span class="sxs-lookup"><span data-stu-id="a11e1-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="a11e1-116">Edici 2017 Community Edition můžete zdarma nainstalovat z [VisualStudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a11e1-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="a11e1-117">Pokud používáte Visual Studio pro Mac, přečtěte si téma [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a11e1-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="a11e1-118">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="a11e1-118">Create a project</span></span>

<span data-ttu-id="a11e1-119">Balíčky NuGet se dají nainstalovat do libovolného projektu .NET, za předpokladu, že balíček podporuje stejnou cílovou architekturu jako projekt.</span><span class="sxs-lookup"><span data-stu-id="a11e1-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="a11e1-120">Pro tento návod použijte jednoduchou aplikaci pro univerzální platformu Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="a11e1-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="a11e1-121">V aplikaci Visual Studio vytvořte projekt pomocí **> soubor nový projekt...** a vyberte možnost **Windows Universal > prázdná aplikace (univerzální pro Windows)** .</span><span class="sxs-lookup"><span data-stu-id="a11e1-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="a11e1-122">Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou verzi a minimální verzi.</span><span class="sxs-lookup"><span data-stu-id="a11e1-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="a11e1-123">Přidejte balíček NuGet Newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="a11e1-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="a11e1-124">Chcete-li nainstalovat balíček, můžete použít buď uživatelské rozhraní Správce balíčků, nebo konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="a11e1-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="a11e1-125">Při instalaci balíčku zaznamená NuGet závislost v souboru projektu nebo `packages.config` v souboru.</span><span class="sxs-lookup"><span data-stu-id="a11e1-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="a11e1-126">Další informace najdete v tématu [Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="a11e1-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="a11e1-127">Uživatelské rozhraní Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="a11e1-127">Package Manager UI</span></span>

1. <span data-ttu-id="a11e1-128">V Průzkumník řešení klikněte pravým tlačítkem na **odkazy** a vyberte **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a11e1-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="a11e1-130">Jako **zdroj balíčku**zvolte "NuGet.org", vyberte kartu **Procházet** , vyhledejte **Newtonsoft. JSON**, vyberte tento balíček v seznamu a vyberte **instalovat**:</span><span class="sxs-lookup"><span data-stu-id="a11e1-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Vyhledání balíčku Newtonsoft. JSON](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="a11e1-132">Přijměte všechny výzvy k licenci.</span><span class="sxs-lookup"><span data-stu-id="a11e1-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="a11e1-133">(Visual Studio 2017) Pokud se zobrazí výzva k výběru formátu správy balíčků, vyberte **v souboru projektu možnost PackageReference**:</span><span class="sxs-lookup"><span data-stu-id="a11e1-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Výběr formátu správy balíčků](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="a11e1-135">Pokud se zobrazí výzva ke kontrole změn, vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="a11e1-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="a11e1-136">Konzola Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="a11e1-136">Package Manager Console</span></span>

1. <span data-ttu-id="a11e1-137">Vyberte **nástroje > správce balíčků NuGet > nabídce konzoly Správce balíčků** .</span><span class="sxs-lookup"><span data-stu-id="a11e1-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="a11e1-138">Po otevření konzoly ověřte, zda je v rozevíracím seznamu **výchozí projekt** uveden projekt, do kterého chcete balíček nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="a11e1-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="a11e1-139">Pokud máte v řešení jeden projekt, je již vybrán.</span><span class="sxs-lookup"><span data-stu-id="a11e1-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Vyhledání balíčku Newtonsoft. JSON](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="a11e1-141">Zadejte příkaz `Install-Package Newtonsoft.Json` (viz [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="a11e1-141">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="a11e1-142">V okně konzoly se zobrazí výstup příkazu.</span><span class="sxs-lookup"><span data-stu-id="a11e1-142">The console window shows output for the command.</span></span> <span data-ttu-id="a11e1-143">Chyby obvykle označují, že balíček není kompatibilní s cílovým rozhraním .NET Framework projektu.</span><span class="sxs-lookup"><span data-stu-id="a11e1-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="a11e1-144">Použití rozhraní API Newtonsoft. JSON v aplikaci</span><span class="sxs-lookup"><span data-stu-id="a11e1-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="a11e1-145">Pomocí balíčku Newtonsoft. JSON v projektu můžete zavolat jeho `JsonConvert.SerializeObject` metodu pro převod objektu na řetězec čitelný z lidského.</span><span class="sxs-lookup"><span data-stu-id="a11e1-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="a11e1-146">`MainPage.xaml` Existující`Grid` prvek otevřete a nahraďte následujícím:</span><span class="sxs-lookup"><span data-stu-id="a11e1-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="a11e1-147">Otevřete soubor (umístěný v Průzkumník řešení `MainPage.xaml` pod uzlem) a vložte následující kód do `MainPage` třídy: `MainPage.xaml.cs`</span><span class="sxs-lookup"><span data-stu-id="a11e1-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` class:</span></span>

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

1. <span data-ttu-id="a11e1-148">I když jste do projektu přidali balíček Newtonsoft. JSON, červené vlnovky se zobrazí v části `JsonConvert` , protože `using` potřebujete příkaz v horní části souboru kódu:</span><span class="sxs-lookup"><span data-stu-id="a11e1-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="a11e1-149">Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem možnosti **ladění > spustit ladění**:</span><span class="sxs-lookup"><span data-stu-id="a11e1-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Počáteční výstup aplikace UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="a11e1-151">Výběrem tlačítka na tomto tlačítku zobrazíte obsah TextBlock nahrazený nějakým textem JSON:</span><span class="sxs-lookup"><span data-stu-id="a11e1-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Výstup aplikace UWP po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a><span data-ttu-id="a11e1-153">Další postup</span><span class="sxs-lookup"><span data-stu-id="a11e1-153">Next steps</span></span>

<span data-ttu-id="a11e1-154">Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="a11e1-154">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a11e1-155">Instalace a Správa balíčků pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a11e1-155">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

<span data-ttu-id="a11e1-156">Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.</span><span class="sxs-lookup"><span data-stu-id="a11e1-156">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="a11e1-157">Přehled a pracovní postup pro spotřebu balíčku</span><span class="sxs-lookup"><span data-stu-id="a11e1-157">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="a11e1-158">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="a11e1-158">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="a11e1-159">Odkazy na balíčky v souborech projektů</span><span class="sxs-lookup"><span data-stu-id="a11e1-159">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
