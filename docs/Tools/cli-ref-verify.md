---
title: "Rozhraní příkazového řádku NuGet ověřte příkaz | Microsoft Docs"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro nuget.exe ověřte příkaz"
keywords: "ověření odkazu na nuget, ověřte příkaz"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a>Zkontrolujte příkaz (NuGet CLI)

**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 4.6 +

Ověřuje balíček.

## <a name="usage"></a>Použití

```cli
nuget verify <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` soubory.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Všechny | Určuje, že všechny možné ověření je třeba provést na balíčky. |
| CertificateFingerprint | Určuje jeden algoritmus SHA-256 certifikát otisky certifikátů (s), které podepsané balíčky musí být podepsány pomocí. Otisk prstu certifikát SHA-256 je hodnota hash SHA-256 certifikátu. Více vstupů by měl být oddělený středníkem. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podpisy | Určuje, že by se měla provést ověření podpisu balíčku. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

## <a name="examples"></a>Příklady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```