---
title: Rozhraní příkazového řádku NuGet důvěryhodné podepisující osoby
description: Referenční dokumentace pro důvěryhodného podepisující osoby příkaz nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324705"
---
# <a name="trusted-signers-command-nuget-cli"></a>příkaz důvěryhodné podepisující osoby (rozhraní příkazového řádku NuGet)

**Platí pro:** balíček spotřeby &bullet; **podporované verze:** 4.9.1+

Získá nebo nastaví podepisující důvěryhodné osoby pro konfiguraci Nugetu. Další využití, naleznete v tématu [konfigurace chování Nugetu](../consume-packages/configuring-nuget-behavior.md). Podrobnosti o jak nuget.config schéma vypadá jako odkazovat [odkaz na soubor NuGet config](../reference/nuget-config-file.md).

## <a name="usage"></a>Použití

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Pokud žádná z `list|add|remove|sync` není zadán, příkaz se ve výchozím nastavení `list`.

## <a name="nuget-trusted-signers-list"></a>seznam důvěryhodných podepsaných nuget

Zobrazí seznam všech důvěryhodných podepsaných v konfiguraci. Tato možnost zahrne všechny certifikáty (s otisku prstu a algoritmus otisk prstu) má každý podepisující osoba. Pokud je certifikát předchozí `[U]`, znamená to, že položka certifikát má `allowUntrustedRoot` nastavit jako `true`.

Tady je příklad výstupu tohoto příkazu:

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

## <a name="nuget-trusted-signers-add-options"></a>Přidat nuget důvěryhodné podepsaných [možnosti]

Přidá ke konfiguraci důvěryhodných podepisující osoba s daným názvem. Tuto možnost má jiné gesta můžete přidat důvěryhodného autora nebo úložiště.

## <a name="options-for-add-based-on-a-package"></a>Možnosti pro přidání závislosti na balíček

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

kde `<package(s)>` je jeden nebo více `.nupkg` soubory.

| Možnost | Popis |
| --- | --- |
| Autor | Určuje, že autor podpis balíčky, které by měl být důvěryhodný. |
| Úložiště | Určuje, že podpis úložiště nebo potvrzovací podpis z balíčky musí být důvěryhodný. |
| AllowUntrustedRoot | Určuje, jestli certifikát pro důvěryhodného podepisující osoba by měla být povolená na řetězce na nedůvěryhodném kořenu. |
| Vlastníci | Středníkem oddělený seznam vlastníků důvěryhodné pro další omezení důvěryhodnosti úložiště. Platné jen v případě použití `-Repository` možnost. |

Poskytuje i `-Author` a `-Repository` není podporováno ve stejnou dobu.

## <a name="options-for-add-based-on-a-service-index"></a>Možnosti pro přidání závislosti na index služby

```cli
nuget trusted-signers add -Name <name> [options]
```

_Poznámka:_: Tato možnost přidá jenom důvěryhodné úložiště. 

| Možnost | Popis |
| --- | --- |
| ServiceIndex | Určuje index služby V3 úložiště považovat za důvěryhodné. Toto úložiště musí podporovat podpisy prostředků úložiště. Pokud se nezadá, bude příkaz vypadat zdroje balíčku se stejným `-Name` a získat index služby z něj. |
| AllowUntrustedRoot | Určuje, jestli certifikát pro důvěryhodného podepisující osoba by měla být povolená na řetězce na nedůvěryhodném kořenu. |
| Vlastníci | Středníkem oddělený seznam vlastníků důvěryhodné pro další omezení důvěryhodnosti úložiště. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Možnosti pro přidání na základě informací o certifikátu

```cli
nuget trusted-signers add -Name <name> [options]
```

_Poznámka:_: Pokud důvěryhodné podepisující osoba s daným názvem již existuje, položku certifikátu se přidají do této podepisující osoba. V opačném případě důvěryhodného autora vytvoří s položkou certifikát z daných informace o certifikátu.

| Možnost | Popis |
| --- | --- |
| CertificateFingerprint | Určuje certifikát, který musí být podepsáno otisky certifikátu, který podepsaných balíčků. Otisk certifikátu je hodnota hash certifikátu. Určuje algoritmus hash sloužící k výpočtu, tato hodnota hash by měla být v `FingerprintAlgorithm` možnost. |
| FingerprintAlgorithm | Určuje algoritmus hash používaný k výpočtu otisku certifikátu. Výchozí hodnota je `SHA256`. Podporované hodnoty jsou `SHA256`, `SHA384` a `SHA512` |
| AllowUntrustedRoot | Určuje, jestli certifikát pro důvěryhodného podepisující osoba by měla být povolená na řetězce na nedůvěryhodném kořenu. |

## <a name="nuget-trusted-signers-remove--name-name"></a>odebrat důvěryhodné nuget-podepsaných – název <name>

Odebere všechny důvěryhodné podepisující osoby, které odpovídají zadaným názvem.

## <a name="nuget-trusted-signers-sync--name-name"></a>důvěryhodné nuget-podepsaných synchronizovat – název <name>

Vyžaduje nejnovější seznam certifikátů používaných v současné době nedůvěryhodný úložiště aktualizovat seznamu existujících certifikátů v důvěryhodné podepisující osoba.

_Poznámka:_: Tato gesta odstraní aktuální seznam certifikátů a nahraďte aktuální seznam z úložiště.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

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
