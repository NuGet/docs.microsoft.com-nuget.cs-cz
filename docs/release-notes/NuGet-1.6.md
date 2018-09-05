---
title: Zpráva k vydání verzí 1.6 verze NuGet
description: Zpráva k vydání verze pro NuGet 1.6, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549009"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="8d704-103">Zpráva k vydání verzí 1.6 verze NuGet</span><span class="sxs-lookup"><span data-stu-id="8d704-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="8d704-104">[Zpráva k vydání verze NuGet 1.5](../release-notes/nuget-1.5.md) | [zpráva k vydání verze NuGet 1.7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="8d704-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="8d704-105">NuGet 1.6 byla vydána 13. prosince 2011.</span><span class="sxs-lookup"><span data-stu-id="8d704-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="8d704-106">Instalace známý problém</span><span class="sxs-lookup"><span data-stu-id="8d704-106">Known Installation Issue</span></span>
<span data-ttu-id="8d704-107">Pokud spustíte VS 2010 SP1, můžete narazit na chybu instalace při pokusu o upgradu Nugetu, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="8d704-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="8d704-108">Alternativním řešením je jednoduše odinstalovat NuGet a nainstalujte ho z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="8d704-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="8d704-109">Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace.</span><span class="sxs-lookup"><span data-stu-id="8d704-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="8d704-110">Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalovat je vypnutá), pak pravděpodobně nutné restartovat Visual Studio pomocí příkazu "Spustit jako správce."</span><span class="sxs-lookup"><span data-stu-id="8d704-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="8d704-111">Funkce</span><span class="sxs-lookup"><span data-stu-id="8d704-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="8d704-112">Podporu pro Semantic Versioning a předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="8d704-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="8d704-113">NuGet 1.6 zavádí podporu pro Semantic Versioning (SemVer).</span><span class="sxs-lookup"><span data-stu-id="8d704-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="8d704-114">Další informace o tom, jak používá SemVer najdete [dokumentace ke službě správy verzí](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8d704-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="8d704-115">Pomocí nástroje NuGet bez vrácení se změnami balíčky (obnovení balíčku)</span><span class="sxs-lookup"><span data-stu-id="8d704-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="8d704-116">NuGet 1.6 teď nabízí prvotřídní podporu pro pracovní postup, ve které NuGet balíčky nejsou přidány do správy zdrojových kódů, ale místo toho se obnoví v okamžiku sestavení Pokud chybí.</span><span class="sxs-lookup"><span data-stu-id="8d704-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="8d704-117">Další podrobnosti najdete v článku [pomocí NuGet bez potvrzení balíčky do správy zdrojových kódů](../consume-packages/packages-and-source-control.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="8d704-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="8d704-118">Šablony položek, které instalují balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="8d704-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="8d704-119">Staví na práce, která podporují předinstalovaný balíček NuGet do šablony projektů Visual Studio, NuGet 1.6 přidává podporu pro položku šablony sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d704-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="8d704-120">Šablony položek mohou být přidruženy balíčky NuGet, které jsou nainstalovány při vyvolání šablony.</span><span class="sxs-lookup"><span data-stu-id="8d704-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="8d704-121">Další informace o tom, jak změnit šablonu projektu/položky k instalaci balíčků NuGet najdete [balíčky v šablony sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="8d704-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="8d704-122">Podpora pro zakázání zdroje balíčků</span><span class="sxs-lookup"><span data-stu-id="8d704-122">Support for disabling package sources</span></span>
<span data-ttu-id="8d704-123">Po nakonfigurování více zdrojů balíčku NuGet bude vypadat v každém z nich balíčky během instalace balíčku a jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="8d704-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="8d704-124">Zdroj balíčku, který je mimo provoz z nějakého důvodu může vážně pomalé dolů NuGet.</span><span class="sxs-lookup"><span data-stu-id="8d704-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="8d704-125">Před NuGet 1.6 může odebrat zdrojový balíček, ale pak je nutné pamatovat si podrobnosti o kdy budete chtít přidat zpátky v.</span><span class="sxs-lookup"><span data-stu-id="8d704-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="8d704-126">NuGet 1.6 umožňuje zrušením zaškrtnutí zdroj balíčku, který ji zakázat, ale zachovat kolem.</span><span class="sxs-lookup"><span data-stu-id="8d704-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Zakázat balíček](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="8d704-128">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="8d704-128">Bug Fixes</span></span>
<span data-ttu-id="8d704-129">NuGet 1.6 bylo celkem 106 pracovní položky opraveno.</span><span class="sxs-lookup"><span data-stu-id="8d704-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="8d704-130">95 z nich byly klasifikovány jako chyby a 10 z nich byly funkce.</span><span class="sxs-lookup"><span data-stu-id="8d704-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="8d704-131">Úplný seznam pracovních položek opravených NuGet 1.6 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="8d704-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
