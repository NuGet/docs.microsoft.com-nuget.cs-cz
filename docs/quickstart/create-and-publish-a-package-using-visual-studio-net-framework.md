---
title: Vytvoření a publikování balíčku .NET Framework pomocí sady Visual Studio na Windows
description: Kurz návod týkající se vytváření a publikování balíčku NuGet pro rozhraní .NET Framework pomocí sady Visual Studio na Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: bf561d36a06bf42c029eb96ff1b7930abffa4c0a
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842048"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="705d5-103">Rychlý start: Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="705d5-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="705d5-104">Vytvoření balíčku NuGet z knihovny tříd .NET Framework zahrnuje vytváření knihovny DLL v sadě Visual Studio ve Windows a pak pomocí nástroje příkazového řádku nuget.exe vytvoření a publikování balíčku.</span><span class="sxs-lookup"><span data-stu-id="705d5-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="705d5-105">V tomto rychlém startu platí pro Visual Studio 2017 pro Windows pouze.</span><span class="sxs-lookup"><span data-stu-id="705d5-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="705d5-106">Visual Studio pro Mac nezahrnuje možnosti popsané tady.</span><span class="sxs-lookup"><span data-stu-id="705d5-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="705d5-107">Použití [nástroje rozhraní příkazového řádku dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) místo.</span><span class="sxs-lookup"><span data-stu-id="705d5-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="705d5-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="705d5-108">Prerequisites</span></span>

1. <span data-ttu-id="705d5-109">Instalaci libovolné edice sady Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy.</span><span class="sxs-lookup"><span data-stu-id="705d5-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="705d5-110">Visual Studio 2017 automaticky zahrnuje NuGet možnosti, když je nainstalovaná úloha .NET.</span><span class="sxs-lookup"><span data-stu-id="705d5-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="705d5-111">Nainstalujte `nuget.exe` rozhraní příkazového řádku, stáhněte si ji z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, který `.exe` soubor vhodný složky a přidání složky do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="705d5-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="705d5-112">[Zaregistrujte si bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="705d5-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="705d5-113">Vytvoření nového účtu se odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="705d5-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="705d5-114">Účet musí ověřit dříve, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="705d5-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="705d5-115">Vytvořte projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="705d5-115">Create a class library project</span></span>

<span data-ttu-id="705d5-116">Můžete použít existující projekt knihovny tříd .NET Framework pro kód, který chcete balíček nebo vytvořit jednoduchý následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="705d5-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="705d5-117">V sadě Visual Studio, zvolte **soubor > Nový > projekt**, vyberte **Visual C#** uzlu, vyberte šablonu "Knihovna tříd (.NET Framework)", pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="705d5-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="705d5-118">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** k Ujistěte se, že projekt je vytvořený řádně.</span><span class="sxs-lookup"><span data-stu-id="705d5-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="705d5-119">Knihovny DLL se nachází složka pro ladění (nebo vydání, pokud vytváříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="705d5-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="705d5-120">V rámci skutečné balíčku NuGet samozřejmě, můžete implementovat mnoho užitečných funkcí, se kterými ostatní můžete vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="705d5-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="705d5-121">Můžete také nastavit cílové rozhraní ale chcete.</span><span class="sxs-lookup"><span data-stu-id="705d5-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="705d5-122">Příklad naleznete v tématu příručky k [UPW](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="705d5-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="705d5-123">V tomto návodu ale nebude napíšete žádný další kód vzhledem k tomu, že knihovna tříd z této šablony je dostatečná pro vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="705d5-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="705d5-124">Pokud chcete některé funkční kód pro balíček, stále, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="705d5-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="705d5-125">Pokud nemáte důvod nerozhodnete jinak, .NET Standard je upřednostňovaným cílem, pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projektů.</span><span class="sxs-lookup"><span data-stu-id="705d5-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="705d5-126">Zobrazit [vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="705d5-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="705d5-127">Konfigurovat vlastnosti projektu pro balíček</span><span class="sxs-lookup"><span data-stu-id="705d5-127">Configure project properties for the package</span></span>

<span data-ttu-id="705d5-128">Obsahuje manifest balíčku NuGet ( `.nuspec` souboru), který obsahuje metadata relevantní jako identifikátor balíčku, číslo verze, popis a další.</span><span class="sxs-lookup"><span data-stu-id="705d5-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="705d5-129">Některé z nich může být odebírány z vlastnosti projektu přímo, díky tomu není nutné samostatně je aktualizovat v manifestu a projektu.</span><span class="sxs-lookup"><span data-stu-id="705d5-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="705d5-130">Tato část popisuje, kde nastavit příslušné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="705d5-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="705d5-131">Vyberte **projektu > vlastnosti** nabídce příkaz a pak vyberte **aplikace** kartu.</span><span class="sxs-lookup"><span data-stu-id="705d5-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="705d5-132">V **název sestavení** pole, zadejte jedinečný identifikátor balíčku.</span><span class="sxs-lookup"><span data-stu-id="705d5-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="705d5-133">Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo cokoli, co můžete hostovat používáte.</span><span class="sxs-lookup"><span data-stu-id="705d5-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="705d5-134">Pro Tento názorný postup doporučujeme, abyste pozdějším kroku publikování provádění balíček veřejně viditelné (i když nepravděpodobné, že kdo bude ve skutečnosti použít) včetně "Ukázkový" nebo "Test" v názvu.</span><span class="sxs-lookup"><span data-stu-id="705d5-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="705d5-135">Při pokusu publikovat balíček s názvem, který již existuje, se zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="705d5-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="705d5-136">Vyberte **informace o sestavení...**  tlačítko, kterým se zobrazí dialogové okno, ve kterém můžete zadat další vlastnosti, které přenášejí do manifestu (viz [odkaz na soubor souboru .nuspec – nahrazení tokeny](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="705d5-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="705d5-137">Nejčastěji používané pole jsou **Title**, **popis**, **společnosti**, **Copyright**, a **verze sestavení**.</span><span class="sxs-lookup"><span data-stu-id="705d5-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="705d5-138">Tyto vlastnosti se zobrazí nakonec součástí vašeho balíčku na hostiteli, jako je nuget.org, proto se ujistěte, že jsou plně popisný.</span><span class="sxs-lookup"><span data-stu-id="705d5-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informace o sestavení v rozhraní .NET Framework projektu v sadě Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="705d5-140">Volitelné: Chcete-li zobrazit a upravit vlastnosti přímo, otevřete `Properties/AssemblyInfo.cs` soubor v projektu.</span><span class="sxs-lookup"><span data-stu-id="705d5-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="705d5-141">Když jsou nastaveny vlastnosti, nastavte konfiguraci projektu **vydání** a znovu sestavte projekt se vygenerovat aktualizované knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="705d5-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="705d5-142">Generovat manifest počáteční</span><span class="sxs-lookup"><span data-stu-id="705d5-142">Generate the initial manifest</span></span>

<span data-ttu-id="705d5-143">S knihovnou DLL v sadě vlastností a projekt, můžete teď použít `nuget spec` příkazu vygenerujte počáteční `.nuspec` soubor z projektu.</span><span class="sxs-lookup"><span data-stu-id="705d5-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="705d5-144">Tento krok zahrnuje relevantní nahrazení tokeny k vykreslení informace ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="705d5-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="705d5-145">Spuštění `nuget spec` jen jednou pro generování počátečního manifestu.</span><span class="sxs-lookup"><span data-stu-id="705d5-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="705d5-146">Při aktualizaci balíčku, můžete buď změnit hodnoty ve vašem projektu, nebo přímo upravit manifest.</span><span class="sxs-lookup"><span data-stu-id="705d5-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="705d5-147">Otevřete příkazový řádek a přejděte do složky projektu obsahujícího `AppLogger.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="705d5-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="705d5-148">Spusťte následující příkaz: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="705d5-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="705d5-149">Zadáním projektu NuGet vytvoří manifest, který odpovídá názvu projektu, v tomto případě `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="705d5-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="705d5-150">Také zahrnovat nahrazení tokeny v manifestu.</span><span class="sxs-lookup"><span data-stu-id="705d5-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="705d5-151">Otevřít `AppLogger.nuspec` v textovém editoru a zkontrolujte jeho obsah, který by měl vypadat následovně:</span><span class="sxs-lookup"><span data-stu-id="705d5-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="705d5-152">Upravit manifest</span><span class="sxs-lookup"><span data-stu-id="705d5-152">Edit the manifest</span></span>

1. <span data-ttu-id="705d5-153">NuGet dojde k chybě při pokusu vytvořit balíček s výchozími hodnotami v vaše `.nuspec` souboru, proto je nutné upravit následující pole, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="705d5-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="705d5-154">V tématu [odkaz na soubor souboru .nuspec – elementy volitelná metadata](../reference/nuspec.md#optional-metadata-elements) popis jak používají.</span><span class="sxs-lookup"><span data-stu-id="705d5-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="705d5-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="705d5-155">licenseUrl</span></span>
    - <span data-ttu-id="705d5-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="705d5-156">projectUrl</span></span>
    - <span data-ttu-id="705d5-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="705d5-157">iconUrl</span></span>
    - <span data-ttu-id="705d5-158">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="705d5-158">releaseNotes</span></span>
    - <span data-ttu-id="705d5-159">značky</span><span class="sxs-lookup"><span data-stu-id="705d5-159">tags</span></span>

1. <span data-ttu-id="705d5-160">Balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost **značky** vlastnost, protože značky pomoci ostatním najít váš balíček na zdroje, jako je nuget.org a pochopit jeho význam.</span><span class="sxs-lookup"><span data-stu-id="705d5-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="705d5-161">Můžete také přidat další prvky do manifestu v tuto chvíli, jak je popsáno v [odkaz na soubor souboru .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="705d5-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="705d5-162">Uložte soubor předtím, než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="705d5-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="705d5-163">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="705d5-163">Run the pack command</span></span>

1. <span data-ttu-id="705d5-164">Na příkazovém řádku ve složce obsahující váš `.nuspec` souboru, spusťte příkaz `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="705d5-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="705d5-165">Generuje NuGet `.nupkg` souboru ve formě *identifikátor version.nupkg*, které zjistíte v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="705d5-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="705d5-166">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="705d5-166">Publish the package</span></span>

<span data-ttu-id="705d5-167">Jakmile budete mít `.nupkg` souboru, ji publikujete do nuget.org pomocí `nuget.exe` pomocí klíče rozhraní API získaných z nuget.org. Pro nuget.org je nutné použít `nuget.exe` 4.1.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="705d5-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="705d5-168">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="705d5-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="705d5-169">Publikování pomocí nuget nasdílení změn</span><span class="sxs-lookup"><span data-stu-id="705d5-169">Publish with nuget push</span></span>

1. <span data-ttu-id="705d5-170">Otevřete příkazový řádek a změňte na složku obsahující `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="705d5-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="705d5-171">Spusťte následující příkaz, zadávání názvu balíčku a nahraďte hodnotu klíče svůj klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="705d5-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="705d5-172">nuget.exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="705d5-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="705d5-173">Zobrazit [nuget nabízených](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="705d5-173">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="705d5-174">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="705d5-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="705d5-175">Správa publikované balíčku</span><span class="sxs-lookup"><span data-stu-id="705d5-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="705d5-176">Související témata</span><span class="sxs-lookup"><span data-stu-id="705d5-176">Related topics</span></span>

- [<span data-ttu-id="705d5-177">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="705d5-177">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="705d5-178">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="705d5-178">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="705d5-179">Balíčky v předběžné verzi</span><span class="sxs-lookup"><span data-stu-id="705d5-179">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="705d5-180">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="705d5-180">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="705d5-181">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="705d5-181">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="705d5-182">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="705d5-182">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
