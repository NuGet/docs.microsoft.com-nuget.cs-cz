---
title: Vytvoření a publikování balíček rozhraní .NET Framework pomocí sady Visual Studio v systému Windows
description: Návod kurz týkající se vytváření a publikování balíčku NuGet pro rozhraní .NET Framework pomocí Visual Studio 2017 v systému Windows.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: ba02b53c6ac0b4172b8611958775980ce401bf9b
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="3143d-103">Rychlý úvod: Vytvoření a publikování balíčku pomocí sady Visual Studio (rozhraní .NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="3143d-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="3143d-104">Vytvoření balíčku NuGet z knihovny tříd rozhraní .NET Framework zahrnuje vytváření knihovny DLL v sadě Visual Studio v systému Windows, a potom pomocí nástroje příkazového řádku nuget.exe vytvoření a publikování balíčku.</span><span class="sxs-lookup"><span data-stu-id="3143d-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="3143d-105">Tento rychlý start platí pro Visual Studio 2017 pro systém Windows jenom.</span><span class="sxs-lookup"><span data-stu-id="3143d-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="3143d-106">Visual Studio pro Mac nezahrnuje možnosti popsané v tomto poli.</span><span class="sxs-lookup"><span data-stu-id="3143d-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="3143d-107">Použití [nástrojů příkazového řádku dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) místo.</span><span class="sxs-lookup"><span data-stu-id="3143d-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3143d-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3143d-108">Prerequisites</span></span>

1. <span data-ttu-id="3143d-109">Nainstalujte všechny edice Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy.</span><span class="sxs-lookup"><span data-stu-id="3143d-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="3143d-110">Visual Studio 2017 automaticky zahrnuje NuGet možností při instalaci rozhraní .NET zatížení.</span><span class="sxs-lookup"><span data-stu-id="3143d-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="3143d-111">Nainstalujte `nuget.exe` CLI stažením z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, `.exe` souboru do složky vhodný, a přidáním této složce do vaší proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="3143d-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="3143d-112">[Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="3143d-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="3143d-113">Vytvoření nového účtu odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="3143d-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="3143d-114">Účet je potřeba zkontrolovat, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="3143d-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="3143d-115">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="3143d-115">Create a class library project</span></span>

<span data-ttu-id="3143d-116">Můžete použít existující projekt knihovna tříd rozhraní .NET Framework pro kód, který chcete balíček nebo vytvořit jednoduchý takto:</span><span class="sxs-lookup"><span data-stu-id="3143d-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="3143d-117">V sadě Visual Studio, vyberte **soubor > Nový > projekt**, vyberte **Visual C#** uzlu, vyberte šablonu, "Knihovny tříd (rozhraní .NET Framework)", název projektu AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="3143d-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="3143d-118">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** a ujistěte se, vytvoření projektu správně.</span><span class="sxs-lookup"><span data-stu-id="3143d-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="3143d-119">Knihovny DLL nachází v rámci ladění složky (nebo verze, pokud vytváříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="3143d-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="3143d-120">V rámci skutečné balíčku NuGet samozřejmě můžete implementovat řadu užitečných funkcí, se kterými ostatní mohou vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="3143d-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="3143d-121">Můžete také nastavit cílové rozhraní, ale chcete.</span><span class="sxs-lookup"><span data-stu-id="3143d-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="3143d-122">Například v tématu příručky pro [UWP](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="3143d-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="3143d-123">V tomto návodu však nebude napsat další kód, protože knihovny tříd ze šablony, stačí vytvořit balíček.</span><span class="sxs-lookup"><span data-stu-id="3143d-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="3143d-124">Pokud chcete některé funkční kód pro balíček, stále, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="3143d-124">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

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
> <span data-ttu-id="3143d-125">Pokud nemáte důvod, proč zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projekty.</span><span class="sxs-lookup"><span data-stu-id="3143d-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="3143d-126">V tématu [vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="3143d-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="3143d-127">Konfigurovat vlastnosti projektu pro balíček</span><span class="sxs-lookup"><span data-stu-id="3143d-127">Configure project properties for the package</span></span>

<span data-ttu-id="3143d-128">Balíček NuGet obsahuje manifest ( `.nuspec` soubor), který obsahuje relevantní metadata, jako je například identifikátor balíčku, číslo verze, popis a další.</span><span class="sxs-lookup"><span data-stu-id="3143d-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="3143d-129">Některé z těchto lze rozlišovat z vlastností projektu přímo, což zabraňuje samostatně nutnost jejich následné aktualizace v projektu a manifest.</span><span class="sxs-lookup"><span data-stu-id="3143d-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="3143d-130">Tato část popisuje, kde se má nastavit příslušné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="3143d-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="3143d-131">Vyberte **Projekt > vlastnosti** nabídky příkazu a pak vyberte **aplikace** kartě.</span><span class="sxs-lookup"><span data-stu-id="3143d-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="3143d-132">V **název sestavení** pole, zadejte svůj balíček jedinečný identifikátor.</span><span class="sxs-lookup"><span data-stu-id="3143d-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="3143d-133">Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte.</span><span class="sxs-lookup"><span data-stu-id="3143d-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="3143d-134">Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).</span><span class="sxs-lookup"><span data-stu-id="3143d-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="3143d-135">Pokud se pokusíte o publikování balíčku s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="3143d-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="3143d-136">Vyberte **informací o sestavení...**  tlačítko, které vyvolá dialogové okno, ve kterém můžete zadat další vlastnosti, které přenášejí do manifestu (viz [odkaz na soubor příponou .nuspec - nahrazení tokeny](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="3143d-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="3143d-137">Nejčastěji používané pole jsou **název**, **popis**, **společnosti**, **Copyright**, a **verze sestavení**.</span><span class="sxs-lookup"><span data-stu-id="3143d-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="3143d-138">Tyto vlastnosti se zobrazí nakonec součástí vašeho balíčku na hostitele, jako je nuget.org, proto se ujistěte, že jsou k plně popisný.</span><span class="sxs-lookup"><span data-stu-id="3143d-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informace o sestavení v rozhraní .NET Framework projektu v sadě Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="3143d-140">Volitelné: Chcete-li zobrazit a upravit vlastnosti přímo, otevřete `Properties/AssemblyInfo.cs` v projektu.</span><span class="sxs-lookup"><span data-stu-id="3143d-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="3143d-141">Pokud jsou nastaveny vlastnosti, nastavte konfiguraci projektu na **verze** a znovu sestavte projekt ke generování aktualizované knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="3143d-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="3143d-142">Vygenerujte manifest počáteční</span><span class="sxs-lookup"><span data-stu-id="3143d-142">Generate the initial manifest</span></span>

<span data-ttu-id="3143d-143">S knihovny DLL v dolním a projekt sady vlastností, můžete teď používat `nuget spec` příkazu vygenerujte počáteční `.nuspec` souboru z projektu.</span><span class="sxs-lookup"><span data-stu-id="3143d-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="3143d-144">Tento krok zahrnuje relevantní nahrazení tokeny k vykreslení informace ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="3143d-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="3143d-145">Při spuštění `nuget spec` pouze jednou pro generování počátečního manifestu.</span><span class="sxs-lookup"><span data-stu-id="3143d-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="3143d-146">Při aktualizaci balíčku, můžete buď změnit hodnoty v projektu, nebo přímo upravit v manifestu.</span><span class="sxs-lookup"><span data-stu-id="3143d-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="3143d-147">Otevřete příkazový řádek a přejděte do složky obsahující projekt `AppLogger.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="3143d-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="3143d-148">Spusťte následující příkaz: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="3143d-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="3143d-149">Zadáním projektu NuGet vytvoří manifestu, který odpovídá názvu projektu, v takovém případě `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="3143d-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="3143d-150">Zahrnují taky nahrazení tokenů v manifestu.</span><span class="sxs-lookup"><span data-stu-id="3143d-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="3143d-151">Otevřete `AppLogger.nuspec` v textovém editoru a pomocí něj prozkoumat její obsah, který by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="3143d-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="3143d-152">Upravte manifest</span><span class="sxs-lookup"><span data-stu-id="3143d-152">Edit the manifest</span></span>

1. <span data-ttu-id="3143d-153">NuGet vytvoří chybu, pokud se pokusíte vytvořit balíček s výchozími hodnotami ve vaší `.nuspec` souboru, proto je nutné upravit následující pole, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="3143d-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="3143d-154">V tématu [odkaz na soubor příponou .nuspec - jednotlivé prvky](../reference/nuspec.md#single-elements) popis toho, jak se používají.</span><span class="sxs-lookup"><span data-stu-id="3143d-154">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="3143d-155">Adresa LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3143d-155">licenseUrl</span></span>
    - <span data-ttu-id="3143d-156">Adrese ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3143d-156">projectUrl</span></span>
    - <span data-ttu-id="3143d-157">IconUrl</span><span class="sxs-lookup"><span data-stu-id="3143d-157">iconUrl</span></span>
    - <span data-ttu-id="3143d-158">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3143d-158">releaseNotes</span></span>
    - <span data-ttu-id="3143d-159">značky</span><span class="sxs-lookup"><span data-stu-id="3143d-159">tags</span></span>

1. <span data-ttu-id="3143d-160">Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **značky** vlastnosti, jako jsou značky ostatní najít váš balíček na zdroje, jako je nuget.org a co provádí.</span><span class="sxs-lookup"><span data-stu-id="3143d-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="3143d-161">Můžete také přidat další prvky k manifestu v tuto chvíli, jak je popsáno na [odkaz na soubor příponou .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="3143d-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="3143d-162">Uložte soubor předtím, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="3143d-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="3143d-163">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="3143d-163">Run the pack command</span></span>

1. <span data-ttu-id="3143d-164">Z příkazového řádku v složku, která obsahuje vaše `.nuspec` souboru, spusťte příkaz `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="3143d-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="3143d-165">Generuje NuGet `.nupkg` soubor ve formátu *identifikátor version.nupkg*, které zjistíte v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="3143d-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="3143d-166">Umožňuje publikovat balíček</span><span class="sxs-lookup"><span data-stu-id="3143d-166">Publish the package</span></span>

<span data-ttu-id="3143d-167">Jakmile máte `.nupkg` souboru ji publikujete pomocí nuget.org `nuget.exe` s klíčem rozhraní API získali z nuget.org. Pro nuget.org je nutné použít `nuget.exe` 4.1.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="3143d-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="3143d-168">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="3143d-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="3143d-169">Publikování pomocí nabízených nuget</span><span class="sxs-lookup"><span data-stu-id="3143d-169">Publish with nuget push</span></span>

1. <span data-ttu-id="3143d-170">Změnit na složku, která obsahuje `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="3143d-170">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="3143d-171">Spusťte následující příkaz, zadáte název balíčku a nahraďte hodnotu klíče klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="3143d-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="3143d-172">nuget.exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="3143d-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="3143d-173">V tématu [nuget nabízené](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="3143d-173">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="3143d-174">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="3143d-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="3143d-175">Spravovat zveřejněný balíček</span><span class="sxs-lookup"><span data-stu-id="3143d-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="3143d-176">Související témata</span><span class="sxs-lookup"><span data-stu-id="3143d-176">Related topics</span></span>

- [<span data-ttu-id="3143d-177">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="3143d-177">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="3143d-178">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="3143d-178">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="3143d-179">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="3143d-179">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="3143d-180">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="3143d-180">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="3143d-181">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="3143d-181">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="3143d-182">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="3143d-182">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
