---
title: Zkontrolujte příkaz NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro nuget.exe ověřte příkaz
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462849"
---
# <a name="verify-command-nuget-cli"></a>Příkaz verify (NuGet CLI)

**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 4.6 +

Ověřuje balíček.

Ověření podepsaný balíčků v .NET Core, v části Mono nebo na jiný systém než Windows platformách ještě není podporovaný.

## <a name="usage"></a>Použití

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` soubory.

## <a name="nuget-verify--all"></a>Ověřte nuget – všechny

Určuje, že všechny možné ověření je třeba provést na balíčky.

## <a name="nuget-verify--signatures"></a>ověřování nuget - podpisů

Určuje, že by se měla provést ověření podpisu balíčku.

## <a name="options-for-verify--signatures"></a>Možnosti pro "ověřit - podpisy"

| Možnost | Popis |
| --- | --- |
| CertificateFingerprint | Určuje jeden algoritmus SHA-256 certifikát otisky certifikátů (s), které podepsané balíčky musí být podepsány pomocí. Otisk prstu certifikát SHA-256 je hodnota hash SHA-256 certifikátu. Více vstupů by měl být oddělený středníkem. |

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

## <a name="examples"></a>Příklady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```