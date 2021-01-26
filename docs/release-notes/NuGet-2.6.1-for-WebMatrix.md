---
title: 2.6.1 NuGet pro poznámky k verzi WebMatrixu
description: Poznámky k verzi NuGet 2.6.1 pro WebMatrix, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780422"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="222fb-103">2.6.1 NuGet pro poznámky k verzi WebMatrixu</span><span class="sxs-lookup"><span data-stu-id="222fb-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="222fb-104">Zpráva k [vydání verze](../release-notes/nuget-2.6.md)  |  NuGet 2,6 Zpráva k [vydání verze NuGet 2,7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="222fb-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="222fb-105">Tým NuGet uvolnil aktualizované rozšíření Správce balíčků NuGet pro WebMatrix na 26. března 2014.</span><span class="sxs-lookup"><span data-stu-id="222fb-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="222fb-106">Tuto aktualizaci můžete nainstalovat z [Galerie rozšíření WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="222fb-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="222fb-107">Otevřít WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="222fb-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="222fb-108">Klikněte na ikonu rozšíření na pásu karet domů.</span><span class="sxs-lookup"><span data-stu-id="222fb-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="222fb-109">Vyberte kartu aktualizace.</span><span class="sxs-lookup"><span data-stu-id="222fb-109">Select the Updates tab</span></span>
1. <span data-ttu-id="222fb-110">Kliknutím můžete aktualizovat Správce balíčků NuGet na 2.6.1</span><span class="sxs-lookup"><span data-stu-id="222fb-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="222fb-111">Zavřít a restartovat WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="222fb-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="222fb-112">Významné změny</span><span class="sxs-lookup"><span data-stu-id="222fb-112">Notable Changes</span></span>

<span data-ttu-id="222fb-113">Tato aktualizace rozšíření řeší dva z největších problémů, které uživatelé čelí využívání balíčků NuGet v rámci WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="222fb-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="222fb-114">První byla chyba verze schématu NuGet a druhá byla chyba vedoucí do složky DLL s nulovým počtem bajtů `bin` .</span><span class="sxs-lookup"><span data-stu-id="222fb-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="222fb-115">Chyba verze schématu NuGet</span><span class="sxs-lookup"><span data-stu-id="222fb-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="222fb-116">Vzhledem k tomu, že byla vydána WebMatrix 3, byly do sady NuGet zavedeny nové funkce, které vyžadují novou verzi schématu pro balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="222fb-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="222fb-117">Při pokusu o správu balíčků NuGet na webu můžou tyto nové balíčky vést k chybám, které vidíte ve WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="222fb-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Došlo k chybě.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="222fb-121">Tato nejnovější vydaná verze poskytuje kompatibilitu s nejnovějšími balíčky NuGet, což brání v výskytu této chyby.</span><span class="sxs-lookup"><span data-stu-id="222fb-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="222fb-122">Nové verze balíčků, včetně Microsoft. AspNet. webpages, se teď dají nainstalovat do WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="222fb-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="222fb-123">Některé z těchto balíčků používaly funkce NuGet, jako jsou [transformace XDT config](../release-notes/nuget-2.6.md#xdt), které se ještě nepodporovaly ve WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="222fb-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="222fb-124">Zero-Byte knihovny DLL ve složce bin</span><span class="sxs-lookup"><span data-stu-id="222fb-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="222fb-125">Někteří uživatelé oznámili, že po instalaci balíčků NuGet ve WebMatrixu, které obsahují knihovny DLL, které kopírují do bin, se knihovny DLL zobrazují ve `bin` složce jako soubory o velikosti 0 bajtů.</span><span class="sxs-lookup"><span data-stu-id="222fb-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="222fb-126">Tím dojde k přerušení aplikace za běhu.</span><span class="sxs-lookup"><span data-stu-id="222fb-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="222fb-127">[Tento problém](https://nuget.codeplex.com/workitem/4060) byl nyní opraven.</span><span class="sxs-lookup"><span data-stu-id="222fb-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="222fb-128">Další nejnovější vylepšení</span><span class="sxs-lookup"><span data-stu-id="222fb-128">Other Recent Improvements</span></span>

<span data-ttu-id="222fb-129">Po vydání Správce balíčků NuGet 2,8 pro Visual Studio jsme vydali také správce balíčků NuGet 2.5.0 pro WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="222fb-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="222fb-130">I když se to zmiňuje v [poznámkách k verzi NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nezmiňujeme vám konkrétní nové funkce, které aktualizace zavádí.</span><span class="sxs-lookup"><span data-stu-id="222fb-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="222fb-131">Aktualizovat vše</span><span class="sxs-lookup"><span data-stu-id="222fb-131">Update All</span></span>

<span data-ttu-id="222fb-132">Nyní můžete aktualizovat všechny balíčky webu v jednom kroku!</span><span class="sxs-lookup"><span data-stu-id="222fb-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="222fb-133">Když otevřete rozšíření NuGet v WebMatrixu, zobrazí se seznam všech balíčků v galerii, nainstalované a ty, které mají dostupné aktualizace.</span><span class="sxs-lookup"><span data-stu-id="222fb-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="222fb-134">Dřív se musí každý balíček aktualizovat jednotlivě, ale teď je užitečné tlačítko Aktualizovat vše, které se zobrazí na kartě aktualizace.</span><span class="sxs-lookup"><span data-stu-id="222fb-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Kliknutím na Aktualizovat vše aktualizujte všechny balíčky s dostupnými aktualizacemi.](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="222fb-136">Přepsat existující soubory</span><span class="sxs-lookup"><span data-stu-id="222fb-136">Overwrite Existing Files</span></span>

<span data-ttu-id="222fb-137">Při instalaci balíčků, které obsahují soubory, které už na vašem webu existují, má NuGet vždycky jenom tiché ignorování těchto souborů (vaše stávající soubory zůstanou beze všech).</span><span class="sxs-lookup"><span data-stu-id="222fb-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="222fb-138">To může vést ke dojmu o tom, že byl balíček nainstalovaný nebo aktualizovaný správně, ale ve skutečnosti to nebylo.</span><span class="sxs-lookup"><span data-stu-id="222fb-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="222fb-139">NuGet se teď zobrazí výzva, aby se soubory přepsaly.</span><span class="sxs-lookup"><span data-stu-id="222fb-139">NuGet will now prompt for files to be overwritten.</span></span>

![Řešení konfliktů souborů](./media/NuGet-2.8/webmatrix-overwrite-file.png)
