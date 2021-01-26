---
title: Zpráva k vydání verze NuGet 1,6
description: Poznámky k verzi pro NuGet 1,6, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777021"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="b26b0-103">Zpráva k vydání verze NuGet 1,6</span><span class="sxs-lookup"><span data-stu-id="b26b0-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="b26b0-104">Zpráva k [vydání verze](../release-notes/nuget-1.5.md)  |  NuGet 1,5 Zpráva k [vydání verze NuGet 1,7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="b26b0-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="b26b0-105">NuGet 1,6 byl vydán 13. prosince 2011.</span><span class="sxs-lookup"><span data-stu-id="b26b0-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="b26b0-106">Známý problém s instalací</span><span class="sxs-lookup"><span data-stu-id="b26b0-106">Known Installation Issue</span></span>
<span data-ttu-id="b26b0-107">Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, spustit chybu instalace.</span><span class="sxs-lookup"><span data-stu-id="b26b0-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="b26b0-108">Alternativním řešením je jednoduše odinstalovat NuGet a pak ji nainstalovat z galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="b26b0-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="b26b0-109">Další informace naleznete v tématu <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="b26b0-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="b26b0-110">Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalace je zakázané), pak budete pravděpodobně muset restartovat Visual Studio pomocí možnosti Spustit jako správce.</span><span class="sxs-lookup"><span data-stu-id="b26b0-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="b26b0-111">Funkce</span><span class="sxs-lookup"><span data-stu-id="b26b0-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="b26b0-112">Podpora sémantických verzí a předprodejních balíčků</span><span class="sxs-lookup"><span data-stu-id="b26b0-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="b26b0-113">NuGet 1,6 zavádí podporu pro sémantickou správu verzí (SemVer).</span><span class="sxs-lookup"><span data-stu-id="b26b0-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="b26b0-114">Další podrobnosti o tom, jak používá SemVer, najdete v [dokumentaci ke správám verzí](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b26b0-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="b26b0-115">Použití NuGet bez vrácení se změnami balíčků (obnovení balíčku)</span><span class="sxs-lookup"><span data-stu-id="b26b0-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="b26b0-116">NuGet 1,6 teď má jako první podporu pro pracovní postup, ve kterém se balíčky NuGet nepřidaly do správy zdrojových kódů, ale v době, kdy chybí, se místo toho obnoví v čase sestavení.</span><span class="sxs-lookup"><span data-stu-id="b26b0-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="b26b0-117">Pokud chcete získat další informace, přečtěte si téma [použití NuGet bez potvrzení balíčků do správy zdrojového kódu](../consume-packages/packages-and-source-control.md) .</span><span class="sxs-lookup"><span data-stu-id="b26b0-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="b26b0-118">Šablony položek, které instalují balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="b26b0-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="b26b0-119">Sada NuGet 1,6 také přidává podporu šablon položek sady Visual Studio, která je postavena na práci pro podporu předinstalovaného balíčku NuGet do šablon projektů sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b26b0-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="b26b0-120">K šablonám položek můžou být přidružené balíčky NuGet, které se nainstalují při vyvolání šablony.</span><span class="sxs-lookup"><span data-stu-id="b26b0-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="b26b0-121">Další informace o tom, jak změnit šablonu projektu nebo položky pro instalaci balíčků NuGet, najdete v tématu [balíčky v tématu šablony sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="b26b0-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="b26b0-122">Podpora pro zakázání zdrojů balíčků</span><span class="sxs-lookup"><span data-stu-id="b26b0-122">Support for disabling package sources</span></span>
<span data-ttu-id="b26b0-123">Pokud je nakonfigurováno více zdrojů balíčků, bude NuGet při instalaci balíčku a jeho závislostech Hledat v každém z nich pro balíčky.</span><span class="sxs-lookup"><span data-stu-id="b26b0-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="b26b0-124">Zdroj balíčku, který je mimo provoz z nějakého důvodu, může vážně zpomalit NuGet.</span><span class="sxs-lookup"><span data-stu-id="b26b0-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="b26b0-125">Před verzí NuGet 1,6 byste mohli odebrat zdroj balíčku, ale pak si musíte pamatovat podrobnosti o tom, kdy ho chcete přidat zpátky do.</span><span class="sxs-lookup"><span data-stu-id="b26b0-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="b26b0-126">NuGet 1,6 umožňuje zrušit kontrolu zdroje balíčku, abyste ho zakázali, ale zachovali si ho.</span><span class="sxs-lookup"><span data-stu-id="b26b0-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Zakázání balíčku](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="b26b0-128">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="b26b0-128">Bug Fixes</span></span>
<span data-ttu-id="b26b0-129">Aktualizace NuGet 1,6 obsahovala celkem 106 pracovních položek.</span><span class="sxs-lookup"><span data-stu-id="b26b0-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="b26b0-130">95 z nich bylo klasifikováno jako chyby a 10 z nich bylo funkcí.</span><span class="sxs-lookup"><span data-stu-id="b26b0-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="b26b0-131">Úplný seznam pracovních položek opravených v NuGet 1,6 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b26b0-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
