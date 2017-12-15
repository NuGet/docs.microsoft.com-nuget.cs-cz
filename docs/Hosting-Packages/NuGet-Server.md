---
title: "Pomocí NuGet.Server k hostování NuGet kanály | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 45138f80-9717-42c2-8b34-9a1bc1fb3eab
description: "Postup vytvoření a hostování balíčku NuGet informačního kanálu na libovolném serveru služby IIS pomocí NuGet.Server, zpřístupnění balíčků prostřednictvím protokolu HTTP a OData."
keywords: "NuGet kanálu, galerie NuGet vzdálených balíčků informačního kanálu, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f37b9b711a2bc8c39314214113045a6485f297a8
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nugetserver"></a><span data-ttu-id="0eb17-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="0eb17-104">NuGet.Server</span></span>

<span data-ttu-id="0eb17-105">NuGet.Server je balíček poskytuje základ .NET, který vytvoří aplikace ASP.NET, která může být hostitelem balíčku kanálu na libovolném serveru, který spouští IIS.</span><span class="sxs-lookup"><span data-stu-id="0eb17-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="0eb17-106">Jednoduše řečeno, NuGet.Server zpřístupní složky na serveru prostřednictvím protokolu HTTP (S) (konkrétně OData).</span><span class="sxs-lookup"><span data-stu-id="0eb17-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="0eb17-107">Je snadno nastavit a je nejvhodnější pro jednoduchého scénáře.</span><span class="sxs-lookup"><span data-stu-id="0eb17-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="0eb17-108">Vytvoření prázdné aplikace technologie ASP.NET v sadě Visual Studio a do ní přidejte balíček NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="0eb17-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="0eb17-109">Konfigurace `Packages` složky v aplikaci a přidání balíčků.</span><span class="sxs-lookup"><span data-stu-id="0eb17-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="0eb17-110">Nasaďte aplikaci do vhodný server.</span><span class="sxs-lookup"><span data-stu-id="0eb17-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="0eb17-111">V následujících částech provede tento proces podrobně pomocí jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="0eb17-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="0eb17-112">Vytvoření a nasazení webové aplikace ASP.NET s NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="0eb17-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="0eb17-113">V sadě Visual Studio, vyberte **soubor > Nový > projekt**, nastavte cílový framework pro rozhraní .NET Framework 4.6 (viz níže), vyhledejte "ASP.NET" a vyberte **webové aplikace ASP.NET (rozhraní .NET Framework)** Šablona pro jazyk C#.</span><span class="sxs-lookup"><span data-stu-id="0eb17-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![Nastavení cílového rozhraní .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="0eb17-115">Zadejte vhodný název aplikace *jiných* než NuGet.Server, výběrem OK a v dialogovém okně Další select **prázdný** šablony a vyberte možnost OK.</span><span class="sxs-lookup"><span data-stu-id="0eb17-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="0eb17-116">Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**a v uživatelském rozhraní Správce balíčků vyhledávat a instalovat nejnovější verzi balíčku NuGet.Server, pokud jste cílení na rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="0eb17-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="0eb17-117">(Můžete ji také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.)</span><span class="sxs-lookup"><span data-stu-id="0eb17-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![Instalace balíčku NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="0eb17-119">Pokud webová aplikace cílí rozhraní .NET Framework 4.5.2, je nutné nainstalovat NuGet Server **2.10.3** místo.</span><span class="sxs-lookup"><span data-stu-id="0eb17-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="0eb17-120">Instalace NuGet.Server převede prázdné webové aplikace do zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="0eb17-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="0eb17-121">Vytvoří `Packages` složky v aplikaci a přepíše `web.config` zahrnout další nastavení (viz komentáře v tomto souboru podrobnosti).</span><span class="sxs-lookup"><span data-stu-id="0eb17-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="0eb17-122">Balíčky k dispozici při publikování aplikace na server, přidáte jejich `.nupkg` souborů do `Packages` složky v sadě Visual Studio, nastavte jejich **akce sestavení** k **obsahu**a **kopírovat do výstupního adresáře** k **vždy Kopírovat**:</span><span class="sxs-lookup"><span data-stu-id="0eb17-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Kopírování balíčků do složky balíčky v projektu](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="0eb17-124">Spuštění tohoto webu místně v sadě Visual Studio (bez ladění, který je Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="0eb17-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="0eb17-125">Domovská stránka poskytuje že balíček kanálu adresy URL:</span><span class="sxs-lookup"><span data-stu-id="0eb17-125">The home page provides the package feed URLs:</span></span>

    ![Výchozí domovskou stránku pro aplikaci s NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="0eb17-127">Klikněte na **sem** v oblasti uvedených výše, pokud chcete zobrazit informační kanál OData balíčků.</span><span class="sxs-lookup"><span data-stu-id="0eb17-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="0eb17-128">Při prvním spuštění aplikace, ke změně struktury NuGet.Server `Packages` složky tak, aby obsahovala složku pro každý balíček.</span><span class="sxs-lookup"><span data-stu-id="0eb17-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="0eb17-129">To odpovídá [rozložení místní úložiště](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) zavedené NuGet 3.3 ke zlepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="0eb17-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="0eb17-130">Když přidáváte další balíčky, postupujte dál podle tuto strukturu.</span><span class="sxs-lookup"><span data-stu-id="0eb17-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="0eb17-131">Jakmile otestujete místní nasazení, nasazení aplikace na jakoukoli jinou lokalitu interních nebo externích podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="0eb17-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="0eb17-132">Po nasazení do `http://<domain>`, bude mít adresu URL, který používáte pro zdroj balíčku `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="0eb17-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="0eb17-133">Konfigurace složky balíčků</span><span class="sxs-lookup"><span data-stu-id="0eb17-133">Configuring the Packages folder</span></span>

<span data-ttu-id="0eb17-134">S `NuGet.Server` verzi 1.5 nebo novější, můžete konkrétně nakonfigurovat složky balíčku pomocí `appSetting/packagesPath` hodnotu `web.config`:</span><span class="sxs-lookup"><span data-stu-id="0eb17-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="0eb17-135">`packagesPath`může být absolutní nebo virtuální cesta.</span><span class="sxs-lookup"><span data-stu-id="0eb17-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="0eb17-136">Když `packagesPath` je tento parametr vynechán nebo ponecháno prázdné, je výchozí složka balíčky `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="0eb17-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="0eb17-137">Přidávání balíčků k informačnímu kanálu externě</span><span class="sxs-lookup"><span data-stu-id="0eb17-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="0eb17-138">Jakmile lokalita NuGet.Server běží, můžete přidat nebo odstranit balíčky pomocí nuget.exe za předpokladu, že nastavíte hodnotu klíče rozhraní API v `web.config`.</span><span class="sxs-lookup"><span data-stu-id="0eb17-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="0eb17-139">Po instalaci balíčku NuGet.Server `web.config` obsahuje prázdnou `appSetting/apiKey` hodnotu:</span><span class="sxs-lookup"><span data-stu-id="0eb17-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="0eb17-140">Když `apiKey` je vynechán nebo je prázdné, když zavedete balíčky k informačnímu kanálu zakázáno.</span><span class="sxs-lookup"><span data-stu-id="0eb17-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="0eb17-141">Chcete-li povolit tuto funkci, nastavte `apiKey` na hodnotu (v ideálním případě silné heslo) a přidejte klíč s názvem `appSettings/requireApiKey` s hodnotou `true`:</span><span class="sxs-lookup"><span data-stu-id="0eb17-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="0eb17-142">Pokud váš server je již zabezpečená nebo v opačném případě nepotřebujete klíč rozhraní API (např. při použití privátního serveru v síti místní team), můžete nastavit `requireApiKey` k `false`.</span><span class="sxs-lookup"><span data-stu-id="0eb17-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="0eb17-143">Všichni uživatelé s přístupem k serveru můžete pak push nebo odstranit balíčky.</span><span class="sxs-lookup"><span data-stu-id="0eb17-143">All users with access to the server can then push or delete packages.</span></span>