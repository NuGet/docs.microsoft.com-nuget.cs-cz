---
title: Přehled NuGet.org
description: Přehled NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427521"
---
# <a name="overview-of-nugetorg"></a>Přehled NuGet.org

NuGet.org je veřejný hostitel balíčků NuGet, které jsou zaměstnány miliony vývojářů .NET a .NET Core každý den.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Úloha NuGet.org v ekosystému NuGet

Ve své roli veřejného hostitele, NuGet.org sám udržuje centrální úložiště více než 100.000 unikátních balíčků na [nuget.org](https://www.nuget.org). NuGet.org není jediným možným hostitelem pro balíčky. Technologie NuGet také umožňuje hostovat balíčky soukromě v cloudu (například na Azure DevOps), v privátní síti nebo dokonce pouze v místním systému souborů. Máte-li zájem o jiný hostitel nebo možnost hostování, viz [Hostování vlastních nugetových kanálů](../hosting-packages/overview.md).

NuGet.org, stejně jako každý hostitel pro balíčky NuGet, slouží jako bod spojení mezi *tvůrci* balíčků a *příjemci*balíčků . Tvůrci vytvářet užitečné balíčky NuGet a publikovat je. Spotřebitelé pak vyhledávají užitečné a kompatibilní balíčky na přístupných hostitelích, stahují a zařazují tyto balíčky do svých projektů. Po instalaci v projektu jsou rozhraní API balíčků k dispozici pro zbytek kódu projektu.

![Vztah mezi tvůrci balíčků, hostiteli balíčků a příjemci balíčků](media/nuget-roles.png)

## <a name="accounts"></a>Účty

Chcete-li publikovat balíčky na NuGet.org, nejprve vytvořte [individuální (uživatelský) účet](individual-accounts.md). To se stane vaší identitou na NuGet.org.

NuGet.org také umožňuje vytvořit [účet organizace](organizations-on-nuget-org.md). Účet organizace má jeden nebo více individuálních účtů jako své členy. Členové mohou spravovat sadu balíčků při zachování jedné identity pro vlastnictví. Prostřednictvím svého individuálního účtu můžete být členem libovolného počtu organizací.

Balíček může patřit k účtu organizace, stejně jako může patřit k individuálnímu účtu. Spotřebitelé balíčků nevidí žádný rozdíl mezi individuálním účtem nebo účtem organizace: oba se zobrazují jako balíček `owners`.

## <a name="api-keys"></a>Klíče rozhraní API

Jakmile máte balíček NuGet (*soubor .nupkg)* publikovat do NuGet.org pomocí rozhraní api nuget.exe nebo dotnet.exe CLI, spolu s [klíčem rozhraní API](scoped-api-keys.md) získaného z NuGet.org.

Při [publikování balíčku](../create-packages/creating-a-package.md)zahrnete hodnotu klíče rozhraní API do příkazu příkazu příkazu příkazu příkazu příkazu.

## <a name="id-prefixes"></a>ID předpony

Při publikování balíčků můžete rezervovat a chránit svou identitu [rezervací předponek ID](id-prefix-reservation.md). Při instalaci balíčku jsou příjemci balíčku opatřeni dalšími informacemi, které označují, že balíček, který spotřebovávají, neklame ve svých identifikačních vlastnostech.

## <a name="api-endpoint-for-nugetorg"></a>Koncový bod rozhraní API pro NuGet.org

Chcete-li použít NuGet.org jako úložiště balíčků s klienty NuGet, měli byste použít následující koncový bod rozhraní API V3: 

`https://api.nuget.org/v3/index.json`

Starší klienti mohou stále používat protokol V2 k dosažení NuGet.org. Upozorňujeme však, že klienti NuGet 3.0 nebo novější budou mít pomalejší a méně spolehlivé služby pomocí protokolu V2:

`https://www.nuget.org/api/v2`**(Prototcol V2 je zastaralá!**)
