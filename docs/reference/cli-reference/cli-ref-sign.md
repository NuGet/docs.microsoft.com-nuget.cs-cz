---
title: NuGet – příkaz Sign CLI
description: Referenční informace k příkazu nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622769"
---
# <a name="sign-command-nuget-cli"></a>Sign – příkaz (NuGet CLI)

**Platí pro:** vytváření balíčků &bullet; **podporuje verze:** 4.6 +

Podepíše všechny balíčky, které odpovídají prvnímu argumentu s certifikátem. Certifikát s privátním klíčem lze získat ze souboru nebo z certifikátu nainstalovaného v úložišti certifikátů zadáním názvu předmětu nebo kryptografického otisku.

> [!Note]
> V rozhraní .NET Core, v mono nebo na platformách jiných než Windows se podepisování balíčků ještě nepodporuje.

## <a name="usage"></a>Využití

```cli
nuget sign <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` souborů.

## <a name="options"></a>Možnosti

- **`-CertificateFingerprint`**

  Určuje otisk SHA-1 certifikátu použitého k hledání místního úložiště certifikátů pro daný certifikát.

- **`-CertificatePassword`**

  V případě potřeby Určuje heslo certifikátu. Pokud je certifikát chráněný heslem, ale není k dispozici žádné heslo, příkaz zobrazí výzvu k zadání hesla za běhu, pokud `-NonInteractive` není možnost předána.

- **`-CertificatePath`**

  Určuje cestu k souboru certifikátu, který se má použít při podepisování balíčku.

- **`-CertificateStoreLocation`**

  Určuje název úložiště certifikátů X. 509, které se používá k vyhledání certifikátu. Výchozí hodnota je "CurrentUser", úložiště certifikátů X. 509 používané aktuálním uživatelem. Tato možnost by se měla použít při zadávání certifikátu prostřednictvím `-CertificateSubjectName` nebo `-CertificateFingerprint` možností.

- **`-CertificateStoreName`**

  Určuje název úložiště certifikátů X. 509, který se použije k vyhledání certifikátu. Výchozí hodnota je my, úložiště certifikátů X. 509 pro osobní certifikáty. Tato možnost by se měla použít při zadávání certifikátu prostřednictvím `-CertificateSubjectName` nebo `-CertificateFingerprint` možností.

- **`-CertificateSubjectName`**

  Určuje název subjektu certifikátu použitého k hledání místního úložiště certifikátů pro daný certifikát.  Hledání je porovnávání řetězců bez rozlišení velkých a malých písmen pomocí zadané hodnoty, která vyhledá všechny certifikáty s názvem subjektu, který tento řetězec obsahuje, bez ohledu na jiné hodnoty předmětu.  Úložiště certifikátů lze zadat pomocí `-CertificateStoreName` `-CertificateStoreLocation` možností a.

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-HashAlgorithm`**

  Algoritmus hash, který se má použít k podepsání balíčku. Výchozí hodnota je SHA256. Možné hodnoty jsou SHA256, SHA384 a SHA512.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-OutputDirectory`**

  Určuje adresář, do kterého se má uložit podepsaný balíček. Ve výchozím nastavení je původní balíček přepsán podepsaným balíčkem.

- **`-Overwrite`**

  Přepněte k označení, zda má být aktuální podpis přepsán. Ve výchozím nastavení se příkaz nezdaří, pokud balíček již má podpis.

- **`-Timestamper`**

  Adresa URL serveru časového razítka RFC 3161.

- **`-TimestampHashAlgorithm`**

  Algoritmus hash, který má používat server časových razítek RFC 3161. Výchozí hodnota je SHA256.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

## <a name="examples"></a>Příklady

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
