---
title: Instalace a použití balíčku NuGet pomocí rozhraní se konstatování dotnet
description: Návod k procesu instalace a používání balíčku NuGet v projektu .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231270"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="6679f-103">Úvodní příručka: Instalace a použití balíčku pomocí rozhraní SE konstatování dotnet</span><span class="sxs-lookup"><span data-stu-id="6679f-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="6679f-104">Balíčky NuGet obsahují opakovaně použitelný kód, který vám ostatní vývojáři zpřístupní pro použití ve vašich projektech.</span><span class="sxs-lookup"><span data-stu-id="6679f-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="6679f-105">Podívejte se [na co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="6679f-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="6679f-106">Balíčky jsou nainstalovány do projektu `dotnet add package` .NET Core pomocí příkazu, jak je popsáno v tomto článku pro populární [newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíček.</span><span class="sxs-lookup"><span data-stu-id="6679f-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="6679f-107">Po instalaci, odkazovat na `using <namespace>` balíček v kódu s kde \<obor názvů\> je specifické pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="6679f-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="6679f-108">Potom můžete použít rozhraní API balíčku.</span><span class="sxs-lookup"><span data-stu-id="6679f-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="6679f-109">**Začněte s nuget.org**: Procházení nuget.org je způsob, jakým vývojáři rozhraní .NET obvykle vyhledávají součásti, které mohou znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="6679f-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="6679f-110">Můžete vyhledávat nuget.org přímo nebo najít a nainstalovat balíčky v rámci sady Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="6679f-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6679f-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6679f-111">Prerequisites</span></span>

- <span data-ttu-id="6679f-112">Sada [.NET Core SDK](https://www.microsoft.com/net/download/) `dotnet` , která poskytuje nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="6679f-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="6679f-113">Počínaje Visual Studio 2017, dotnet CLI se automaticky nainstaluje s všechny úlohy související s jádrem .NET.</span><span class="sxs-lookup"><span data-stu-id="6679f-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="6679f-114">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="6679f-114">Create a project</span></span>

<span data-ttu-id="6679f-115">Balíčky NuGet lze nainstalovat do projektu .NET nějakého druhu.</span><span class="sxs-lookup"><span data-stu-id="6679f-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="6679f-116">Pro tento návod vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="6679f-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="6679f-117">Vytvořte složku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="6679f-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="6679f-118">Otevřete příkazový řádek a přepněte do nové složky.</span><span class="sxs-lookup"><span data-stu-id="6679f-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="6679f-119">Vytvořte projekt pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="6679f-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="6679f-120">Slouží `dotnet run` k testování, že aplikace byla vytvořena správně.</span><span class="sxs-lookup"><span data-stu-id="6679f-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="6679f-121">Přidat balíček Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="6679f-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="6679f-122">K instalaci `Newtonsoft.json` balíčku použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="6679f-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="6679f-123">Po dokončení příkazu otevřete soubor a `.csproj` zotřite přidaný odkaz:</span><span class="sxs-lookup"><span data-stu-id="6679f-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="6679f-124">Použití rozhraní Newtonsoft.Json API v aplikaci</span><span class="sxs-lookup"><span data-stu-id="6679f-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="6679f-125">Otevřete `Program.cs` soubor a v horní části souboru přidejte následující řádek:</span><span class="sxs-lookup"><span data-stu-id="6679f-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="6679f-126">K `class Program` řádku přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="6679f-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="6679f-127">Nahraďte `Main` funkci následujícím:</span><span class="sxs-lookup"><span data-stu-id="6679f-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="6679f-128">Vytvořte a spusťte `dotnet run` aplikaci pomocí příkazu.</span><span class="sxs-lookup"><span data-stu-id="6679f-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="6679f-129">Výstupem by měla být reprezentace `Account` JSON objektu v kódu:</span><span class="sxs-lookup"><span data-stu-id="6679f-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="6679f-130">Související video</span><span class="sxs-lookup"><span data-stu-id="6679f-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="6679f-131">Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="6679f-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6679f-132">Další kroky</span><span class="sxs-lookup"><span data-stu-id="6679f-132">Next steps</span></span>

<span data-ttu-id="6679f-133">Gratulujeme k instalaci a používání vašeho prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="6679f-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6679f-134">Instalace a použití balíčků pomocí rozhraní SE kontinu pro dotnet</span><span class="sxs-lookup"><span data-stu-id="6679f-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="6679f-135">Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.</span><span class="sxs-lookup"><span data-stu-id="6679f-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="6679f-136">Přehled a pracovní postup spotřeby balíků</span><span class="sxs-lookup"><span data-stu-id="6679f-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="6679f-137">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="6679f-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="6679f-138">Odkazy na balíčky v souborech projektů</span><span class="sxs-lookup"><span data-stu-id="6679f-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
