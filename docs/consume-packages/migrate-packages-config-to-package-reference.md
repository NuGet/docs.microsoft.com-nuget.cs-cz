---
title: Migrace z formátu package.config na PackageReference
description: Podrobnosti o migraci projektu z formátu správy package.config do packagereference podporované nuget 4.0+ a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428889"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrace z packages.config na PackageReference

Visual Studio 2017 verze 15.7 a novější podporuje migraci projektu z formátu [správy packages.config](../reference/packages-config.md) do formátu [PackageReference.](../consume-packages/Package-References-in-Project-Files.md)

## <a name="benefits-of-using-packagereference"></a>Výhody použití PackageReference

* **Spravovat všechny závislosti projektu na jednom místě**: Stejně jako projekt na odkazy na `PackageReference` projekt a odkazy na sestavení, Odkazy na balíčky NuGet (pomocí uzlu) jsou spravovány přímo v rámci souborů projektu, nikoli pomocí samostatného souboru packages.config.
* **Přehledné zobrazení závislostí nejvyšší úrovně**: Na rozdíl od packages.config packagereference uvádí pouze ty balíčky NuGet, které jste přímo nainstalovali v projektu. V důsledku toho nuget správce balíčků uj.
* **Vylepšení výkonu**: Při použití PackageReference balíčky jsou udržovány ve složce *globální balíčky* (jak `packages` je popsáno na správa globální [balíčky a složky mezipaměti,](../consume-packages/managing-the-global-packages-and-cache-folders.md) nikoli ve složce v rámci řešení. V důsledku toho PackageReference provádí rychleji a spotřebovává méně místa na disku.
* **Jemná kontrola nad závislostmi a tok obsahu**: Pomocí existujících funkcí MSBuild umožňuje [podmíněně odkazovat na balíček NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) a zvolit odkazy na balíček podle cílového rozhraní, konfigurace, platformy nebo jiných pivotů.
* **PackageReference je v aktivním vývoji**: Viz [PackageReference problémy na GitHubu](https://aka.ms/nuget-pr-improvements). soubor packages.config již není v aktivním vývoji.

### <a name="limitations"></a>Omezení

* NuGet PackageReference není k dispozici ve Visual Studiu 2015 a starší. Migrované projekty lze otevřít pouze v sadě Visual Studio 2017 a novější.
* Migrace není v současné době k dispozici pro projekty jazyka C++ a ASP.NET.
* Některé balíčky nemusí být plně kompatibilní s PackageReference. Další informace naleznete v tématu [problémy s kompatibilitou balíčků](#package-compatibility-issues).

Kromě toho existují určité rozdíly ve způsobu, jakým PackageReferences fungují ve srovnání s packages.config. Například - [omezení upgradu verze](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) není supprted packagereference, ale přidat podporu pro [plovoucí verze](../consume-packages/package-references-in-project-files.md#floating-versions).

### <a name="known-issues"></a>Známé problémy

1. Tato `Migrate packages.config to PackageReference...` možnost není k dispozici v kontextové nabídce po kliknutí pravým tlačítkem myši. 

#### <a name="issue"></a>Problém 
 
Při prvním otevření projektu NuGet nemusí mít inicializována, dokud není provedena operace NuGet. To způsobí, že možnost migrace se nezobrazí v `packages.config` `References`místní nabídce pravým tlačítkem myši na nebo . 

#### <a name="workaround"></a>Alternativní řešení 

Proveďte některou z následujících akcí NuGet: 
* Otevřete ui Správce balíčků – `References` klikněte pravým tlačítkem myši a vyberte`Manage NuGet Packages...` 
* Otevřete konzolu Správce `Tools > NuGet Package Manager`balíčků – od , vyberte`Package Manager Console` 
* Spuštění obnovení NuGet – klikněte pravým tlačítkem myši na uzel řešení v Průzkumníku řešení a vyberte`Restore NuGet Packages` 
* Sestavení projektu, který také aktivuje obnovení NuGet 

Nyní byste měli mít možnost zobrazit možnost migrace. Všimněte si, že tato možnost není podporována a nezobrazí se pro typy projektů ASP.NET a C++. 

## <a name="migration-steps"></a>Kroky migrace

> [!Note]
> Před zahájením migrace visual studio vytvoří zálohu projektu, která vám umožní [vrátit se zpět na soubor packages.config](#how-to-roll-back-to-packagesconfig) v případě potřeby.

1. Otevřete řešení obsahující `packages.config`projekt pomocí .

1. V **Průzkumníku řešení**klepněte pravým tlačítkem `packages.config` myši na uzel **Odkazy** nebo na soubor a vyberte příkaz **Migrovat packages.config na PackageReference...**.

1. Migrator analyzuje odkazy na balíček NuGet projektu a pokusí se je kategorizovat do **závislostí nejvyšší úrovně (balíčky** NuGet, které jste nainstalovali přímo) a **přenositelné závislosti (balíčky,** které byly nainstalovány jako závislosti balíčků nejvyšší úrovně).

   > [!Note]
   > PackageReference podporuje přenosité obnovení balíčků a dynamicky řeší závislosti, což znamená, že přenosné závislosti nemusí být nainstalovány explicitně.

1. (Nepovinné) Můžete se rozhodnout považovat balíček NuGet klasifikovaný jako přenositelnou závislost jako závislost nejvyšší úrovně výběrem možnosti **nejvyšší úrovně** pro balíček. Tato možnost je automaticky nastavena pro balíčky obsahující datové zdroje, `build` `buildCrossTargeting`které `contentFiles`neproudí přechodně (ty v , , nebo `analyzers` složky) a ty, které jsou označeny jako závislost na vývoji (`developmentDependency = "true"`).

1. Zkontrolujte všechny [problémy s kompatibilitou balíčků](#package-compatibility-issues).

1. Chcete-li zahájit migraci, vyberte **možnost OK.**

1. Na konci migrace Visual Studio poskytuje sestavu s cestou k zálohování, seznam nainstalovaných balíčků (nejvyšší úrovně závislostí), seznam balíčků odkazovaných jako přenositelné závislosti a seznam problémů s kompatibilitou zjištěných na začátku migrace. Sestava je uložena do záložní složky.

1. Ověřte, že řešení sestaví a spustí. Pokud narazíte na problémy, [soubor problém na GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Jak vrátit zpět na packages.config

1. Zavřete migrovaný projekt.

1. Zkopírujte soubor `packages.config` projektu a ze `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`zálohy (obvykle) do složky projektu. Odstraňte složku obj, pokud existuje v kořenovém adresáři projektu.

1. Otevřete projekt.

1. Otevřete konzolu Správce balíčků pomocí příkazu **Příkaz u nástroje > Správce balíčků > konzoly správce balíčků.**

1. V konzole spusťte následující příkaz:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Vytvoření balíčku po migraci

Po dokončení migrace doporučujeme přidat odkaz na [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget balíček a potom použijte [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) k vytvoření balíčku. Ačkoli v některých `dotnet.exe pack` `msbuild -t:pack`scénářích můžete použít místo , se nedoporučuje.

## <a name="package-compatibility-issues"></a>Problémy s kompatibilitou balíčků

Některé aspekty, které byly podporovány v packages.config nejsou podporovány v PackageReference. Migrator analyzuje a detekuje tyto problémy. Jakýkoli balíček, který má jeden nebo více z následujících problémů nemusí chovat podle očekávání po migraci.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Skripty "install.ps1" jsou ignorovány při instalaci balíčku po migraci

| | |
| --- | --- |
| **Popis** | S PackageReference, install.ps1 a uninstall.ps1 PowerShell skripty nejsou spuštěny při instalaci nebo odinstalaci balíčku. |
| **Potenciální dopad** | Balíčky, které závisí na těchto skriptů nakonfigurovat některé chování v cílovém projektu nemusí fungovat podle očekávání. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"obsah" prostředky nejsou k dispozici, pokud je balíček nainstalován po migraci

| | |
| --- | --- |
| **Popis** | Prostředky ve `content` složce balíčku nejsou podporovány s PackageReference a jsou ignorovány. PackageReference přidává `contentFiles` podporu pro lepší přenositou podporu a sdílený obsah.  |
| **Potenciální dopad** | Prostředky `content` v aplikaci nejsou zkopírovány do kódu projektu a projekt, který závisí na přítomnosti těchto prostředků vyžaduje refaktoring.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>XDT transformace nejsou použity při instalaci balíčku po upgradu

| | |
| --- | --- |
| **Popis** | XDT transformace nejsou podporovány s `.xdt` PackageReference a soubory jsou ignorovány při instalaci nebo odinstalaci balíčku.   |
| **Potenciální dopad** | Transformace XDT nejsou použity pro žádné soubory XML `web.config.install.xdt` `web.config.uninstall.xdt`projektu, nejčastěji a` web.config` , což znamená, že soubor projektu není aktualizován při instalaci nebo odinstalaci balíčku. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Sestavení v kořenovém adresáři lib jsou ignorována při instalaci balíčku po migraci

| | |
| --- | --- |
| **Popis** | S PackageReference jsou ignorovány sestavení `lib` přítomné v kořenovém adresáři složky bez podsložky specifické pro cílovou architekturu. NuGet hledá podsložku odpovídající zástupný název cílové ho rozhraní (TFM) odpovídající cílové rozhraní projektu a nainstaluje odpovídající sestavení do projektu. |
| **Potenciální dopad** | Balíčky, které nemají podsložku odpovídající zástupný název cílové ho rozhraní (TFM) odpovídající cílové rozhraní projektu nemusí chovat podle očekávání po přechodu nebo selhání instalace během migrace |

## <a name="found-an-issue-report-it"></a>Našli jste problém? Nahlašte to!

Pokud narazíte na problém s migrací, [nahlaste problém v úložišti NuGet GitHub](https://github.com/NuGet/Home/issues/).
