---
title: Obsah archivu Project. JSON pro NuGet
description: Různé bity obsahu Project. JSON se odebraly z jiných oblastí dokumentace k NuGetu.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 8d732e87f01c55bde87da0a2e382fd6d509886a3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317015"
---
# <a name="projectjson-archive"></a>Archiv Project. JSON

Formát `project.json` správy byl představen s NuGet 3. x a používá se pro určité typy projektů. Byla zastaralá s představením formátu PackageReference, ve kterém jsou závislosti uvedeny přímo v souboru projektu.

Viz také:

- [project.json schema](project-json.md)
- [dopad Project. JSON na autory balíčku](project-json-impact.md)
- [project.json a UPW](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Formát souboru pro správu project.json

*Původně v [balíčku pro obnovení](../what-is-nuget.md).*

V seznamu formátů správy:

- [`project.json`](project-json.md): *(nepoužívané)* soubor JSON, který uchovává seznam závislostí projektu s celkovým grafem balíčku v přidruženém souboru `project.lock.json`. Tento formát je zastaralý a má přednost před PackageReference.

## <a name="nuget-restore-on-mono"></a>obnovení nugetu na mono

*Původně se [nainstalovaly klientské nástroje NuGet](../install-nuget-client-tools.md).*

Pracuje s `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Omezení verzí balíčku s obnovením

*Původně v [balíčku pro obnovení](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*

- `project.json`: Zadejte rozsah verzí přímo s číslem verze závislosti. Příklad:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Příkazy NuGet CLI

- `nuget install`nefunguje s `project.json`.
- `nuget restore`: s projekty používající `project.json`, `project.lock.json` vygeneruje v případě potřeby `<project>.nuget.props` soubor a soubor. (Oba soubory mohou být vynechány ze správy zdrojového kódu.) Argument může odkazovat na soubor a má stejné `packages.config` chování jako odkazuje na soubor projektu nebo. `project.json` `<projectPath>` V pořadí podle priority pro složky `%userprofile%\.nuget\packages` balíčku se při použití `project.json`prohledává jako první.
- `nuget update`: V mono tento příkaz nefunguje s projekty pomocí `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Rozlišení závislosti s PackageReference

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Chování PackageReference se vztahuje také na `project.json`. NuGet Restore uloží graf závislosti do souboru s názvem `project.lock.json` společně `project.json`.

## <a name="managing-dependency-assets"></a>Správa prostředků závislosti

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Při použití `project.json` formátu můžete řídit, které prostředky se mají směrovat do projektu nejvyšší úrovně. Podrobnosti naleznete v tématu [Project. JSON](project-json.md).

## <a name="excluding-references"></a>Vyloučení odkazů

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: přidejte `"exclude" : "all"` v závislosti pro PackageC:

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

## <a name="resolving-incompatible-package-errors"></a>Řešení chyb nekompatibilních balíčků

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Přidaný způsob řešení chyb:

- **Nedoporučuje**se: jako dočasné řešení, když pracujete s autorem balíčku, projekty `netcore`, `netstandard`které cílí `netcoreapp` na, a můžou navšimnout dalších platforem jako kompatibility, takže balíčky cílí na tyto jiné. rozhraní, která se mají použít. Viz [importy Project. JSON](project-json.md#imports) a [PackageTargetFallback cíl obnovení nástroje MSBuild](../reference/msbuild-targets.md#packagetargetfallback). To může způsobit neočekávané chování, takže znovu je vhodné vyřešit nekompatibilitu balíčků pomocí práce s autorem balíčku při aktualizaci.

## <a name="target-frameworks"></a>Cílové architektury

*Původně v [cílových rozhraních](../reference/target-frameworks.md).*

- [project.json](project-json.md): `frameworks` Uzel Určuje verze rozhraní, pro které může být projekt zkompilován.

## <a name="creating-a-package"></a>Vytvoření balíčku

*Původně v [vytváření balíčku](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Nastavení typu balíčku

Pokud je v rozhraní .NET Core 1. x nainstalován balíček DotnetCliTool, sada Visual Studio umístí balíček místo `project.json` `dependencies` uzlu do `tools` uzlu.

Typy balíčků jsou nastaveny v `project.json`.

- `project.json`: Určete typ balíčku v rámci `packOptions.packageType` JSON vlastnosti:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Přidání cílů a vlastností pro MSBuild

*Původně v [rámci vytváření .NET Standard balíčků NuGet pomocí sady Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Při použití `project.json`nejsou cíle přidány do projektu, ale jsou zpřístupněny `project.lock.json`prostřednictvím.

### <a name="package-versioning"></a>Správa verzí balíčků

*Původně ve [verzi balíčku](../reference/package-versioning.md).*

Při použití `project.json` formátu NuGet podporuje také použití zástupných znaků \*, v případě částí čísla hlavní, dílčí, opravné a předběžné verze.

### <a name="nugetconfig-reference"></a>Referenční dokumentace NuGet. config

*Původně v [odkazu NuGet. config](../reference/nuget-config-file.md).*

`globalPackagesFolder`platí pouze pro `project.json`. (Přidání poznámky: platí také pro PackageReference.)

### <a name="nuspec-file-reference"></a>odkaz na soubor nuspec

*Původně v [nuspec reference](../reference/nuspec.md).*

Element je použit `<files>` místo s `project.json`. `<contentFiles>`

### <a name="package-manager-options-control"></a>Řízení možností Správce balíčků

*Původně v [odkazu na uživatelské rozhraní Správce balíčků](../consume-packages/install-use-packages-visual-studio.md).*

Projekty, `project.json` které používají formát správy, zobrazují pouze možnost **Zobrazit okno náhledu** .

### <a name="visual-studio-templates"></a>Šablony aplikace Visual Studio

*Původně v [balíčcích NuGet v šablonách sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Osvědčené postupy: šablony `project.json` neobsahují soubor a neobsahují ani žádné odkazy nebo obsah, které by se přidaly při instalaci balíčků NuGet.