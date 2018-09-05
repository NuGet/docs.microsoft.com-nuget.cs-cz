---
title: Použití NuGet.Server k hostování NuGet informační kanály
description: Jak vytvořit a hostovat balíček NuGet kanálu na libovolný server se službou IIS pomocí NuGet.Server, zpřístupnění balíčků prostřednictvím protokolu HTTP a protokolu OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: e99d42744ec860976ae098be94e747ec4bc9a7c6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551953"
---
# <a name="nugetserver"></a><span data-ttu-id="61db6-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="61db6-103">NuGet.Server</span></span>

<span data-ttu-id="61db6-104">NuGet.Server je balíček poskytované .NET Foundation, který vytváří aplikaci ASP.NET, který může hostovat balíček kanálu na libovolném serveru, na kterém běží služby IIS.</span><span class="sxs-lookup"><span data-stu-id="61db6-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="61db6-105">Jednoduše ale nutné dodat, NuGet.Server zpřístupňuje složky na serveru prostřednictvím protokolu HTTP (S) (konkrétně OData).</span><span class="sxs-lookup"><span data-stu-id="61db6-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="61db6-106">Je snadné nastavení a je nejvhodnější pro jednoduché scénáře.</span><span class="sxs-lookup"><span data-stu-id="61db6-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="61db6-107">Vytvořit prázdnou webovou aplikaci ASP.NET v sadě Visual Studio a přidejte do ní balíček NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="61db6-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="61db6-108">Konfigurace `Packages` složky v aplikaci a přidání balíčků.</span><span class="sxs-lookup"><span data-stu-id="61db6-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="61db6-109">Nasaďte aplikaci do vhodný server.</span><span class="sxs-lookup"><span data-stu-id="61db6-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="61db6-110">V následujících částech si tento proces podrobně pomocí jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="61db6-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="61db6-111">Pokud máte další otázky týkající se NuGet.Server, vytvoření problému na [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="61db6-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="61db6-112">Vytvoření a nasazení webové aplikace ASP.NET s NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="61db6-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="61db6-113">V sadě Visual Studio, vyberte **soubor > Nový > projekt**, vyhledejte "ASP.NET", vyberte **webová aplikace ASP.NET (.NET Framework)** šablony pro C# a sady **Framework** ".NET Framework 4.6":</span><span class="sxs-lookup"><span data-stu-id="61db6-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Nastavení cílový rámec pro nový projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="61db6-115">Zadejte vhodný název aplikace *jiných* než NuGet.Server, vyberte OK a v dalším dialogovém okně vyberte **prázdný** šablony, pak vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="61db6-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="61db6-116">Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="61db6-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="61db6-117">V uživatelském rozhraní Správce balíčků, vyberte **Procházet** kartě pak vyhledávat a instalovat nejnovější verzi balíčku NuGet.Server, pokud se zaměřujete na rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="61db6-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="61db6-118">(Můžete ho také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.) Pokud se zobrazí výzva, přijměte licenční podmínky.</span><span class="sxs-lookup"><span data-stu-id="61db6-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instaluje se balíček NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="61db6-120">Prázdná webová aplikace instalace NuGet.Server převede na zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="61db6-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="61db6-121">Nainstaluje celou řadu dalších balíčků, vytvoří `Packages` složky v aplikaci a změní `web.config` zahrnout další nastavení (viz poznámky v tomto souboru podrobnosti).</span><span class="sxs-lookup"><span data-stu-id="61db6-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="61db6-122">Pečlivě zkontrolujte `web.config` po dokončení své změny do tohoto souboru balíčku NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="61db6-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="61db6-123">NuGet.Server může přepsat stávající elementy, ale místo toho vytvořit duplicitní prvky.</span><span class="sxs-lookup"><span data-stu-id="61db6-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="61db6-124">Tyto duplikáty způsobí "vnitřní chyba serveru", když zkusíte později, spusťte projekt.</span><span class="sxs-lookup"><span data-stu-id="61db6-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="61db6-125">Například pokud vaše `web.config` obsahuje `<compilation debug="true" targetFramework="4.5.2" />` před instalací NuGet.Server balíček nepřepíše ho ale vloží sekundy `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="61db6-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="61db6-126">V takovém případě odstraňte prvek starší verze rozhraní framework.</span><span class="sxs-lookup"><span data-stu-id="61db6-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="61db6-127">K dispozici balíčky v informačním kanálu publikování aplikace na serveru, přidejte všechny `.nupkg` soubory `Packages` složky v sadě Visual Studio, nastavte každé z nich **akce sestavení** k **obsahu**a **kopírovat do výstupního adresáře** k **vždy Kopírovat**:</span><span class="sxs-lookup"><span data-stu-id="61db6-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Balíčky se kopírují do složky balíčků v projektu](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="61db6-129">Spuštění tohoto webu místně v sadě Visual Studio (pomocí **ladit > Spustit bez ladění** nebo Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="61db6-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="61db6-130">Domovská stránka obsahuje balíček kanálu adresy URL, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="61db6-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="61db6-131">Pokud se zobrazí chyby, pečlivě zkontrolujte vaše `web.config` pro duplicitní prvky jsou jste si předtím poznamenali v kroku 5.</span><span class="sxs-lookup"><span data-stu-id="61db6-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Výchozí domovskou stránku pro aplikaci s NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="61db6-133">Klikněte na **tady** v oblasti zobrazíte kanál OData, které balíčky uvedené výše.</span><span class="sxs-lookup"><span data-stu-id="61db6-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="61db6-134">Při prvním spuštění aplikace, ke změně struktury NuGet.Server `Packages` složku tak, aby obsahovala složku pro každý balíček.</span><span class="sxs-lookup"><span data-stu-id="61db6-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="61db6-135">To odpovídá [rozložení místní úložiště](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) představeny s nástrojem NuGet 3.3 ke zlepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="61db6-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="61db6-136">Při přidávání dalších balíčků, i nadále tuto strukturu.</span><span class="sxs-lookup"><span data-stu-id="61db6-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="61db6-137">Jakmile jste otestovali místní nasazení, podle potřeby nasadíte aplikace na další interní nebo externí web.</span><span class="sxs-lookup"><span data-stu-id="61db6-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="61db6-138">Po nasazení chcete `http://<domain>`, bude mít adresu URL, který používáte pro zdroj balíčku `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="61db6-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="61db6-139">Konfigurace složky balíčků</span><span class="sxs-lookup"><span data-stu-id="61db6-139">Configuring the Packages folder</span></span>

<span data-ttu-id="61db6-140">S `NuGet.Server` 1.5 a novější, můžete přesněji řečeno nakonfigurovat pomocí složku balíčku `appSetting/packagesPath` hodnota v `web.config`:</span><span class="sxs-lookup"><span data-stu-id="61db6-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="61db6-141">`packagesPath` může být absolutní nebo virtuální cesta.</span><span class="sxs-lookup"><span data-stu-id="61db6-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="61db6-142">Když `packagesPath` je vynechán nebo prázdné, je výchozí složka balíčky `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="61db6-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="61db6-143">Přidávají se balíčky do informačního kanálu externě</span><span class="sxs-lookup"><span data-stu-id="61db6-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="61db6-144">Jakmile NuGet.Server Web spuštěný, může přidání balíčků s využitím [nuget nabízených](../tools/cli-ref-push.md) za předpokladu, že nastavíte hodnotu klíče rozhraní API v `web.config`.</span><span class="sxs-lookup"><span data-stu-id="61db6-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="61db6-145">Po instalaci balíčku NuGet.Server `web.config` obsahuje prázdnou `appSetting/apiKey` hodnotu:</span><span class="sxs-lookup"><span data-stu-id="61db6-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="61db6-146">Když `apiKey` je vynechán, nebo prázdná, nahráním balíčky do informačního kanálu je zakázána.</span><span class="sxs-lookup"><span data-stu-id="61db6-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="61db6-147">Chcete-li povolit tuto funkci, nastavte `apiKey` na hodnotu (v ideálním případě silné heslo) a přidejte klíč s názvem `appSettings/requireApiKey` s hodnotou `true`:</span><span class="sxs-lookup"><span data-stu-id="61db6-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="61db6-148">Pokud váš server je již zabezpečený nebo jinak nepožadujete klíč rozhraní API (například při použití privátní server na místní team sítě), můžete nastavit `requireApiKey` k `false`.</span><span class="sxs-lookup"><span data-stu-id="61db6-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="61db6-149">Všichni uživatelé s přístupem k serveru pak můžete nabízet balíčky.</span><span class="sxs-lookup"><span data-stu-id="61db6-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="61db6-150">Odebrání balíčků z informačního kanálu</span><span class="sxs-lookup"><span data-stu-id="61db6-150">Removing packages from the feed</span></span>

<span data-ttu-id="61db6-151">S NuGet.Server [nuget odstranit](../tools/cli-ref-delete.md) příkaz odebere balíček z úložiště, za předpokladu, že obsahovat klíč rozhraní API s komentářem.</span><span class="sxs-lookup"><span data-stu-id="61db6-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="61db6-152">Pokud chcete změnit chování výmazu místo zápisu balíček (se v něm k dispozici pro obnovení balíčku), změnit `enableDelisting` klíče v `web.config` na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="61db6-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="61db6-153">Podpora NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="61db6-153">NuGet.Server support</span></span>

<span data-ttu-id="61db6-154">Pokud potřebujete další pomoc pomocí NuGet.Server, vytvoření problému na [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="61db6-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>