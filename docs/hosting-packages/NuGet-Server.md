---
title: Použití NuGet. Server k hostování kanálů NuGet
description: Postup vytvoření a hostování informačního kanálu balíčku NuGet na jakémkoli serveru se službou IIS pomocí NuGet. Server, zpřístupnění balíčků prostřednictvím protokolu HTTP a OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 82b353450ff1da23a17e5b1c6a825ad32782bf75
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610595"
---
# <a name="nugetserver"></a><span data-ttu-id="a44d2-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a44d2-103">NuGet.Server</span></span>

<span data-ttu-id="a44d2-104">NuGet. Server je balíček poskytovaný rozhraním .NET Foundation, který vytváří aplikaci ASP.NET, která může hostovat kanál balíčku na jakémkoli serveru, na kterém je spuštěna služba IIS.</span><span class="sxs-lookup"><span data-stu-id="a44d2-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="a44d2-105">Jednoduše řečeno, NuGet. server zpřístupňuje složku na serveru prostřednictvím protokolu HTTP (konkrétně OData).</span><span class="sxs-lookup"><span data-stu-id="a44d2-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="a44d2-106">U jednoduchých scénářů se snadno nastavuje a je nejvhodnější.</span><span class="sxs-lookup"><span data-stu-id="a44d2-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="a44d2-107">Vytvořte prázdnou webovou aplikaci v ASP.NET v aplikaci Visual Studio a přidejte do ní balíček NuGet. Server.</span><span class="sxs-lookup"><span data-stu-id="a44d2-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="a44d2-108">Nakonfigurujte složku `Packages` v aplikaci a přidejte balíčky.</span><span class="sxs-lookup"><span data-stu-id="a44d2-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="a44d2-109">Nasaďte aplikaci na vhodný server.</span><span class="sxs-lookup"><span data-stu-id="a44d2-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="a44d2-110">Následující části podrobně popisují tento proces pomocí nástroje C#.</span><span class="sxs-lookup"><span data-stu-id="a44d2-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="a44d2-111">Pokud máte další dotazy k NuGet. Server, vytvořte problém na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="a44d2-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="a44d2-112">Vytvoření a nasazení webové aplikace v ASP.NET pomocí NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="a44d2-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="a44d2-113">V sadě Visual Studio vyberte **soubor > nový > projekt**, vyhledejte "ASP.NET", vyberte šablonu **ASP.NET Web Application (.NET Framework)** pro C#a nastavte **rozhraní** na ".NET Framework 4,6":</span><span class="sxs-lookup"><span data-stu-id="a44d2-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Nastavení cílové architektury pro nový projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="a44d2-115">Poskytněte aplikaci vhodný *jiný* název než NuGet. Server, vyberte OK a v dalším dialogovém okně vyberte **prázdnou** šablonu a pak vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="a44d2-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="a44d2-116">Klikněte pravým tlačítkem na projekt a vyberte **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a44d2-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="a44d2-117">V uživatelském rozhraní Správce balíčků vyberte kartu **Procházet** a pak vyhledejte a nainstalujte nejnovější verzi balíčku NuGet. Server, pokud cílíte .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="a44d2-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="a44d2-118">(Můžete ji také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.) Pokud se zobrazí výzva, přijměte licenční podmínky.</span><span class="sxs-lookup"><span data-stu-id="a44d2-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalace balíčku NuGet. Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="a44d2-120">Instalace NuGet. Server převede prázdnou webovou aplikaci na zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="a44d2-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="a44d2-121">Nainstaluje celou řadu dalších balíčků, vytvoří v aplikaci složku `Packages` a upraví `web.config` tak, aby zahrnovala další nastavení (podrobnosti najdete v komentářích v tomto souboru).</span><span class="sxs-lookup"><span data-stu-id="a44d2-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="a44d2-122">Pečlivě zkontrolujte `web.config` poté, co balíček NuGet. Server dokončil změny v tomto souboru.</span><span class="sxs-lookup"><span data-stu-id="a44d2-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="a44d2-123">NuGet. Server nemůže přepsat existující prvky, ale místo toho vytvoří duplicitní prvky.</span><span class="sxs-lookup"><span data-stu-id="a44d2-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="a44d2-124">Tyto duplicity způsobí při pozdějším spuštění projektu "interní chybu serveru".</span><span class="sxs-lookup"><span data-stu-id="a44d2-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="a44d2-125">Pokud například `web.config` obsahuje `<compilation debug="true" targetFramework="4.5.2" />` před instalací NuGet. Server, balíček ho nepřepíše, ale vloží druhý `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="a44d2-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="a44d2-126">V takovém případě odstraňte element se starší verzí rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a44d2-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="a44d2-127">Chcete-li zpřístupnit balíčky v informačním kanálu při publikování aplikace na server, přidejte jednotlivé soubory `.nupkg` do složky `Packages` v sadě Visual Studio a pak nastavte každou **akci sestavení** na **obsah** a **Kopírovat do výstupního adresáře** .  **vždy**:</span><span class="sxs-lookup"><span data-stu-id="a44d2-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Kopírování balíčků do složky Packages v projektu](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="a44d2-129">Místní spuštění webu v aplikaci Visual Studio (použití **ladění > spustit bez ladění** nebo CTRL + F5).</span><span class="sxs-lookup"><span data-stu-id="a44d2-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="a44d2-130">Domovská stránka poskytuje adresy URL kanálu balíčku, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="a44d2-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="a44d2-131">Pokud se zobrazí chyby, pečlivě zkontrolujte `web.config` pro duplicitní prvky, které jsou uvedeny dříve v kroku 5.</span><span class="sxs-lookup"><span data-stu-id="a44d2-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Výchozí domovská stránka aplikace s NuGet. Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="a44d2-133">Kliknutím **sem** v oblasti uvedené výše zobrazíte kanál OData pro balíčky.</span><span class="sxs-lookup"><span data-stu-id="a44d2-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="a44d2-134">Při prvním spuštění aplikace NuGet. Server restrukturuje složku `Packages` tak, aby obsahovala složku pro každý balíček.</span><span class="sxs-lookup"><span data-stu-id="a44d2-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="a44d2-135">To odpovídá [rozložení místního úložiště](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) zavedenému pomocí NuGet 3,3 pro zlepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="a44d2-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="a44d2-136">Při přidávání dalších balíčků pokračujte podle této struktury.</span><span class="sxs-lookup"><span data-stu-id="a44d2-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="a44d2-137">Po otestování místního nasazení Nasaďte aplikaci na jakoukoli jinou interní nebo externí lokalitu podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="a44d2-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="a44d2-138">Po nasazení na `http://<domain>`se adresa URL, kterou použijete pro zdroj balíčku, `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="a44d2-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="a44d2-139">Konfigurace složky balíčků</span><span class="sxs-lookup"><span data-stu-id="a44d2-139">Configuring the Packages folder</span></span>

<span data-ttu-id="a44d2-140">U `NuGet.Server` 1,5 a novějších verzí můžete složku balíčku přesněji konfigurovat pomocí `appSetting/packagesPath` hodnoty v `web.config`:</span><span class="sxs-lookup"><span data-stu-id="a44d2-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="a44d2-141">`packagesPath` může být absolutní nebo virtuální cesta.</span><span class="sxs-lookup"><span data-stu-id="a44d2-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="a44d2-142">Pokud je `packagesPath` vynechána nebo je ponecháno prázdné, složka Packages je výchozí `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="a44d2-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="a44d2-143">Přidávají se balíčky do externího kanálu externě.</span><span class="sxs-lookup"><span data-stu-id="a44d2-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="a44d2-144">Po spuštění serveru NuGet. Server můžete balíčky přidat pomocí [nabízených oznámení NuGet](../reference/cli-reference/cli-ref-push.md) , pokud nastavíte hodnotu klíče rozhraní API v `web.config`.</span><span class="sxs-lookup"><span data-stu-id="a44d2-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="a44d2-145">Po instalaci balíčku NuGet. Server `web.config` obsahuje prázdnou `appSetting/apiKey` hodnotu:</span><span class="sxs-lookup"><span data-stu-id="a44d2-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a44d2-146">Pokud je hodnota `apiKey` vynechána nebo je prázdná, je zablokováno vkládání balíčků do informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="a44d2-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="a44d2-147">Pokud chcete tuto funkci povolit, nastavte `apiKey` na hodnotu (ideálně silné heslo) a přidejte klíč s názvem `appSettings/requireApiKey` s hodnotou `true`:</span><span class="sxs-lookup"><span data-stu-id="a44d2-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a44d2-148">Pokud je váš server už zabezpečený nebo pokud nepotřebujete klíč rozhraní API (například při použití privátního serveru v místní týmové síti), můžete nastavit `requireApiKey` na `false`.</span><span class="sxs-lookup"><span data-stu-id="a44d2-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="a44d2-149">Všichni uživatelé s přístupem k serveru pak můžou nabízet balíčky.</span><span class="sxs-lookup"><span data-stu-id="a44d2-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="a44d2-150">Odebírají se balíčky z informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="a44d2-150">Removing packages from the feed</span></span>

<span data-ttu-id="a44d2-151">Pomocí NuGet. Server odebere příkaz [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) balíček z úložiště, do kterého jste zadali klíč rozhraní API s komentářem.</span><span class="sxs-lookup"><span data-stu-id="a44d2-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="a44d2-152">Pokud chcete změnit chování pro devýpis balíčku (nechat ho k dispozici pro obnovení balíčku), změňte `enableDelisting` klíč v `web.config` na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="a44d2-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="a44d2-153">Podpora NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="a44d2-153">NuGet.Server support</span></span>

<span data-ttu-id="a44d2-154">Pokud chcete další nápovědu k používání NuGet. Server, vytvořte problém na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="a44d2-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>