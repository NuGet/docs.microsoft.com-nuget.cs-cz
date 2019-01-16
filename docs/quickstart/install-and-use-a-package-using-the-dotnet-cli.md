---
title: Úvodní příručka k pomocí NuGet balíčky pomocí rozhraní příkazového řádku dotnet
description: Kurz návod týkající se procesu instalace a použití balíčku NuGet v projektu .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 4b593cc215ad68629e5a93d1f17c90e53c0b4f4f
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324627"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="74c9d-103">Rychlý start: Instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="74c9d-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="74c9d-104">Balíčky NuGet obsahují opakovaně použitelný kód, který jinými vývojáři zpřístupnit je pro použití ve vašich projektech.</span><span class="sxs-lookup"><span data-stu-id="74c9d-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="74c9d-105">Zobrazit [co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="74c9d-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="74c9d-106">Balíčky se nainstalují do projektu .NET Core s použitím `dotnet add package` příkaz, jak je popsáno v tomto článku pro oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku.</span><span class="sxs-lookup"><span data-stu-id="74c9d-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="74c9d-107">Po instalaci se odkazovat na balíček v kódu s `using <namespace>` kde \<obor názvů\> je specifický pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="74c9d-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="74c9d-108">Pak můžete použít rozhraní API balíčku.</span><span class="sxs-lookup"><span data-stu-id="74c9d-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="74c9d-109">**Začněte s nuget.org**: Procházení nuget.org je, jak vývojáři na platformě .NET obvykle najdete součásti můžete znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="74c9d-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="74c9d-110">Můžete vyhledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="74c9d-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74c9d-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="74c9d-111">Prerequisites</span></span>

- <span data-ttu-id="74c9d-112">[.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="74c9d-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="74c9d-113">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="74c9d-113">Create a project</span></span>

<span data-ttu-id="74c9d-114">Balíčky NuGet můžete nainstalovat do projektu .NET určitého druhu.</span><span class="sxs-lookup"><span data-stu-id="74c9d-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="74c9d-115">V tomto návodu vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="74c9d-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="74c9d-116">Vytvořte složku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="74c9d-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="74c9d-117">Vytvořte projekt pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="74c9d-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="74c9d-118">Použití `dotnet run` k otestování, zda aplikace byl vytvořen správně.</span><span class="sxs-lookup"><span data-stu-id="74c9d-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="74c9d-119">Přidejte balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="74c9d-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="74c9d-120">Použijte následující příkaz k instalaci `Newtonsoft.json` balíčku:</span><span class="sxs-lookup"><span data-stu-id="74c9d-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="74c9d-121">Po dokončení příkazu Otevřít `.csproj` soubor přidaný odkaz:</span><span class="sxs-lookup"><span data-stu-id="74c9d-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="74c9d-122">Použít Newtonsoft.Json rozhraní API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="74c9d-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="74c9d-123">Otevřít `Program.cs` a přidejte následující řádek na začátek souboru:</span><span class="sxs-lookup"><span data-stu-id="74c9d-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="74c9d-124">Přidejte následující kód před `class Program` řádku:</span><span class="sxs-lookup"><span data-stu-id="74c9d-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="74c9d-125">Nahradit `Main` funkce následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="74c9d-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="74c9d-126">Sestavte a spusťte aplikaci pomocí `dotnet run` příkazu.</span><span class="sxs-lookup"><span data-stu-id="74c9d-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="74c9d-127">Výstup by měl být reprezentaci JSON `Account` objekt v kódu:</span><span class="sxs-lookup"><span data-stu-id="74c9d-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="74c9d-128">Související články</span><span class="sxs-lookup"><span data-stu-id="74c9d-128">Related articles</span></span>

- [<span data-ttu-id="74c9d-129">Přehled a pracovní postup využití balíčků</span><span class="sxs-lookup"><span data-stu-id="74c9d-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="74c9d-130">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="74c9d-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="74c9d-131">Způsoby instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="74c9d-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="74c9d-132">Konfigurace chování NuGetu</span><span class="sxs-lookup"><span data-stu-id="74c9d-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
