---
title: Migrace ze souborů package.config do PackageReference formátů
description: Podrobnosti o tom, jak migrovat projekt z formátu souborů package.config správy do PackageReference podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: b05192038bff071ca7a5b8f2e0f735696d09bef6
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508267"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrovat ze souboru packages.config na PackageReference

Visual Studio 2017 verze 15.7 a novějších verzích podporuje migraci projektů z [souboru packages.config](./packages-config.md) správu formát [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formátu.

## <a name="benefits-of-using-packagereference"></a>Výhody použití PackageReference

* **Spravovat všechny závislosti projektu na jednom místě**: stejně jako odkazy typu projekt na projekt a odkazy na sestavení odkazuje na balíček NuGet (pomocí `PackageReference` uzlu) se spravují přímo v rámci souborů projektu, spíše než samostatné soubor Packages.config.
* **Nezahlcený zobrazení nejvyšší úrovně závislosti**: na rozdíl od souboru packages.config, PackageReference uvádí jenom balíčky NuGet v projektu přímo nainstalován. Uživatelské rozhraní Správce balíčků NuGet a soubor projektu nejsou v důsledku toho nepotřebná data, se závislostmi nižší úrovně.
* **Vylepšení výkonu**: při použití PackageReference balíčky jsou zachována ve *global-packages* složky (jak je popsáno na [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md) spíše než v `packages` složky v rámci řešení. PackageReference v důsledku toho provádí rychleji a spotřebovávají méně místa na disku.
* **Jemné kontrolu nad závislostí a obsahu toku**: použití stávajících funkcí nástroje MSBuild umožňuje [podmíněně odkázat na balíček NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) a odkazy na balíček na cílovou architekturu, vyberte konfiguraci platformu, nebo jiné pivotů.
* **PackageReference se aktivně vyvíjí**: viz [PackageReference problémů na Githubu](https://aka.ms/nuget-pr-improvements). soubor Packages.config se už nebude aktivně vyvíjí.

### <a name="limitations"></a>Omezení

* NuGet PackageReference není k dispozici v sadě Visual Studio 2015 a starší. Migrované projektů lze otevřít pouze v sadě Visual Studio 2017.
* Migrace není aktuálně k dispozici pro projekty jazyka C++ a technologií ASP.NET.
* Některé balíčky nemusí být plně kompatibilní s PackageReference. Další informace najdete v tématu [problémy s kompatibilitou balíčků](#package-compatibility-issues).

### <a name="known-issues"></a>Známé problémy

1. `Migrate packages.config to PackageReference...` Možnost není k dispozici v místní nabídce klikněte pravým tlačítkem na 

#### <a name="issue"></a>Problém 
 
Při prvním otevření projektu NuGet nemusí mít inicializace, dokud se provádí operace NuGet. To způsobí, že není uveden v místní nabídce klikněte pravým tlačítkem na možnost migrace `packages.config` nebo `References`. 

#### <a name="workaround"></a>Alternativní řešení 

Proveďte některou z následujících akcí NuGet: 
* Otevřít uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem na `References` a vyberte `Manage NuGet Packages...` 
* Otevřete konzolu Správce balíčků pro - ze `Tools > NuGet Package Manager`vyberte `Package Manager Console` 
* Spuštění obnovení NuGet – klikněte pravým tlačítkem na uzel řešení v Průzkumníku řešení a vyberte `Restore NuGet Packages` 
* Sestavte projekt, který také aktivuje obnovení NuGet 

Teď by měl být vidět možnost migrace. Všimněte si, že tato možnost není podporována a nezobrazí se pro typy projektů ASP.NET a C++. 

## <a name="migration-steps"></a>Kroky migrace

> [!Note]
> Před zahájením migrace, sada Visual Studio vytvoří zálohu projektu, aby bylo možné [vrácení zpět do souboru packages.config](#how-to-roll-back-to-packagesconfig) v případě potřeby.

1. Otevřete řešení obsahující projekt pomocí `packages.config`.

1. V **Průzkumníka řešení**, klikněte pravým tlačítkem na **odkazy** uzlu nebo `packages.config` a vyberte možnost **migrovat packages.config na PackageReference...** .

1. Migrator analyzuje odkazy na balíčky NuGet projektu a pokusí se zařadit do **závislosti nejvyšší úrovně** (balíčky NuGet, které jste nainstalovali přímo) a **přechodné závislosti** (balíčky, které byly nainstalovány jako závislosti balíčků nejvyšší úrovně).

   > [!Note]
   > PackageReference podporuje obnovení přenosných balíčků a řeší závislosti dynamicky, což znamená, že přechodné závislosti nemusí explicitně nainstalována.

1. (Volitelné) Můžete se rozhodnout zacházet se balíček NuGet jsou klasifikovány jako přechodné závislosti jako závislost nejvyšší úrovně tak, že vyberete **nejvyšší úrovně** možnost pro balíček. Tato možnost se automaticky nastaví pro balíčky obsahující prostředky, které nejsou tok přechodně (těm `build`, `buildCrossTargeting`, `contentFiles`, nebo `analyzers` složky) a jsou označeny jako vývojovou závislost (`developmentDependency = "true"`).

1. Kontroly všech [problémy s kompatibilitou balíčků](#package-compatibility-issues).

1. Vyberte **OK** zahájíte migraci.

1. Na konci migrace Visual Studio poskytuje sestavy s cestou k zálohování, seznam nainstalovaných balíčků (závislosti nejvyšší úrovně), seznam balíčků na něho odkazovat jako přechodné závislosti a seznam problémů s kompatibilitou identifikovali na začátku migrace. Sestava je uložena v zálohovací složce.

1. Ověřte, že toto řešení vytvoří a spustí. Pokud narazíte na potíže, [založte problém na Githubu](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Tom, jak vrátit zpět do souboru packages.config

1. Zavřete migrovaného projektu.

1. Zkopírujte soubor projektu a `packages.config` ze zálohy (obvykle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) do složky projektu. Odstraňte složku obj, pokud existuje v kořenovém adresáři projektu.

1. Otevřete projekt.

1. Otevřete konzolu Správce balíčků pro použití **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu nabídky.

1. V konzole spusťte následující příkaz:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problémy s kompatibilitou balíčků

Některé aspekty, které byly k dispozici v souboru packages.config nepodporuje PackageReference. Migrator analyzuje a rozpoznává tyto problémy. Libovolný balíček, který má jeden nebo více z následujících problémů nemusí chovat dle očekávání po migraci.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"install.ps1" skripty jsou ignorovány, pokud je tento balíček nainstaluje po migraci

| | |
| --- | --- |
| **Popis** | S PackageReference install.ps1 a uninstall.ps1 skripty prostředí PowerShell nebudou provedeny během instalace nebo odinstalace balíčku. |
| **Potenciální dopad** | Balíčky, které jsou závislé na tyto skripty pro konfiguraci některých chování v cílový projekt nemusí fungovat podle očekávání. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"obsah" prostředky nejsou k dispozici, když se balíček nainstaluje po migraci

| | |
| --- | --- |
| **Popis** | Prostředky v balíčku `content` složku s PackageReference se nepodporují a budou ignorovány. PackageReference přidává podporu pro `contentFiles` lépe přenositelný podpory a sdíleného obsahu.  |
| **Potenciální dopad** | Prostředky v `content` nejsou zkopírovány do projektu a projekt vyžaduje refaktoring kódu, který závisí na přítomnosti tyto prostředky.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformace XDT se nepoužívají při instalaci balíčku po upgradu

| | |
| --- | --- |
| **Popis** | Transformace XDT nepodporuje PackageReference a `.xdt` souborů jsou ignorovány, pokud instalace nebo odinstalace balíčku.   |
| **Potenciální dopad** | Transformace XDT se nepoužije žádné soubory XML projektu nejčastěji `web.config.install.xdt` a `web.config.uninstall.xdt`, což znamená, že projekt` web.config` soubor není aktualizován při instalaci nebo odinstalaci balíčku. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Sestavení v kořenovém adresáři lib jsou ignorovány, pokud je tento balíček nainstaluje po migraci

| | |
| --- | --- |
| **Popis** | S PackageReference, sestavení k dispozici v kořenovém adresáři `lib` složku bez přípony cílové rozhraní framework konkrétní dílčí složky jsou ignorovány. Vyhledá dílčí složku odpovídající odpovídající cílové rozhraní projektu moniker cílového rozhraní (TFM) a nainstaluje odpovídající sestavení do projektu NuGet. |
| **Potenciální dopad** | Balíčky, které nemají odpovídající moniker cílového rozhraní (TFM) odpovídající cílové rozhraní projektu podsložku nemusí chovat dle očekávání po přechodu nebo selhání instalace během migrace |

## <a name="found-an-issue-report-it"></a>Najít chyby? Nahlaste to!

Pokud narazíte na potíže s prostředím migrace, [založit problém na úložiště NuGet GitHub](https://github.com/NuGet/Home/issues/).
