---
title: Úvodní příručka k vytváření a publikování balíčku NuGet rozhraní .NET Framework pomocí sady Visual Studio
description: Návod kurz týkající se vytváření a publikování Visual Studio 2017 pomocí balíčku NuGet pro rozhraní .NET Framework.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: quickstart
ms.openlocfilehash: 01760034a121b1ff6f227e006415779898c4cf6d
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="036d6-103">Rychlý úvod: Vytvoření a publikování balíčku pomocí sady Visual Studio (rozhraní .NET Framework)</span><span class="sxs-lookup"><span data-stu-id="036d6-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="036d6-104">Vytvoření balíčku NuGet z knihovny tříd rozhraní .NET Framework zahrnuje vytváření knihovny DLL v sadě Visual Studio a potom pomocí nástroje příkazového řádku nuget.exe vytvoření a publikování balíčku.</span><span class="sxs-lookup"><span data-stu-id="036d6-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="036d6-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="036d6-105">Prerequisites</span></span>

1. <span data-ttu-id="036d6-106">Nainstalujte všechny edice Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy.</span><span class="sxs-lookup"><span data-stu-id="036d6-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="036d6-107">Visual Studio 2017 automaticky zahrnuje NuGet možností při instalaci rozhraní .NET zatížení.</span><span class="sxs-lookup"><span data-stu-id="036d6-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="036d6-108">Nainstalujte `nuget.exe` CLI stažením z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, `.exe` souboru do složky vhodný, a přidáním této složce do vaší proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="036d6-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="036d6-109">[Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="036d6-109">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="036d6-110">Vytvoření nového účtu odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="036d6-110">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="036d6-111">Účet je potřeba zkontrolovat, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="036d6-111">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="036d6-112">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="036d6-112">Create a class library project</span></span>

<span data-ttu-id="036d6-113">Můžete použít existující projekt knihovna tříd rozhraní .NET Framework pro kód, který chcete balíček nebo vytvořit jednoduchý takto:</span><span class="sxs-lookup"><span data-stu-id="036d6-113">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="036d6-114">V sadě Visual Studio, vyberte **soubor > Nový > projekt**, vyberte **Visual C#** uzlu, vyberte šablonu, "Knihovny tříd (rozhraní .NET Framework)", název projektu AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="036d6-114">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="036d6-115">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** a ujistěte se, vytvoření projektu správně.</span><span class="sxs-lookup"><span data-stu-id="036d6-115">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="036d6-116">Knihovny DLL nachází v rámci ladění složky (nebo verze, pokud vytváříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="036d6-116">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="036d6-117">V rámci skutečné balíčku NuGet samozřejmě můžete implementovat řadu užitečných funkcí, se kterými ostatní mohou vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="036d6-117">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="036d6-118">Můžete také nastavit cílové rozhraní, ale chcete.</span><span class="sxs-lookup"><span data-stu-id="036d6-118">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="036d6-119">Například v tématu příručky pro [UWP](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="036d6-119">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="036d6-120">V tomto návodu však nebude napsat další kód, protože knihovny tříd ze šablony, stačí vytvořit balíček.</span><span class="sxs-lookup"><span data-stu-id="036d6-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="036d6-121">Pokud chcete některé funkční kód pro balíček, stále, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="036d6-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="036d6-122">Pokud nemáte důvod, proč zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projekty.</span><span class="sxs-lookup"><span data-stu-id="036d6-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="036d6-123">V tématu [vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="036d6-123">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="036d6-124">Konfigurovat vlastnosti projektu pro balíček</span><span class="sxs-lookup"><span data-stu-id="036d6-124">Configure project properties for the package</span></span>

<span data-ttu-id="036d6-125">Balíček NuGet obsahuje manifest ( `.nuspec` soubor), který obsahuje relevantní metadata, jako je například identifikátor balíčku, číslo verze, popis a další.</span><span class="sxs-lookup"><span data-stu-id="036d6-125">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="036d6-126">Některé z těchto lze rozlišovat z vlastností projektu přímo, což zabraňuje samostatně nutnost jejich následné aktualizace v projektu a manifest.</span><span class="sxs-lookup"><span data-stu-id="036d6-126">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="036d6-127">Tato část popisuje, kde se má nastavit příslušné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="036d6-127">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="036d6-128">Vyberte **Projekt > vlastnosti** nabídky příkazu a pak vyberte **aplikace** kartě.</span><span class="sxs-lookup"><span data-stu-id="036d6-128">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="036d6-129">V **název sestavení** pole, zadejte svůj balíček jedinečný identifikátor.</span><span class="sxs-lookup"><span data-stu-id="036d6-129">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="036d6-130">Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte.</span><span class="sxs-lookup"><span data-stu-id="036d6-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="036d6-131">Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).</span><span class="sxs-lookup"><span data-stu-id="036d6-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="036d6-132">Pokud se pokusíte o publikování balíčku s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="036d6-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="036d6-133">Vyberte **informací o sestavení...**  tlačítko, které vyvolá dialogové okno, ve kterém můžete zadat další vlastnosti, které přenášejí do manifestu (viz [odkaz na soubor příponou .nuspec - nahrazení tokeny](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="036d6-133">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="036d6-134">Nejčastěji používané pole jsou **název**, **popis**, **společnosti**, **Copyright**, a **verze sestavení**.</span><span class="sxs-lookup"><span data-stu-id="036d6-134">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="036d6-135">Tyto vlastnosti se zobrazí nakonec součástí vašeho balíčku na hostitele, jako je nuget.org, proto se ujistěte, že jsou k plně popisný.</span><span class="sxs-lookup"><span data-stu-id="036d6-135">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informace o sestavení v rozhraní .NET Framework projektu v sadě Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="036d6-137">Volitelné: Chcete-li zobrazit a upravit vlastnosti přímo, otevřete `Properties/AssemblyInfo.cs` v projektu.</span><span class="sxs-lookup"><span data-stu-id="036d6-137">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="036d6-138">Pokud jsou nastaveny vlastnosti, nastavte konfiguraci projektu na **verze** a znovu sestavte projekt ke generování aktualizované knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="036d6-138">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="036d6-139">Vygenerujte manifest počáteční</span><span class="sxs-lookup"><span data-stu-id="036d6-139">Generate the initial manifest</span></span>

<span data-ttu-id="036d6-140">S knihovny DLL v dolním a projekt sady vlastností, můžete teď používat `nuget spec` příkazu vygenerujte počáteční `.nuspec` souboru z projektu.</span><span class="sxs-lookup"><span data-stu-id="036d6-140">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="036d6-141">Tento krok zahrnuje relevantní nahrazení tokeny k vykreslení informace ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="036d6-141">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="036d6-142">Při spuštění `nuget spec` pouze jednou pro generování počátečního manifestu.</span><span class="sxs-lookup"><span data-stu-id="036d6-142">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="036d6-143">Při aktualizaci balíčku, můžete buď změnit hodnoty v projektu, nebo přímo upravit v manifestu.</span><span class="sxs-lookup"><span data-stu-id="036d6-143">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="036d6-144">Otevřete příkazový řádek a přejděte do složky obsahující projekt `AppLogger.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="036d6-144">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="036d6-145">Spusťte následující příkaz: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="036d6-145">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="036d6-146">Zadáním projektu NuGet vytvoří manifestu, který odpovídá názvu projektu, v takovém případě `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="036d6-146">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="036d6-147">Zahrnují taky nahrazení tokenů v manifestu.</span><span class="sxs-lookup"><span data-stu-id="036d6-147">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="036d6-148">Otevřete `AppLogger.nuspec` v textovém editoru a pomocí něj prozkoumat její obsah, který by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="036d6-148">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="036d6-149">Upravte manifest</span><span class="sxs-lookup"><span data-stu-id="036d6-149">Edit the manifest</span></span>

1. <span data-ttu-id="036d6-150">NuGet vytvoří chybu, pokud se pokusíte vytvořit balíček s výchozími hodnotami ve vaší `.nuspec` souboru, proto je nutné upravit následující pole, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="036d6-150">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="036d6-151">V tématu [odkaz na soubor příponou .nuspec - jednotlivé prvky](../reference/nuspec.md#single-elements) popis toho, jak se používají.</span><span class="sxs-lookup"><span data-stu-id="036d6-151">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="036d6-152">Adresa LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="036d6-152">licenseUrl</span></span>
    - <span data-ttu-id="036d6-153">Adrese ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="036d6-153">projectUrl</span></span>
    - <span data-ttu-id="036d6-154">IconUrl</span><span class="sxs-lookup"><span data-stu-id="036d6-154">iconUrl</span></span>
    - <span data-ttu-id="036d6-155">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="036d6-155">releaseNotes</span></span>
    - <span data-ttu-id="036d6-156">značky</span><span class="sxs-lookup"><span data-stu-id="036d6-156">tags</span></span>

1. <span data-ttu-id="036d6-157">Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **značky** vlastnosti, jako jsou značky ostatní najít váš balíček na zdroje, jako je nuget.org a co provádí.</span><span class="sxs-lookup"><span data-stu-id="036d6-157">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="036d6-158">Můžete také přidat další prvky k manifestu v tuto chvíli, jak je popsáno na [odkaz na soubor příponou .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="036d6-158">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="036d6-159">Uložte soubor předtím, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="036d6-159">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="036d6-160">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="036d6-160">Run the pack command</span></span>

1. <span data-ttu-id="036d6-161">Z příkazového řádku v složku, která obsahuje vaše `.nuspec` souboru, spusťte příkaz `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="036d6-161">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="036d6-162">Generuje NuGet `.nupkg` soubor ve formátu *identifikátor version.nupkg*, které zjistíte v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="036d6-162">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="036d6-163">Umožňuje publikovat balíček</span><span class="sxs-lookup"><span data-stu-id="036d6-163">Publish the package</span></span>

<span data-ttu-id="036d6-164">Jakmile máte `.nupkg` souboru ji publikujete pomocí nuget.org `nuget.exe` s klíčem rozhraní API získali z nuget.org. Pro nuget.org je nutné použít `nuget.exe` 4.1.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="036d6-164">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="036d6-165">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="036d6-165">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="036d6-166">Publikování pomocí nabízených nuget</span><span class="sxs-lookup"><span data-stu-id="036d6-166">Publish with nuget push</span></span>

1. <span data-ttu-id="036d6-167">Změnit na složku, která obsahuje `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="036d6-167">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="036d6-168">Spusťte následující příkaz, zadáte název balíčku a nahraďte hodnotu klíče klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="036d6-168">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="036d6-169">nuget.exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="036d6-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="036d6-170">V tématu [nuget nabízené](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="036d6-170">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="036d6-171">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="036d6-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="036d6-172">Spravovat zveřejněný balíček</span><span class="sxs-lookup"><span data-stu-id="036d6-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="036d6-173">Související témata</span><span class="sxs-lookup"><span data-stu-id="036d6-173">Related topics</span></span>

- [<span data-ttu-id="036d6-174">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="036d6-174">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="036d6-175">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="036d6-175">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="036d6-176">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="036d6-176">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="036d6-177">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="036d6-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="036d6-178">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="036d6-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="036d6-179">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="036d6-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
