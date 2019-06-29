---
title: Vytvoření a publikování balíčku .NET Standard ve Windows pomocí sady Visual Studio
description: Kurz návod týkající se vytváření a publikování balíčku .NET Standard NuGet pomocí sady Visual Studio 2017 na Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c75785d361f25564c8a59d7a2d85924c570a7b9a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467816"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="30b33-103">Rychlý start: Vytvoření a publikování balíčku NuGet pomocí sady Visual Studio (.NET Standard, jenom Windows)</span><span class="sxs-lookup"><span data-stu-id="30b33-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="30b33-104">Je jednoduchý proces vytvoření balíčku NuGet z knihovny .NET Standard třídy v sadě Visual Studio ve Windows a potom ji publikovat na nuget.org pomocí nástroje příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="30b33-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="30b33-105">V tomto rychlém startu platí pro Visual Studio 2017 pro Windows pouze.</span><span class="sxs-lookup"><span data-stu-id="30b33-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="30b33-106">Visual Studio pro Mac nezahrnuje možnosti popsané tady.</span><span class="sxs-lookup"><span data-stu-id="30b33-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="30b33-107">Použití [nástroje rozhraní příkazového řádku dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) místo.</span><span class="sxs-lookup"><span data-stu-id="30b33-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30b33-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="30b33-108">Prerequisites</span></span>

1. <span data-ttu-id="30b33-109">Instalaci libovolné edice sady Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy.</span><span class="sxs-lookup"><span data-stu-id="30b33-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="30b33-110">Visual Studio 2017 automaticky zahrnuje NuGet možnosti, když je nainstalovaná úloha .NET.</span><span class="sxs-lookup"><span data-stu-id="30b33-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="30b33-111">Nainstalujte jedním z nástrojů rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="30b33-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="30b33-112">Pro `dotnet` rozhraní příkazového řádku, nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="30b33-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="30b33-113">Dotnet CLI se vyžaduje pro .NET Standard projekty, které používají formát SDK – vizuální styl (atribut SDK).</span><span class="sxs-lookup"><span data-stu-id="30b33-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="30b33-114">Pro `nuget.exe` rozhraní příkazového řádku, si ji stáhnout z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), uložení `.exe` soubor vhodný složky a přidání složky do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="30b33-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="30b33-115">Rozhraní příkazového řádku nuget.exe se používá pro knihovny .NET Standard ve formátu sady SDK style.</span><span class="sxs-lookup"><span data-stu-id="30b33-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="30b33-116">[Zaregistrujte si bezplatný účet na nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="30b33-116">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="30b33-117">Vytvoření nového účtu se odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="30b33-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="30b33-118">Účet musí ověřit dříve, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="30b33-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="30b33-119">Vytvořte projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="30b33-119">Create a class library project</span></span>

<span data-ttu-id="30b33-120">Můžete použít existující projekt knihovna tříd rozhraní .NET Standard pro kód, který chcete balíček nebo vytvořit jednoduchý následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="30b33-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="30b33-121">V sadě Visual Studio, zvolte **soubor > Nový > projekt**, rozbalte **Visual C# > .NET Standard** uzlu, vyberte šablonu "Knihovna tříd (.NET Standard)", pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="30b33-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="30b33-122">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** k Ujistěte se, že projekt je vytvořený řádně.</span><span class="sxs-lookup"><span data-stu-id="30b33-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="30b33-123">Knihovny DLL se nachází složka pro ladění (nebo vydání, pokud vytváříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="30b33-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="30b33-124">V rámci skutečné balíčku NuGet samozřejmě, můžete implementovat mnoho užitečných funkcí, se kterými ostatní můžete vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="30b33-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="30b33-125">V tomto návodu ale nebude napíšete žádný další kód vzhledem k tomu, že knihovna tříd z této šablony je dostatečná pro vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="30b33-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="30b33-126">Pokud chcete některé funkční kód pro balíček, stále, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="30b33-126">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="30b33-127">Pokud nemáte důvod nerozhodnete jinak, .NET Standard je upřednostňovaným cílem, pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projektů.</span><span class="sxs-lookup"><span data-stu-id="30b33-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="30b33-128">Konfigurace vlastností balíčku</span><span class="sxs-lookup"><span data-stu-id="30b33-128">Configure package properties</span></span>

1. <span data-ttu-id="30b33-129">Vyberte **projektu > vlastnosti** nabídce příkaz a pak vyberte **balíčku** kartu. ( **Balíčku** kartě se zobrazí pouze pro projekty knihovny tříd .NET Standard; Pokud se zaměřujete na rozhraní .NET Framework, přečtěte si téma [vytvoření a publikování balíčku .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) místo.</span><span class="sxs-lookup"><span data-stu-id="30b33-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="30b33-130">Pokud se nezobrazí pro projekt .NET Standard, budete muset aktualizovat na nejnovější verzi sady Visual Studio 2017.)</span><span class="sxs-lookup"><span data-stu-id="30b33-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Vlastnosti balíčku NuGet v projektu sady Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="30b33-132">Balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost **značky** vlastnost, protože značky pomoci ostatním najít váš balíček a pochopit jeho význam.</span><span class="sxs-lookup"><span data-stu-id="30b33-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="30b33-133">Zadejte jedinečný identifikátor balíčku a vyplňte všechny požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="30b33-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="30b33-134">Popis různých vlastností najdete v tématu [odkaz na soubor souboru .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="30b33-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="30b33-135">Všechny vlastnosti zde pohledu `.nuspec` manifestu, který sada Visual Studio vytvoří pro projekt.</span><span class="sxs-lookup"><span data-stu-id="30b33-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="30b33-136">Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo cokoli, co můžete hostovat používáte.</span><span class="sxs-lookup"><span data-stu-id="30b33-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="30b33-137">Pro Tento názorný postup doporučujeme, abyste pozdějším kroku publikování provádění balíček veřejně viditelné (i když nepravděpodobné, že kdo bude ve skutečnosti použít) včetně "Ukázkový" nebo "Test" v názvu.</span><span class="sxs-lookup"><span data-stu-id="30b33-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="30b33-138">Při pokusu publikovat balíček s názvem, který již existuje, se zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="30b33-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="30b33-139">Volitelné: Pokud chcete zobrazit vlastnosti přímo v souboru projektu, klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **upravit AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="30b33-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="30b33-140">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="30b33-140">Run the pack command</span></span>

1. <span data-ttu-id="30b33-141">Nastavení konfigurace **vydání**.</span><span class="sxs-lookup"><span data-stu-id="30b33-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="30b33-142">Klikněte pravým tlačítkem myši na projekt v **Průzkumníka řešení** a vyberte **Pack** příkaz:</span><span class="sxs-lookup"><span data-stu-id="30b33-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Příkaz balíčku NuGet v místní nabídce projektu sady Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="30b33-144">Visual Studio vytvoří projekt a vytvoří `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="30b33-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="30b33-145">Zkontrolujte **výstup** okna podrobnosti (podobně jako následující), který obsahuje cestu k souboru balíčku.</span><span class="sxs-lookup"><span data-stu-id="30b33-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="30b33-146">Všimněte si také, že sestavení je v `bin\Release\netstandard2.0` befits jako cílové rozhraní .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="30b33-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="30b33-147">Alternativní možnost: balíček pomocí nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="30b33-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="30b33-148">Jako alternativu k použití **Pack** příkaz nabídky, NuGet 4.x+ a podporuje MSBuild 15.1 + `pack` cílit při projekt obsahuje data potřebný balíček.</span><span class="sxs-lookup"><span data-stu-id="30b33-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="30b33-149">Otevřete příkazový řádek, přejděte do složky vašeho projektu a spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="30b33-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="30b33-150">(Obvykle chcete spustit "Pro vývojáře příkazového řádku pro Visual Studio" z nabídky Start, jak bude nakonfigurován s všechny nezbytné cesty pro MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="30b33-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="30b33-151">Balíček pak najdete v `bin\Release` složky.</span><span class="sxs-lookup"><span data-stu-id="30b33-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="30b33-152">Další možnosti s `msbuild -t:pack`, naleznete v tématu [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="30b33-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="30b33-153">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="30b33-153">Publish the package</span></span>

<span data-ttu-id="30b33-154">Jakmile budete mít `.nupkg` souboru, ji publikujete do nuget.org buď pomocí `nuget.exe` rozhraní příkazového řádku nebo `dotnet.exe` rozhraní příkazového řádku spolu s klíčem rozhraní API získaných z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="30b33-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="30b33-155">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="30b33-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="30b33-156">Publikování pomocí nasdílení změn nuget dotnet (rozhraní příkazového řádku dotnet)</span><span class="sxs-lookup"><span data-stu-id="30b33-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="30b33-157">Tento krok je alternativou k používání `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="30b33-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="30b33-158">Publikování pomocí nasdílení změn nuget (nuget.exe rozhraní příkazového řádku)</span><span class="sxs-lookup"><span data-stu-id="30b33-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="30b33-159">Tento krok je alternativou k používání `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="30b33-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="30b33-160">Změnit na složku obsahující `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="30b33-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="30b33-161">Spusťte následující příkaz, zadávání názvu balíčku a nahraďte hodnotu klíče svůj klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="30b33-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="30b33-162">nuget.exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="30b33-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="30b33-163">Zobrazit [nuget nabízených](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="30b33-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="30b33-164">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="30b33-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="30b33-165">Správa publikované balíčku</span><span class="sxs-lookup"><span data-stu-id="30b33-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="30b33-166">Přidání souboru readme a další soubory</span><span class="sxs-lookup"><span data-stu-id="30b33-166">Adding a readme and other files</span></span>

<span data-ttu-id="30b33-167">Přímo zadat soubory, které chcete zahrnout do balíčku, upravte soubor projektu a použít `content` vlastnost:</span><span class="sxs-lookup"><span data-stu-id="30b33-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="30b33-168">Tato možnost zahrne soubor s názvem `readme.txt` v kořenovém adresáři balíčku.</span><span class="sxs-lookup"><span data-stu-id="30b33-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="30b33-169">Visual Studio zobrazí okamžitě po instalaci balíčku přímo obsah tohoto souboru jako prostý text.</span><span class="sxs-lookup"><span data-stu-id="30b33-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="30b33-170">(Soubory Readme nejsou zobrazeny pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="30b33-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="30b33-171">Tady je například jak se zobrazí v souboru readme HtmlAgilityPack balíčku:</span><span class="sxs-lookup"><span data-stu-id="30b33-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazit soubor readme pro balíček NuGet při instalaci](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="30b33-173">V něm nebudou zahrnuty do výsledný balíček nebude výsledkem pouze přidání readme.txt v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="30b33-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="30b33-174">Související témata</span><span class="sxs-lookup"><span data-stu-id="30b33-174">Related topics</span></span>

- [<span data-ttu-id="30b33-175">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="30b33-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="30b33-176">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="30b33-176">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="30b33-177">Balíčky v předběžné verzi</span><span class="sxs-lookup"><span data-stu-id="30b33-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="30b33-178">Podpora více cílových platforem</span><span class="sxs-lookup"><span data-stu-id="30b33-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="30b33-179">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="30b33-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="30b33-180">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="30b33-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="30b33-181">Dokumentace ke službě knihovna .NET standard</span><span class="sxs-lookup"><span data-stu-id="30b33-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="30b33-182">Portování do .NET Core v rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="30b33-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
