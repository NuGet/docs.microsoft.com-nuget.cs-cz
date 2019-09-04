---
title: Instalace a použití balíčku NuGet v Visual Studio pro Mac
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu Visual Studio pro Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238525"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="cfb08-103">Rychlý start: Instalace a použití balíčku v Visual Studio pro Mac</span><span class="sxs-lookup"><span data-stu-id="cfb08-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="cfb08-104">Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři.</span><span class="sxs-lookup"><span data-stu-id="cfb08-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="cfb08-105">Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="cfb08-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="cfb08-106">Balíčky se nainstalují do Visual Studio pro Mac projektu pomocí Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="cfb08-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="cfb08-107">Tento článek popisuje proces použití oblíbeného balíčku [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) a projektu konzoly .NET Core.</span><span class="sxs-lookup"><span data-stu-id="cfb08-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="cfb08-108">Stejný postup platí pro všechny ostatní projekty Xamarin nebo .NET Core.</span><span class="sxs-lookup"><span data-stu-id="cfb08-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="cfb08-109">Po instalaci se podívejte na balíček v kódu `using <namespace>` , kde \<obor názvů\> je specifický pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="cfb08-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="cfb08-110">Po provedení odkazu můžete balíček volat prostřednictvím jeho rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="cfb08-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="cfb08-111">**Začínáme s NuGet.org**: Procházení *NuGet.org* je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="cfb08-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="cfb08-112">Můžete vyhledat *NuGet.org* přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="cfb08-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="cfb08-113">Obecné informace najdete v tématu [vyhledání a vyhodnocení balíčků NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="cfb08-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfb08-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="cfb08-114">Prerequisites</span></span>

- <span data-ttu-id="cfb08-115">Visual Studio 2019 pro Mac.</span><span class="sxs-lookup"><span data-stu-id="cfb08-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="cfb08-116">Edici 2019 Community Edition můžete zdarma nainstalovat z [VisualStudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.</span><span class="sxs-lookup"><span data-stu-id="cfb08-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="cfb08-117">Pokud používáte sadu Visual Studio ve Windows, přečtěte si téma [instalace a použití balíčku v aplikaci Visual Studio (pouze Windows)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="cfb08-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="cfb08-118">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="cfb08-118">Create a project</span></span>

<span data-ttu-id="cfb08-119">Balíčky NuGet se dají nainstalovat do libovolného projektu .NET, za předpokladu, že balíček podporuje stejnou cílovou architekturu jako projekt.</span><span class="sxs-lookup"><span data-stu-id="cfb08-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="cfb08-120">Pro tento návod použijte jednoduchou konzolovou aplikaci .NET Core.</span><span class="sxs-lookup"><span data-stu-id="cfb08-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="cfb08-121">Vytvořit projekt v Visual Studio pro Mac pomocí **souborového > nové řešení...** vyberte šablonu **konzolové aplikace > aplikace .NET Core >** .</span><span class="sxs-lookup"><span data-stu-id="cfb08-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="cfb08-122">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="cfb08-122">Click **Next**.</span></span> <span data-ttu-id="cfb08-123">Po zobrazení výzvy přijměte výchozí hodnoty pro **cílovou architekturu** .</span><span class="sxs-lookup"><span data-stu-id="cfb08-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="cfb08-124">Visual Studio vytvoří projekt, který se otevře v Průzkumník řešení.</span><span class="sxs-lookup"><span data-stu-id="cfb08-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="cfb08-125">Přidejte balíček NuGet Newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="cfb08-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="cfb08-126">K instalaci balíčku použijte Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="cfb08-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="cfb08-127">Při instalaci balíčku zaznamená NuGet závislost v souboru projektu nebo `packages.config` v souboru (v závislosti na formátu projektu).</span><span class="sxs-lookup"><span data-stu-id="cfb08-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="cfb08-128">Další informace najdete v tématu [Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="cfb08-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="cfb08-129">Správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="cfb08-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="cfb08-130">V Průzkumník řešení klikněte pravým tlačítkem na **závislosti** a vyberte **Přidat balíčky...** .</span><span class="sxs-lookup"><span data-stu-id="cfb08-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="cfb08-132">V levém horním rohu dialogového okna vyberte "nuget.org" jako **zdroj balíčku** a vyhledejte **Newtonsoft. JSON**, vyberte tento balíček v seznamu a vyberte **Přidat balíčky...** :</span><span class="sxs-lookup"><span data-stu-id="cfb08-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Vyhledání balíčku Newtonsoft. JSON](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="cfb08-134">Pokud chcete získat další informace o Správci balíčků NuGet, přečtěte si téma [instalace a Správa balíčků pomocí Visual Studio pro Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="cfb08-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="cfb08-135">Použití rozhraní API Newtonsoft. JSON v aplikaci</span><span class="sxs-lookup"><span data-stu-id="cfb08-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="cfb08-136">Pomocí balíčku Newtonsoft. JSON v projektu můžete zavolat jeho `JsonConvert.SerializeObject` metodu pro převod objektu na řetězec čitelný z lidského.</span><span class="sxs-lookup"><span data-stu-id="cfb08-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="cfb08-137">`Program.cs` Otevřete soubor (umístěný v oblast řešení) a nahraďte jeho obsah následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="cfb08-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

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

1. <span data-ttu-id="cfb08-138">Sestavte a spusťte aplikaci výběrem možnosti **spustit > spustit ladění**:</span><span class="sxs-lookup"><span data-stu-id="cfb08-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="cfb08-139">Po spuštění aplikace se v konzole zobrazí serializovaný výstup JSON:</span><span class="sxs-lookup"><span data-stu-id="cfb08-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Výstup aplikace konzoly](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="cfb08-141">Další postup</span><span class="sxs-lookup"><span data-stu-id="cfb08-141">Next steps</span></span>
<span data-ttu-id="cfb08-142">Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="cfb08-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cfb08-143">Instalace a Správa balíčků pomocí Visual Studio pro Mac</span><span class="sxs-lookup"><span data-stu-id="cfb08-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="cfb08-144">Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.</span><span class="sxs-lookup"><span data-stu-id="cfb08-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="cfb08-145">Přehled a pracovní postup pro spotřebu balíčku</span><span class="sxs-lookup"><span data-stu-id="cfb08-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="cfb08-146">Odkazy na balíčky v souborech projektů</span><span class="sxs-lookup"><span data-stu-id="cfb08-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
