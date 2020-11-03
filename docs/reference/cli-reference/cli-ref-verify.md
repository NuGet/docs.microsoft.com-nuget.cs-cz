---
title: NuGet CLI – příkaz ověření
description: Odkaz na příkaz nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238137"
---
# <a name="verify-command-nuget-cli"></a>VERIFY – příkaz (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** 4.6 +

Ověří balíček.

Ověřování podepsaných balíčků ještě není v mono podporováno.

## <a name="usage"></a>Využití

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` souborů.

## <a name="nuget-verify--all"></a>NuGet ověřit – vše

Určuje, že u balíčků by se měly provést všechna možná ověření.

## <a name="nuget-verify--signatures"></a>ověření NuGet – signatury

Určuje, že by mělo být provedeno ověření podpisu balíčku.

## <a name="options-for-verify--signatures"></a>Možnosti pro "ověřit-podpisy"

- **`-CertificateFingerprint`**

  Určuje jeden nebo více otisků certifikátů SHA-256 certifikátů, které musí být podepsané balíčky podepsány. Otisk certifikátu SHA-256 je hodnota hash SHA-256 certifikátu. Více vstupů by mělo být odděleno středníkem.

## <a name="options"></a>Možnosti

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

## <a name="examples"></a>Příklady

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```