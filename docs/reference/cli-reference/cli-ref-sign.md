---
title: NuGet – příkaz Sign CLI
description: Referenční informace o příkazu NuGet. exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e596fd5eb3de8ca4802d9b7b8e7cb623568e3dcb
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231120"
---
# <a name="sign-command-nuget-cli"></a>Příkaz sign (NuGet CLI)

**Platí pro:** vytvoření balíčku &bullet; **podporované verze:** 4.6 +

Podepíše všechny balíčky, které odpovídají prvnímu argumentu s certifikátem. Certifikát s privátním klíčem lze získat ze souboru nebo z certifikátu nainstalovaného v úložišti certifikátů zadáním názvu předmětu nebo kryptografického otisku.

> [!Note]
> V rozhraní .NET Core, v mono nebo na platformách jiných než Windows se podepisování balíčků ještě nepodporuje.

## <a name="usage"></a>Využití

```cli
nuget sign <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` souborů.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| CertificateFingerprint | Určuje otisk SHA-1 certifikátu použitého k hledání místního úložiště certifikátů pro daný certifikát. |
| CertificatePassword | V případě potřeby Určuje heslo certifikátu. Pokud je certifikát chráněný heslem, ale není k dispozici žádné heslo, příkaz zobrazí výzvu k zadání hesla v době běhu, pokud není předána možnost-neinteraktivní. |
| CertificatePath | Určuje cestu k souboru certifikátu, který se má použít při podepisování balíčku. |
| certificateStoreLocation | Určuje název úložiště certifikátů X. 509, které se používá k vyhledání certifikátu. Výchozí hodnota je "CurrentUser", úložiště certifikátů X. 509 používané aktuálním uživatelem. Tato možnost by se měla použít při zadávání certifikátu prostřednictvím možností-CertificateSubjectName nebo-CertificateFingerprint. |
| certificateStoreName | Určuje název úložiště certifikátů X. 509, který se použije k vyhledání certifikátu. Výchozí hodnota je my, úložiště certifikátů X. 509 pro osobní certifikáty. Tato možnost by se měla použít při zadávání certifikátu prostřednictvím možností-CertificateSubjectName nebo-CertificateFingerprint. |
| CertificateSubjectName | Určuje název subjektu certifikátu použitého k hledání místního úložiště certifikátů pro daný certifikát.  Hledání je porovnávání řetězců bez rozlišení velkých a malých písmen pomocí zadané hodnoty, která vyhledá všechny certifikáty s názvem subjektu, který tento řetězec obsahuje, bez ohledu na jiné hodnoty předmětu.  Úložiště certifikátů lze zadat pomocí možností-CertificateStoreName a-CertificateStoreLocation. |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| HashAlgorithm | Algoritmus hash, který se má použít k podepsání balíčku. Výchozí hodnota je SHA256. Možné hodnoty jsou SHA256, SHA384 a SHA512. |
| Nápověda | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| OutputDirectory | Určuje adresář, do kterého se má uložit podepsaný balíček. Ve výchozím nastavení je původní balíček přepsán podepsaným balíčkem. |
| Přepsat | Přepněte k označení, zda má být aktuální podpis přepsán. Ve výchozím nastavení se příkaz nezdaří, pokud balíček již má podpis. |
| Časové razítko | Adresa URL serveru časového razítka RFC 3161. |
| TimestampHashAlgorithm | Algoritmus hash, který má používat server časových razítek RFC 3161. Výchozí hodnota je SHA256. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*. |

## <a name="examples"></a>Příklady

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
