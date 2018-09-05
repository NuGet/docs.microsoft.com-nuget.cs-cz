---
title: NuGet 2.6.1 pro WebMatrix poznámky
description: Zpráva k vydání verze pro NuGet 2.6.1 pro WebMatrix, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550314"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="dfa7e-103">NuGet 2.6.1 pro WebMatrix poznámky</span><span class="sxs-lookup"><span data-stu-id="dfa7e-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="dfa7e-104">[Zpráva k vydání verze NuGet 2.6](../release-notes/nuget-2.6.md) | [zpráva k vydání verze NuGet 2.7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="dfa7e-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="dfa7e-105">Tým NuGet vydána aktualizace rozšíření Správce balíčků NuGet pro službu WebMatrix 26. března 2014.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="dfa7e-106">Tato aktualizace se dá nainstalovat z [Galerie rozšíření nástroje WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="dfa7e-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="dfa7e-107">Otevřete nástroj WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="dfa7e-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="dfa7e-108">Klepněte na ikonu rozšíření na pásu karet Domů</span><span class="sxs-lookup"><span data-stu-id="dfa7e-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="dfa7e-109">Vyberte kartu aktualizace</span><span class="sxs-lookup"><span data-stu-id="dfa7e-109">Select the Updates tab</span></span>
1. <span data-ttu-id="dfa7e-110">Klikněte na tlačítko Aktualizovat správce balíčků NuGet 2.6.1</span><span class="sxs-lookup"><span data-stu-id="dfa7e-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="dfa7e-111">Zavřete a znovu spusťte službu WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="dfa7e-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="dfa7e-112">Upozorňují na důležité změny</span><span class="sxs-lookup"><span data-stu-id="dfa7e-112">Notable Changes</span></span>

<span data-ttu-id="dfa7e-113">Tato rozšíření aktualizace řeší dvou největších problémů uživatelů mají ve využívání balíčků NuGet v rámci služby WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="dfa7e-114">První: došlo k chybě schématu verze NuGet a druhým byla chyba vede na nula bajtů knihovny DLL v `bin` složky.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="dfa7e-115">Chyba verze schématu NuGet</span><span class="sxs-lookup"><span data-stu-id="dfa7e-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="dfa7e-116">Od vydání služby WebMatrix 3 byly zavedeny nové funkce do NuGet, které vyžadují nové schéma verze pro balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="dfa7e-117">Při pokusu o správu vašich balíčků NuGet na vašem webu, tyto nové balíčky může vést k chybám, které se zobrazí ve službě WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Došlo k chybě.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="dfa7e-121">Tato nejnovější vydaná verze poskytuje kompatibilitu s nejnovějšími balíčky NuGet, brání výskytu této chyby.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="dfa7e-122">Nové verze balíčků, včetně Microsoft.AspNet.WebPages lze nyní nainstalovat ve Webmatrixu.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="dfa7e-123">Některé z těchto balíčků byly jako například používání funkcí NuGet [XDT konfigurační transformaci](../release-notes/nuget-2.6.md#xdt), který nebyl podporován ve službě WebMatrix až doteď.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="dfa7e-124">Nula bajtů knihovny DLL ve složce bin</span><span class="sxs-lookup"><span data-stu-id="dfa7e-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="dfa7e-125">Někteří uživatelé nahlásili, která po instalaci NuGet zabalí ve službě WebMatrix, které obsahují knihovny DLL, které se zkopíruje do adresáře bin, který zobrazit knihovny DLL v `bin` složky jako soubory 0 bajtů.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="dfa7e-126">Tím je prolomen aplikace za běhu.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="dfa7e-127">[Tento problém](https://nuget.codeplex.com/workitem/4060) nyní byla opravena.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="dfa7e-128">Další nedávné vylepšení</span><span class="sxs-lookup"><span data-stu-id="dfa7e-128">Other Recent Improvements</span></span>

<span data-ttu-id="dfa7e-129">Pokud pro sadu Visual Studio byla vydána 2.8 Správce balíčků NuGet, jsme také vydali Správce balíčků NuGet 2.5.0 pro službu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="dfa7e-130">Když to jsem už zmínili v [zpráva k vydání verze NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), jsme neměli uvést konkrétní novým funkcím tuto aktualizaci zavedena.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="dfa7e-131">Aktualizovat vše</span><span class="sxs-lookup"><span data-stu-id="dfa7e-131">Update All</span></span>

<span data-ttu-id="dfa7e-132">Teď můžete aktualizovat všechny balíčky webové stránky v jednom kroku.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="dfa7e-133">Při otevření rozšíření NuGet v nástroji WebMatrix zobrazí seznam všech balíčků ve galerii, které máte nainstalované a ty s aktualizacemi, které jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="dfa7e-134">Dříve všech balíčků byste museli možné aktualizovat jednotlivě, ale teď je užitečné tlačítko "Aktualizovat vše", který se zobrazuje na kartě aktualizace.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Klikněte na tlačítko Aktualizovat vše aktualizovat všechny balíčky dostupnými aktualizacemi](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="dfa7e-136">Přepsat existující soubory</span><span class="sxs-lookup"><span data-stu-id="dfa7e-136">Overwrite Existing Files</span></span>

<span data-ttu-id="dfa7e-137">Při instalaci balíčků, které obsahují soubory, které již existují na vašem webu, NuGet má vždy jen tiše ignorováno těchto souborů (existující soubory opuštění samostatně).</span><span class="sxs-lookup"><span data-stu-id="dfa7e-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="dfa7e-138">To může vést k dojem, že balíček byl nainstalovány nebo aktualizovány správně, když ve skutečnosti nebylo.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="dfa7e-139">NuGet teď vyzve pro soubory přepsání.</span><span class="sxs-lookup"><span data-stu-id="dfa7e-139">NuGet will now prompt for files to be overwritten.</span></span>

![Řešení konfliktů souborů](./media/NuGet-2.8/webmatrix-overwrite-file.png)
