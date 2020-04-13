---
title: Instalace a použití balíčku NuGet v Sadě Visual Studio pro Mac
description: Návod k procesu instalace a používání balíčku NuGet v projektu Visual Studio for Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238525"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="7ae79-103">Úvodní příručka: Instalace a použití balíčku v Visual Studiu pro Mac</span><span class="sxs-lookup"><span data-stu-id="7ae79-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="7ae79-104">Balíčky NuGet obsahují opakovaně použitelný kód, který vám ostatní vývojáři zpřístupní pro použití ve vašich projektech.</span><span class="sxs-lookup"><span data-stu-id="7ae79-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="7ae79-105">Podívejte se [na co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="7ae79-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="7ae79-106">Balíčky jsou nainstalovány do projektu Sady Visual Studio pro Mac pomocí Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ae79-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="7ae79-107">Tento článek ukazuje proces pomocí populárního balíčku [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) a konzolového projektu .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7ae79-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="7ae79-108">Stejný proces platí pro všechny ostatní Xamarin nebo .NET Core projektu.</span><span class="sxs-lookup"><span data-stu-id="7ae79-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="7ae79-109">Po instalaci, odkazovat na `using <namespace>` balíček v kódu s kde \<obor názvů\> je specifické pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="7ae79-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="7ae79-110">Jakmile je odkaz, můžete volat balíček prostřednictvím jeho rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="7ae79-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="7ae79-111">**Začněte s nuget.org**: Procházení *nuget.org* je způsob, jakým vývojáři rozhraní .NET obvykle vyhledávají součásti, které mohou znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="7ae79-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="7ae79-112">Můžete hledat *nuget.org* přímo nebo najít a nainstalovat balíčky v rámci sady Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="7ae79-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="7ae79-113">Obecné informace naleznete v [tématu Hledání a vyhodnocení balíčků NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7ae79-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ae79-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7ae79-114">Prerequisites</span></span>

- <span data-ttu-id="7ae79-115">Visual Studio 2019 pro Mac.</span><span class="sxs-lookup"><span data-stu-id="7ae79-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="7ae79-116">Můžete nainstalovat edici Community 2019 zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7ae79-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="7ae79-117">Pokud používáte Visual Studio ve Windows, přečtěte si informace [o instalaci a použití balíčku v sadě Visual Studio (jenom windows).](install-and-use-a-package-in-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="7ae79-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="7ae79-118">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="7ae79-118">Create a project</span></span>

<span data-ttu-id="7ae79-119">Balíčky NuGet lze nainstalovat do libovolného projektu .NET za předpokladu, že balíček podporuje stejný cílový rámec jako projekt.</span><span class="sxs-lookup"><span data-stu-id="7ae79-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="7ae79-120">Pro tento návod použijte jednoduchou aplikaci .NET Core Console.</span><span class="sxs-lookup"><span data-stu-id="7ae79-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="7ae79-121">Vytvořte projekt ve Visual Studiu for Mac pomocí **souboru > novéřešení...**, vyberte šablonu **aplikace .NET Core > App > Console.**</span><span class="sxs-lookup"><span data-stu-id="7ae79-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="7ae79-122">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-122">Click **Next**.</span></span> <span data-ttu-id="7ae79-123">Při přijetí výchozích hodnot pro **cílovou architekturu** po zobrazení výzvy.</span><span class="sxs-lookup"><span data-stu-id="7ae79-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="7ae79-124">Visual Studio vytvoří projekt, který se otevře v Průzkumníku řešení.</span><span class="sxs-lookup"><span data-stu-id="7ae79-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="7ae79-125">Přidat balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="7ae79-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="7ae79-126">Chcete-li nainstalovat balíček, použijte Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ae79-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="7ae79-127">Při instalaci balíčku NuGet zaznamenává závislost v souboru projektu `packages.config` nebo souboru (v závislosti na formátu projektu).</span><span class="sxs-lookup"><span data-stu-id="7ae79-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="7ae79-128">Další informace naleznete v [tématu Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="7ae79-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="7ae79-129">Správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="7ae79-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="7ae79-130">V Průzkumníku řešení klikněte pravým **tlačítkem** myši na závislosti a zvolte **Přidat balíčky...**.</span><span class="sxs-lookup"><span data-stu-id="7ae79-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="7ae79-132">V levém horním rohu dialogového okna zvolte "nuget.org" jako **zdroj balíčku** a vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte **Přidat balíčky...**:</span><span class="sxs-lookup"><span data-stu-id="7ae79-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Lokalizace newtonsoft.json balíčku](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="7ae79-134">Pokud chcete další informace o Správci balíčků NuGet, přečtěte si informace [o instalaci a správě balíčků pomocí Sady Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="7ae79-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="7ae79-135">Použití rozhraní Newtonsoft.Json API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="7ae79-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="7ae79-136">S newtonsoft.Json balíček v projektu, `JsonConvert.SerializeObject` můžete volat jeho metodu převést objekt na člověka čitelný řetězec.</span><span class="sxs-lookup"><span data-stu-id="7ae79-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="7ae79-137">Otevřete `Program.cs` soubor (umístěný v panelu řešení) a nahraďte obsah souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="7ae79-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="7ae79-138">Vytvořte a spusťte aplikaci tak, že vyberete **Spustit > Spustit ladění**:</span><span class="sxs-lookup"><span data-stu-id="7ae79-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="7ae79-139">Po spuštění aplikace se v konzole zobrazí serializovaný výstup JSON:</span><span class="sxs-lookup"><span data-stu-id="7ae79-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Výstup aplikace Konzola](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="7ae79-141">Další kroky</span><span class="sxs-lookup"><span data-stu-id="7ae79-141">Next steps</span></span>
<span data-ttu-id="7ae79-142">Gratulujeme k instalaci a používání vašeho prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="7ae79-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ae79-143">Instalace a správa balíčků pomocí Visual Studia pro Mac</span><span class="sxs-lookup"><span data-stu-id="7ae79-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="7ae79-144">Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.</span><span class="sxs-lookup"><span data-stu-id="7ae79-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="7ae79-145">Přehled a pracovní postup spotřeby balíků</span><span class="sxs-lookup"><span data-stu-id="7ae79-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="7ae79-146">Odkazy na balíčky v souborech projektů</span><span class="sxs-lookup"><span data-stu-id="7ae79-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
