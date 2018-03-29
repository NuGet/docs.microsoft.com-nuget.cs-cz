---
title: Obsah archivu project.json NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Různé bity project.json obsah byl odebrán z jiných oblastí v dokumentaci NuGet.
keywords: Soubor project.json NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a>Project.JSON archivu

`project.json` Formátu správy byla zavedena v systému NuGet 3.x a použít pro určité typy projektů. Byl již nepoužívá, se zavedením PackageReference formát, ve kterém jsou uvedeny závislosti přímo v souboru projektu.

Viz také:

- [project.json schema](project-json.md)
- [Project.JSON dopad na autoři balíčku](project-json-impact.md)
- [project.json a UPW](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Formát souboru Project.JSON správy

*Původně v [obnovení balíčků](../what-is-nuget.md).*

V seznamu správy formátů:

- [`project.json`](project-json.md): *(nepoužívané)* A JSON soubor, který udržuje seznam závislosti projektu s celkové balíček grafu v přidružený soubor, `project.lock.json`. Tento formát je zastaralý považuje PackageReference.

## <a name="nuget-restore-on-mono"></a>nuget restore na Mono

*Původně v [nástrojích klienta nainstalovat NuGet](../install-nuget-client-tools.md).*

Funguje s `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Omezení verze balíčku s obnovením

*Původně v [obnovení balíčků](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*

- `project.json`: Určete rozsah verze přímo s číslem verze této závislosti. Příklad:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>NuGet rozhraní příkazového řádku

- `nuget install` nefunguje s `project.json`.
- `nuget restore`: pomocí projektů pomocí `project.json`, generuje `project.lock.json` souboru a `<project>.nuget.props` souborů, v případě potřeby. (Oba soubory lze vynechat od správy zdrojového kódu.) `<projectPath>` Argument může ukazovat `project.json` souborů a má stejné chování jako odkazující na `packages.config` nebo soubor projektu. V pořadí podle priority pro složky balíčku `%userprofile%\.nuget\packages` prohledají se nejprve při použití `project.json`.
- `nuget update`: Na Mono, tento příkaz nefunguje s projektů pomocí `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Řešení závislostí s PackageReference

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Chování PackageReference platí také pro `project.json`. NuGet restore zapisuje do souboru s názvem graf závislostí `project.lock.json` spolu s `project.json`.

## <a name="managing-dependency-assets"></a>Správa závislostí prostředky

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Při použití `project.json` formátu, můžete řídit, které prostředky z toku závislosti do nejvyšší úrovně projektu. Podrobnosti najdete v tématu [project.json](project-json.md).

## <a name="excluding-references"></a>S výjimkou odkazy

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: Přidejte `"exclude" : "all"` v závislost PackageC:

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

## <a name="resolving-incompatible-package-errors"></a>Řešení chyb při nekompatibilní balíčku

*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Přidání způsob řešení chyb:

- **Nedoporučuje se**: jako dočasné řešení při práci s autora balíčku projekty cílení na `netcore`, `netstandard`, a `netcoreapp` mohou ostatní platformy jako kompatibilní, a tím umožní balíčky cílené na těch, které označují ostatní platformy, který se má použít. V tématu [project.json importuje](project-json.md#imports) a [cíl obnovení MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). To může způsobit neočekávané chování, proto znovu, je vhodné řešení nekompatibility balíček ve spolupráci s autora balíčku na aktualizace.

## <a name="target-frameworks"></a>Cílové rozhraní

*Původně v [cílové rozhraní](../reference/target-frameworks.md).*

- [Project.JSON](project-json.md): `frameworks` uzlu určuje framework verze, které mohou být zkompilovány projektu proti.

## <a name="creating-a-package"></a>Vytváření balíčku

*Původně v [vytváření balíčku](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Balíček typ nastavení

S .NET Core 1.x, když je nainstalovaný balíček DotnetCliTool, Visual Studio umístí balíčku `project.json` `tools` uzlu místo `dependencies` uzlu.

Balíček typy jsou nastaveny v `project.json`.

- `project.json`: Označuje typ balíčku v rámci `packOptions.packageType` vlastnosti json:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Přidání cíle a props pro nástroje MSBuild

*Původně v [vytvořit balíčky NuGet standardní .NET s Visual Studiem 2015](../guides/create-net-standard-packages-vs2015.md).*

Při použití `project.json`, cíle nejsou přidány do projektu, ale jsou k dispozici prostřednictvím `project.lock.json`.

### <a name="package-versioning"></a>Správa verzí balíčku

*Původně v [Správa verzí balíčku](../reference/package-versioning.md).*

Při použití `project.json` formátu, NuGet také podporuje notaci zástupný znak, \*, pro hlavní, vedlejší, opravy a příponu předběžné verze součástí číslo.

### <a name="nugetconfig-reference"></a>Odkaz na soubor nuget.config.

*Původně v [NuGet.Config odkaz](../reference/nuget-config-file.md).*

`globalPackagesFolder` platí pouze pro `project.json`. (Byla přidána poznámka: platí také pro PackageReference.)

### <a name="nuspec-file-reference"></a>odkaz na soubor nuspec

*Původně v [odkaz na soubor nuspec](../reference/nuspec.md).*

`<contentFiles>` Element se používá namísto `<files>` s `project.json`.

### <a name="package-manager-options-control"></a>Balíček správce možnosti řízení

*Původně v [reference k uživatelskému rozhraní Správce balíčků](../tools/package-manager-ui.md).*

Projekty pomocí `project.json` správu formátu zobrazit pouze **zobrazit okno náhledu** možnost.

### <a name="visual-studio-templates"></a>Šablony aplikace Visual Studio

*Původně v [balíčky NuGet ve šablony sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Osvědčené postupy: šablony neobsahují `project.json` souboru a nezahrnují nebo žádné odkazy nebo obsah, který by byl přidán, když se instalují balíčky NuGet.