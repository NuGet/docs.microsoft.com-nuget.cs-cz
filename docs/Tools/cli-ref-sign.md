---
title: "Příkaz přihlašovací NuGet rozhraní příkazového řádku | Microsoft Docs"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz nuget.exe přihlášení"
keywords: "nuget přihlašovací odkaz, příkaz přihlášení"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: f600a0830472703f40ef62f1b1538c53671703a9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="sign-command-nuget-cli"></a>příkaz přihlašovací (NuGet CLI)

**Platí pro:** balíček vytvoření &bullet; **podporované verze:** 4.6 +

Podepisuje všechny balíčky odpovídající první argument s certifikátem. Ze souboru nebo z nainstalovaný v úložišti certifikátů zadáním názvu subjektu nebo kryptografický otisk certifikátu je možné získat certifikát s privátním klíčem.

Podpis balíčku se ještě nepodporuje pod Mono nebo na jiný systém než Windows platformách.

## <a name="usage"></a>Použití

```cli
nuget sign <package(s)> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` soubory.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| CertificateFingerprint | Určuje algoritmus SHA-1 otisk certifikátu používaného pro vyhledávání místního úložiště certifikátů pro certifikát. |
| CertificatePassword | Určuje heslo certifikátu v případě potřeby. Pokud certifikát je chráněný heslem, ale je k dispozici žádné heslo, příkaz zobrazí výzvu k zadání hesla v době běhu, pokud-neinteraktivní možnost je předán. |
| CertificatePath | Určuje cestu k souboru na certifikát, který chcete použít v podpisu balíčku. |
| CertificateStoreLocation | Určuje název použití úložiště certifikátů X.509 pro vyhledání certifikátu. Výchozí hodnota je "CurrentUser", úložišti certifikátů X.509, který je aktuální uživatel používá. Tuto možnost byste měli použít při zadávání certifikát pomocí - CertificateSubjectName nebo - CertificateFingerprint možnosti. |
| CertificateStoreName | Určuje název úložiště certifikátu X.509, které chcete použít k vyhledání certifikátu. Výchozí hodnota je "Moje", úložiště certifikátů X.509 pro osobní certifikáty. Tuto možnost byste měli použít při zadávání certifikát pomocí - CertificateSubjectName nebo - CertificateFingerprint možnosti. |
| CertificateSubjectName | Určuje název subjektu certifikátu používaného pro vyhledávání místního úložiště certifikátů pro certifikát.  Hledání je pomocí zadané hodnoty, který zjistí všechny certifikáty s názvem subjektu, který obsahuje tento řetězec, bez ohledu na ostatní hodnoty subjektu porovnání řetězců velká a malá písmena.  Úložiště certifikátů může být určena Název_úložiště_certifikátů - a - CertificateStoreLocation možnosti. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Algoritmus has | Algoritmus hash, který se má použít k podpisu balíčku. Výchozí hodnota SHA256. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Výstupnísložka | Určuje adresář, kde má být uložen podepsaného balíčku. Ve výchozím nastavení se přepíše původní balíček podepsaný balíček. |
| Přepsat | Přepínač k označení, pokud by měl být přepsány aktuálního podpisu. Ve výchozím nastavení příkaz se nezdaří, pokud již podpis balíčku. |
| Timestamper | Adresa URL k serveru RFC 3161 časových razítek. |
| TimestampHashAlgorithm | Algoritmus hash, který se má použít časové razítko serverem RFC 3161. Výchozí hodnota SHA256. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

## <a name="examples"></a>Příklady

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```