---
title: "Úvodní příručka k používání balíčků NuGet z Visual Studia | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Návod kurz týkající se procesu instalace a použití balíčku NuGet v sadě Visual Studio projektu."
keywords: "Nainstalujte NuGet, využívání balíčku NuGet, instalace balíčků NuGet, odkazů na balíček NuGet, pomocí balíčků NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff905fec6d6af4fa40fd4331cb970121b6eb0879
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="35859-104">Instalace a použití balíčku v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35859-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="35859-105">Balíčky NuGet obsahovat opakovaně použitelný kód, který jinými vývojáři zpřístupnění pro použití ve vašich projektů.</span><span class="sxs-lookup"><span data-stu-id="35859-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="35859-106">V tématu [co je NuGet?](../What-is-NuGet.md) pozadí.</span><span class="sxs-lookup"><span data-stu-id="35859-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="35859-107">Balíčky jsou nainstalovány do projektu Visual Studia pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků, jak je popsáno v tomto článku Oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíček a projekt univerzální platformu Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="35859-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console, as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span>

<span data-ttu-id="35859-108">Po instalaci odkazovat na balíček v kódu pomocí `using <namespace>` kde \<obor názvů\> je specifická pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="35859-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="35859-109">Jakmile se odkazuje, můžete volat balíček prostřednictvím jejího rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="35859-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="35859-110">**Začněte s nuget.org**: procházení nuget.org je, jak .NET vývojáři obvykle najít součásti můžete opakovaně použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="35859-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="35859-111">Můžete hledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="35859-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35859-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="35859-112">Prerequisites</span></span>

- <span data-ttu-id="35859-113">Visual Studio 2017 se zatížením, vývoj pro univerzální platformu Windows, nebo</span><span class="sxs-lookup"><span data-stu-id="35859-113">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="35859-114">Visual Studio 2015 Update 3 pomocí nástrojů pro univerzální aplikace pro Windows.</span><span class="sxs-lookup"><span data-stu-id="35859-114">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="35859-115">Edice Community 2017 můžete nainstalovat zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použijte edice Professional nebo Enterprise.</span><span class="sxs-lookup"><span data-stu-id="35859-115">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="35859-116">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="35859-116">Create a project</span></span>

<span data-ttu-id="35859-117">Balíčky NuGet lze nainstalovat do projektu .NET určitého druhu.</span><span class="sxs-lookup"><span data-stu-id="35859-117">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="35859-118">V tomto návodu použijete jednoduchou aplikaci Universal Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="35859-118">For this walkthrough, you use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="35859-119">Vytvoření projektu v sadě Visual Studio pomocí **soubor > Nový projekt...**  a výběrem **univerzální pro Windows > prázdná aplikace (univerzální pro Windows)**.</span><span class="sxs-lookup"><span data-stu-id="35859-119">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="35859-120">Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.</span><span class="sxs-lookup"><span data-stu-id="35859-120">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="35859-121">Přidejte balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="35859-121">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="35859-122">Chcete-li nainstalovat balíček, můžete použít uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="35859-122">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="35859-123">Při instalaci balíčku NuGet zaznamenává závislost buď souboru projektu nebo `packages.config` souboru.</span><span class="sxs-lookup"><span data-stu-id="35859-123">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="35859-124">Další informace najdete v tématu [balíček spotřeba přehled a pracovní postup](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="35859-124">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="35859-125">Uživatelského rozhraní Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="35859-125">Package Manager UI</span></span>

1. <span data-ttu-id="35859-126">V Průzkumníku řešení klikněte pravým tlačítkem na **odkazy** a zvolte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="35859-126">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Správa balíčků NuGet příkaz pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="35859-128">Vyberte "nuget.org" jako **zdroj balíčku**, vyberte **Procházet** kartě, vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte  **Nainstalujte**:</span><span class="sxs-lookup"><span data-stu-id="35859-128">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Vyhledání Newtonsoft.Json balíčku](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="35859-130">Přijměte zobrazování výzev licence.</span><span class="sxs-lookup"><span data-stu-id="35859-130">Accept any license prompts.</span></span>

1. <span data-ttu-id="35859-131">(Visual Studio 2017) Po zobrazení výzvy vyberte formát balíček správy, vyberte **PackageReference v souboru projektu**:</span><span class="sxs-lookup"><span data-stu-id="35859-131">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Výběr formátu odkaz na balíček](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="35859-133">Pokud budete vyzváni ke zkontrolování změn, vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="35859-133">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="35859-134">Konzola správce balíčků</span><span class="sxs-lookup"><span data-stu-id="35859-134">Package Manager Console</span></span>

1. <span data-ttu-id="35859-135">Vyberte **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="35859-135">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="35859-136">Jakmile se otevře se konzola, zkontrolujte, zda **výchozí projekt** rozevíracího seznamu zobrazuje projekt, do kterého chcete nainstalovat balíček.</span><span class="sxs-lookup"><span data-stu-id="35859-136">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="35859-137">Pokud máte jeden projekt v řešení, je již vybrána.</span><span class="sxs-lookup"><span data-stu-id="35859-137">If you have a single project in the solution, it is already selected.</span></span>

    ![Vyhledání Newtonsoft.Json balíčku](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="35859-139">Zadejte příkaz `Install-Package Newtonsoft.json` (viz [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="35859-139">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="35859-140">V okně konzoly zobrazí výstup příkazu.</span><span class="sxs-lookup"><span data-stu-id="35859-140">The console window shows output for the command.</span></span> <span data-ttu-id="35859-141">Chyby obvykle naznačují, že balíček není kompatibilní s cílový framework projektu na.</span><span class="sxs-lookup"><span data-stu-id="35859-141">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="35859-142">Použít Newtonsoft.Json rozhraní API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="35859-142">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="35859-143">S balíčkem Newtonsoft.Json v projektu, můžete volat jeho `JsonConvert.SerializeObject` způsobů, jak převést objekt na řetězec čitelná pro člověka.</span><span class="sxs-lookup"><span data-stu-id="35859-143">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="35859-144">Otevřete `MainPage.xaml` a nahradit existující `Grid` element s následující:</span><span class="sxs-lookup"><span data-stu-id="35859-144">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="35859-145">Otevřete `MainPage.xaml.cs` souboru (umístěné v Průzkumníku řešení v části `MainPage.xaml` uzlu) a vložte následující kód do `MainPage` konstruktor:</span><span class="sxs-lookup"><span data-stu-id="35859-145">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="35859-146">I když jste přidali Newtonsoft.Json balíčku do projektu, se zobrazí červený podtržení vlnovkou pod `JsonConvert` vzhledem k tomu, že budete potřebovat `using` příkaz v horní části souboru kódu:</span><span class="sxs-lookup"><span data-stu-id="35859-146">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="35859-147">Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **ladění > Spustit ladění**:</span><span class="sxs-lookup"><span data-stu-id="35859-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Počáteční výstup aplikace UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="35859-149">Vyberte na tlačítko Zobrazit obsah TextBlock nahradí JSON text:</span><span class="sxs-lookup"><span data-stu-id="35859-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Výstup aplikace UWP po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="35859-151">Související články</span><span class="sxs-lookup"><span data-stu-id="35859-151">Related articles</span></span>

- [<span data-ttu-id="35859-152">Přehled a pracovní postup spotřeby balíčku</span><span class="sxs-lookup"><span data-stu-id="35859-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="35859-153">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="35859-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="35859-154">Způsoby, jak nainstalovat balíček</span><span class="sxs-lookup"><span data-stu-id="35859-154">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="35859-155">Konfigurace chování NuGetu</span><span class="sxs-lookup"><span data-stu-id="35859-155">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
