---
title: "Poznámky k verzi NuGet 1.6 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.6 NuGet."
keywords: "NuGet 1.6 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="1218a-104">Poznámky k verzi 1.6 verzi NuGet</span><span class="sxs-lookup"><span data-stu-id="1218a-104">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="1218a-105">[Poznámky k verzi NuGet 1.5](../release-notes/nuget-1.5.md) | [NuGet 1.7 poznámky k verzi](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="1218a-105">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="1218a-106">NuGet 1.6 byla vydána 13 prosince 2011.</span><span class="sxs-lookup"><span data-stu-id="1218a-106">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="1218a-107">Instalace známý problém</span><span class="sxs-lookup"><span data-stu-id="1218a-107">Known Installation Issue</span></span>
<span data-ttu-id="1218a-108">Pokud používáte VS 2010 SP1, můžete spustit došlo k chybě instalace při pokusu o upgrade NuGet, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="1218a-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="1218a-109">Alternativní řešení je jednoduše odinstalovat NuGet a nainstalujte ji z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="1218a-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="1218a-110">V tématu [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Další informace.</span><span class="sxs-lookup"><span data-stu-id="1218a-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="1218a-111">Poznámka: Pokud Visual Studio nebude možné odinstalovat rozšíření (k dispozici tlačítko Odinstalovat), bude pravděpodobně nutné restartujte Visual Studio pomocí "Spustit jako správce."</span><span class="sxs-lookup"><span data-stu-id="1218a-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="1218a-112">Funkce</span><span class="sxs-lookup"><span data-stu-id="1218a-112">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="1218a-113">Podpora pro sémantické verze a předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="1218a-113">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="1218a-114">NuGet 1.6 zavádí podporu pro sémantické verze (SemVer).</span><span class="sxs-lookup"><span data-stu-id="1218a-114">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="1218a-115">Další informace o tom, jak ji používá SemVer, přečtěte si [Správa verzí dokumentace](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="1218a-115">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="1218a-116">Pomocí nástroje NuGet bez kontroly v balíčcích (obnovení balíčku)</span><span class="sxs-lookup"><span data-stu-id="1218a-116">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="1218a-117">NuGet 1.6 teď nabízí prvotřídní podporu pro pracovní postup v který NuGet balíčky nejsou přidány do správy zdrojového kódu, ale místo toho jsou obnoveny v čase vytvoření buildu Pokud chybí.</span><span class="sxs-lookup"><span data-stu-id="1218a-117">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="1218a-118">Další informace najdete [pomocí NuGet bez potvrzení balíčky do správy zdrojového kódu](../consume-packages/packages-and-source-control.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="1218a-118">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="1218a-119">Šablony položek, které instalace balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="1218a-119">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="1218a-120">Sestavování na práci pro podporu předinstalované balíček NuGet do projektu šablony sady Visual Studio, NuGet 1.6 přidává podporu pro šablony sady Visual Studio položky.</span><span class="sxs-lookup"><span data-stu-id="1218a-120">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="1218a-121">Šablony položek může mít přidružené balíčky NuGet, které jsou nainstalovány při vyvolání šablony.</span><span class="sxs-lookup"><span data-stu-id="1218a-121">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="1218a-122">Další informace o tom, jak změnit šablonu projektu/položky instalace balíčků NuGet najdete [balíčky v šablony sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="1218a-122">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="1218a-123">Podpora pro zakázání zdroje balíčků</span><span class="sxs-lookup"><span data-stu-id="1218a-123">Support for disabling package sources</span></span>
<span data-ttu-id="1218a-124">Po nakonfigurování více zdrojů balíčku NuGet Hledat v každé z nich pro balíčky během instalace balíček a jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="1218a-124">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="1218a-125">Zdroj balíčku, která je mimo provoz z nějakého důvodu může vážně pomalu dolů NuGet.</span><span class="sxs-lookup"><span data-stu-id="1218a-125">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="1218a-126">Před NuGet 1.6 by mohl odebrat zdroje balíčku, ale pak je nutné pamatovat na to, podrobnosti o když chcete přidat ji zpátky.</span><span class="sxs-lookup"><span data-stu-id="1218a-126">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="1218a-127">NuGet 1.6 umožňuje zdroj balíčku, který ji zakázat, ale je udržovat kolem zaškrtnutí políčka.</span><span class="sxs-lookup"><span data-stu-id="1218a-127">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Zakázání balíčku](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="1218a-129">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="1218a-129">Bug Fixes</span></span>
<span data-ttu-id="1218a-130">NuGet 1.6 měl celkem 106 pracovní položky, které jsou pevné.</span><span class="sxs-lookup"><span data-stu-id="1218a-130">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="1218a-131">95 těchto byly klasifikovány jako chyby a 10 těchto byly funkce.</span><span class="sxs-lookup"><span data-stu-id="1218a-131">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="1218a-132">Úplný seznam pracovní položky pevná ve NuGet 1.6 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="1218a-132">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
