---
title: Migrace z package.config na PackageReference formáty
description: Podrobnosti o tom, jak migrovat projektu z formátu package.config správy do PackageReference podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: e0a4363a2807874ec8e2693c5b1c1a0eb2e8af0e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818783"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrovat ze souboru packages.config PackageReference

Visual Studio 2017 verze 15.7 Preview 3 a novějších verzích podporuje migraci z projektu [packages.config](./packages-config.md) správu formát, který se [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formátu.

## <a name="benefits-of-using-packagereference"></a>Výhody použití PackageReference

* **Spravovat všechny závislosti projektu na jednom místě**: stejně jako odkazy na projekt na projekt a odkazy na sestavení, odkazuje na balíček NuGet (pomocí `PackageReference` uzlu) spravuje přímo v rámci soubory projektu, nikoli pomocí samostatné soubor Packages.config.
* **Přeplněná zobrazení nejvyšší úrovně závislosti**: na rozdíl od souboru packages.config, PackageReference uvádí jenom tyto balíčky NuGet, které jsou přímo nainstalované v projektu. V důsledku toho uživatelského rozhraní Správce balíčků NuGet a soubor projektu nejsou zaplněny závislosti nižší úrovně.
* **Vylepšení výkonu**: při použití PackageReference, balíčky jsou zachována ve *globální balíčky* složky (jak je popsáno na [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md) spíše než v `packages` složku v rámci řešení. V důsledku toho PackageReference rychlejší a odebírá méně místa na disku.
* **Přesně řídit závislosti a obsahu toku**: použití stávajících funkcí nástroje MSBuild umožňuje [podmíněně odkazují na balíček NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) a vyberte balíček odkazuje na cílové rozhraní, konfiguraci, platformy, nebo jiné pivotů.
* **PackageReference je ve vývoji active**: najdete v části [PackageReference problémy na Githubu](https://aka.ms/nuget-pr-improvements). soubor Packages.config se už vyvíjí aktivní.

### <a name="limitations"></a>Omezení

* NuGet PackageReference není k dispozici v sadě Visual Studio 2015 a starší. Migrované projekty může otevřít pouze v Visual Studio 2017.
* Migrace není aktuálně k dispozici pro projekt C++ a ASP.NET.
* Některé balíčky nemusí být plně kompatibilní s PackageReference. Další informace najdete v tématu [balíček problémy s kompatibilitou](#package-compatibility-issues).

### <a name="known-issues"></a>Známé problémy

1. `Migrate packages.config to PackageReference...` Možnost není dostupná v místní nabídce klikněte pravým tlačítkem na 

#### <a name="issue"></a>Problém 
 
Při prvním otevření projektu, nemusí mít NuGet inicializovat, dokud nebude provedena operace NuGet. To způsobí, že není zobrazena v místní nabídce klikněte pravým tlačítkem na možnost migrace `packages.config` nebo `References`. 

#### <a name="workaround"></a>Alternativní řešení 

Či kterékoli z následujících akcí NuGet: 
* Otevřete uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem na `References` a vyberte `Manage NuGet Packages...` 
* Otevřete konzolu Správce balíčků - z `Tools > NuGet Package Manager`, vyberte možnost `Package Manager Console` 
* Spuštění obnovení NuGet - klikněte pravým tlačítkem na uzel řešení v Průzkumníku řešení a vyberte `Restore NuGet Packages` 
* Sestavte projekt, který také aktivuje obnovení NuGet 

Teď by měla být moci zobrazit možnost migrace. Všimněte si, že tato možnost není podporována a nezobrazí se pro typy projektů ASP.NET a C++. 

## <a name="migration-steps"></a>Kroky migrace

> [!Note]
> Před zahájením migrace, Visual Studio vytvoří zálohu projektu umožňují [vrácení zpět do souboru packages.config](#how-to-roll-back-to-packagesconfig) v případě potřeby.

1. Otevřete řešení obsahující projekt pomocí `packages.config`.

1. V **Průzkumníku řešení**, klikněte pravým tlačítkem na **odkazy** uzlu nebo `packages.config` soubor a vyberte **migrovat souboru packages.config PackageReference...** .

1. Migrator analyzuje odkazy na balíček NuGet projektu a pokusí se zařadit do **nejvyšší úrovně závislosti** (balíčky NuGet tento adresář můžete nainstalovat) a **přenositelné závislosti**(balíčky, které byly nainstalovány jako závislých součástí pro balíčky nejvyšší úrovně).

   > [!Note]
   > PackageReference podporuje obnovení přenositelné balíčku a přeloží závislosti dynamicky, což znamená, že explicitně nemusí nainstalované přenositelné závislosti.

1. (Volitelné) Můžete se rozhodnout zacházet s balíčku NuGet jsou klasifikovány jako závislost přenositelné jako závislost nejvyšší úrovně výběrem **nejvyšší úrovně** možnost pro balíček. Tato možnost bude automaticky nastavena pro balíčky, které obsahují prostředky, které není toku přechodně (ty v `build`, `buildCrossTargeting`, `contentFiles`, nebo `analyzers` složky) a ty označen jako závislost vývoj (`developmentDependency = "true"`).

1. Zkontrolujte všechny [balíček problémy s kompatibilitou](#package-compatibility-issues).

1. Vyberte **OK** zahájíte migrace.

1. Na konci migrace Visual Studio poskytuje sestavy s cestou k zálohování, seznam balíčků nainstalovaných (nejvyšší úrovně závislosti), seznam balíčků na něj odkazuje jako přenositelné závislosti a seznam na začátku identifikovat problémy s kompatibilitou migrace. Sestava je uložena v zálohovací složce.

1. Ověřte, zda řešení vytvoří a spustí. Pokud narazíte na potíže, [souboru problém na Githubu](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Postup vrácení souboru Packages.config je.

1. Zavřete migrované projektu.

1. Zkopírujte soubor projektu a `packages.config` ze zálohy (obvykle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) ke složce projektu. Odstraňte složku obj, pokud existuje v kořenovém adresáři projektu.

1. Otevřete projekt.

1. Otevřete konzolu Správce balíčků pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu nabídky.

1. V konzole, spusťte následující příkaz:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problémy s kompatibilitou balíčku

PackageReference nepodporuje některé aspekty, které byly k dispozici v souboru Packages.config je. Migrator analyzuje a zjistí tyto problémy. Všechny balíček, který má jeden nebo více z následujících důvodů nefungují dle očekávání po migraci.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"install.ps1" skripty jsou ignorovány, při instalaci balíčku po migraci

| | |
| --- | --- |
| **Popis** | S PackageReference nejsou při instalování nebo odinstalování balíčku provést install.ps1 a uninstall.ps1 skriptů prostředí PowerShell. |
| **Potenciální dopad** | Balíčky, které jsou závislé na tyto skripty ke konfiguraci některých chování v cílovém projektu nemusí fungovat podle očekávání. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"obsah" prostředky nejsou k dispozici při instalaci balíčku po migraci

| | |
| --- | --- |
| **Popis** | Prostředky v balíčku na `content` složky nejsou podporovány s PackageReference a budou ignorovány. PackageReference přidává podporu pro `contentFiles` lépe přenositelné podporu a sdíleného obsahu.  |
| **Potenciální dopad** | Prostředky v `content` nebudou zkopírovány do projekt a projekt vyžaduje refaktoring kód, který závisí na přítomnost tyto prostředky.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Při instalaci balíčku po upgradu neaplikují XDT transformací

| | |
| --- | --- |
| **Popis** | Transformace XDT nepodporuje PackageReference a `.xdt` soubory jsou při instalování nebo odinstalování balíčku ignorovány.   |
| **Potenciální dopad** | Transformace XDT nejsou použity pro všechny soubory XML projektu nejčastěji `web.config.install.xdt` a `web.config.uninstall.xdt`, což znamená, že projektu` web.config` souboru nebudou aktualizovány, jestliže tento balíček je nainstalována nebo odinstalována. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Při instalaci balíčku po migraci jsou ignorovány sestavení v kořenovém adresáři lib

| | |
| --- | --- |
| **Popis** | Sestavení s PackageReference, k dispozici v kořenovém adresáři `lib` bez cílový framework konkrétní dílčí složku složky jsou ignorovány. NuGet hledá podsložky odpovídající odpovídající cílový framework projektu na Přezdívka cílový framework (TFM) a nainstaluje odpovídající sestavení do projektu. |
| **Potenciální dopad** | Balíčky, které nemají odpovídající Přezdívka cílový framework (TFM) odpovídající cílový framework projektu na podsložku nemusí chovat podle očekávání po přechodu nebo selhání instalace během migrace |

## <a name="found-an-issue-report-it"></a>Našel problém? Nahlaste to!

Pokud narazíte na potíže s prostředím migrace, [souborů problém v úložišti NuGet GitHub](https://github.com/NuGet/Home/issues/).
