---
title: Použití nuget.serveru k hostování informačních kanálů NuGet
description: Jak vytvořit a hostovat informační kanál balíčku NuGet na libovolném serveru se spuštěnou službou IIS pomocí souboru NuGet.Server, čímž jsou balíčky zpřístupněny prostřednictvím protokolů HTTP a OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059523"
---
# <a name="nugetserver"></a><span data-ttu-id="ecc2e-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="ecc2e-103">NuGet.Server</span></span>

<span data-ttu-id="ecc2e-104">NuGet.Server je balíček poskytovaný službou .NET Foundation, který vytváří ASP.NET aplikaci, která může hostovat zdroj balíčků na libovolném serveru se službou IIS.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="ecc2e-105">Jednoduše řečeno, NuGet.Server zpřístupňuje složku na serveru prostřednictvím HTTP(S) (konkrétně OData).</span><span class="sxs-lookup"><span data-stu-id="ecc2e-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="ecc2e-106">Je snadné nastavit a je nejlepší pro jednoduché scénáře.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="ecc2e-107">Vytvořte prázdnou ASP.NET webovou aplikaci v sadě Visual Studio a přidejte do ní balíček NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="ecc2e-108">Nakonfigurujte `Packages` složku v aplikaci a přidejte balíčky.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="ecc2e-109">Nasazení aplikace na vhodný server.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="ecc2e-110">Následující části podrobně procházejí tímto procesem pomocí jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="ecc2e-111">Máte-li další dotazy týkající se nuget.server, vytvořte problém na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="ecc2e-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="ecc2e-112">Vytvoření a nasazení webové aplikace ASP.NET pomocí serveru NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="ecc2e-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="ecc2e-113">V sadě Visual Studio vyberte **soubor > nový > project**, vyhledejte "ASP.NET webovou aplikaci (.NET Framework)", vyberte odpovídající šablonu pro C#.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for C#.</span></span>

    ![Výběr šablony webového projektu rozhraní .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="ecc2e-115">Nastavte **framework** na ".NET Framework 4.6".</span><span class="sxs-lookup"><span data-stu-id="ecc2e-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Nastavení cílového rámce pro nový projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="ecc2e-117">Pojmenujte aplikaci jiný *název* než NuGet.Server, vyberte OK a v dalším dialogovém okně vyberte **prázdnou** šablonu a pak vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Výběr prázdného webového projektu](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="ecc2e-119">Klikněte pravým tlačítkem myši na projekt a vyberte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="ecc2e-120">V unovém rozhraní Správce balíčků vyberte kartu **Procházet** a pak vyhledejte a nainstalujte nejnovější verzi balíčku NuGet.Server, pokud cílíte na rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="ecc2e-121">(Můžete jej také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.) Při přijetí výzvy přijměte licenční podmínky.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalace balíčku NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="ecc2e-123">Instalace nuget.serveru převede prázdnou webovou aplikaci na zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="ecc2e-124">Nainstaluje řadu dalších balíčků, vytvoří `Packages` složku v aplikaci a `web.config` upraví zahrnout další nastavení (podrobnosti naleznete v komentářích v tomto souboru).</span><span class="sxs-lookup"><span data-stu-id="ecc2e-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="ecc2e-125">Pečlivě `web.config` zkontrolujte po NuGet.Server balíček dokončil své změny tohoto souboru.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="ecc2e-126">NuGet.Server nemusí přepsat existující prvky, ale místo toho vytvořit duplicitní prvky.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="ecc2e-127">Tyto duplikáty způsobí "Vnitřní chyba serveru" při pozdějším pokusu o spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="ecc2e-128">Například pokud `web.config` vaše `<compilation debug="true" targetFramework="4.5.2" />` obsahuje před instalací NuGet.Server, balíček není přepsat, `<compilation debug="true" targetFramework="4.6" />`ale vloží druhý .</span><span class="sxs-lookup"><span data-stu-id="ecc2e-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="ecc2e-129">V takovém případě odstraňte prvek se starší verzí frameworku.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="ecc2e-130">Spusťte web místně v sadě Visual Studio (pomocí **ladění > spustit bez ladění** nebo Ctrl+F5).</span><span class="sxs-lookup"><span data-stu-id="ecc2e-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="ecc2e-131">Domovská stránka obsahuje adresy URL zdroje balíčků, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="ecc2e-132">Pokud se zobrazí chyby, pečlivě zkontrolujte `web.config` duplicitní prvky, jak je uvedeno dříve.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![Výchozí domovská stránka aplikace s NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="ecc2e-134">Při prvním spuštění aplikace NuGet.Server restrukturalizuje `Packages` složku tak, aby obsahovala složku pro každý balíček.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="ecc2e-135">To odpovídá [rozložení místního úložiště](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) zavedené s NuGet 3.3 ke zlepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="ecc2e-136">Při přidávání dalšíbalíčky, pokračovat v následující struktuře.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="ecc2e-137">Po otestování místního nasazení nasaďte aplikaci do jakékoli jiné interní nebo externí lokality podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="ecc2e-138">Po nasazení `http://<domain>`do , bude adresa URL, kterou `http://<domain>/nuget`používáte pro zdroj balíčku .</span><span class="sxs-lookup"><span data-stu-id="ecc2e-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="ecc2e-139">Externí přidávání balíků do informačního kanálu</span><span class="sxs-lookup"><span data-stu-id="ecc2e-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="ecc2e-140">Po spuštění webu NuGet.Server můžete přidat balíčky pomocí [nuget push](../reference/cli-reference/cli-ref-push.md) za předpokladu, že nastavíte hodnotu klíče rozhraní API v aplikaci `web.config`.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="ecc2e-141">Po instalaci balíčku NuGet.Server `web.config` obsahuje `appSetting/apiKey` prázdnou hodnotu:</span><span class="sxs-lookup"><span data-stu-id="ecc2e-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="ecc2e-142">Pokud `apiKey` je vynechánnebo prázdný, odesílání balíčků do informačního kanálu je zakázáno.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="ecc2e-143">Chcete-li tuto funkci `apiKey` povolit, nastavte hodnotu (v ideálním `appSettings/requireApiKey` případě silné `true`heslo) a přidejte klíč volaný s hodnotou :</span><span class="sxs-lookup"><span data-stu-id="ecc2e-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="ecc2e-144">Pokud je server již zabezpečený nebo jinak nepotřebujete klíč rozhraní API (například při použití `requireApiKey` privátního serveru v místní týmové síti), můžete nastavit na . `false`</span><span class="sxs-lookup"><span data-stu-id="ecc2e-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="ecc2e-145">Všechny uživatele s přístupem k serveru pak mohou vymísťovat balíčky.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="ecc2e-146">Počínaje nuget.server 3.0.0, url pro odesílání `http://<domain>/nuget`balíčků byla změna na .</span><span class="sxs-lookup"><span data-stu-id="ecc2e-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="ecc2e-147">Před vydáním verze 3.0.0 byla `http://<domain>/api/v2/package`adresa URL push .</span><span class="sxs-lookup"><span data-stu-id="ecc2e-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="ecc2e-148">S NuGet 3.2.1 a novější, `/api/v2/package` tato starší `/nuget` adresa URL `enableLegacyPushRoute: true` je povolena kromě`NuGetODataConfig.cs` ve výchozím nastavení prostřednictvím možnosti v spouštěcí konfiguraci (ve výchozím nastavení).</span><span class="sxs-lookup"><span data-stu-id="ecc2e-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="ecc2e-149">Všimněte si, že tato funkce nefunguje, pokud více informačních kanálů jsou hostovány ve stejném projektu.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="ecc2e-150">Odebrání balíčků z informačního kanálu</span><span class="sxs-lookup"><span data-stu-id="ecc2e-150">Removing packages from the feed</span></span>

<span data-ttu-id="ecc2e-151">S NuGet.Server [nuget delete](../reference/cli-reference/cli-ref-delete.md) příkaz odebere balíček z úložiště za předpokladu, že zahrnete klíč rozhraní API s komentářem.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="ecc2e-152">Pokud chcete změnit chování, aby delist balíček místo (ponechat `enableDelisting` k `web.config` dispozici pro obnovení balíčku), změňte klíč v true.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="ecc2e-153">Konfigurace složky Balíčky</span><span class="sxs-lookup"><span data-stu-id="ecc2e-153">Configuring the Packages folder</span></span>

<span data-ttu-id="ecc2e-154">Pomocí `NuGet.Server` položky 1.5 a novějšímůžete přizpůsobit `appSettings/packagesPath` složku `web.config`balíčku pomocí hodnoty v části :</span><span class="sxs-lookup"><span data-stu-id="ecc2e-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="ecc2e-155">`packagesPath`může být absolutní nebo virtuální cesta.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="ecc2e-156">Pokud `packagesPath` je vynechánnebo ponechán prázdný, složka `~/Packages`balíčky je výchozí .</span><span class="sxs-lookup"><span data-stu-id="ecc2e-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="ecc2e-157">Zpřístupnění balíčků při publikování webové aplikace</span><span class="sxs-lookup"><span data-stu-id="ecc2e-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="ecc2e-158">Chcete-li balíčky zpřístupnit v informačním kanálu při `.nupkg` publikování aplikace `Packages` na server, přidejte jednotlivé soubory do složky v sadě Visual Studio a potom nastavte každý z nich **akce sestavení** na **obsah** a kopírovat **do výstupního adresáře** **ke kopírování vždy**:</span><span class="sxs-lookup"><span data-stu-id="ecc2e-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Kopírování balíčků do složky Balíčky v projektu](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="ecc2e-160">Poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="ecc2e-160">Release Notes</span></span>

<span data-ttu-id="ecc2e-161">Poznámky k verzi pro NuGet.Server jsou k dispozici na [stránce vydání GitHubu](https://github.com/NuGet/NuGet.Server/releases).</span><span class="sxs-lookup"><span data-stu-id="ecc2e-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="ecc2e-162">To zahrnuje podrobnosti o opravách chyb a nových funkcích, které jsou přidány.</span><span class="sxs-lookup"><span data-stu-id="ecc2e-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="ecc2e-163">Podpora nuget.server</span><span class="sxs-lookup"><span data-stu-id="ecc2e-163">NuGet.Server support</span></span>

<span data-ttu-id="ecc2e-164">Další nápovědu pomocí souboru NuGet.Server získáte vytvořením problému v aplikaci [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="ecc2e-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
