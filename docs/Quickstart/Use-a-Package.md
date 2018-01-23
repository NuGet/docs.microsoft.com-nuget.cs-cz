---
title: "Úvodní příručka k používání balíčků NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "Návod kurz týkající se procesu instalace a použití balíčku NuGet v projektu."
keywords: "Nainstalujte NuGet, využívání balíčku NuGet, instalace balíčků NuGet, odkazů na balíček NuGet, pomocí balíčků NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ffba868bbbf1fe373fd45a9459eab7072f4c19b3
ms.sourcegitcommit: 9ac1fa23a4a8ce098692de93328b1db4136fe3d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="bc552-104">Instalace a použití balíčku</span><span class="sxs-lookup"><span data-stu-id="bc552-104">Install and use a package</span></span>

<span data-ttu-id="bc552-105">Balíčky NuGet jsou jednotky opakovaně použitelný kód, který jinými vývojáři zpřístupnění pro použití ve vašich projektů.</span><span class="sxs-lookup"><span data-stu-id="bc552-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="bc552-106">V tématu [co je NuGet?](../What-is-NuGet.md) pozadí.</span><span class="sxs-lookup"><span data-stu-id="bc552-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="bc552-107">Po instalaci odkazovat na balíček v kódu pomocí `using <namespace>` kde \<obor názvů\> je specifická pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="bc552-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="bc552-108">Jakmile se odkazuje, můžete volat balíček prostřednictvím jejího rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="bc552-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="bc552-109">Zbývající část tohoto tématu provede procesem instalace oblíbených pomocí uživatelského rozhraní Správce balíčků [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíček v projektu univerzální platformu Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="bc552-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="bc552-110">Poté zobrazí příklad použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="bc552-110">It then shows an example of using the package.</span></span> <span data-ttu-id="bc552-111">Podobně jako pracovní postup se používá pro jiné balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="bc552-111">You use a similar workflow for other NuGet packages.</span></span>

- [<span data-ttu-id="bc552-112">Nainstalujte požadavky</span><span class="sxs-lookup"><span data-stu-id="bc552-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="bc552-113">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="bc552-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="bc552-114">Přidejte balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="bc552-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="bc552-115">Použít Newtonsoft.Json rozhraní API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="bc552-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="bc552-116">**Začněte s nuget.org**: instalace balíčků z nuget.org je běžné pracovní postup, který .NET vývojáři použít k vyhledání součásti, které mohou používat ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="bc552-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can use in their own applications.</span></span> <span data-ttu-id="bc552-117">Můžete vždy hledání nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="bc552-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="bc552-118">Nainstalujte požadavky</span><span class="sxs-lookup"><span data-stu-id="bc552-118">Install pre-requisites</span></span>

<span data-ttu-id="bc552-119">Tento kurz vyžaduje Visual Studio 2015 Update 3 pomocí nástrojů pro univerzální aplikace pro Windows nebo Visual Studio 2017 se zatížením, vývoj pro univerzální platformu Windows.</span><span class="sxs-lookup"><span data-stu-id="bc552-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="bc552-120">Pokud již máte nainstalovanou sadu Visual Studio, můžete spustit instalační program znovu a přidat UWP nástroje.</span><span class="sxs-lookup"><span data-stu-id="bc552-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="bc552-121">Edice Community můžete nainstalovat zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použijte edice Professional nebo Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bc552-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="bc552-122">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="bc552-122">Create a project</span></span>

<span data-ttu-id="bc552-123">Pokud chcete nainstalovat balíček NuGet, je nutné některé druh. Na základě NET projektu v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc552-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="bc552-124">V tomto návodu můžete použít jednoduchou aplikaci Windows Presentation Foundation (WPF) nebo Universal Windows (UWP):</span><span class="sxs-lookup"><span data-stu-id="bc552-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="bc552-125">WPF (Windows 7 +), zvolte **soubor > Nový > projekt**, rozbalte položku **Visual C#**, vyberte **klasický desktopový Windows > aplikace WPF (rozhraní .NET Framework)**a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc552-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="bc552-126">Pro UPW (Windows 10), použijte **univerzální pro Windows > prázdná aplikace (univerzální pro Windows)** místo.</span><span class="sxs-lookup"><span data-stu-id="bc552-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="bc552-127">Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.</span><span class="sxs-lookup"><span data-stu-id="bc552-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="bc552-128">Přidejte balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="bc552-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="bc552-129">V Průzkumníku řešení klikněte pravým tlačítkem na **odkazy** a zvolte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="bc552-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Správa balíčků NuGet příkaz pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="bc552-131">Vyberte "nuget.org" jako **zdroj balíčku**, vyberte **Procházet** kartě, vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte  **Nainstalujte**:</span><span class="sxs-lookup"><span data-stu-id="bc552-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Vyhledání Newtonsoft.Json balíčku](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="bc552-133">Po zobrazení výzvy vyberte formát balíček správy zvolit PackageReference (doporučeno) a `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="bc552-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Výběr formátu odkaz na balíček](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="bc552-135">Pokud budete vyzváni ke zkontrolování změn, vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc552-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="bc552-136">V Průzkumníku řešení klikněte pravým tlačítkem a vyberte **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="bc552-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="bc552-137">Tím se obnoví všechny balíčky NuGet uvedených v části **odkazy**.</span><span class="sxs-lookup"><span data-stu-id="bc552-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="bc552-138">Další podrobnosti najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="bc552-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="bc552-139">Použít Newtonsoft.Json rozhraní API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="bc552-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="bc552-140">S balíčkem Newtonsoft.Json v projektu, můžete volat jeho `JsonConvert.SerializeObject` způsobů, jak převést objekt na řetězec čitelná pro člověka.</span><span class="sxs-lookup"><span data-stu-id="bc552-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="bc552-141">Otevřete `MainWindow.xaml` (WPF) nebo `MainPage.xaml` (UWP) a nahradit existující `Grid` element s následující:</span><span class="sxs-lookup"><span data-stu-id="bc552-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="bc552-142">Rozbalte `MainWindow.xaml` (WPF) nebo `MainPage.xaml` uzlu (UPW) v Průzkumníku řešení otevřete `.cs` soubor a vložte následující kód do `MainWindow` nebo `MainPage` po konstruktor – třída:</span><span class="sxs-lookup"><span data-stu-id="bc552-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="bc552-143">I když jste přidali Newtonsoft.Json balíčku do projektu, se zobrazí červený podtržení vlnovkou pod `JsonConvert` vzhledem k tomu, že budete potřebovat `using` příkaz.</span><span class="sxs-lookup"><span data-stu-id="bc552-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="bc552-144">Najeďte myší podtrženou `JsonConvert` a uvidíte žárovek a možnost **zobrazit potenciální opravy**:</span><span class="sxs-lookup"><span data-stu-id="bc552-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Žárovek s zobrazit potenciální opravy příkazu](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="bc552-146">Klikněte na **zobrazit potenciální opravy** (nebo žárovek) a vyberte první navrhované opravu `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="bc552-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="bc552-147">Tento postup přidá nezbytné řádku do horní části souboru.</span><span class="sxs-lookup"><span data-stu-id="bc552-147">This adds the necessary line to the top of the file.</span></span>

    ![Poskytnutí možnosti přidat pomocí žárovek – příkaz](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="bc552-149">Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **ladění > Spustit ladění** (UPW zobrazeny zde; WPF je podobný):</span><span class="sxs-lookup"><span data-stu-id="bc552-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Počáteční výstup aplikace UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="bc552-151">Vyberte na tlačítko Zobrazit obsah TextBlock nahradí JSON text:</span><span class="sxs-lookup"><span data-stu-id="bc552-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Výstup aplikace UWP po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="bc552-153">Související témata</span><span class="sxs-lookup"><span data-stu-id="bc552-153">Related topics</span></span>

- [<span data-ttu-id="bc552-154">Přehled a pracovní postup spotřeby balíčku</span><span class="sxs-lookup"><span data-stu-id="bc552-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="bc552-155">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="bc552-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="bc552-156">Konfigurace chování NuGetu</span><span class="sxs-lookup"><span data-stu-id="bc552-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
