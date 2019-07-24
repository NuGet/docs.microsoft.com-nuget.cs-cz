---
title: Vytvoření a publikování .NET Framework balíčku NuGet pomocí sady Visual Studio ve Windows
description: Návod k vytvoření a publikování .NET Framework balíčku NuGet pomocí sady Visual Studio ve Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 75160bf2b01f6d4707162e019a6263ddc64a6f5e
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342522"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="f0acd-103">Rychlý start: Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="f0acd-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="f0acd-104">Vytvoření balíčku NuGet z knihovny tříd .NET Framework zahrnuje vytvoření knihovny DLL v aplikaci Visual Studio ve Windows a následné vytvoření a publikování balíčku pomocí nástroje příkazového řádku NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="f0acd-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="f0acd-105">Tento rychlý Start se týká jenom sady Visual Studio 2017 pro Windows.</span><span class="sxs-lookup"><span data-stu-id="f0acd-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="f0acd-106">Visual Studio pro Mac nezahrnuje funkce popsané tady.</span><span class="sxs-lookup"><span data-stu-id="f0acd-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="f0acd-107">Místo toho použijte [nástroje DOTNET CLI](create-and-publish-a-package-using-the-dotnet-cli.md) .</span><span class="sxs-lookup"><span data-stu-id="f0acd-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0acd-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f0acd-108">Prerequisites</span></span>

1. <span data-ttu-id="f0acd-109">Nainstalujte jakoukoli edici sady Visual Studio 2017 z [VisualStudio.com](https://www.visualstudio.com/) s libovolným. Zatížení související s NET.</span><span class="sxs-lookup"><span data-stu-id="f0acd-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="f0acd-110">Pokud je nainstalovaná úloha .NET, Visual Studio 2017 automaticky zahrnuje funkce NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0acd-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="f0acd-111">Nainstalujte rozhraní `nuget.exe` příkazového řádku stažením z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), uložte tento `.exe` soubor do vhodné složky a přidejte tuto složku do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="f0acd-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="f0acd-112">[Zaregistrujte si bezplatný účet na NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) , pokud ho ještě nemáte.</span><span class="sxs-lookup"><span data-stu-id="f0acd-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="f0acd-113">Když se vytvoří nový účet, pošle se potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="f0acd-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="f0acd-114">Než budete moct nahrát balíček, musíte účet potvrdit.</span><span class="sxs-lookup"><span data-stu-id="f0acd-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="f0acd-115">Vytvořit projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="f0acd-115">Create a class library project</span></span>

<span data-ttu-id="f0acd-116">Můžete použít existující .NET Framework projekt knihovny tříd pro kód, který chcete zabalit, nebo vytvořit jednoduchý, a to následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="f0acd-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="f0acd-117">V aplikaci Visual Studio zvolte **soubor > Nový > projekt**, vyberte uzel **vizuálů C#**  , vyberte šablonu knihovny tříd (.NET Framework), pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0acd-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="f0acd-118">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavit** , abyste se ujistili, že se projekt vytvořil správně.</span><span class="sxs-lookup"><span data-stu-id="f0acd-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="f0acd-119">Knihovna DLL se nachází ve složce ladění (nebo v případě, že tuto konfiguraci sestavíte místo toho).</span><span class="sxs-lookup"><span data-stu-id="f0acd-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="f0acd-120">V rámci skutečného balíčku NuGet samozřejmě implementujete spoustu užitečných funkcí, se kterými můžou sestavovat aplikace i ostatní.</span><span class="sxs-lookup"><span data-stu-id="f0acd-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="f0acd-121">Můžete také nastavit cílové architektury, například.</span><span class="sxs-lookup"><span data-stu-id="f0acd-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="f0acd-122">Podívejte se například na příručky pro [UWP](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="f0acd-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="f0acd-123">Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostačující k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="f0acd-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="f0acd-124">I když chcete pro balíček použít nějaký funkční kód, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="f0acd-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="f0acd-125">Pokud nemáte důvod vybrat jinak, .NET Standard je upřednostňovaným cílem pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.</span><span class="sxs-lookup"><span data-stu-id="f0acd-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="f0acd-126">Přečtěte si téma [Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f0acd-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="f0acd-127">Konfigurovat vlastnosti projektu pro balíček</span><span class="sxs-lookup"><span data-stu-id="f0acd-127">Configure project properties for the package</span></span>

<span data-ttu-id="f0acd-128">Balíček NuGet obsahuje manifest ( `.nuspec` soubor), který obsahuje relevantní metadata, jako je například identifikátor balíčku, číslo verze, popis a další.</span><span class="sxs-lookup"><span data-stu-id="f0acd-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="f0acd-129">Některé z nich lze vykreslit přímo z vlastností projektu a zabránit tak jejich samostatné aktualizaci v projektu i v manifestu.</span><span class="sxs-lookup"><span data-stu-id="f0acd-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="f0acd-130">V této části se dozvíte, kde můžete nastavit příslušné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="f0acd-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="f0acd-131">Vyberte příkaz nabídky **Vlastnosti projektu >** a pak vyberte kartu **aplikace** .</span><span class="sxs-lookup"><span data-stu-id="f0acd-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="f0acd-132">V poli **název sestavení** poskytněte balíčku jedinečný identifikátor.</span><span class="sxs-lookup"><span data-stu-id="f0acd-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="f0acd-133">Balíčku musíte dát identifikátor, který je jedinečný v rámci nuget.org nebo libovolného hostitele, který používáte.</span><span class="sxs-lookup"><span data-stu-id="f0acd-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="f0acd-134">Pro tento návod doporučujeme, abyste v názvu jako pozdější krok publikování použili "Sample" nebo "test", aby byl balíček veřejně viditelný (i když je to nepravděpodobné, že ho kdokoli bude používat).</span><span class="sxs-lookup"><span data-stu-id="f0acd-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="f0acd-135">Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="f0acd-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="f0acd-136">Vyberte tlačítko **informace o sestavení...** , které zobrazí dialogové okno, ve kterém můžete zadat další vlastnosti, které se přenesou do manifestu (viz [soubor. nuspec – náhradní tokeny reference](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="f0acd-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="f0acd-137">Nejčastěji používaná pole jsou **název**, **Popis**, **Společnost**, **Copyright**a **verze sestavení**.</span><span class="sxs-lookup"><span data-stu-id="f0acd-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="f0acd-138">Tyto vlastnosti se nakonec zobrazí s vaším balíčkem na hostiteli, jako je nuget.org, a ujistěte se, že jsou plně popisné.</span><span class="sxs-lookup"><span data-stu-id="f0acd-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informace o sestavení v projektu .NET Framework v aplikaci Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="f0acd-140">Volitelné: Chcete-li zobrazit a upravit vlastnosti přímo, otevřete `Properties/AssemblyInfo.cs` soubor v projektu.</span><span class="sxs-lookup"><span data-stu-id="f0acd-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="f0acd-141">Po nastavení vlastností nastavte konfiguraci projektu na vydaná a znovu  Sestavte projekt, aby se vygenerovala Aktualizovaná knihovna DLL.</span><span class="sxs-lookup"><span data-stu-id="f0acd-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="f0acd-142">Generování počátečního manifestu</span><span class="sxs-lookup"><span data-stu-id="f0acd-142">Generate the initial manifest</span></span>

<span data-ttu-id="f0acd-143">Když je knihovna DLL v rukou a nastavené vlastnosti projektu, můžete nyní `nuget spec` použít příkaz k vygenerování `.nuspec` počátečního souboru z projektu.</span><span class="sxs-lookup"><span data-stu-id="f0acd-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="f0acd-144">Tento krok zahrnuje relevantní náhradní tokeny k vykreslování informací ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="f0acd-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="f0acd-145">Pro vygenerování počátečního manifestu se spustí `nuget spec` jenom jednou.</span><span class="sxs-lookup"><span data-stu-id="f0acd-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="f0acd-146">Při aktualizaci balíčku můžete buď změnit hodnoty v projektu, nebo přímo upravit manifest.</span><span class="sxs-lookup"><span data-stu-id="f0acd-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="f0acd-147">Otevřete příkazový řádek a přejděte do složky projektu obsahující `AppLogger.csproj` soubor.</span><span class="sxs-lookup"><span data-stu-id="f0acd-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="f0acd-148">Spusťte následující příkaz: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="f0acd-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="f0acd-149">Když zadáte projekt, NuGet vytvoří v tomto případě `AppLogger.nuspec`manifest, který se shoduje s názvem projektu.</span><span class="sxs-lookup"><span data-stu-id="f0acd-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="f0acd-150">Obsahuje také náhradní tokeny v manifestu.</span><span class="sxs-lookup"><span data-stu-id="f0acd-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="f0acd-151">Otevřete `AppLogger.nuspec` v textovém editoru, abyste prozkoumali jeho obsah, který by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="f0acd-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="f0acd-152">Upravit manifest</span><span class="sxs-lookup"><span data-stu-id="f0acd-152">Edit the manifest</span></span>

1. <span data-ttu-id="f0acd-153">NuGet vyvolá chybu, pokud se pokusíte vytvořit balíček s výchozími hodnotami v `.nuspec` souboru, takže před pokračováním musíte upravit následující pole.</span><span class="sxs-lookup"><span data-stu-id="f0acd-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="f0acd-154">Viz [odkaz na soubor. nuspec – volitelné prvky metadat](../reference/nuspec.md#optional-metadata-elements) pro popis způsobu jejich použití.</span><span class="sxs-lookup"><span data-stu-id="f0acd-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="f0acd-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="f0acd-155">licenseUrl</span></span>
    - <span data-ttu-id="f0acd-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="f0acd-156">projectUrl</span></span>
    - <span data-ttu-id="f0acd-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="f0acd-157">iconUrl</span></span>
    - <span data-ttu-id="f0acd-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="f0acd-158">releaseNotes</span></span>
    - <span data-ttu-id="f0acd-159">značky</span><span class="sxs-lookup"><span data-stu-id="f0acd-159">tags</span></span>

1. <span data-ttu-id="f0acd-160">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **značek** , protože značky můžou ostatním uživatelům najít balíček na zdrojích, jako je NuGet.org, a pochopit, co dělá.</span><span class="sxs-lookup"><span data-stu-id="f0acd-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="f0acd-161">V tomto okamžiku můžete také přidat další prvky do manifestu, jak je popsáno v [souboru. nuspec reference](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f0acd-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="f0acd-162">Než budete pokračovat, soubor uložte.</span><span class="sxs-lookup"><span data-stu-id="f0acd-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="f0acd-163">Spuštění příkazu Pack</span><span class="sxs-lookup"><span data-stu-id="f0acd-163">Run the pack command</span></span>

1. <span data-ttu-id="f0acd-164">Z příkazového řádku ve složce, která obsahuje `.nuspec` váš soubor, spusťte příkaz `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="f0acd-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="f0acd-165">NuGet vygeneruje `.nupkg` soubor ve formě identifikátoru *Version. nupkg*, který najdete v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="f0acd-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f0acd-166">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="f0acd-166">Publish the package</span></span>

<span data-ttu-id="f0acd-167">Jakmile budete mít `.nupkg` soubor, publikujete ho pro NuGet.org pomocí `nuget.exe` klíče rozhraní API získaného z NuGet.org. Pro NuGet.org musíte použít `nuget.exe` 4.1.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="f0acd-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="f0acd-168">Získání klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="f0acd-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="f0acd-169">Publikování s nabízeným oznámením NuGet</span><span class="sxs-lookup"><span data-stu-id="f0acd-169">Publish with nuget push</span></span>

1. <span data-ttu-id="f0acd-170">Otevřete příkazový řádek a přejděte do složky, která obsahuje `.nupkg` soubor.</span><span class="sxs-lookup"><span data-stu-id="f0acd-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="f0acd-171">Spusťte následující příkaz, zadáním názvu balíčku a nahrazením hodnoty klíče vaším klíčem rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="f0acd-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="f0acd-172">NuGet. exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="f0acd-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="f0acd-173">Viz [push NuGet](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="f0acd-173">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="f0acd-174">Chyby publikování</span><span class="sxs-lookup"><span data-stu-id="f0acd-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="f0acd-175">Správa publikovaného balíčku</span><span class="sxs-lookup"><span data-stu-id="f0acd-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="f0acd-176">Další kroky</span><span class="sxs-lookup"><span data-stu-id="f0acd-176">Next steps</span></span>

<span data-ttu-id="f0acd-177">Blahopřejeme k vytvoření prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="f0acd-177">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f0acd-178">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="f0acd-178">Create a Package</span></span>](../create-packages/creating-a-package.md)

<span data-ttu-id="f0acd-179">Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.</span><span class="sxs-lookup"><span data-stu-id="f0acd-179">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="f0acd-180">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="f0acd-180">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="f0acd-181">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="f0acd-181">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="f0acd-182">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="f0acd-182">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f0acd-183">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="f0acd-183">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f0acd-184">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="f0acd-184">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
