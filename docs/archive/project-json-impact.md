---
title: project.jsdopad na autory balíčku NuGet
description: Podrobnosti o tom, jak implementace project.jsv nástroji NuGet 3. x ovlivňuje autory balíčků, jako jsou nepodporované funkce, obsah a formát balíčku.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 82b7ce7962ecccc9559ae25a8fe35a3820238049
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775394"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Dopad project.jsna při vytváření balíčků

> [!Important]
> Tento obsah je zastaralý. Projekty by měly používat buď `packages.config` formáty PackageReference nebo.

`project.json`Systém použitý v NuGet 3 + má vliv na autory balíčku několika způsoby, jak je popsáno v následujících částech.

## <a name="changes-affecting-existing-packages-usage"></a>Změny ovlivňující existující využití balíčků

Tradiční balíčky NuGet podporují sadu funkcí, které se nepřenášejí do přenosného světa.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Skripty pro instalaci a odinstalaci se ignorují.

Model přenositelných obnovení, který je popsaný v tématu [řešení závislostí](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), nemá koncept "doba instalace balíčku". Balíček je buď přítomen, nebo není přítomen, ale při instalaci balíčku se nevyskytnou žádné konzistentní procesy.

Také je možné nainstalovat skripty pouze v aplikaci Visual Studio. Jiné IDEs muselo napodobovat rozhraní API rozšiřitelnosti sady Visual Studio, aby se pokusilo tyto skripty podporovat, a v běžných editorech a nástrojích příkazového řádku nebyla žádná podpora k dispozici.

### <a name="content-transforms-are-not-supported"></a>Transformace obsahu nejsou podporovány.

Podobně jako při instalaci skriptů se transformace spouští při instalaci balíčku a obvykle se neidempotentní. Vzhledem k tomu, že už není k dispozici žádný čas instalace, transformace XDT a podobné funkce se nepodporují a budou se ignorovat, pokud se takový balíček používá v přenosném scénáři.

### <a name="content"></a>Content

Tradiční balíčky NuGet jsou soubory obsahu, jako je zdrojový kód a konfigurační soubory. Obvykle se používají ve dvou scénářích:

1. Počáteční soubory vynechané do projektu, aby ji uživatel mohl později upravit. Běžným příkladem jsou výchozí konfigurační soubory.

1. Soubory obsahu používané jako doprovodné soubory pro sestavení nainstalovaná v projektu. Příkladem může být obrázek loga používaný sestavením.

Podpora obsahu je v současné době zakázaná pro podobné důvody pro skripty a transformace, ale v procesu navrhování podpory obsahu.

Soubory obsahu je stále možné přenášet uvnitř balíčků a jsou v současné době ignorovány, ale koncový uživatel je stále může zkopírovat do správného místa.

Můžete si prohlédnout jeden z návrhů pro vracení souborů obsahu a postupovat podle jeho průběhu, tady: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627) .

## <a name="impact-for-package-authors"></a>Dopad pro autory balíčku

Balíčky používající výše uvedené funkce by musely použít jiný mechanismus. Nejefektivnějším užitečným mechanismem by byly cíle nebo props nástroje MSBuild, které budou nadále plně podporovány. Systém sestavení se může rozhodnout v balíčku vybrat jiné konvence. To je způsob, jakým jsou podporovány cíle nástroje MSBuild i analyzátory Roslyn. Je možné vytvářet balíčky, které podporují cíle a analyzátory pro `packages.config` scénáře a `project.json` .

Balíčky, které se pokoušejí změnit projekt tak, aby se při spuštění normálně pracovaly v velmi omezené sadě scénářů, a místo toho byste měli zadat soubor Readme nebo pokyny k použití balíčku.

Většina existujících balíčků by neměla vyžadovat použití formátu balíčku popsaného níže.

Formát umožňuje použití nativního obsahu jako první třídy. To znamená, že spravovaná sestavení jsou závislá na konečné implementaci hardwaru pro dodávání binárních implementací společně se spravovanými sestaveními na základě cílové platformy. Například System. IO. Compression balíček tuto technologii využívá. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

V souhrnu Pokud výše uvedené funkce není nezbytně nutné, doporučujeme použít stávající formát balíčku, protože formát, který je zde popsán, je podporován pouze NuGet 3. x +.

Mohli byste sestavit balíčky, které budou fungovat jak pro scénáře, tak i `packages.config` `project.json` přes překrývá se, ale často je jednodušší jenom strukturovat balíčky tradičním způsobem, bez zastaralých funkcí uvedených výše.

## <a name="3x-package-format"></a>3. x – formát balíčku

Formát balíčku 3. x umožňuje několik dalších funkcí mimo NuGet 2. x:

1. Definování referenčního sestavení používaného pro kompilaci a sady implementačních sestavení používaných pro modul runtime na různých platformách/zařízeních. Díky tomu můžete využít výhod rozhraní API specifických pro konkrétní platformu a zároveň zajistit pro svoje zákazníky společnou oblast Surface. Konkrétně to usnadňuje psaní zprostředkujících přenosných knihoven.

1. Umožňuje balíčkům vytvářet na platformách, například operační systémy nebo architektura procesoru.

1. Umožňuje oddělení implementace specifických pro platformu pro doprovodné balíčky.

1. Podpora nativních závislostí jako první občan třídy.
