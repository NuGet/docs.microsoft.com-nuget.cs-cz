---
title: Úvodní příručka k pomocí NuGet balíčky pomocí rozhraní příkazového řádku dotnet
description: Kurz návod týkající se procesu instalace a použití balíčku NuGet v projektu .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 1060d98278fed89ac63ee17c1896ae8bdce72a9e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426169"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="7c795-103">Rychlý start: Instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="7c795-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="7c795-104">Balíčky NuGet obsahují opakovaně použitelný kód, který jinými vývojáři zpřístupnit je pro použití ve vašich projektech.</span><span class="sxs-lookup"><span data-stu-id="7c795-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="7c795-105">Zobrazit [co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="7c795-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="7c795-106">Balíčky se nainstalují do projektu .NET Core s použitím `dotnet add package` příkaz, jak je popsáno v tomto článku pro oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku.</span><span class="sxs-lookup"><span data-stu-id="7c795-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="7c795-107">Po instalaci se odkazovat na balíček v kódu s `using <namespace>` kde \<obor názvů\> je specifický pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="7c795-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="7c795-108">Pak můžete použít rozhraní API balíčku.</span><span class="sxs-lookup"><span data-stu-id="7c795-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="7c795-109">**Začněte s nuget.org**: Procházení nuget.org je, jak vývojáři na platformě .NET obvykle najdete součásti můžete znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="7c795-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="7c795-110">Můžete vyhledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="7c795-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c795-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7c795-111">Prerequisites</span></span>

- <span data-ttu-id="7c795-112">[.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="7c795-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="7c795-113">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="7c795-113">Create a project</span></span>

<span data-ttu-id="7c795-114">Balíčky NuGet můžete nainstalovat do projektu .NET určitého druhu.</span><span class="sxs-lookup"><span data-stu-id="7c795-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="7c795-115">V tomto návodu vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="7c795-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="7c795-116">Vytvořte složku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="7c795-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="7c795-117">Vytvořte projekt pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="7c795-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="7c795-118">Použití `dotnet run` k otestování, zda aplikace byl vytvořen správně.</span><span class="sxs-lookup"><span data-stu-id="7c795-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="7c795-119">Přidejte balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="7c795-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="7c795-120">Použijte následující příkaz k instalaci `Newtonsoft.json` balíčku:</span><span class="sxs-lookup"><span data-stu-id="7c795-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="7c795-121">Po dokončení příkazu Otevřít `.csproj` soubor přidaný odkaz:</span><span class="sxs-lookup"><span data-stu-id="7c795-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="7c795-122">Použít Newtonsoft.Json rozhraní API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="7c795-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="7c795-123">Otevřít `Program.cs` a přidejte následující řádek na začátek souboru:</span><span class="sxs-lookup"><span data-stu-id="7c795-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="7c795-124">Přidejte následující kód před `class Program` řádku:</span><span class="sxs-lookup"><span data-stu-id="7c795-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="7c795-125">Nahradit `Main` funkce následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="7c795-125">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="7c795-126">Sestavte a spusťte aplikaci pomocí `dotnet run` příkazu.</span><span class="sxs-lookup"><span data-stu-id="7c795-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="7c795-127">Výstup by měl být reprezentaci JSON `Account` objekt v kódu:</span><span class="sxs-lookup"><span data-stu-id="7c795-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="7c795-128">Související články</span><span class="sxs-lookup"><span data-stu-id="7c795-128">Related articles</span></span>

- [<span data-ttu-id="7c795-129">Nainstalovat a používat balíčky pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="7c795-129">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)
- [<span data-ttu-id="7c795-130">Přehled a pracovní postup využití balíčků</span><span class="sxs-lookup"><span data-stu-id="7c795-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="7c795-131">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="7c795-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="7c795-132">Obvyklé konfigurace NuGet</span><span class="sxs-lookup"><span data-stu-id="7c795-132">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
