---
title: Příkaz pro vyhledávání NuGet CLI
description: Referenční informace pro příkaz nuget.exe Search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323658"
---
# <a name="search-command-nuget-cli"></a>Search – příkaz (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** 5,8 +

Vyhledá zadaný zdroj pomocí zadaného řetězce dotazu. Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v% data% \NuGet\NuGet.Config.

## <a name="usage"></a>Využití

```cli
nuget search [search terms] [options]
```

kde jsou použity hledané výrazy pro názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v nuget.org.

## <a name="options"></a>Možnosti

| Název | Description | Využití |
| ---  |     ---     |  :-:  |
| Předběžné verze | Balíčky předběžného vydání nejsou ve výchozím nastavení zahrnuty, ale mohou být zahrnuty pomocí tohoto argumentu. | – Předběžná verze |
| Zdroj | Konkrétní zdroje balíčků pro vyhledávání místo dotazování na výchozí zdroje v __nuget.config__ | -Source `<Source URL>`|
| Take | Počet výsledků, které se mají vrátit. Výchozí hodnota je 20. | – Převzít `<positive integer>` |
| Podrobnosti | Úroveň podrobností, která se má zobrazit ve výstupu Výchozí hodnota je _Normal_. (Viz poznámka níže)  | – Podrobnosti `<quiet|normal|detailed>` |
| Help | Zobrazí informace o nápovědě k příkazu. | -Help |

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
