---
title: Příkaz pro vyhledávání NuGet CLI
description: Referenční informace pro příkaz nuget.exe Search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779165"
---
# <a name="search-command-nuget-cli"></a>Search – příkaz (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** 5,8 +

Vyhledá zadaný zdroj pomocí zadaného řetězce dotazu. Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v% data% \NuGet\NuGet.config.

## <a name="usage"></a>Využití

```cli
nuget search [search terms] [options]
```

kde jsou použity hledané výrazy pro názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v nuget.org.

## <a name="options"></a>Možnosti

| Název | Popis | Využití |
| ---  |     ---     |  :-:  |
| Předběžné verze | Balíčky předběžného vydání nejsou ve výchozím nastavení zahrnuty, ale mohou být zahrnuty pomocí tohoto argumentu. | – Předběžná verze |
| Zdroj | Konkrétní zdroje balíčků pro vyhledávání místo dotazování na výchozí zdroje v __nuget.config__ | -Source `<Source URL>`|
| Take | Počet výsledků, které se mají vrátit. Výchozí hodnota je 20. | – Převzít `<positive integer>` |
| Podrobnosti | Úroveň podrobností, která se má zobrazit ve výstupu Výchozí hodnota je _Normal_. (Viz poznámka níže)  | – Podrobnosti `<quiet|normal|detailed>` |
| Nápověda | Zobrazí informace o nápovědě k příkazu. | -Help |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

> [!NOTE] 
> Úrovně podrobností:
> * _quiet_ – ID balíčku, verze
> * _Normal_ – ID balíčku, verze, soubory ke stažení, náhled popisu
> * _podrobné_ – ID balíčku, verze, soubory ke stažení, úplný popis, další informace, jako je například adresa URL dotazu

## <a name="examples"></a>Příklady

Vyhledat balíčky související s *protokolováním* z výchozích zdrojů:
```
nuget search logging
```
Vyhledejte balíčky související s *protokolováním* s podrobnostmi:
```
nuget search logging -Verbosity detailed
```
Vyhledejte balíčky související s *protokolováním* a zobrazte pouze prvních 5 výsledků:
```
nuget search logging -Take 5
```
Vyhledat balíčky související s *JSON*, včetně předběžných verzí, ze zadaného zdroje/informačního kanálu:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Hledat balíčky související s *JSON* z několika zdrojů nebo kanálů:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
