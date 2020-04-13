---
title: Vytvoření a publikování balíčku .NET Framework NuGet pomocí sady Visual Studio v systému Windows
description: Návod k vytvoření a publikování balíčku .NET Framework NuGet pomocí sady Visual Studio v systému Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380648"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="03547-103">Úvodní příručka: Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="03547-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="03547-104">Vytvoření balíčku NuGet z knihovny tříd rozhraní .NET Framework zahrnuje vytvoření knihovny DLL v sadě Visual Studio v systému Windows a následné vytvoření a publikování balíčku pomocí nástroje příkazového řádku nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="03547-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="03547-105">Tento úvodní příručka se vztahuje pouze na visual studio 2017 a vyšší verze pro Windows.</span><span class="sxs-lookup"><span data-stu-id="03547-105">This Quickstart applies to Visual Studio 2017 and higher versions for Windows only.</span></span> <span data-ttu-id="03547-106">Visual Studio pro Mac neobsahuje zde popsané funkce.</span><span class="sxs-lookup"><span data-stu-id="03547-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="03547-107">Místo toho použijte [nástroje rozhraní SE kontinua dotnet.](create-and-publish-a-package-using-the-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="03547-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03547-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="03547-108">Prerequisites</span></span>

1. <span data-ttu-id="03547-109">Nainstalujte libovolnou edici Visual Studia 2017 nebo vyšší z [visualstudio.com](https://www.visualstudio.com/) s libovolným . NET související s úlohou.</span><span class="sxs-lookup"><span data-stu-id="03547-109">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="03547-110">Visual Studio 2017 automaticky zahrnuje funkce NuGet při instalaci úlohy .NET.</span><span class="sxs-lookup"><span data-stu-id="03547-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="03547-111">Nainstalujte `nuget.exe` rozhraní se konstatování pomocí `.exe` nuget.org [,](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)uložíte jej do vhodné složky a přidáte tuto složku do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="03547-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="03547-112">[Zaregistrujte se zdarma účet na nuget.org,](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) pokud nemáte ještě jeden.</span><span class="sxs-lookup"><span data-stu-id="03547-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="03547-113">Vytvoření nového účtu odešle potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="03547-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="03547-114">Před nahráním balíčku musíte účet potvrdit.</span><span class="sxs-lookup"><span data-stu-id="03547-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="03547-115">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="03547-115">Create a class library project</span></span>

<span data-ttu-id="03547-116">Můžete použít existující projekt knihovny tříd rozhraní .NET Framework pro kód, který chcete zabalit, nebo vytvořit jednoduchý následující:</span><span class="sxs-lookup"><span data-stu-id="03547-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="03547-117">V sadě Visual Studio zvolte **Soubor > Nový > project**, vyberte uzel Visual **C#,** vyberte šablonu "Knihovna tříd (.NET Framework)", pojmenujte projekt AppLogger a klepněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="03547-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="03547-118">Klikněte pravým tlačítkem myši na výsledný soubor projektu a vyberte **sestavení,** abyste se ujistili, že byl projekt vytvořen správně.</span><span class="sxs-lookup"><span data-stu-id="03547-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="03547-119">DLL se nachází ve složce Ladění (nebo verze, pokud vytvoříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="03547-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="03547-120">V rámci skutečného balíčku NuGet samozřejmě implementovat mnoho užitečných funkcí, s nimiž ostatní mohou vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="03547-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="03547-121">Můžete také nastavit cílové architektury, jak se vám líbí.</span><span class="sxs-lookup"><span data-stu-id="03547-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="03547-122">Například naleznete v průvodcích pro [UPW](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="03547-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="03547-123">Pro tento návod však nebudete psát žádný další kód, protože knihovna tříd ze šablony je dostatečná k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="03547-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="03547-124">Přesto, pokud chcete nějaký funkční kód pro balíček, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="03547-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="03547-125">Pokud nemáte důvod zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.</span><span class="sxs-lookup"><span data-stu-id="03547-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="03547-126">Viz [Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard).](create-and-publish-a-package-using-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="03547-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="03547-127">Konfigurace vlastností projektu pro balíček</span><span class="sxs-lookup"><span data-stu-id="03547-127">Configure project properties for the package</span></span>

<span data-ttu-id="03547-128">Balíček NuGet obsahuje manifest `.nuspec` (soubor), který obsahuje relevantní metadata, jako je například identifikátor balíčku, číslo verze, popis a další.</span><span class="sxs-lookup"><span data-stu-id="03547-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="03547-129">Některé z nich lze vyvodit z vlastností projektu přímo, což zabraňuje nutnosti samostatně aktualizovat v projektu i manifestu.</span><span class="sxs-lookup"><span data-stu-id="03547-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="03547-130">Tato část popisuje, kde nastavit příslušné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="03547-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="03547-131">Vyberte příkaz Nabídky **Vlastnosti projektu >** a pak vyberte kartu **Aplikace.**</span><span class="sxs-lookup"><span data-stu-id="03547-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="03547-132">V poli **Název sestavení** pojmenujte balíček jedinečným identifikátorem.</span><span class="sxs-lookup"><span data-stu-id="03547-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="03547-133">Balíček je nutné poskytnout identifikátor, který je jedinečný v celé nuget.org nebo libovolného hostitele, který používáte.</span><span class="sxs-lookup"><span data-stu-id="03547-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="03547-134">Pro tento návod doporučujeme zahrnout "Ukázka" nebo "Test" v názvu jako pozdější krok publikování dělá balíček veřejně viditelné (i když je nepravděpodobné, že někdo bude skutečně používat).</span><span class="sxs-lookup"><span data-stu-id="03547-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="03547-135">Pokud se pokusíte publikovat balíček s názvem, který již existuje, zobrazí se chyba.</span><span class="sxs-lookup"><span data-stu-id="03547-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="03547-136">Vyberte tlačítko **Informace o sestavení...** tlačítko, ve kterém se zobrazí dialogové okno, ve kterém můžete zadat další vlastnosti, které se přenášejí do manifestu (viz [.nuspec odkaz na soubor - náhradní tokeny](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="03547-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="03547-137">Nejčastěji používanými poli jsou **verze Název**, **Popis**, **Společnost**, **Autorská práva**a **Sestava**.</span><span class="sxs-lookup"><span data-stu-id="03547-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="03547-138">Tyto vlastnosti se nakonec zobrazí s balíčkem na hostiteli, jako je nuget.org, takže se ujistěte, že jsou plně popisné.</span><span class="sxs-lookup"><span data-stu-id="03547-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informace o sestavení v projektu rozhraní .NET Framework v sadě Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="03547-140">Volitelné: chcete-li vlastnosti zobrazit `Properties/AssemblyInfo.cs` a upravit přímo, otevřete soubor v projektu.</span><span class="sxs-lookup"><span data-stu-id="03547-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="03547-141">Když jsou vlastnosti nastaveny, nastavte konfiguraci projektu na **Release** a znovu vytvořte projekt, abyste vygenerovali aktualizovanou dll.</span><span class="sxs-lookup"><span data-stu-id="03547-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="03547-142">Generovat počáteční manifest</span><span class="sxs-lookup"><span data-stu-id="03547-142">Generate the initial manifest</span></span>

<span data-ttu-id="03547-143">Se sadou vlastností DLL a vlastností `nuget spec` projektu nyní `.nuspec` pomocí příkazu vygenerujete počáteční soubor z projektu.</span><span class="sxs-lookup"><span data-stu-id="03547-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="03547-144">Tento krok zahrnuje příslušné náhradní tokeny pro kreslení informací ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="03547-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="03547-145">Spuštění `nuget spec` pouze jednou generovat počáteční manifest.</span><span class="sxs-lookup"><span data-stu-id="03547-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="03547-146">Při aktualizaci balíčku můžete buď změnit hodnoty v projektu, nebo přímo upravit manifest.</span><span class="sxs-lookup"><span data-stu-id="03547-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="03547-147">Otevřete příkazový řádek a přejděte `AppLogger.csproj` do složky projektu obsahující soubor.</span><span class="sxs-lookup"><span data-stu-id="03547-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="03547-148">Spusťte následující `nuget spec AppLogger.csproj`příkaz: .</span><span class="sxs-lookup"><span data-stu-id="03547-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="03547-149">Zadáním projektu, NuGet vytvoří manifest, který odpovídá názvu projektu, `AppLogger.nuspec`v tomto případě .</span><span class="sxs-lookup"><span data-stu-id="03547-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="03547-150">Zahrnuje také náhradní tokeny v manifestu.</span><span class="sxs-lookup"><span data-stu-id="03547-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="03547-151">Otevřete `AppLogger.nuspec` v textovém editoru a prohlédněte si jeho obsah, který by se měl zobrazit takto:</span><span class="sxs-lookup"><span data-stu-id="03547-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="03547-152">Úprava manifestu</span><span class="sxs-lookup"><span data-stu-id="03547-152">Edit the manifest</span></span>

1. <span data-ttu-id="03547-153">NuGet vytvoří chybu, pokud se pokusíte vytvořit balíček s výchozí hodnoty v `.nuspec` souboru, takže je nutné upravit následující pole před pokračováním.</span><span class="sxs-lookup"><span data-stu-id="03547-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="03547-154">Viz [.nuspec odkaz na soubor - volitelné prvky metadat](../reference/nuspec.md#optional-metadata-elements) pro popis, jak jsou použity.</span><span class="sxs-lookup"><span data-stu-id="03547-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="03547-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="03547-155">licenseUrl</span></span>
    - <span data-ttu-id="03547-156">projektUrl</span><span class="sxs-lookup"><span data-stu-id="03547-156">projectUrl</span></span>
    - <span data-ttu-id="03547-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="03547-157">iconUrl</span></span>
    - <span data-ttu-id="03547-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="03547-158">releaseNotes</span></span>
    - <span data-ttu-id="03547-159">tags</span><span class="sxs-lookup"><span data-stu-id="03547-159">tags</span></span>

1. <span data-ttu-id="03547-160">U balíčků vytvořených pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **Tags,** protože značky pomáhají ostatním najít váš balíček na zdrojích, jako je nuget.org a pochopit, co dělá.</span><span class="sxs-lookup"><span data-stu-id="03547-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="03547-161">V tuto chvíli můžete také přidat do manifestu další prvky, jak je popsáno [v odkazu na soubor .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="03547-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="03547-162">Před pokračováním soubor uložte.</span><span class="sxs-lookup"><span data-stu-id="03547-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="03547-163">Spuštění příkazu pack</span><span class="sxs-lookup"><span data-stu-id="03547-163">Run the pack command</span></span>

1. <span data-ttu-id="03547-164">Z příkazového řádku ve složce obsahující `.nuspec` soubor `nuget pack`spusťte příkaz .</span><span class="sxs-lookup"><span data-stu-id="03547-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="03547-165">NuGet generuje `.nupkg` soubor ve formě *identifier-version.nupkg*, který najdete v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="03547-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="03547-166">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="03547-166">Publish the package</span></span>

<span data-ttu-id="03547-167">Jakmile máte `.nupkg` soubor, publikujete jej `nuget.exe` nuget.org pomocí klíče rozhraní API získaného z nuget.org. Pro nuget.org musíte `nuget.exe` použít 4.1.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="03547-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="03547-168">Získání klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="03547-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="03547-169">Publikovat pomocí nuget push</span><span class="sxs-lookup"><span data-stu-id="03547-169">Publish with nuget push</span></span>

1. <span data-ttu-id="03547-170">Otevřete příkazový řádek a změňte `.nupkg` na složku obsahující soubor.</span><span class="sxs-lookup"><span data-stu-id="03547-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="03547-171">Spusťte následující příkaz, zadejte název balíčku a nahraďte hodnotu klíče klíčem rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="03547-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="03547-172">nuget.exe zobrazí výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="03547-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="03547-173">Viz [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="03547-173">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="03547-174">Chyby publikování</span><span class="sxs-lookup"><span data-stu-id="03547-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="03547-175">Správa publikovaného balíčku</span><span class="sxs-lookup"><span data-stu-id="03547-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="03547-176">Další kroky</span><span class="sxs-lookup"><span data-stu-id="03547-176">Next steps</span></span>

<span data-ttu-id="03547-177">Gratulujeme k vytvoření prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="03547-177">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03547-178">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="03547-178">Create a Package</span></span>](../create-packages/creating-a-package.md)

<span data-ttu-id="03547-179">Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.</span><span class="sxs-lookup"><span data-stu-id="03547-179">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="03547-180">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="03547-180">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="03547-181">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="03547-181">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="03547-182">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="03547-182">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="03547-183">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="03547-183">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="03547-184">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="03547-184">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
