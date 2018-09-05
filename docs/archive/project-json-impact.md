---
title: dopad Project.JSON autory balíčku NuGet
description: Podrobnosti o jak provádění project.json v NuGet 3.x ovlivňuje balíček autoři, jako jsou nepodporované funkce, obsah a formát balíčků.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 8c85c1a89469c491c6be1f81961197450744349c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545570"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Dopad project.json při vytváření balíčků

> [!Important]
> Tento obsah je zastaralý. Projekty by měl použít buď `packages.config` nebo PackageReference formátů.

`project.json` Systému NuGet 3 + ovlivňuje autory balíčku několika způsoby, jak je popsáno v následujících částech.

## <a name="changes-affecting-existing-packages-usage"></a>Změny ovlivňující existující balíčky využití

Tradiční balíčky NuGet podporují sadu funkcí, které nejsou přeneseny do světa tranzitivní.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Instalace a odinstalace skripty jsou ignorovány.

Model tranzitivní obnovení, je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), nemá koncept "čas instalace balíčku". Balíček je k dispozici nebo není k dispozici, ale neexistuje žádný konzistentní proces, ke které dojde při instalaci balíčku.

Také nainstalujte skripty byly podporovány pouze v sadě Visual Studio. Jiná Integrovaná vývojová prostředí museli napodobení rozšiřitelnost sady Visual Studio rozhraní API, pokusí se podporují tyto skripty a bez podpory nebyl k dispozici v běžných editorů a nástroje příkazového řádku.

### <a name="content-transforms-are-not-supported"></a>Transformace obsahu nejsou podporovány.

Podobně jako u skriptů instalace, transformace spustit na balíček nainstalovat a obvykle nejsou idempotentní. Protože neexistuje žádný čas instalace už, XDT transformaci a podobné funkce nejsou podporované a jsou ignorovány, pokud takové balíčku se používá v případě přechodné.

### <a name="content"></a>Obsah

Tradiční balíčky NuGet dodávají soubory obsahu, jako je zdrojový kód a konfigurační soubory. Zde jsou obvykle nepoužívá ve dvou scénářích:

1. Počáteční soubory přetáhnout do projektu, aby uživatel mohl upravit později. Běžným příkladem je výchozí konfigurační soubory.

1. Soubory obsahu použít jako companions pro sestavení nainstalovaná v projektu. Tento příklad by obrázek loga používané sestavení.

Podpora pro obsah je aktuálně zakázáno podobné z důvodů pro skripty a transformace, ale Připravujeme k navrhování podpory pro obsah.

Obsah souborů stále se dá provést uvnitř balíčky a ignorují aktuálně, ale koncový uživatel může stále zkopírují se do správné místo.

Můžete sledovat některé návrhy přináší zpět soubory obsahu a postupujte podle jeho průběh, tady: [ https://github.com/NuGet/Home/issues/627 ](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Dopad pro autory balíčku

Balíčky pomocí výše uvedené funkce byste měli používat jiný mechanismus. Nejčastěji užitečné mechanismus by nástroj MSBuild cíle/vlastnosti, které nadále Získejte plnou podporu. Systém sestavení můžete ke sbírání jiné konvence v balíčku. To je, jak jsou cíle nástroje MSBuild podporované a také analyzátory Roslyn. Je možné sestavovat balíčky, které podporuje cíle a analyzátory pro `packages.config` a `project.json` scénáře.

Balíčky, které se pokusí změnit projekt k usnadnění spuštění obvykle fungují v velmi omezená sada scénářů a by měl místo toho zadejte soubor readme nebo pokyny o tom, jak pomocí balíčku.

Většina stávajících balíčků by neměl muset použít balíček formátu popsaném níže.

Formát umožňuje nativní obsah jako první třídy scénář. To znamená, že spravovaná sestavení závisí na blízko hardwaru implementace dodávat binární implementace spolu s spravovaná sestavení založené na cílové platformě. Třeba balíček System.IO.Compression využívá tuto technologii. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

V souhrnu Pokud výše uvedené funkce není nezbytně nutné, doporučujeme nastolit existující balíček formátu, formátu popsaném tady podporuje pouze NuGet 3.x+.

Je možné vytvořit balíčky pro obě `packages.config` a `project.json` scénáře prostřednictvím překrývá se, ale často je jednodušší právě strukturovat balíčky tradičním způsobem, bez zastaralých funkcí uvedených výše.

## <a name="3x-package-format"></a>Formát balíčku 3.x

Formát balíčku 3.x umožňuje některé další funkce nad rámec NuGet 2.x:

1. Definování referenční sestavení při kompilaci a sadu sestavení implementace používá pro modul runtime na různých platformách a zařízeních. Tomu můžete využít výhod platformy konkrétní rozhraní API poskytuje běžné plochy pro vaše zákazníky. Konkrétně to usnadňuje vytváření zprostředkující přenosné knihovny jednodušší.

1. Umožňuje balíčky zaměření na platformách, například operační systémy nebo architekturu procesoru.

1. Umožňuje oddělit implementace pro konkrétní platformy doprovodná balíčků.

1. Nativní závislosti služeb podpory jako doma.
