---
title: Migrace z packages.config na formáty PackageReference
description: Podrobnosti o tom, jak migrovat projekt z formátu správy packages.config do PackageReference, jak je podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8161f4a39d4adfdb9efb25bcb840b20b85a58e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774784"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrace z packages.config na PackageReference

Visual Studio 2017 verze 15,7 a novější podporuje migraci projektu z formátu správy [packages.config](../reference/packages-config.md) do formátu [PackageReference](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Výhody použití PackageReference

* **Spravovat všechny závislosti projektu na jednom místě**: stejně jako odkazy na projekt a odkazy na sestavení, odkazy na balíček NuGet (pomocí `PackageReference` uzlu) se spravují přímo v souborech projektu místo použití samostatného souboru packages.config.
* **Nepotřebné zobrazení závislostí nejvyšší úrovně**: na rozdíl od packages.config vypíše PackageReference jenom balíčky NuGet, které jste přímo nainstalovali v projektu. V důsledku toho uživatelské rozhraní Správce balíčků NuGet a soubor projektu nejsou v závislosti na nižší úrovni nepotřebné.
* **Vylepšení výkonu**: při použití PackageReference jsou balíčky udržovány ve složce *Global-Packages* (jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md) , nikoli ve `packages` složce v rámci řešení. V důsledku toho PackageReference provádí rychlejší a spotřebovává méně místa na disku.
* **Přesnější řízení závislostí a toku obsahu**: pomocí existujících funkcí nástroje MSBuild můžete [podmíněně odkazovat na balíček NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) a vybrat odkazy na balíčky pro cílovou architekturu, konfiguraci, platformu nebo jiné pivoty.
* **PackageReference je v aktivním vývoji**: viz [problémy PackageReference na GitHubu](https://aka.ms/nuget-pr-improvements). packages.config už není v aktivním vývoji.

### <a name="limitations"></a>Omezení

* V aplikaci Visual Studio 2015 a starší není PackageReference NuGet k dispozici. Migrované projekty lze otevřít pouze v aplikaci Visual Studio 2017 nebo novější.
* Migrace není aktuálně k dispozici pro projekty v jazyce C++ a ASP.NET.
* Některé balíčky nemusí být plně kompatibilní s PackageReference. Další informace najdete v tématu [problémy s kompatibilitou balíčků](#package-compatibility-issues).

Kromě toho existují určité rozdíly v tom, jak PackageReferences funguje v porovnání s packages.config. Například [verze upgradu s omezením](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) nejsou supprted pomocí PackageReference, ale přidávají podporu pro [plovoucí verze](../consume-packages/package-references-in-project-files.md#floating-versions).

### <a name="known-issues"></a>Známé problémy

1. Tato `Migrate packages.config to PackageReference...` možnost není k dispozici v místní nabídce kliknutím pravým tlačítkem myši. 

#### <a name="issue"></a>Problém 
 
Při prvním otevření projektu se nemusí NuGet inicializovat, dokud se neprovede operace NuGet. To způsobí, že se možnost migrace nebude zobrazovat v místní nabídce klikněte pravým tlačítkem myši na `packages.config` nebo `References` . 

#### <a name="workaround"></a>Alternativní řešení 

Proveďte jednu z následujících akcí NuGet: 
* Otevřete uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem na `References` a vyberte `Manage NuGet Packages...` 
* Otevřete konzolu Správce balíčků – v `Tools > NuGet Package Manager` Vyberte `Package Manager Console` 
* Spustit obnovení NuGet – pravým tlačítkem myši klikněte na uzel řešení v Průzkumník řešení a vyberte `Restore NuGet Packages` 
* Sestavení projektu, který také aktivuje obnovení NuGet 

Nyní byste měli být schopni zobrazit možnost migrace. Všimněte si, že tato možnost není podporovaná a nebude se zobrazovat pro typy projektů ASP.NET a C++. 

## <a name="migration-steps"></a>Kroky migrace

> [!Note]
> Před zahájením migrace vytvoří Visual Studio zálohu projektu, abyste v případě potřeby mohli [vrátit zpět na packages.config](#how-to-roll-back-to-packagesconfig) .

1. Otevřete řešení obsahující projekt pomocí `packages.config` .

1. V **Průzkumník řešení** klikněte pravým tlačítkem myši na uzel **odkazy** nebo na `packages.config` soubor a vyberte **migrovat packages.config na PackageReference...**.

1. Migrace analyzuje odkazy na balíček NuGet projektu a pokusy o jejich kategorizaci do **závislostí na nejvyšší úrovni** (balíčky NuGet, které jste nainstalovali přímo), a **přenosných závislostí** (balíčky, které byly nainstalovány jako závislosti balíčků nejvyšší úrovně).

   > [!Note]
   > PackageReference podporuje dynamické obnovení a překládání závislostí, což znamená, že přenositelné závislosti není nutné instalovat explicitně.

1. Volitelné Můžete se rozhodnout zacházet s balíčkem NuGet klasifikovaným jako tranzitivní závislost jako se závislostí na nejvyšší úrovni, a to tak, že vyberete možnost **nejvyšší úrovně** pro balíček. Tato možnost je automaticky nastavena pro balíčky obsahující prostředky, které nezpůsobují průjezd (ty v `build` složkách, `buildCrossTargeting` , `contentFiles` nebo `analyzers` ), a ty, které jsou označeny jako závislost pro vývoj ( `developmentDependency = "true"` ).

1. Projděte si všechny [problémy s kompatibilitou balíčku](#package-compatibility-issues).

1. Kliknutím na **OK** zahajte migraci.

1. Na konci migrace poskytuje Visual Studio zprávu s cestou k zálohování, seznam nainstalovaných balíčků (závislostí nejvyšší úrovně), seznam balíčků, na které se odkazuje jako na přenositelné závislosti, a seznam problémů s kompatibilitou zjištěných na začátku migrace. Sestava se uloží do zálohovací složky.

1. Ověřte, že řešení sestavuje a spouští. Pokud narazíte na problémy, zapište [problém na GitHubu](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Jak se vrátit zpět k packages.config

1. Zavřete migrovaný projekt.

1. Zkopírujte soubor projektu a `packages.config` ze zálohy (obvykle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\` ) do složky projektu. Odstraňte složku obj, pokud existuje v kořenovém adresáři projektu.

1. Otevřete projekt.

1. Otevřete konzolu Správce balíčků pomocí **nástrojů > správce balíčků NuGet > konzole správce balíčků** .

1. V konzole spusťte následující příkaz:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Vytvoření balíčku po migraci

Po dokončení migrace doporučujeme přidat odkaz na balíček NuGet [. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) a pak pomocí nástroje [MSBuild-t:Pack](../reference/msbuild-targets.md#pack-target) vytvořit balíček. I když v některých scénářích můžete použít `dotnet.exe pack` místo `msbuild -t:pack` , nedoporučuje se.

## <a name="package-compatibility-issues"></a>Problémy s kompatibilitou balíčků

Některé aspekty, které byly podporovány v packages.config, nejsou v PackageReference podporovány. Migrace analyzuje a detekuje takové problémy. Každý balíček, který má jeden nebo více následujících problémů, se nemusí po migraci chovat podle očekávání.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Při instalaci balíčku po migraci se skripty "install.ps1" ignorují.

| | |
| --- | --- |
| **Popis** | Při instalaci nebo odinstalaci balíčku se pomocí PackageReference nespustí skripty PowerShellu pro install.ps1 a uninstall.ps1. |
| **Potenciální dopad** | Balíčky, které závisí na těchto skriptech ke konfiguraci určitého chování v cílovém projektu, nemusí fungovat podle očekávání. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>prostředky Content nejsou dostupné, když se balíček nainstaluje po migraci.

| | |
| --- | --- |
| **Popis** | Prostředky ve složce balíčku nejsou `content` podporovány v PackageReference a jsou ignorovány. PackageReference přidává podporu pro `contentFiles` pro zajištění lepší přenosové podpory a sdíleného obsahu.  |
| **Potenciální dopad** | Prostředky v `content` nejsou zkopírovány do projektu a kód projektu, který závisí na přítomnosti těchto assetů, vyžaduje refaktoring.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformace XDT se neaplikují, když se balíček nainstaluje po upgradu.

| | |
| --- | --- |
| **Popis** | Transformace XDT nejsou podporované PackageReference a `.xdt` soubory se při instalaci nebo odinstalaci balíčku ignorují.   |
| **Potenciální dopad** | Transformace XDT nejsou aplikovány na žádné soubory XML projektu, nejčastěji `web.config.install.xdt` a `web.config.uninstall.xdt` , což znamená, že soubor projektu není ` web.config` aktualizován při instalaci nebo odinstalaci balíčku. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Sestavení v kořenovém adresáři lib se při instalaci balíčku po migraci ignorují.

| | |
| --- | --- |
| **Popis** | V PackageReference, sestavení přítomná v kořenu `lib` složky bez konkrétní podsložky cílového rozhraní, se ignorují. NuGet vyhledá podsložku odpovídající monikeru cílového rozhraní (TFM), který odpovídá cílovému rozhraní .NET Framework projektu, a nainstaluje odpovídající sestavení do projektu. |
| **Potenciální dopad** | Balíčky, které nemají podsložku odpovídající cílovému monikeru rozhraní .NET Framework (TFM) odpovídající cílovému rozhraní projektu, se nemusí chovat podle očekávání po přechodu nebo při neúspěšné instalaci během migrace. |

## <a name="found-an-issue-report-it"></a>Našel se problém? Report IT!

Pokud narazíte na problém s možností migrace, uveďte [problém v úložišti GitHub NuGet](https://github.com/NuGet/Home/issues/).
