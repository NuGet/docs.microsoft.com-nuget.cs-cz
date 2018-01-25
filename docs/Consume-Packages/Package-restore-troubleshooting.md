---
title: "Řešení potíží s balíček NuGet obnovit v sadě Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Popis běžné NuGet obnovit chyby v sadě Visual Studio a řešení potíží s nimi."
keywords: "Řešení potíží s obnovení balíčku NuGet, obnovení balíčků, řešení potíží"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 374e385ecd9b9bcd71b1c61914ea03a072a5f182
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="60413-104">Řešení potíží s chybami obnovení balíčku v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="60413-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="60413-105">Tato stránka se zaměřuje na běžné chyby při obnovování balíčků v sadě Visual Studio a kroky k jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="60413-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="60413-106">Pro postup obnovení balíčků, najdete v části [obnovení balíčků](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="60413-106">For how-to restore packages, see [Package restore](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="60413-107">Ve výchozím nastavení sestavení projektu v sadě Visual Studio automaticky obnoví balíčky NuGet, kterou se odkazuje v projektu.</span><span class="sxs-lookup"><span data-stu-id="60413-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="60413-108">Ale sestavení selže, pokud se obnovení balíčku je zakázána v **nástroje > Možnosti > Správce balíčků NuGet > Obnovení balíčků** nastavení a potřebné balíčky nejsou k dispozici ve vašem počítači.</span><span class="sxs-lookup"><span data-stu-id="60413-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="60413-109">V těchto případech se může zobrazit následující chyby:</span><span class="sxs-lookup"><span data-stu-id="60413-109">In these cases you may see the following errors:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="60413-110">Pokud chcete povolit obnovení balíčků, otevřete **nástroje > Možnosti > Správce balíčků NuGet** a vyberte požadované možnosti pro **umožnit správci balíčků NuGet stáhnout chybějící balíčky** a **automaticky, zda nechybí balíčků během sestavení v sadě Visual Studio**:</span><span class="sxs-lookup"><span data-stu-id="60413-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![Povolit obnovení balíčků NuGet v Nástroje/možnosti](../Consume-Packages/media/restore-01-autorestoreoptions.png)
