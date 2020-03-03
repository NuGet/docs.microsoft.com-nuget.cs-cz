---
title: Instalace a použití balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231270"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="d7f5e-103">Rychlý Start: instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="d7f5e-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="d7f5e-104">Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="d7f5e-105">Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="d7f5e-106">Balíčky jsou nainstalovány do projektu .NET Core pomocí příkazu `dotnet add package`, jak je popsáno v tomto článku pro oblíbený balíček [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) .</span><span class="sxs-lookup"><span data-stu-id="d7f5e-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="d7f5e-107">Po instalaci se podívejte na balíček v kódu s `using <namespace>`, kde \<oboru názvů\> je specifické pro balíček, který používáte.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="d7f5e-108">Pak můžete použít rozhraní API balíčku.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="d7f5e-109">**Začínáme s NuGet.org**: prohlížení NuGet.org je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="d7f5e-110">Můžete vyhledat nuget.org přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7f5e-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d7f5e-111">Prerequisites</span></span>

- <span data-ttu-id="d7f5e-112">[.NET Core SDK](https://www.microsoft.com/net/download/), který poskytuje nástroj příkazového řádku `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="d7f5e-113">Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="d7f5e-114">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="d7f5e-114">Create a project</span></span>

<span data-ttu-id="d7f5e-115">Balíčky NuGet se dají nainstalovat do projektu .NET nějakého druhu.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="d7f5e-116">Pro tento návod vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d7f5e-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="d7f5e-117">Vytvořte složku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="d7f5e-118">Otevřete příkazový řádek a přepněte do nové složky.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="d7f5e-119">Vytvořte projekt pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="d7f5e-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="d7f5e-120">Použijte `dotnet run` k otestování, jestli se aplikace správně vytvořila.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="d7f5e-121">Přidejte balíček NuGet Newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="d7f5e-122">K instalaci balíčku `Newtonsoft.json` použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="d7f5e-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="d7f5e-123">Po dokončení příkazu otevřete soubor `.csproj`, abyste viděli přidaný odkaz:</span><span class="sxs-lookup"><span data-stu-id="d7f5e-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="d7f5e-124">Použití rozhraní API Newtonsoft. JSON v aplikaci</span><span class="sxs-lookup"><span data-stu-id="d7f5e-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="d7f5e-125">Otevřete soubor `Program.cs` a do horní části souboru přidejte následující řádek:</span><span class="sxs-lookup"><span data-stu-id="d7f5e-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="d7f5e-126">Přidejte následující kód před `class Program` řádek:</span><span class="sxs-lookup"><span data-stu-id="d7f5e-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="d7f5e-127">Nahraďte funkci `Main` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d7f5e-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="d7f5e-128">Sestavte a spusťte aplikaci pomocí příkazu `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="d7f5e-129">Výstupem by měl být reprezentace JSON objektu `Account` v kódu:</span><span class="sxs-lookup"><span data-stu-id="d7f5e-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="d7f5e-130">Související video</span><span class="sxs-lookup"><span data-stu-id="d7f5e-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="d7f5e-131">Další videa k NuGetu najdete na webu [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="d7f5e-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7f5e-132">Další kroky</span><span class="sxs-lookup"><span data-stu-id="d7f5e-132">Next steps</span></span>

<span data-ttu-id="d7f5e-133">Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="d7f5e-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7f5e-134">Instalace a použití balíčků pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="d7f5e-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="d7f5e-135">Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.</span><span class="sxs-lookup"><span data-stu-id="d7f5e-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="d7f5e-136">Přehled a pracovní postup pro spotřebu balíčku</span><span class="sxs-lookup"><span data-stu-id="d7f5e-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="d7f5e-137">Vyhledání a výběr balíčků</span><span class="sxs-lookup"><span data-stu-id="d7f5e-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="d7f5e-138">Odkazy na balíčky v souborech projektů</span><span class="sxs-lookup"><span data-stu-id="d7f5e-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
