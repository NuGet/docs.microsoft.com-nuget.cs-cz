---
title: Poznámky k verzi 1.7 NuGet
description: Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.7 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="06f5b-103">Poznámky k verzi 1.7 NuGet</span><span class="sxs-lookup"><span data-stu-id="06f5b-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="06f5b-104">[Poznámky k verzi NuGet 1.6](../release-notes/nuget-1.6.md) | [NuGet 1.8 poznámky k verzi](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="06f5b-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="06f5b-105">NuGet 1.7 byla vydána 4. dubna 2012.</span><span class="sxs-lookup"><span data-stu-id="06f5b-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="06f5b-106">Instalace známý problém</span><span class="sxs-lookup"><span data-stu-id="06f5b-106">Known Installation Issue</span></span>
<span data-ttu-id="06f5b-107">Pokud používáte VS 2010 SP1, můžete spustit došlo k chybě instalace při pokusu o upgrade NuGet, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="06f5b-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="06f5b-108">Alternativní řešení je jednoduše odinstalovat NuGet a nainstalujte ji z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="06f5b-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="06f5b-109">V tématu [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace.</span><span class="sxs-lookup"><span data-stu-id="06f5b-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="06f5b-110">Poznámka: Pokud Visual Studio nebude možné odinstalovat rozšíření (k dispozici tlačítko Odinstalovat), bude pravděpodobně nutné restartujte Visual Studio pomocí "Spustit jako správce."</span><span class="sxs-lookup"><span data-stu-id="06f5b-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="06f5b-111">Funkce</span><span class="sxs-lookup"><span data-stu-id="06f5b-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="06f5b-112">Podporuje otevření souboru readme.txt po instalaci</span><span class="sxs-lookup"><span data-stu-id="06f5b-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="06f5b-113">Novinka v 1.7, pokud obsahuje váš balíček `readme.txt` soubor v kořenovém adresáři balíčku NuGet se automaticky otevře tento soubor po dokončení instalace vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="06f5b-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="06f5b-114">Zobrazit v dialogovém okně Spravovat balíčky NuGet balíčky předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="06f5b-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="06f5b-115">Dialogové okno Spravovat balíčky NuGet nyní zahrnuje rozevírací nabídce, která poskytuje možnost zobrazit předběžné verze balíčků.</span><span class="sxs-lookup"><span data-stu-id="06f5b-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Zobrazuje předběžné verze balíčků](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="06f5b-117">Obnovení balíčků tlačítko zobrazit, když jsou soubory balíčku chybí</span><span class="sxs-lookup"><span data-stu-id="06f5b-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="06f5b-118">Pokud otevřete konzolu Správce balíčků nebo NuGet Správce balíčků dialogové okno, zkontrolujte Pokud současné řešení má povolen režim obnovení balíčků NuGet a v případě, že všechny soubory v balíčku chybí `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="06f5b-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="06f5b-119">Pokud jsou tyto dvě podmínky splněny, NuGet vás upozorní a zobrazí pohodlný tlačítko obnovení.</span><span class="sxs-lookup"><span data-stu-id="06f5b-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="06f5b-120">Kliknutím na toto tlačítko spustí NuGet obnovit všechny chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="06f5b-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Tlačítko Obnovit balíček v dialogovém okně](./media/packagerestore-dialog.png)

![Tlačítko Obnovit balíčku v konzole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="06f5b-123">Přidejte soubor packages.config úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="06f5b-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="06f5b-124">V předchozích verzích NuGet, každý projekt má `packages.config` souboru, který uchovává informace o jaké balíčky NuGet jsou nainstalované v tomto projektu.</span><span class="sxs-lookup"><span data-stu-id="06f5b-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="06f5b-125">Na úrovni řešení ke sledování řešení úrovni balíčky se však žádný podobně jako soubor.</span><span class="sxs-lookup"><span data-stu-id="06f5b-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="06f5b-126">V důsledku toho se žádný způsob, jak obnovení balíčků řešení úrovni.</span><span class="sxs-lookup"><span data-stu-id="06f5b-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="06f5b-127">Tato funkce se teď implementuje v NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="06f5b-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="06f5b-128">Úroveň řešení `packages.config` soubor je umístěn v `.nuget` ve složce řešení kořenový uživatel a uloží pouze řešení na úrovni balíčků.</span><span class="sxs-lookup"><span data-stu-id="06f5b-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="06f5b-129">Odeberte příkaz nového balíčku</span><span class="sxs-lookup"><span data-stu-id="06f5b-129">Remove New-Package command</span></span>
<span data-ttu-id="06f5b-130">Z důvodu nízkém zatížení byla odebrána příkaz nový balíček.</span><span class="sxs-lookup"><span data-stu-id="06f5b-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="06f5b-131">Vývojáři se doporučuje použít k vytvoření balíčků nuget.exe nebo užitečný Průzkumníka balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="06f5b-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="06f5b-132">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="06f5b-132">Bug Fixes</span></span>
<span data-ttu-id="06f5b-133">NuGet 1.7 má vyřešili mnoho chyb kolem scénáře sítě nebo zdrojového kódu a pracovní postup obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="06f5b-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="06f5b-134">Úplný seznam pracovní položky pevná ve NuGet 1.7 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="06f5b-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
