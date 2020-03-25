---
title: Zpráva k vydání verze NuGet 5,5
description: Poznámky k verzi pro NuGet 5,5, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148295"
---
# <a name="nuget-55-release-notes"></a>Zpráva k vydání verze NuGet 5,5

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v sadě .NET SDK|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core

## <a name="summary-whats-new-in-55"></a>Shrnutí: Novinky v 5,5

* Vylepšené možnosti usnadnění přístupu a čtečky obrazovky pro uživatelské rozhraní Správce balíčků NuGet v aplikaci Visual Studio
    * Problémy s přístupností v prostředí čtečky obrazovky, chybějící altText a přístupný název pro nainstalované textové pole atd. [#9059](https://github.com/NuGet/Home/issues/9059)
    * Problémy s přístupností v prostředí čtečky obrazovky v seznamu balíčků – [#9077](https://github.com/NuGet/Home/issues/9077)
    * Problémy s přístupností v prostředí čtečky obrazovky související s kartami "Procházet", "instalace", "aktualizace" – [#9078](https://github.com/NuGet/Home/issues/9078)
    * Narrator neoznamuje "prázdné", "No Dependencies", "NuGet. org", "MIT" popisek odkazu [#9157](https://github.com/NuGet/Home/issues/9157)

* Podpora pro zpřístupnění samostatné ikony v uživatelském rozhraní Správce balíčků sady Visual Studio pro balíčky hostované v místních informačních kanálech – [#8189](https://github.com/NuGet/Home/issues/8189)

* Výrazně se zvýšil výkon při obnovení no-op pomocí `RestoreUseStaticGraphEvaluation`, které urychlují hodnocení voláním rozhraní API statického grafu nástroje MSBuild – [8791](https://github.com/NuGet/Home/issues/8791)

* Vylepšená funkce dotnet. exe při ověřování pomocí modulů plug-in pro různé platformy
    * selhání dotnet restore s TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Modul plug-in: úloha byla zrušena. došlo k problému s ověřováním ADO. - [#8528](https://github.com/NuGet/Home/issues/8528)

* Přidat `dotnet nuget <add|remove|update|disable|enable|list> source` příkaz- [#4126](https://github.com/NuGet/Home/issues/4126)

* Podpory for `--skip-duplicate` pomocí příkazu dotnet NuGet push- [#8778](https://github.com/NuGet/Home/issues/8778)

* Podpora `packages.config` s MSBuild/Restore – [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Štěnic**

* Opětovné fungování samoobslužné aktualizace s rozhraními API V3- [#4197](https://github.com/NuGet/Home/issues/4197)

* Nesprávná verze závislostí balíčku, pokud je verze závislosti balíčku nastavená na *- [#6697](https://github.com/NuGet/Home/issues/6697)

* ErrorUnsafePackageEntry chybové zprávy neukazují na zdroj potíží – [#7505](https://github.com/NuGet/Home/issues/7505)

* Soubor zámku se nedodržuje ve scénářích "*" – [#8073](https://github.com/NuGet/Home/issues/8073)

* Nástroj NuGet. exe neumožňuje překládat na nejnovější verzi balíčku při použití * v PackageReference (MSBuild/dotnet/VS Restore) – [#8432](https://github.com/NuGet/Home/issues/8432)

* balíček seznamu dotnet s cíleným projektem WPF – [#8463](https://github.com/NuGet/Home/issues/8463)

* Zvýšení ConcurrencyUtilities (snížení využití CPU) – [#8653](https://github.com/NuGet/Home/issues/8653)

* Specifikace DG pro Neuvolněné projektové scénáře by se neměly zapisovat do obnovení verze Preview- [#8793](https://github.com/NuGet/Home/issues/8793)

* Balíčky NuGet sady Visual Studio (RestoreManagerPackage) musí automaticky načíst při událostech sestavení řešení – [#8796](https://github.com/NuGet/Home/issues/8796)

* Zablokování v VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)

* Sada nástrojů VisualStudio není naplněna z balíčku NuGet, pokud je projekt umístěn ve složce řešení – [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: obnovení řešení se trvale nezdařilo z důvodu konfliktu časování – [#8881](https://github.com/NuGet/Home/issues/8881)

* Konstanta "načítání.." na nainstalované kartě a "hledání <term>.. "na kartě aktualizace – [#8890](https://github.com/NuGet/Home/issues/8890)

* Chybějící vložené ikony v uživatelském rozhraní VS PM po vypršení platnosti mezipaměti – [#9069](https://github.com/NuGet/Home/issues/9069)

* Spuštění uživatelského rozhraní FireAndForget PM – [#9112](https://github.com/NuGet/Home/issues/9112)

* Obnovení: implementace IncludeExcludeFiles. Equals (...) je nesprávná – [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore: PackageSpec. Clone () vytvoří neshodnou kopii [#9211](https://github.com/NuGet/Home/issues/9211)

* Seznam chyb zobrazený, přestože při dokončení sestavení s chybami není zaškrtnuto- [#8190](https://github.com/NuGet/Home/issues/8190) "Always show seznam chyb

* Statické obnovení grafu by nemělo předávat prázdné SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061)

* Obnovení: vypočítáno uzavření pro každý projekt 4 časy – [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore: DependencyGraphSpec. Load (...) nepotřebuje JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* Obnovení: velké řetězce vytvořené v haldě pro velké objekty (LOH) – [#9031](https://github.com/NuGet/Home/issues/9031)

* Vlastní nástroj NuGet. exe na novější mono může být přerušený kvůli Překladači sady MSBuild SDK – [8848](https://github.com/NuGet/Home/issues/8848)

* obnovení se nepovede, když NuGet. argument dgspec. JSON používá jiný proces – [8692](https://github.com/NuGet/Home/issues/8692) .

**Chcete odeslat obecnou**

* Logika v _GetRestoreProjectStyle musí být v rámci úlohy – [#8804](https://github.com/NuGet/Home/issues/8804)

* Ve výchozím nastavení přidejte informace o zastaralosti na kartě installed – [#8541](https://github.com/NuGet/Home/issues/8541)

**[Seznam všech problémů opravených v této verzi – 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
