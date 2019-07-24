---
title: NuGet CLI – příkaz ověření
description: Referenční informace o příkazu NuGet. exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328252"
---
# <a name="verify-command-nuget-cli"></a>Příkaz verify (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** 4.6 +

Ověří balíček.

Ověřování podepsaných balíčků se ještě nepodporuje v .NET Core, v mono nebo na platformách jiných než Windows.

## <a name="usage"></a>Použití

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` souborů.

## <a name="nuget-verify--all"></a>NuGet ověřit – vše

Určuje, že u balíčků by se měly provést všechna možná ověření.

## <a name="nuget-verify--signatures"></a>ověření NuGet – signatury

Určuje, že by mělo být provedeno ověření podpisu balíčku.

## <a name="options-for-verify--signatures"></a>Možnosti pro "ověřit-podpisy"

| Možnost | Popis |
| --- | --- |
| CertificateFingerprint | Určuje jeden nebo více otisků certifikátů SHA-256 certifikátů, které musí být podepsané balíčky podepsány. Otisk certifikátu SHA-256 je hodnota hash SHA-256 certifikátu. Více vstupů by mělo být odděleno středníkem. |

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| ForceEnglishOutput | Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

## <a name="examples"></a>Příklady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```