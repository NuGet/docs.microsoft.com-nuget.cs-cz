---
title: Poznámky k verzi 1.7 NuGet
description: Zpráva k vydání verze pro NuGet 1.7, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551464"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="ce4f0-103">Poznámky k verzi 1.7 NuGet</span><span class="sxs-lookup"><span data-stu-id="ce4f0-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="ce4f0-104">[Zpráva k vydání verze NuGet 1.6](../release-notes/nuget-1.6.md) | [zpráva k vydání verze NuGet 1.8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="ce4f0-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="ce4f0-105">NuGet 1.7 byla vydána 4. dubna 2012.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ce4f0-106">Instalace známý problém</span><span class="sxs-lookup"><span data-stu-id="ce4f0-106">Known Installation Issue</span></span>
<span data-ttu-id="ce4f0-107">Pokud spustíte VS 2010 SP1, můžete narazit na chybu instalace při pokusu o upgradu Nugetu, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ce4f0-108">Alternativním řešením je jednoduše odinstalovat NuGet a nainstalujte ho z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ce4f0-109">Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="ce4f0-110">Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalovat je vypnutá), pak pravděpodobně nutné restartovat Visual Studio pomocí příkazu "Spustit jako správce."</span><span class="sxs-lookup"><span data-stu-id="ce4f0-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="ce4f0-111">Funkce</span><span class="sxs-lookup"><span data-stu-id="ce4f0-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="ce4f0-112">Podpora otevírání souboru readme.txt po instalaci</span><span class="sxs-lookup"><span data-stu-id="ce4f0-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="ce4f0-113">Novinka v 1.7, pokud balíček obsahuje `readme.txt` souboru v kořenovém adresáři balíčku NuGet se automaticky otevře tento soubor po dokončení instalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="ce4f0-114">Zobrazit v dialogovém okně Spravovat balíčky NuGet balíčky předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="ce4f0-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="ce4f0-115">Dialogové okno Spravovat balíčky NuGet nyní obsahuje rozevírací seznam, který poskytuje možnost zobrazit předběžné verze balíčků.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Zobrazuje předběžné verze balíčků](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="ce4f0-117">Zobrazit tlačítko pro obnovení balíčků, když nebyly nalezeny soubory balíčku</span><span class="sxs-lookup"><span data-stu-id="ce4f0-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="ce4f0-118">Pokud otevřete konzolu Správce balíčků nebo balíčky NuGet správce dialogového okna, NuGet zkontroluje, pokud se aktuální řešení má povolený režim obnovení balíčků a v případě, že všechny soubory v balíčku chybí `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="ce4f0-119">Pokud tyto dvě podmínky jsou splněny, NuGet vás upozorní a zobrazí pohodlný tlačítko Obnovit.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="ce4f0-120">Kliknutím na toto tlačítko spustí obnovit všechny chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Tlačítko Obnovit balíček v dialogovém okně](./media/packagerestore-dialog.png)

![Tlačítko Obnovit balíček v konzole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="ce4f0-123">Přidat soubor packages.config úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="ce4f0-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="ce4f0-124">V předchozích verzích balíčku nuget, má každý projekt `packages.config` souboru, který uchovává informace o jaké balíčky NuGet jsou nainstalované v daném projektu.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="ce4f0-125">Na úrovni řešení k udržení přehledu o balíčcích úrovni řešení byla však žádný podobně jako soubor.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="ce4f0-126">V důsledku toho neexistoval způsob, jak k obnovení balíčků úrovni řešení.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="ce4f0-127">Tato funkce je nyní implementována v NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="ce4f0-128">Úroveň řešení `packages.config` soubor umístěn v rámci `.nuget` ve složce řešení kořenové a budou ukládat balíčky pouze úrovni řešení.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="ce4f0-129">Odebrat příkaz New-Package</span><span class="sxs-lookup"><span data-stu-id="ce4f0-129">Remove New-Package command</span></span>
<span data-ttu-id="ce4f0-130">Z důvodu s nízkým využitím byl odebrán příkazu New-Package.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="ce4f0-131">Vývojáři se doporučuje použít k vytváření balíčků nuget.exe nebo po ruce Průzkumníku balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ce4f0-132">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="ce4f0-132">Bug Fixes</span></span>
<span data-ttu-id="ce4f0-133">NuGet 1.7 chyba opravena řada chyb kolem pracovního postupu obnovení balíčků a scénáře řízení síťového nebo zdroje.</span><span class="sxs-lookup"><span data-stu-id="ce4f0-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="ce4f0-134">Úplný seznam pracovních položek opravených NuGet 1.7 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="ce4f0-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
