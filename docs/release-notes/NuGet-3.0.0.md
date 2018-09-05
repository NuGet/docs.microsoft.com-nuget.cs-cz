---
title: Poznámky k verzi 3.0 NuGet
description: Zpráva k vydání verze pro NuGet 3.0.0 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551860"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="6d720-103">Poznámky k verzi 3.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="6d720-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="6d720-104">[Zpráva k vydání verze NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [zpráva k vydání verze NuGet 3.1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="6d720-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="6d720-105">20. července 2015 byla vydána NuGet 3.0 jako rozšíření sady Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6d720-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="6d720-106">Můžeme nabídnout poskytovat této vydané verzi sady Visual Studio tak, aby kompletní aktualizované prostředí NuGet 3.0 by být k dispozici pro nové uživatele služby Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d720-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="6d720-107">Tato verze rozšíření NuGet dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6d720-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="6d720-108">Doporučujeme, abyste tyto vývojáře, kteří mají přístup ke službě update Galerie sady Visual Studio na nejnovější verzi, která je k dispozici, protože aktualizace publikujeme krátce po vydání sady Visual Studio 2015, která obsahuje podporu pro vývoj pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6d720-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="6d720-109">Celkem, jsme uzavřeli 240 problémech ve verzi 3.0 a můžete zkontrolovat [úplný seznam všech problémů na Githubu](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="6d720-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="6d720-110">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="6d720-110">Known Issues</span></span>

<span data-ttu-id="6d720-111">Došlo k několika problémech doručit v této vydané verzi a všechny tyto položky jsou opravené v našich plánovaných verzi 3.1 se shoduje s verzí Windows 10 na 29. července.</span><span class="sxs-lookup"><span data-stu-id="6d720-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="6d720-112">Budete moct aktualizovat vaše rozšíření sady Visual Studio z Galerie nebo po tomto datu k řešení těchto známých problémů.</span><span class="sxs-lookup"><span data-stu-id="6d720-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="6d720-113">Překlad není k dispozici pro "není tuto zprávu nezobrazovat" popisek v okně verze preview a "Autoři" popisek v okně Popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="6d720-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="6d720-114">Když pracujete na projektu pomocí TFS ovládací prvek zdroje, NuGet nelze prezentovat Správce balíčků uživatelské rozhraní je-li soubor Nuget.Config je označena jako jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="6d720-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="6d720-115">**Alternativní řešení** rezervovat soubor ze serveru TFS.</span><span class="sxs-lookup"><span data-stu-id="6d720-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="6d720-116">Text žlutě "restartování bar", v okně Powershellu NuGet není viditelný, při použití tmavého motivu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d720-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="6d720-117">**Alternativní řešení** pomocí sady Visual Studio světlý motiv.</span><span class="sxs-lookup"><span data-stu-id="6d720-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="6d720-118">Přehled hlavních problémů vyřešit</span><span class="sxs-lookup"><span data-stu-id="6d720-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="6d720-119">Sítě časté aktualizace se volá, když se aktualizuje okno Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="6d720-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="6d720-120">Zpožděné posuvníku při změně na instalaci zobrazení ve správci balíčků</span><span class="sxs-lookup"><span data-stu-id="6d720-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="6d720-121">Volání sítě by měl běžet na vlákně na pozadí</span><span class="sxs-lookup"><span data-stu-id="6d720-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="6d720-122">Přidá zaškrtávací políčko "Nezobrazovat okno náhledu.</span><span class="sxs-lookup"><span data-stu-id="6d720-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="6d720-123">Přidání procesu omezování ke snížení využití procesoru</span><span class="sxs-lookup"><span data-stu-id="6d720-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="6d720-124">Vylepšené zpracování odkaz na přenosné knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="6d720-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="6d720-125">Automatické dokončování službě se malá a velká písmena</span><span class="sxs-lookup"><span data-stu-id="6d720-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="6d720-126">Aktualizace znovu zavést pověření základního ověřování</span><span class="sxs-lookup"><span data-stu-id="6d720-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="6d720-127">Vylepšené chybové protokolování</span><span class="sxs-lookup"><span data-stu-id="6d720-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="6d720-128">Vylepšené prostředí powershell chybových zpráv při volání metody Update-Package</span><span class="sxs-lookup"><span data-stu-id="6d720-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="6d720-129">Oprava propojení, kde se dozvíte o možnostech' aby se zabránilo selhání ve Windows 10</span><span class="sxs-lookup"><span data-stu-id="6d720-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="6d720-130">Mějte na paměti nastavení zaškrtávacího políčka předběžné verze</span><span class="sxs-lookup"><span data-stu-id="6d720-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="6d720-131">Vylepšené shromažďování výkonu díky ukládání do mezipaměti výsledky ve všech projektech v řešení</span><span class="sxs-lookup"><span data-stu-id="6d720-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="6d720-132">Současně se dají shromáždit víc balíčků.</span><span class="sxs-lookup"><span data-stu-id="6d720-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="6d720-133">Odebrat install-package-force příkaz</span><span class="sxs-lookup"><span data-stu-id="6d720-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="6d720-134">Prosím dohlížet na [náš blog o](http://blog.nuget.org) další průběh a oznámení podle Připravíme k poskytování podpory pro vývoj pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6d720-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>