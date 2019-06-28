---
title: Přehled NuGet.org
description: Přehled NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427521"
---
# <a name="overview-of-nugetorg"></a>Přehled NuGet.org

NuGet.org je veřejný hostitel balíčků NuGet, které se použijí podle miliony vývojářů .NET a .NET Core každý den.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Role NuGet.org do ekosystému a NuGet

V jeho role jako veřejný hostitel NuGet.org, sama udržuje centrálním úložišti víc než 100 000 jedinečné balíčky v [nuget.org](https://www.nuget.org). NuGet.org není možné dosáhnout pouze hostitelem pro balíčky. Technologie NuGet také umožňuje hostování balíčků soukromě v cloudu (například na Azure DevOps), v privátní síti, nebo dokonce i na právě vašeho místního systému souborů. Pokud vás zajímají jiného hostitele nebo možnost hostování, přečtěte si téma [hostování vlastní kanály NuGet](../hosting-packages/overview.md).

NuGet.org, stejně jako všechny hostitele pro balíčky NuGet, slouží jako bod připojení mezi balíček *creators* a balíček *příjemci*. Tvůrce sestavení užitečné balíčky NuGet a publikujte je. Příjemci vyhledejte balíčky užitečné a kompatibilní na hostitelích přístupné, stahování a včetně těchto balíčků ve svých projektech. Po instalaci v projektu, rozhraní API balíčky jsou k dispozici pro zbývající část kódu projektu.

![Vztah mezi Tvůrce balíčku, balíčku hostitele a spotřebitele balíčku](media/nuget-roles.png)

## <a name="accounts"></a>Účty

Publikování balíčků na NuGet.org, je třeba nejprve vytvořit [osoba (uživatel) účtu](individual-accounts.md). To se stane svoji identitu na NuGet.org.

NuGet.org také umožňuje vytvořit [účet organizace](organizations-on-nuget-org.md). Účet organizace má jeden nebo více samostatné účty jako členy. Členové mohou spravovat sadu balíčků při zachování jedinou identitu pro vlastnictví. Pomocí svého individuálního účtu může být členem jakékoli číslo organizace.

Balíček může patřit k účtu organizace jako můžou patřit do individuálního účtu. Balíček příjemci nezobrazuje žádný rozdíl mezi samostatný účet nebo účet organizace: oba se objeví jako balíček `owners`.

## <a name="api-keys"></a>Klíče rozhraní API

Jakmile budete mít balíčku NuGet ( *.nupkg* souboru) k publikování, ji publikujete do pomocí rozhraní příkazového řádku nuget.exe nebo dotnet.exe rozhraní příkazového řádku, spolu s NuGet.org [klíč rozhraní API](scoped-api-keys.md) získaných z NuGet.org.

Pokud jste [publikování balíčku](../create-packages/creating-a-package.md), zahrnují hodnotu klíče rozhraní API v příkazu rozhraní příkazového řádku.

## <a name="id-prefixes"></a>Předpony ID

Při publikování balíčků si můžete rezervovat a chránit vaši identitu pomocí [rezervace předpony ID](id-prefix-reservation.md). Při instalaci balíčku, balíčku příjemci jsou k dispozici společně s dalšími informacemi označující, že balíček, který se spotřebovávají není podvodný v jeho identifikující vlastnosti.

## <a name="api-endpoint-for-nugetorg"></a>Koncový bod rozhraní API pro NuGet.org

Pokud chcete použít jako úložiště balíčků s klienty NuGet NuGet.org, měli byste použít následující koncový bod rozhraní API V3: 

`https://api.nuget.org/v3/index.json`

Starší klienti stále může použít protokol V2 k dosažení NuGet.org. Upozorňujeme, klienti 3.0 nebo vyšší budou mít nižší a méně spolehlivé služby pomocí protokolu V2 NuGet:

`https://www.nuget.org/api/v2` (**Protokol the V2 sítě se již nepoužívá.** )
