---
title: Zpráva k vydání verze NuGet 3,0
description: Poznámky k verzi pro NuGet 3.0.0, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776548"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="37e70-103">Zpráva k vydání verze NuGet 3,0</span><span class="sxs-lookup"><span data-stu-id="37e70-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="37e70-104">Poznámky k verzi [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  Zpráva k [vydání verze NuGet 3,1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="37e70-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="37e70-105">Sada NuGet 3,0 byla vydána 20. července 2015 jako rozšíření sady Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="37e70-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="37e70-106">Vložili jsme tuto verzi do sady Visual Studio, aby byly k dispozici kompletní aktualizované prostředí NuGet 3,0 pro nové uživatele sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37e70-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="37e70-107">Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="37e70-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="37e70-108">Doporučujeme vývojářům, kteří mají přístup k aktualizaci galerie sady Visual Studio, k nejnovější verzi, která je k dispozici, protože publikujeme krátce po vydání sady Visual Studio 2015, které obsahuje podporu pro vývoj pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="37e70-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="37e70-109">V Total jsme uzavřeli 240 problémů ve verzi 3,0 a můžete si prohlédnout [úplný seznam problémů na GitHubu](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="37e70-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="37e70-110">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="37e70-110">Known Issues</span></span>

<span data-ttu-id="37e70-111">V této verzi se dostalo několik známých problémů. všechny tyto položky jsou opravené v naší plánované verzi 3,1, aby se shodovaly s vydáním Windows 10 v červenci vysílání 29..</span><span class="sxs-lookup"><span data-stu-id="37e70-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="37e70-112">Můžete aktualizovat rozšíření aplikace Visual Studio z Galerie od tohoto data a opravit tyto známé problémy.</span><span class="sxs-lookup"><span data-stu-id="37e70-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="37e70-113">Pro popisek "Nezobrazovat znovu" v okně náhledu a v popisku "autoři" v okně Popis balíčku není překlad k dispozici.</span><span class="sxs-lookup"><span data-stu-id="37e70-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="37e70-114">Při práci na projektu pomocí správy zdrojového kódu TFS nemůže NuGet prezentovat uživatelské rozhraní Správce balíčků, pokud je soubor Nuget.Config označený jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="37e70-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="37e70-115">**Alternativní řešení** Rezervujte soubor z TFS.</span><span class="sxs-lookup"><span data-stu-id="37e70-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="37e70-116">Když použijete tmavý motiv sady Visual Studio, text ve žlutém "pravém panelu" v okně PowerShellu NuGet se nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="37e70-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="37e70-117">**Alternativní řešení** Použijte světlý motiv sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37e70-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="37e70-118">Shrnutí nejdůležitějších vyřešených problémů</span><span class="sxs-lookup"><span data-stu-id="37e70-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="37e70-119">Častá volání síťové aktualizace po aktualizaci okna Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="37e70-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="37e70-120">Zpožděný posun při změně na nainstalované zobrazení ve Správci balíčků</span><span class="sxs-lookup"><span data-stu-id="37e70-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="37e70-121">Síťová volání by se měla spustit ve vlákně na pozadí.</span><span class="sxs-lookup"><span data-stu-id="37e70-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="37e70-122">Přidáno zaškrtávací políčko nezobrazit Náhled okna</span><span class="sxs-lookup"><span data-stu-id="37e70-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="37e70-123">Přidání omezení procesů pro snížení využití procesoru</span><span class="sxs-lookup"><span data-stu-id="37e70-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="37e70-124">Vylepšené zpracování odkazů na přenositelné knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="37e70-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="37e70-125">Služba automatického dokončování rozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="37e70-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="37e70-126">Aktualizace pro znovu zavedení přihlašovacích údajů základního ověřování</span><span class="sxs-lookup"><span data-stu-id="37e70-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="37e70-127">Vylepšené protokolování chyb</span><span class="sxs-lookup"><span data-stu-id="37e70-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="37e70-128">Vylepšené chybové zprávy PowerShellu při volání rutiny Update-Package</span><span class="sxs-lookup"><span data-stu-id="37e70-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="37e70-129">Opravte odkaz "informace o možnostech", aby se zabránilo chybám ve Windows 10</span><span class="sxs-lookup"><span data-stu-id="37e70-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="37e70-130">Zapamatovat si nastavení zaškrtávacího políčka předběžného vydání</span><span class="sxs-lookup"><span data-stu-id="37e70-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="37e70-131">Lepší výkon při shromažďování díky ukládání výsledků do mezipaměti napříč projekty v řešení</span><span class="sxs-lookup"><span data-stu-id="37e70-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="37e70-132">Paralelní shromažďování více balíčků</span><span class="sxs-lookup"><span data-stu-id="37e70-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="37e70-133">Odebraný příkaz Install-Package-Force</span><span class="sxs-lookup"><span data-stu-id="37e70-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="37e70-134">Pořiďte si prosím svůj [blog na našem blogu](http://blog.nuget.org) a získejte další informace o průběhu a oznámeních, jak jsme připraveni doručovat podporu pro vývoj pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="37e70-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>