---
title: Příkaz NuGet CLI Trusted-signers
description: Referenční informace k příkazu NuGet. exe Trusted-signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610337"
---
# <a name="trusted-signers-command-nuget-cli"></a>příkaz důvěryhodného přihlášení (NuGet CLI)

**Platí pro:** spotřeba balíčku &bullet; **podporované verze:** 4.9.1 +

Získá nebo nastaví důvěryhodné podepisující osoby na konfiguraci NuGet. Další informace o využití najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md). Podrobnosti o tom, jak vypadá schéma NuGet. config, najdete v odkazu na [konfigurační soubor NuGet](../nuget-config-file.md).

## <a name="usage"></a>Použití

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Pokud není zadán žádný z `list|add|remove|sync`, bude příkaz ve výchozím nastavení `list`.

## <a name="nuget-trusted-signers-list"></a>seznam důvěryhodných podpisů NuGet

Zobrazí seznam všech důvěryhodných přihlášení v konfiguraci. Tato možnost zahrne všechny certifikáty (s otiskem prstu a otiskem prstu) každého podepsaného. Pokud certifikát obsahuje předchozí `[U]`, znamená to, že položka certifikátu má `allowUntrustedRoot` nastavená jako `true`.

Níže je uvedený příklad výstupu z tohoto příkazu:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>Důvěryhodní přihlášení NuGet – přidat [možnosti]

Přidá důvěryhodného podepisujícího se zadaným názvem do konfiguračního souboru. Tato možnost obsahuje různá gesta pro přidání důvěryhodného autora nebo úložiště.

## <a name="options-for-add-based-on-a-package"></a>Možnosti pro přidání na základě balíčku

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` souborů.

| Možnost | Popis |
| --- | --- |
| Autorizova | Určuje, že podpis autora balíčků by měl být důvěryhodný. |
| Úložištì | Určuje, že signatura úložiště nebo potvrzovací podpisy balíčků by měly být důvěryhodné. |
| AllowUntrustedRoot | Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři. |
| vlastníka | Středníkem oddělený seznam důvěryhodných vlastníků, aby bylo možné dále omezit důvěryhodnost úložiště. Platí pouze při použití možnosti `-Repository`. |

Poskytování `-Author` i `-Repository` ve stejnou dobu není podporováno.

## <a name="options-for-add-based-on-a-service-index"></a>Možnosti pro přidání na základě indexu služby

```cli
nuget trusted-signers add -Name <name> [options]
```

_Poznámka_: Tato možnost bude přidávat jenom důvěryhodná úložiště. 

| Možnost | Popis |
| --- | --- |
| ServiceIndex | Určuje index služby V3 úložiště, který se má důvěřovat. Toto úložiště musí podporovat prostředek pro podpisy úložišť. Pokud není zadaný, příkaz bude hledat zdroj balíčku se stejným `-Name` a z něj získá index služby. |
| AllowUntrustedRoot | Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři. |
| vlastníka | Středníkem oddělený seznam důvěryhodných vlastníků, aby bylo možné dále omezit důvěryhodnost úložiště. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Možnosti pro přidání na základě informací o certifikátu

```cli
nuget trusted-signers add -Name <name> [options]
```

_Poznámka_: Pokud důvěryhodný podpis se zadaným názvem již existuje, bude položka certifikátu přidána k tomuto podepsanému. V opačném případě bude vytvořen důvěryhodný autor s položkou certifikátu z daných informací o certifikátu.

| Možnost | Popis |
| --- | --- |
| CertificateFingerprint | Určuje otisky certifikátu certifikátu, pomocí kterého musí být podepsané balíčky podepsané. Otisk certifikátu je hodnota hash certifikátu. Algoritmus hash použitý pro výpočet tohoto algoritmu hash by měl být určený v možnosti `FingerprintAlgorithm`. |
| FingerprintAlgorithm | Určuje algoritmus hash používaný k výpočtu otisku prstu certifikátu. Výchozí hodnota je `SHA256`. Podporované hodnoty jsou `SHA256`, `SHA384` a `SHA512` |
| AllowUntrustedRoot | Určuje, jestli by měl být certifikát pro důvěryhodného podepisujícího povolený řetězení k nedůvěryhodnému kořenovému adresáři. |

## <a name="nuget-trusted-signers-remove--name-name"></a>Trusted-Signer NuGet – jméno \<název\>

Odebere všechny důvěryhodné podepisující osoby, které odpovídají danému názvu.

## <a name="nuget-trusted-signers-sync--name-name"></a>\<název synchronizace NuGet-Signer Name\>

Vyžádá nejnovější seznam certifikátů používaných v aktuálně důvěryhodném úložišti, aby aktualizoval existující seznam certifikátů v důvěryhodném přihlášení.

_Poznámka_: Tento gesto odstraní aktuální seznam certifikátů a nahradí je aktuálním seznamem z úložiště.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Nápověda | Zobrazí informace o nápovědě k příkazu. |
| Podrobnosti | Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*. |

## <a name="examples"></a>Příklady

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
