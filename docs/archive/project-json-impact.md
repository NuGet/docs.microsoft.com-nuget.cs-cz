---
title: Project.JSON dopad na autoři balíček NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Podrobnosti o tom, jak implementace project.json v NuGet 3.x ovlivňuje balíček autoři, jako je například nepodporované funkce, obsahu a formátu balíčku.
keywords: Balíček NuGet a project.json, project.json dopad vytváření aspekty, project.json funkce
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6e8af98504a2866106e84943989aeb91f2e9c1fb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Dopad project.json při vytváření balíčků

> [!Important]
> Tento obsah je zastaralý. Projekty využít buď `packages.config` nebo PackageReference formáty.

`project.json` Systém používaný v NuGet 3 + ovlivňuje balíček autoři několika způsoby, jak je popsáno v následujících částech.

## <a name="changes-affecting-existing-packages-usage"></a>Změny, které mají vliv na použití existujícího balíčky

Tradiční balíčky NuGet podporovat sadu funkcí, které nejsou přenášejí do přenositelné world.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Instalace a odinstalace skripty jsou ignorovány.

Model obnovení přenositelné popsané v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), nemá koncept "čas instalace balíčku". Balíček není přítomen nebo není přítomné, ale neexistuje žádný konzistentní proces, který nastane, když je balíček nainstalován.

Navíc instalace skripty byly podporovány pouze v sadě Visual Studio. Další integrovaného vývojového prostředí měla model rozšiřitelnosti Visual Studio rozhraní API se pokusit o podporu takové skripty a bez podpory nebylo k dispozici v běžné editory a nástroje příkazového řádku.

### <a name="content-transforms-are-not-supported"></a>Transformace obsahu nejsou podporovány.

Podobně jako nainstaluje skripty, transformací spustit na balíček nainstalovat a nejsou obvykle idempotent. Vzhledem k tomu, že už žádný čas instalace se transformace XDT a podobné funkce nejsou podporovány a jsou ignorovány, pokud takové balíčku se používá ve scénáři přenositelné.

### <a name="content"></a>Obsah

Tradiční balíčky NuGet jsou distribuovat soubory obsahu, jako je například zdrojového kódu a konfigurační soubory. Zde jsou obvykle se používá ve dvou scénářích:

1. Počáteční soubory vyřadit do projektu, takže uživatel může upravit později. Častým příkladem je výchozí konfigurační soubory.

1. Soubory obsahu použít jako companions na sestavení nainstalované v projektu. V příkladu v tomto poli může být obrázek loga používané sestavení.

Podpora pro obsah je nyní zakázána pro podobné důvody pro skripty a transformace, ale Snažíme se vyřešit navrhování podporu pro obsah.

Obsah souborů se dá pořád provést uvnitř balíčky a ignorují aktuálně, ale koncový uživatel kopírovat je na správné místo.

Najdete v jednom návrhů přináší zpět soubory obsahu a postupujte podle jeho průběh zde: [ https://github.com/NuGet/Home/issues/627 ](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Dopad pro autory balíčku

Balíčky pomocí výše uvedené funkce muset použít jiný mechanismus. Nejčastěji užitečné mechanismus by MSBuild cíle nebo props, které nadále získat plně podporované. Můžete zvolit systém sestavení vyzvedávat další konvence v balíčku. Toto je, jak jsou podporovány cíle MSBuild a také Roslyn analyzátorů. Je možné vytvořit balíčky, které podporuje cíle a analyzátory pro `packages.config` a `project.json` scénáře.

Balíčky, které se pokusí změnit projekt, který má obvykle usnadňují spuštění ve velmi omezená sada scénářů fungovat a musí místo toho zadejte readme nebo pokyny o tom, jak pomocí balíčku.

Většina stávajících balíčků by neměl muset použít formát balíčku, který je popsaný níže.

Formát umožňuje nativní obsah jako první třídy scénáře. To znamená, že spravovaná sestavení závisí na blízko implementace hardwaru pro odeslání binární implementace spolu s spravované sestavení založená na cílové platformy. System.IO.Compression balíčku je třeba využitím této technologie. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

V souhrnu Pokud funkci výše není nezbytně nutné, doporučujeme provedením vykrvovacího vpichu s formátem existující balíček jako formát popsaný v tomto poli je podporován pouze NuGet 3.x+.

Je možné vytvořit balíčky pro obě `packages.config` a `project.json` scénáře prostřednictvím shimming, ale je často jednodušší právě struktury balíčky tradičním způsobem, bez zastaralých funkcí uvedených výše.

## <a name="3x-package-format"></a>Formát balíčku 3.x

Formát balíčku 3.x umožňuje několika další funkce nad rámec NuGet 2.x:

1. Definování referenční sestavení používá pro kompilaci a sadu sestavení implementace používá pro modul runtime na různých platformách nebo zařízení. Která umožňuje využít výhod platformy konkrétní rozhraní API při současném poskytování běžné útoku pro uživatele. Konkrétně to usnadňuje vytváření zprostředkující přenosné knihovny jednodušší.

1. Umožňuje balíčky do otáčení na platformách, například operační systémy nebo architekturu procesoru.

1. Umožňuje oddělení platformy konkrétní implementace doprovodné balíčky.

1. Jako první třídy občanem podporují nativní závislosti.
