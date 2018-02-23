---
title: "Poznámky k verzi služby WebMatrix NuGet 2.6.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Poznámky k verzi pro NuGet 2.6.1 pro službu WebMatrix, včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "Funkce, chcete přidat NuGet 2.6.1 pro poznámky k verzi služby WebMatrix, opravy chyb, známé problémy"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 633b71011dd1bc897ad95fd706337cef3aeef34c
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="f89d3-104">NuGet 2.6.1 poznámky k verzi služby WebMatrix</span><span class="sxs-lookup"><span data-stu-id="f89d3-104">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="f89d3-105">[Poznámky k verzi NuGet 2.6](../release-notes/nuget-2.6.md) | [NuGet 2.7 poznámky k verzi](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="f89d3-105">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="f89d3-106">Týmem NuGet vydala aktualizované rozšíření Správce balíčků NuGet pro službu WebMatrix 26 března 2014.</span><span class="sxs-lookup"><span data-stu-id="f89d3-106">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="f89d3-107">Tato aktualizace se dá nainstalovat z [Galerie rozšíření prostředí WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="f89d3-107">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="f89d3-108">Otevřete službu WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="f89d3-108">Open WebMatrix 3</span></span>
1. <span data-ttu-id="f89d3-109">Klikněte na ikonu rozšíření na pásu karet Domů</span><span class="sxs-lookup"><span data-stu-id="f89d3-109">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="f89d3-110">Vyberte kartu aktualizace</span><span class="sxs-lookup"><span data-stu-id="f89d3-110">Select the Updates tab</span></span>
1. <span data-ttu-id="f89d3-111">Klikněte na tlačítko Aktualizovat na verzi 2.6.1 Správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="f89d3-111">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="f89d3-112">Zavřete a znovu spusťte službu WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="f89d3-112">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="f89d3-113">Upozorňují na důležité změny</span><span class="sxs-lookup"><span data-stu-id="f89d3-113">Notable Changes</span></span>

<span data-ttu-id="f89d3-114">Tato rozšíření aktualizace řeší dva největších problémů uživatelů mají potýkají náročné balíčků NuGet v rámci služby WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f89d3-114">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="f89d3-115">První došlo k chybě verze schématu NuGet a druhý byl chyby vedoucí k knihovny DLL nula bajtů v `bin` složky.</span><span class="sxs-lookup"><span data-stu-id="f89d3-115">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="f89d3-116">Chyba verze schématu NuGet</span><span class="sxs-lookup"><span data-stu-id="f89d3-116">NuGet Schema Version Error</span></span>

<span data-ttu-id="f89d3-117">Vzhledem k tomu, že byl vydán služba WebMatrix 3, byly zavedeny nové funkce do NuGet, které vyžadují novou verzi schématu pro balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="f89d3-117">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="f89d3-118">Při pokusu o spravovat vaše balíčky NuGet ve vašem webu, tyto nové balíčky může vést k chybám, které se zobrazí ve službě WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f89d3-118">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Došlo k chybě.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="f89d3-122">Tato nejnovější verze poskytuje kompatibilitu s nejnovější balíčky NuGet, brání výskytu této chyby.</span><span class="sxs-lookup"><span data-stu-id="f89d3-122">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="f89d3-123">Nové verze, včetně Microsoft.AspNet.WebPages balíčky můžete nyní nainstalovat ve službě WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f89d3-123">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="f89d3-124">Některé z těchto balíčků byly pomocí funkce NuGet, jako [XDT konfigurační transformaci](../release-notes/nuget-2.6.md#xdt), který dosud nebyl podporován ve službě WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f89d3-124">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="f89d3-125">Nula bajtů knihovny DLL ve složce Koš</span><span class="sxs-lookup"><span data-stu-id="f89d3-125">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="f89d3-126">Někteří uživatelé hlásili, která po instalaci NuGet zabalí ve službě WebMatrix, které zahrnují knihovny DLL, které jsou kopírovány do přihrádky, který zobrazení knihovny DLL v `bin` složky jako soubory 0 bajtů.</span><span class="sxs-lookup"><span data-stu-id="f89d3-126">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="f89d3-127">Tím se přeruší aplikace za běhu.</span><span class="sxs-lookup"><span data-stu-id="f89d3-127">This breaks the application at runtime.</span></span>

<span data-ttu-id="f89d3-128">[Tento problém](https://nuget.codeplex.com/workitem/4060) nyní byl opraven.</span><span class="sxs-lookup"><span data-stu-id="f89d3-128">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="f89d3-129">Další vylepšení poslední</span><span class="sxs-lookup"><span data-stu-id="f89d3-129">Other Recent Improvements</span></span>

<span data-ttu-id="f89d3-130">Když 2.8 Správce balíčků NuGet byl vydán pro sadu Visual Studio, vydala společnost Microsoft také Správce balíčků NuGet 2.5.0 pro službu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f89d3-130">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="f89d3-131">Pokud to bylo uvedeno v [poznámky k verzi 2.8 NuGet](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nebyla jsme zmínili, konkrétní nových funkcí tuto aktualizaci zavedená.</span><span class="sxs-lookup"><span data-stu-id="f89d3-131">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="f89d3-132">Aktualizuje všechny</span><span class="sxs-lookup"><span data-stu-id="f89d3-132">Update All</span></span>

<span data-ttu-id="f89d3-133">Teď můžete aktualizovat všechny balíčky webové stránky v jednom kroku!</span><span class="sxs-lookup"><span data-stu-id="f89d3-133">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="f89d3-134">Když otevřete rozšíření NuGet ve službě WebMatrix, zobrazí seznam všech balíčků v galerii, nainstalované a ty aktualizace, které jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="f89d3-134">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="f89d3-135">Dříve se jednotlivě aktualizovat všechny balíčky, ale nyní je užitečné tlačítko "Aktualizovat vše", které se zobrazí na kartě aktualizace.</span><span class="sxs-lookup"><span data-stu-id="f89d3-135">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Klikněte na Aktualizovat vše aktualizovat všechny balíčky s aktualizacemi, k dispozici](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="f89d3-137">Přepsat existující soubory</span><span class="sxs-lookup"><span data-stu-id="f89d3-137">Overwrite Existing Files</span></span>

<span data-ttu-id="f89d3-138">Při instalaci balíčků, které obsahují soubory, které již existují na webovém serveru, NuGet ignorovala vždy bezobslužně tyto soubory (a nechat existující soubory samostatně).</span><span class="sxs-lookup"><span data-stu-id="f89d3-138">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="f89d3-139">To může vést k dojem, že byl nainstalován balíček, nebo správně aktualizován, když ve skutečnosti fungovat.</span><span class="sxs-lookup"><span data-stu-id="f89d3-139">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="f89d3-140">NuGet se nyní zobrazí výzvu k přepisovat soubory.</span><span class="sxs-lookup"><span data-stu-id="f89d3-140">NuGet will now prompt for files to be overwritten.</span></span>

![Řešení konfliktů souborů](./media/NuGet-2.8/webmatrix-overwrite-file.png)
