---
title: Zpráva k vydání verze NuGet 1,7
description: Poznámky k verzi pro NuGet 1,7, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777061"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="a6eaf-103">Zpráva k vydání verze NuGet 1,7</span><span class="sxs-lookup"><span data-stu-id="a6eaf-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="a6eaf-104">Zpráva k [vydání verze](../release-notes/nuget-1.6.md)  |  NuGet 1,6 Zpráva k [vydání verze NuGet 1,8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="a6eaf-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="a6eaf-105">NuGet 1,7 byl vydán 4. dubna 2012.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="a6eaf-106">Známý problém s instalací</span><span class="sxs-lookup"><span data-stu-id="a6eaf-106">Known Installation Issue</span></span>
<span data-ttu-id="a6eaf-107">Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, spustit chybu instalace.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="a6eaf-108">Alternativním řešením je jednoduše odinstalovat NuGet a pak ji nainstalovat z galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="a6eaf-109">Další informace naleznete v tématu <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="a6eaf-110">Poznámka: Pokud Visual Studio neumožní odinstalovat rozšíření (tlačítko Odinstalace je zakázané), pak budete pravděpodobně muset restartovat Visual Studio pomocí možnosti Spustit jako správce.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="a6eaf-111">Funkce</span><span class="sxs-lookup"><span data-stu-id="a6eaf-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="a6eaf-112">Podpora otevírání souboru readme.txt po instalaci</span><span class="sxs-lookup"><span data-stu-id="a6eaf-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="a6eaf-113">Novinka v 1,7, pokud balíček obsahuje `readme.txt` soubor v kořenu balíčku, NuGet po dokončení instalace balíčku automaticky otevře tento soubor.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="a6eaf-114">Zobrazit předběžné verze balíčků v dialogovém okně Spravovat balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="a6eaf-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="a6eaf-115">Dialog spravovat balíčky NuGet teď obsahuje rozevírací seznam, který nabízí možnost zobrazovat předběžné verze balíčků.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Zobrazení předprodejních balíčků](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="a6eaf-117">Po chybějících souborech balíčku zobrazit tlačítko pro obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="a6eaf-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="a6eaf-118">Když otevřete dialogové okno konzoly Správce balíčků nebo správce balíčků NuGet, nástroj NuGet zkontroluje, jestli aktuální řešení nemá povolený režim obnovení balíčku, a jestli ve složce chybí nějaké soubory balíčku `packages` .</span><span class="sxs-lookup"><span data-stu-id="a6eaf-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="a6eaf-119">Pokud jsou splněné tyto dvě podmínky, NuGet vás upozorní a zobrazí pohodlné tlačítko obnovení.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="a6eaf-120">Po kliknutí na toto tlačítko se spustí NuGet pro obnovení všech chybějících balíčků.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Tlačítko pro obnovení balíčku v dialogovém okně](./media/packagerestore-dialog.png)

![Tlačítko pro obnovení balíčku v konzole](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="a6eaf-123">Přidat soubor packages.config na úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="a6eaf-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="a6eaf-124">V předchozích verzích NuGet má každý projekt `packages.config` soubor, který uchovává přehled o tom, jaké balíčky NuGet jsou v projektu nainstalované.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="a6eaf-125">Na úrovni řešení ale neexistuje žádný podobný soubor, aby bylo možné sledovat balíčky na úrovni řešení.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="a6eaf-126">V důsledku toho neexistuje žádný způsob, jak obnovit balíčky na úrovni řešení.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="a6eaf-127">Tato funkce je nyní implementována v NuGet 1,7.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="a6eaf-128">Soubor na úrovni řešení `packages.config` je umístěn pod `.nuget` složkou v části kořen řešení a bude ukládat pouze balíčky na úrovni řešení.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="a6eaf-129">Příkaz Remove New-Package</span><span class="sxs-lookup"><span data-stu-id="a6eaf-129">Remove New-Package command</span></span>
<span data-ttu-id="a6eaf-130">Z důvodu nízkého využití se odebral příkaz New-Package.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="a6eaf-131">Pro vytváření balíčků doporučujeme vývojářům použít nuget.exe nebo praktického Průzkumníka balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a6eaf-132">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="a6eaf-132">Bug Fixes</span></span>
<span data-ttu-id="a6eaf-133">Sada NuGet 1,7 opravila mnoho chyb kolem pracovního postupu obnovení balíčku a scénářů správy sítě a zdrojů.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="a6eaf-134">Úplný seznam pracovních položek opravených v NuGet 1,7 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a6eaf-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
