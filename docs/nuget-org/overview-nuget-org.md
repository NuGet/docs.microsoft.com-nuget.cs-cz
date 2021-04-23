---
title: Přehled NuGet.org
description: Přehled NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901873"
---
# <a name="overview-of-nugetorg"></a>Přehled NuGet.org

NuGet.org je veřejným hostitelem balíčků NuGet, které každý den pracují s miliony vývojářů .NET a .NET Core.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Role NuGet.org v ekosystému NuGet

NuGet.org sám v roli jako veřejný hostitel udržuje centrální úložiště více než 100 000 jedinečných balíčků na [NuGet.org](https://www.nuget.org). NuGet.org není jediným možným hostitelem pro balíčky. Technologie NuGet také umožňuje hostovat balíčky soukromě v cloudu (například na Azure DevOps), v privátní síti nebo dokonce jenom v místním systému souborů. Pokud vás zajímá jiný hostitel nebo možnost hostování, přečtěte si téma [hostování vlastních kanálů NuGet](../hosting-packages/overview.md).

NuGet.org, podobně jako jakýkoli hostitel pro balíčky NuGet, slouží jako bod připojení mezi *tvůrci* balíčků a *uživatele* balíčku. Tvůrci sestavují užitečné balíčky NuGet a publikují je. Příjemci pak hledají užitečné a kompatibilní balíčky na dostupných hostitelích, stahují a zahrnují tyto balíčky v jejich projektech. Po instalaci v projektu jsou balíčky rozhraní API k dispozici pro zbytek kódu projektu.

![Vztah mezi tvůrci balíčků, hostiteli balíčků a příjemci balíčku](media/nuget-roles.png)

## <a name="accounts"></a>Účty

Pokud chcete publikovat balíčky na NuGet.org, musíte nejdřív vytvořit [individuální (uživatelský) účet](individual-accounts.md). Tím se vaše identita bude NuGet.org.

NuGet.org také umožňuje vytvořit [účet organizace](organizations-on-nuget-org.md). Účet organizace má jako členy jeden nebo více jednotlivých účtů. Členové mohou spravovat sadu balíčků a přitom zachovat jedinou identitu pro vlastnictví. Prostřednictvím individuálního účtu můžete být členem libovolného počtu organizací.

Balíček může patřit k účtu organizace, jako by mohl patřit k individuálnímu účtu. Uživatelé balíčku nevidí žádný rozdíl mezi jednotlivými účty nebo účtem organizace: obě se zobrazí jako balíčky `owners` .

## <a name="api-keys"></a>Klíče rozhraní API

Jakmile budete mít k publikování balíček NuGet (soubor *. nupkg* ), publikujete ho do NuGet.org pomocí rozhraní příkazového řádku nuget.exe nebo rozhraní příkazového řádku dotnet.exe, společně s [klíčem rozhraní API](scoped-api-keys.md) získaným z NuGet.org.

Když [publikujete balíček](../create-packages/creating-a-package.md), zahrnete do příkazu CLI hodnotu klíče rozhraní API.

## <a name="id-prefixes"></a>Předpony ID

Když publikujete balíčky, můžete si vyhradit a chránit svoji identitu tím, že si [zachováte předpony ID](id-prefix-reservation.md). Při instalaci balíčku jsou k dispozici příjemci balíčku s dalšími informacemi, které označují, že daný balíček je neklamný v jeho identifikačních vlastnostech.

## <a name="api-endpoint-for-nugetorg"></a>Koncový bod rozhraní API pro NuGet.org

Pokud chcete používat NuGet.org jako úložiště balíčků s klienty NuGet, měli byste použít následující koncový bod rozhraní API V3: 

`https://api.nuget.org/v3/index.json`

Starší klienti stále můžou k přístupu k NuGet.org používat protokol v2. Upozorňujeme však, že klienti NuGet 3,0 nebo novější budou mít pomalejší a méně spolehlivější službu pomocí protokolu v2:

`https://www.nuget.org/api/v2` (**Protokol v2 je zastaralý!**)
