---
title: Úvodní příručka k použití NuGet balíčky prostřednictvím rozhraní příkazového řádku dotnet.
description: Návod kurz týkající se procesu instalace a použití balíčku NuGet v projektu .NET Core.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 41a249394a8a0504cc8841d3bdb67ad29ec2dc26
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="120a3-103">Rychlý úvod: Instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="120a3-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="120a3-104">Balíčky NuGet obsahovat opakovaně použitelný kód, který jinými vývojáři zpřístupnění pro použití ve vašich projektů.</span><span class="sxs-lookup"><span data-stu-id="120a3-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="120a3-105">V tématu [co je NuGet?](../What-is-NuGet.md) pozadí.</span><span class="sxs-lookup"><span data-stu-id="120a3-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="120a3-106">Balíčky jsou nainstalovány do projektu .NET Core pomocí `dotnet add package` příkaz, jak je popsáno v tomto článku Oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku.</span><span class="sxs-lookup"><span data-stu-id="120a3-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="120a3-107">Po instalaci odkazovat na balíček v kódu pomocí `using <namespace>` kde \<obor názvů\> je specifická pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="120a3-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="120a3-108">Pak můžete použít rozhraní API balíčku.</span><span class="sxs-lookup"><span data-stu-id="120a3-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="120a3-109">**Začněte s nuget.org**: procházení nuget.org je, jak .NET vývojáři obvykle najít součásti můžete opakovaně použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="120a3-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="120a3-110">Můžete hledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="120a3-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="120a3-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="120a3-111">Prerequisites</span></span>

- <span data-ttu-id="120a3-112">[.NET Core SDK](https://www.microsoft.com/net/download/), který poskytuje `dotnet` nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="120a3-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="120a3-113">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="120a3-113">Create a project</span></span>

<span data-ttu-id="120a3-114">Balíčky NuGet lze nainstalovat do projektu .NET určitého druhu.</span><span class="sxs-lookup"><span data-stu-id="120a3-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="120a3-115">Pro účely tohoto postupu vytvoření jednoduché projektu konzoly .NET Core následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="120a3-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="120a3-116">Vytvořte složku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="120a3-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="120a3-117">Vytvoření projektu pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="120a3-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="120a3-118">Použití `dotnet run` k testování, aby byla správně vytvořená aplikace.</span><span class="sxs-lookup"><span data-stu-id="120a3-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="120a3-119">Přidejte balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="120a3-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="120a3-120">Použijte následující příkaz k instalaci `Newtonsoft.json` balíčku:</span><span class="sxs-lookup"><span data-stu-id="120a3-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="120a3-121">Po dokončení příkazu, otevřete `.csproj` soubor přidaný odkaz:</span><span class="sxs-lookup"><span data-stu-id="120a3-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="120a3-122">Použít Newtonsoft.Json rozhraní API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="120a3-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="120a3-123">Otevřete `Program.cs` souborů a v horní části souboru přidejte následující řádek:</span><span class="sxs-lookup"><span data-stu-id="120a3-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="120a3-124">Přidejte následující kód, než `class Program` řádku:</span><span class="sxs-lookup"><span data-stu-id="120a3-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="120a3-125">Nahraďte `Main` funkce následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="120a3-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="120a3-126">Sestavení a spuštění aplikace pomocí `dotnet run` příkaz.</span><span class="sxs-lookup"><span data-stu-id="120a3-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="120a3-127">Výstup by měl být reprezentaci JSON `Account` objektu v kódu:</span><span class="sxs-lookup"><span data-stu-id="120a3-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="120a3-128">Související články</span><span class="sxs-lookup"><span data-stu-id="120a3-128">Related articles</span></span>

- [<span data-ttu-id="120a3-129">Přehled a pracovní postup spotřeby balíčku</span><span class="sxs-lookup"><span data-stu-id="120a3-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="120a3-130">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="120a3-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="120a3-131">Způsoby, jak nainstalovat balíček</span><span class="sxs-lookup"><span data-stu-id="120a3-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="120a3-132">Konfigurace chování NuGetu</span><span class="sxs-lookup"><span data-stu-id="120a3-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
