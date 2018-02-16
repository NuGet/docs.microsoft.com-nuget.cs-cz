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
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Řešení potíží s chybami obnovení balíčku v sadě Visual Studio

> [!Note]
> Tato stránka se zaměřuje na běžné chyby při obnovování balíčků v sadě Visual Studio a kroky k jejich řešení. Pro postup obnovení balíčků, najdete v části [obnovení balíčků](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Ve výchozím nastavení sestavení projektu v sadě Visual Studio automaticky obnoví balíčky NuGet, kterou se odkazuje v projektu. Ale sestavení selže, pokud se obnovení balíčku je zakázána v **nástroje > Možnosti > Správce balíčků NuGet > Obnovení balíčků** nastavení a potřebné balíčky nejsou k dispozici ve vašem počítači. V těchto případech se může zobrazit následující chyby:

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

Pokud chcete povolit obnovení balíčků, otevřete **nástroje > Možnosti > Správce balíčků NuGet** a vyberte požadované možnosti pro **umožnit správci balíčků NuGet stáhnout chybějící balíčky** a **automaticky, zda nechybí balíčků během sestavení v sadě Visual Studio**:

![Povolit obnovení balíčků NuGet v Nástroje/možnosti](../consume-packages/media/restore-01-autorestoreoptions.png)
