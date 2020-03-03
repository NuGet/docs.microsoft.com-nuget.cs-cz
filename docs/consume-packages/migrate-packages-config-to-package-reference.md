---
title: Migrace ze souboru Package. config do formátů PackageReference
description: Podrobnosti o tom, jak migrovat projekt z formátu správy Package. config na PackageReference, který podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231264"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrace ze souboru Packages. config na PackageReference

Visual Studio 2017 verze 15,7 a novější podporuje migraci projektu z formátu správy [Packages. config](../reference/packages-config.md) na formát [PackageReference](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Výhody použití PackageReference

* **Spravovat všechny závislosti projektu na jednom místě**: stejně jako odkazy na projekt na projekt a odkazy na sestavení, odkazy na balíček NuGet (pomocí `PackageReference`ho uzlu) se spravují přímo v souborech projektu, a ne pomocí samostatného souboru Packages. config.
* Nekonzistentní **pohled na závislosti nejvyšší úrovně**: na rozdíl od souboru Packages. config vypíše PackageReference jenom balíčky NuGet, které jste přímo nainstalovali v projektu. V důsledku toho uživatelské rozhraní Správce balíčků NuGet a soubor projektu nejsou v závislosti na nižší úrovni nepotřebné.
* **Vylepšení výkonu**: při použití PackageReference jsou balíčky udržovány ve složce *Global-Packages* (jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md) , nikoli ve složce `packages` v rámci řešení. V důsledku toho PackageReference provádí rychlejší a spotřebovává méně místa na disku.
* **Přesnější řízení závislostí a toku obsahu**: pomocí existujících funkcí nástroje MSBuild můžete [podmíněně odkazovat na balíček NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) a vybrat odkazy na balíčky pro cílovou architekturu, konfiguraci, platformu nebo jiné pivoty.
* **PackageReference je v aktivním vývoji**: viz [problémy PackageReference na GitHubu](https://aka.ms/nuget-pr-improvements). soubor Packages. config už není v aktivním vývoji.

### <a name="limitations"></a>Omezení

* V aplikaci Visual Studio 2015 a starší není PackageReference NuGet k dispozici. Migrované projekty lze otevřít pouze v aplikaci Visual Studio 2017 nebo novější.
* Migrace není aktuálně k dispozici C++ pro projekty a ASP.NET.
* Některé balíčky nemusí být plně kompatibilní s PackageReference. Další informace najdete v tématu [problémy s kompatibilitou balíčků](#package-compatibility-issues).

Kromě toho existují určité rozdíly v tom, jak PackageReferences funguje v porovnání s balíčky. config. Například [verze upgradu s omezením](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) nejsou supprted pomocí PackageReference, ale přidávají podporu pro [plovoucí verze](../consume-packages/package-references-in-project-files.md#floating-versions).

### <a name="known-issues"></a>Známé problémy

1. Možnost `Migrate packages.config to PackageReference...` není k dispozici v místní nabídce kliknutím pravým tlačítkem myši. 

#### <a name="issue"></a>Problém 
 
Při prvním otevření projektu se nemusí NuGet inicializovat, dokud se neprovede operace NuGet. To způsobí, že se možnost migrace nebude zobrazovat v místní nabídce `packages.config` nebo `References`kliknutím pravým tlačítkem myši. 

#### <a name="workaround"></a>Alternativní řešení 

Proveďte jednu z následujících akcí NuGet: 
* Otevřete uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem na `References` a vyberte `Manage NuGet Packages...` 
* Otevřete konzolu Správce balíčků – z `Tools > NuGet Package Manager`vyberte `Package Manager Console` 
* Spustit obnovení NuGet – pravým tlačítkem myši klikněte na uzel řešení v Průzkumník řešení a vyberte `Restore NuGet Packages` 
* Sestavení projektu, který také aktivuje obnovení NuGet 

Nyní byste měli být schopni zobrazit možnost migrace. Všimněte si, že tato možnost není podporovaná a nebude se zobrazovat pro ASP.NET C++ a typy projektů. 

## <a name="migration-steps"></a>Kroky migrace

> [!Note]
> Před zahájením migrace vytvoří Visual Studio zálohu projektu, abyste v případě potřeby mohli [vrátit zpět do souboru Packages. config](#how-to-roll-back-to-packagesconfig) .

1. Otevřete řešení obsahující projekt pomocí `packages.config`.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na uzel **odkazy** nebo na `packages.config` soubor a vyberte **migrovat Packages. config na PackageReference...**.

1. Migrace analyzuje odkazy na balíček NuGet projektu a pokusy o jejich kategorizaci do **závislostí na nejvyšší úrovni** (balíčky NuGet, které jste nainstalovali přímo), a **přenosných závislostí** (balíčky, které byly nainstalovány jako závislosti balíčků nejvyšší úrovně).

   > [!Note]
   > PackageReference podporuje dynamické obnovení a překládání závislostí, což znamená, že přenositelné závislosti není nutné instalovat explicitně.

1. Volitelné Můžete se rozhodnout zacházet s balíčkem NuGet klasifikovaným jako tranzitivní závislost jako se závislostí na nejvyšší úrovni, a to tak, že vyberete možnost **nejvyšší úrovně** pro balíček. Tato možnost je automaticky nastavená pro balíčky obsahující prostředky, které se netoků přenášejí (ty v `build`, `buildCrossTargeting`, `contentFiles`nebo `analyzers` složky) a ty, které jsou označené jako závislost pro vývoj (`developmentDependency = "true"`).

1. Projděte si všechny [problémy s kompatibilitou balíčku](#package-compatibility-issues).

1. Kliknutím na **OK** zahajte migraci.

1. Na konci migrace poskytuje Visual Studio zprávu s cestou k zálohování, seznam nainstalovaných balíčků (závislostí nejvyšší úrovně), seznam balíčků, na které se odkazuje jako na přenositelné závislosti, a seznam problémů s kompatibilitou zjištěných na začátku migrace. Sestava se uloží do zálohovací složky.

1. Ověřte, že řešení sestavuje a spouští. Pokud narazíte na problémy, zapište [problém na GitHubu](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Postup vrácení zpět do souboru Packages. config

1. Zavřete migrovaný projekt.

1. Zkopírujte soubor projektu a `packages.config` ze zálohy (obvykle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) do složky projektu. Odstraňte složku obj, pokud existuje v kořenovém adresáři projektu.

1. Otevřete projekt.

1. Otevřete konzolu Správce balíčků pomocí **nástrojů > správce balíčků NuGet > konzole správce balíčků** .

1. V konzole spusťte následující příkaz:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Vytvoření balíčku po migraci

Po dokončení migrace doporučujeme přidat odkaz na balíček NuGet [. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) a pak pomocí nástroje [MSBuild-t:Pack](../reference/msbuild-targets.md#pack-target) vytvořit balíček. I když v některých scénářích můžete místo `msbuild -t:pack`použít `dotnet.exe pack`, nedoporučuje se.

## <a name="package-compatibility-issues"></a>Problémy s kompatibilitou balíčků

Některé aspekty, které byly podporovány v souboru Packages. config, nejsou v PackageReference podporovány. Migrace analyzuje a detekuje takové problémy. Každý balíček, který má jeden nebo více následujících problémů, se nemusí po migraci chovat podle očekávání.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>skripty Install. ps1 se při instalaci balíčku po migraci ignorují.

| | |
| --- | --- |
| **Popis** | Pomocí PackageReference nainstalujte. ps1 a odinstalujte. ps1 skripty PowerShellu se při instalaci nebo odinstalaci balíčku nespustí. |
| **Potenciální dopad** | Balíčky, které závisí na těchto skriptech ke konfiguraci určitého chování v cílovém projektu, nemusí fungovat podle očekávání. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>prostředky Content nejsou dostupné, když se balíček nainstaluje po migraci.

| | |
| --- | --- |
| **Popis** | Prostředky ve složce `content` balíčku nejsou u PackageReference podporovány a jsou ignorovány. PackageReference přidává podporu `contentFiles` pro lepší přenosovou podporu a sdílený obsah.  |
| **Potenciální dopad** | Prostředky v `content` nejsou zkopírovány do projektu a kód projektu, který závisí na přítomnosti těchto assetů, vyžaduje refaktoring.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformace XDT se neaplikují, když se balíček nainstaluje po upgradu.

| | |
| --- | --- |
| **Popis** | Transformace XDT nejsou podporované PackageReference a soubory `.xdt` se při instalaci nebo odinstalaci balíčku ignorují.   |
| **Potenciální dopad** | Transformace XDT nejsou aplikovány na žádné soubory XML projektu, nejčastěji `web.config.install.xdt` a `web.config.uninstall.xdt`, což znamená, že soubor` web.config` projektu není aktualizován při instalaci nebo odinstalaci balíčku. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Sestavení v kořenovém adresáři lib se při instalaci balíčku po migraci ignorují.

| | |
| --- | --- |
| **Popis** | V PackageReference sestavení přítomná v kořenu složky `lib`, aniž by byla specifická podsložka cílového Frameworku, se ignorují. NuGet vyhledá podsložku odpovídající monikeru cílového rozhraní (TFM), který odpovídá cílovému rozhraní .NET Framework projektu, a nainstaluje odpovídající sestavení do projektu. |
| **Potenciální dopad** | Balíčky, které nemají podsložku odpovídající cílovému monikeru rozhraní .NET Framework (TFM) odpovídající cílovému rozhraní projektu, se nemusí chovat podle očekávání po přechodu nebo při neúspěšné instalaci během migrace. |

## <a name="found-an-issue-report-it"></a>Našel se problém? Report IT!

Pokud narazíte na problém s možností migrace, uveďte [problém v úložišti GitHub NuGet](https://github.com/NuGet/Home/issues/).
