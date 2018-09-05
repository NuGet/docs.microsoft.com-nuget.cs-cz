---
title: Rozhraní příkazového řádku NuGet přihlašování
description: Referenční informace pro příkaz nuget.exe znak
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546360"
---
# <a name="sign-command-nuget-cli"></a>Příkaz sign (NuGet CLI)

**Platí pro:** vytvoření balíčku &bullet; **podporované verze:** 4.6 +

Zaregistruje všechny balíčky odpovídající první argument s certifikátem. Ze souboru nebo z nainstalován v úložišti certifikátů zadáním názvu předmětu nebo kryptografického otisku certifikátu je možné získat certifikát s privátním klíčem.

Podepisování balíčků se ještě nepodporuje v .NET Core, mono, nebo na platformách než Windows.

## <a name="usage"></a>Použití

```cli
nuget sign <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` soubory.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| CertificateFingerprint | Určuje otisk SHA-1 certifikátu používaného pro vyhledávání místního úložiště certifikátů pro certifikát. |
| CertificatePassword | Určuje heslo certifikátu v případě potřeby. Pokud certifikát je chráněn heslem ale Azure nenabízí žádné heslo, příkaz vás vyzve k zadání hesla v době běhu, není-li-neinteraktivní možnost je předán. |
| CertificatePath | Určuje cestu k certifikátu, který se má použít při podepisování balíčku. |
| CertificateStoreLocation | Určuje název použití úložiště certifikátů X.509 pro vyhledání certifikátu. Výchozí hodnota je "CurrentUser", úložiště certifikátů X.509 používá aktuálního uživatele. Tato možnost by měla sloužit při určení certifikátu prostřednictvím - CertificateSubjectName nebo - CertificateFingerprint možností. |
| Název_úložiště_certifikátů | Určuje název úložiště certifikátu X.509 slouží k vyhledání certifikátu. Výchozí hodnota je "My", úložiště certifikátů X.509 pro osobní certifikáty. Tato možnost by měla sloužit při určení certifikátu prostřednictvím - CertificateSubjectName nebo - CertificateFingerprint možností. |
| CertificateSubjectName | Určuje název subjektu certifikátu používaného pro vyhledávání místního úložiště certifikátů pro certifikát.  Hledání je porovnání nerozlišuje velikost písmen řetězců pomocí zadané hodnoty, které bude vyhledat všechny certifikáty s názvem subjektu, který obsahuje tento řetězec bez ohledu na ostatní hodnoty pro předmět.  Úložiště certifikátů je možné zadat tak Název_úložiště_certifikátů - a - CertificateStoreLocation možnosti. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| HashAlgorithm | Hashovací algoritmus se použije k podpisu balíčku. Výchozí hodnota SHA256. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| OutputDirectory | Určuje adresář, kterého chcete uložit podepsaný balíček. Ve výchozím nastavení se původní balíček přepíše podepsaným balíčkem. |
| Přepsat | Přepínač, který určuje, pokud se má přepsat aktuální podpis. Ve výchozím nastavení se příkaz nezdaří, pokud je balíček už podpis. |
| Timestamper | Adresa URL serveru časového razítka RFC 3161. |
| TimestampHashAlgorithm | Hashovací algoritmus používaný serverem časového razítka RFC 3161. Výchozí hodnota SHA256. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

## <a name="examples"></a>Příklady

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```