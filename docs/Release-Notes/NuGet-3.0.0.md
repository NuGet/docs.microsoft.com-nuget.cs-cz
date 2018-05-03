---
title: Poznámky k verzi 3.0 NuGet
description: Poznámky k verzi pro včetně NuGet 3.0.0 – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="45527-103">Poznámky k verzi 3.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="45527-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="45527-104">[Poznámky k verzi RC2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 poznámky k verzi](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="45527-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="45527-105">NuGet 3.0 byla vydána 20. července 2015 jako sada rozšíření pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="45527-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="45527-106">Jsme nabídnutých k poskytování této verze pomocí sady Visual Studio, takže dokončení aktualizované NuGet 3.0 prostředí budou k dispozici pro nové uživatele v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45527-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="45527-107">Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="45527-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="45527-108">Doporučujeme, abyste tyto vývojáři, kteří mají přístup k sadě Visual Studio Galerie aktualizaci na nejnovější verzi, která je k dispozici, protože jsme publikují aktualizace krátce po vydání sady Visual Studio 2015, který obsahuje podporu pro vývoj pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="45527-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="45527-109">Celkem, jsme uzavřený 240 problémy ve verzi 3.0 a vy můžete zkontrolovat [úplný seznam problémů na Githubu](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="45527-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="45527-110">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="45527-110">Known Issues</span></span>

<span data-ttu-id="45527-111">Došlo k několika známých problémů doručit v této verzi a všechny tyto položky jsou pevné v našem naplánované 3.1 verzi se shoduje s verzí Windows 10 na července 29.</span><span class="sxs-lookup"><span data-stu-id="45527-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="45527-112">Budete moci aktualizovat vaše rozšíření sady Visual Studio z galerie stejné nebo pozdější datum o vyřešení těchto známých problémů.</span><span class="sxs-lookup"><span data-stu-id="45527-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="45527-113">Překlad není k dispozici pro popisek "Nezobrazovat tuto" na okno náhledu a popisku "Autoři" v okně Popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="45527-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="45527-114">Pokud jste práci na projektu pomocí sady TFS ovládací prvek zdroje, NuGet nelze prezentovat Správce balíčků uživatelské rozhraní Pokud souboru Nuget.Config je označena jako jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="45527-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="45527-115">**Alternativní řešení** rezervovat soubor ze sady TFS.</span><span class="sxs-lookup"><span data-stu-id="45527-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="45527-116">Text v žlutý "restartování pruh" v okně NuGet Powershell není viditelný, při použití tmavý motiv sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45527-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="45527-117">**Alternativní řešení** použít motiv světlý Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45527-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="45527-118">Souhrn nejvyšší vyřešení problémů</span><span class="sxs-lookup"><span data-stu-id="45527-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="45527-119">Aktualizace časté sítě volá při aktualizuje okno Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="45527-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="45527-120">Odložené scroll při zobrazení změna na instalaci v Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="45527-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="45527-121">Volání sítě by měl být spouštěn na vlákna na pozadí</span><span class="sxs-lookup"><span data-stu-id="45527-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="45527-122">Přidat zaškrtávací políčko "Nezobrazovat okno náhledu.</span><span class="sxs-lookup"><span data-stu-id="45527-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="45527-123">Omezení ke snížení využití procesoru přidané procesů</span><span class="sxs-lookup"><span data-stu-id="45527-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="45527-124">Vylepšené zpracování reference knihovny tříd portable</span><span class="sxs-lookup"><span data-stu-id="45527-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="45527-125">Služba pro automatické dokončování se malá a velká písmena</span><span class="sxs-lookup"><span data-stu-id="45527-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="45527-126">Aktualizace znovu zavést pověření základního ověřování</span><span class="sxs-lookup"><span data-stu-id="45527-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="45527-127">Chyba vylepšené protokolování</span><span class="sxs-lookup"><span data-stu-id="45527-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="45527-128">Vylepšené prostředí powershell chybové zprávy při volání metody balíčku aktualizace</span><span class="sxs-lookup"><span data-stu-id="45527-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="45527-129">Pevný odkaz "Další informace o možnostech, aby se zabránilo chybám ve Windows 10</span><span class="sxs-lookup"><span data-stu-id="45527-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="45527-130">Mějte na paměti, nastavení předběžné verze zaškrtávací políčko</span><span class="sxs-lookup"><span data-stu-id="45527-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="45527-131">Vylepšené shromáždění výkonu pomocí ukládání do mezipaměti výsledky napříč projekty v řešení</span><span class="sxs-lookup"><span data-stu-id="45527-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="45527-132">Paralelní se dají shromáždit více balíčků.</span><span class="sxs-lookup"><span data-stu-id="45527-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="45527-133">Odebrat install-package-force příkaz</span><span class="sxs-lookup"><span data-stu-id="45527-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="45527-134">Prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a oznámení jako jsme Příprava poskytovat podporu pro vývoj pro Windows 10.</span><span class="sxs-lookup"><span data-stu-id="45527-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>