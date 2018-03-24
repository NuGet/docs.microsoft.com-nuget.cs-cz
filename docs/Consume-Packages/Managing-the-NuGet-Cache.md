---
title: Jak spravovat balíček ukládání do mezipaměti v NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Jak spravovat jiný balíček NuGet ukládá do mezipaměti, který neexistuje na počítači, které se používají při instalaci nebo obnovují se balíčky.
keywords: Mezipaměť balíčku NuGet, balíček ukládání do mezipaměti, mezipaměti NuGet, Správa mezipaměti, místní mezipaměti NuGet, globální mezipaměti NuGet, místní hodnoty – příkaz NuGet, vymazání mezipaměti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09b3560d67ff8a38677dd1e27d85cdf234495aae
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2018
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="50a00-104">Správa mezipaměti NuGet</span><span class="sxs-lookup"><span data-stu-id="50a00-104">Managing the NuGet cache</span></span>

<span data-ttu-id="50a00-105">NuGet spravuje několik místní mezipaměti, aby se zabránilo stahovali balíčky, které jsou již v počítači a zajistit podporu offline režimu.</span><span class="sxs-lookup"><span data-stu-id="50a00-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="50a00-106">NuGet automaticky spadne zpět do mezipaměti při instalaci nebo přeinstalování balíčky bez připojení k síti.</span><span class="sxs-lookup"><span data-stu-id="50a00-106">NuGet automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="50a00-107">Umístění mezipaměti, jsou k dispozici pomocí [místní hodnoty – příkaz](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="50a00-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```cli
nuget locals all -list
```

<span data-ttu-id="50a00-108">Typické výstup vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="50a00-108">Typical output is as follows:</span></span>

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

<span data-ttu-id="50a00-109">Pokud dojde k potížím instalace balíčku nebo jinak potřeba zajistit, že instalujete balíčky ze vzdáleného galerie, použijte `locals -clear` možnost:</span><span class="sxs-lookup"><span data-stu-id="50a00-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="50a00-110">Všimněte si, že správa mezipaměti v současné době podporuje pouze z příkazového řádku NuGet a není v sadě Visual Studio nebo pomocí konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="50a00-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="50a00-111">Navíc Správa mezipaměti 2.x není podporována v NuGet 3.6 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="50a00-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="50a00-112">Následující chyby může stát při použití `nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="50a00-112">The following errors can occur when using `nuget locals`:</span></span>

- <span data-ttu-id="50a00-113">**Vymazání místních prostředků se nezdařilo: nelze odstranit jeden nebo více souborů**</span><span class="sxs-lookup"><span data-stu-id="50a00-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
- <span data-ttu-id="50a00-114">**Adresář není prázdná**</span><span class="sxs-lookup"><span data-stu-id="50a00-114">**The directory is not empty**</span></span>

<span data-ttu-id="50a00-115">Ty naznačují, že buď nemáte oprávnění k odstranění souborů v mezipaměti, nebo že jeden nebo další soubory v mezipaměti se používá jiný proces, který musí být uzavřeny před odebráním soubory.</span><span class="sxs-lookup"><span data-stu-id="50a00-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the files can be removed.</span></span>
