---
title: Zkontrolujte příkaz rozhraní příkazového řádku NuGet
description: Ověření odkazu nuget.exe příkaz
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545210"
---
# <a name="verify-command-nuget-cli"></a>Příkaz verify (NuGet CLI)

**Platí pro:** balíček spotřeby &bullet; **podporované verze:** 4.6 +

Ověří balíčku.

V .NET Core, mono, nebo na platformách než Windows zatím nepodporuje ověření podepsaných balíčků.

## <a name="usage"></a>Použití

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` soubory.

## <a name="nuget-verify--all"></a>ověřit nuget – vše

Určuje, že všechny možné ověření je třeba provést na balíčky.

## <a name="nuget-verify--signatures"></a>ověřování nuget - podpisů

Určuje, že by se měla provést ověření podpisu balíčku.

## <a name="options-for-verify--signatures"></a>Možnosti pro "ověřování - podpisů"

| Možnost | Popis |
| --- | --- |
| CertificateFingerprint | Určuje jeden nebo více SHA-256 certifikát otisky prstů certifikátů (s), které podepsané balíčky musí být podepsán. Otisk certifikátu SHA-256 se hashovací algoritmus SHA-256 certifikátu. Více vstupů by měl být oddělený středníkem. |

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

## <a name="examples"></a>Příklady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```