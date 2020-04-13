---
title: project.json dopad na autory balíčků NuGet
description: Podrobnosti o tom, jak implementace project.json v NuGet 3.x ovlivňuje autory balíčků, jako jsou nepodporované funkce, obsah a formát balíčku.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488200"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Dopad souboru project.json při vytváření balíčků

> [!Important]
> Tento obsah je zastaralé. Projekty by `packages.config` měly používat formáty nebo PackageReference.

Systém `project.json` používaný v NuGet 3+ ovlivňuje autory balíčků několika způsoby, jak je popsáno v následujících částech.

## <a name="changes-affecting-existing-packages-usage"></a>Změny ovlivňující použití existujících balíčků

Tradiční balíčky NuGet podporují sadu funkcí, které nejsou přeneseny do přenosného světa.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Instalace a odinstalace skriptů jsou ignorovány

Model přenosnéobnovení, popsané v [rozlišení závislostí](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), nemá koncept "čas instalace balíčku". Balíček je k dispozici nebo není k dispozici, ale neexistuje žádný konzistentní proces, ke kterému dochází při instalaci balíčku.

Instalační skripty byly také podporovány pouze v sadě Visual Studio. Ostatní IDC musel zesměšňovat rozhraní API rozšiřitelnosti sady Visual Studio k pokusu o podporu těchto skriptů a žádná podpora byla k dispozici v běžných editorů a nástrojů příkazového řádku.

### <a name="content-transforms-are-not-supported"></a>Transformace obsahu nejsou podporovány.

Podobně jako instalační skripty, transformace spustit při instalaci balíčku a obvykle nejsou idempotentní. Vzhledem k tomu, že již neexistuje žádný čas instalace, XDT Transformace a podobné funkce nejsou podporovány a jsou ignorovány, pokud takový balíček se používá v přenositelném scénáři.

### <a name="content"></a>Obsah

Tradiční balíčky NuGet jsou odesílání souborů obsahu, jako je zdrojový kód a konfigurační soubory. Obvykle se používají ve dvou scénářích:

1. Počáteční soubory klesly do projektu, takže uživatel může upravit později. Běžným příkladem jsou výchozí konfigurační soubory.

1. Soubory obsahu používané jako doprovodné sestavení nainstalovaných v projektu. Příkladem zde by byl obrázek loga používaný sestavením.

Podpora obsahu je v současné době zakázána z podobných důvodů pro skripty a transformace, ale jsme v procesu navrhování podpory obsahu.

Soubory obsahu mohou být stále přenášeny uvnitř balíčků a jsou v současné době ignorovány, ale koncový uživatel je stále může zkopírovat na správné místo.

Můžete vidět jeden z návrhů na vrácení souborů obsahu a sledovat [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)jeho průběh, zde: .

## <a name="impact-for-package-authors"></a>Dopad pro autory balíčků

Balíčky používající výše uvedené funkce by musely používat jiný mechanismus. Nejčastěji užitečný mechanismus pro to by msbuild cíle nebo rekvizity, které i nadále získat plně podporovány. Systém sestavení můžete zvolit vyzvednout další konvence v balíčku. Tímto způsobem jsou podporovány cíle MSBuild a analyzátory Roslyn. Je možné vytvářet balíčky, které `packages.config` podporuje `project.json` cíle a analyzátory pro a scénáře.

Balíčky, které se pokoušejí upravit projekt pro usnadnění spuštění obvykle pracovat ve velmi omezené sadě scénářů a místo toho by měly poskytnout soubor readme nebo pokyny, jak použít balíček.

Většina existujících balíčků by neměla používat formát balíčku popsaný níže.

Formát umožňuje nativní obsah jako scénář první třídy. To znamená, že spravovaná sestavení závisí na implementacich v blízkosti hardwaru pro dodávku binárních implementací spolu se spravovanými sestaveními založenými na cílové platformě. Například System.IO.Compression balíček využívá tuto technologii. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Stručně řečeno, pokud výše uvedené funkce není nezbytně nutné, doporučujeme držet se stávající formát balíčku, jako formát popsaný zde je podporován pouze NuGet 3.x +.

Bylo by možné vytvářet balíčky `packages.config` `project.json` pro práci pro oba a scénáře prostřednictvím shimming, ale je to často jednodušší jen strukturovat balíčky tradičním způsobem, bez zastaralé funkce uvedené výše.

## <a name="3x-package-format"></a>Formát balíčku 3.x

Formát balíčku 3.x umožňuje několik dalších funkcí mimo NuGet 2.x:

1. Definování referenčnísestavení používané pro kompilaci a sadu sestavení implementace používané pro runtime na různých platformách nebo zařízeních. Což vám umožní využít výhod specifických pro platformu API a zároveň poskytuje společnou plochu pro vaše spotřebitele. Konkrétně to usnadňuje psaní zprostředkujících přenosných knihoven.

1. Umožňuje, aby se balíčky otáčely na platformách, například na operačních systémech nebo architektuře procesoru.

1. Umožňuje oddělení implementace specifické pro platformu doprovodné balíčky.

1. Podpora nativní závislosti jako prvotřídní občan.
