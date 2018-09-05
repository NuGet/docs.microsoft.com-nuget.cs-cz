---
title: Obsah archivu project.json NuGet
description: Různé části project.json obsah odstraněný z jiných oblastí dokumentace pro NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: aa5cd1a2f3e3a6707a9d68204306db85651b0a18
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545197"
---
# <a name="projectjson-archive"></a>Archiv Project.JSON

`project.json` Formátu správy byla zavedena v systému NuGet 3.x a používanou pro konkrétní typy projektů. Se přestala nabízet, se zavedením PackageReference formát, ve kterém jsou uvedené závislosti přímo v souboru projektu.

Viz také:

- [project.json schema](project-json.md)
- [dopad Project.JSON autory balíčku](project-json-impact.md)
- [project.json a UPW](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Formát správu Project.JSON

*Původně v [obnovení balíčku](../what-is-nuget.md).*

V seznamu management formáty:

- [`project.json`](project-json.md): *(zastaralé)* souboru A JSON, který udržuje seznam závislostí projektu s celkový graf balíčku v souboru přidružené `project.lock.json`. Tento formát je zastaralé a místo toho použití PackageReference.

## <a name="nuget-restore-on-mono"></a>obnovení nuget v Mono

*Původně v [klientských nástrojů Nugetu nainstalovat](../install-nuget-client-tools.md).*

Funguje s `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Omezující verze balíčků pomocí obnovení

*Původně v [obnovení balíčku](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*

- `project.json`: Zadejte rozsah verzí přímo s číslem verze na závislost. Příklad:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Příkazy rozhraní příkazového řádku NuGet

- `nuget install` nefunguje s `project.json`.
- `nuget restore`: pomocí projektů s použitím `project.json`, generuje `project.lock.json` souboru a `<project>.nuget.props` souboru, v případě potřeby. (Oba soubory může vynechat ze správy zdrojového kódu.) `<projectPath>` Argument může odkazovat `project.json` souborů a má stejné chování jako odkazující `packages.config` nebo soubor projektu. V pořadí podle priority pro složky balíčku `%userprofile%\.nuget\packages` prohledáván jako první při použití `project.json`.
- `nuget update`: V Mono, tento příkaz nefunguje s projekty pomocí `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Řešení závislostí s PackageReference

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Chování PackageReference platí také pro `project.json`. Obnovení NuGet zapisuje do souboru s názvem grafu závislostí `project.lock.json` spolu s `project.json`.

## <a name="managing-dependency-assets"></a>Správa závislostí prostředky

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Při použití `project.json` formátu, můžete určit, jaké prostředky z toku závislostí do nejvyšší úrovně projektu. Podrobnosti najdete v tématu [project.json](project-json.md).

## <a name="excluding-references"></a>Kromě odkazů

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: přidání `"exclude" : "all"` v závislostí pro PackageC:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Řešení chyb nekompatibilní balíček

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Přidání prostředků řešení chyb:

- **Není doporučeno**: jako dočasné řešení při práci s autora balíčku projekty cílení `netcore`, `netstandard`, a `netcoreapp` označit jako kompatibilní, což balíčky cílí na ty ostatní platformy Další architektury, který se má použít. Zobrazit [project.json importuje](project-json.md#imports) a [cíl obnovení nástroje MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). To může způsobit neočekávané chování, proto znovu, je nejlepší řešení nekompatibility balíček při práci s autora balíčku na aktualizace.

## <a name="target-frameworks"></a>Cílové architektury

*Původně v [platforem](../reference/target-frameworks.md).*

- [Project.JSON](project-json.md): `frameworks` uzlu určuje verze rozhraní framework projektu může být zkompilována proti.

## <a name="creating-a-package"></a>Vytvoření balíčku

*Původně v [vytvoření balíčku](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Nastavení typ balíčku

S .NET Core 1.x, když DotnetCliTool balíček nainstalován, Visual Studio umístí v balíčku `project.json` `tools` uzel místo `dependencies` uzlu.

Balíček typy mají nastavený `project.json`.

- `project.json`: Označuje typ balíčku v rámci `packOptions.packageType` vlastnosti json:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Přidání cíle a vlastnosti pro MSBuild

*Původně v [vytvořit balíčky .NET NuGet standardní pomocí sady Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Při použití `project.json`, cíle nebyly přidány do projektu, ale jsou k dispozici prostřednictvím `project.lock.json`.

### <a name="package-versioning"></a>Správa verzí balíčků

*Původně v [Správa verzí balíčků](../reference/package-versioning.md).*

Při použití `project.json` formátování, NuGet také podporuje notaci zástupný znak, \*pro hlavní, vedlejší, opravy a příponu předběžné verze část čísla.

### <a name="nugetconfig-reference"></a>Odkaz na soubor NuGet.Config

*Původně v [odkaz na soubor NuGet.Config](../reference/nuget-config-file.md).*

`globalPackagesFolder` platí jenom pro `project.json`. (Přidání poznámky: platí také pro PackageReference.)

### <a name="nuspec-file-reference"></a>odkaz na soubor nuspec

*Původně v [odkaz na soubor nuspec](../reference/nuspec.md).*

`<contentFiles>` Element se použije namísto `<files>` s `project.json`.

### <a name="package-manager-options-control"></a>Ovládací prvek možnosti Správce balíčků

*Původně v [Reference k uživatelskému rozhraní Správce balíčků](../tools/package-manager-ui.md).*

Projekty pomocí `project.json` správu formátu zobrazit pouze **zobrazit okno náhledu** možnost.

### <a name="visual-studio-templates"></a>Šablony aplikace Visual Studio

*Původně v [balíčky NuGet v sadě Visual Studio šablony](../visual-studio-extensibility/visual-studio-templates.md).*

Osvědčené postupy: šablony nezahrnují `project.json` souboru a nezahrnuje nebo odkazy nebo obsah, který se přidá při instalaci balíčků NuGet.