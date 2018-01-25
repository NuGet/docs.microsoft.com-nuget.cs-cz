---
title: Odkaz na soubor Project.JSON pro NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "V některých typů projektu project.json udržuje seznam balíčky NuGet použité v projektu."
keywords: "Balíček NuGet NuGet project.json, odkazy, závislostí NuGet, project.lock.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2e2c521b18dd67e49942cc20eafef0be7f91573a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-reference"></a>odkaz na Project.JSON

*NuGet 3.x+*

`project.json` Souboru udržuje seznam balíčků používat v projektu, označuje jako formátu odkaz na balíček. Nahrazuje `packages.config` ale zase nahrazena [PackageReference](../consume-packages/package-references-in-project-files.md) s NuGet 4.0 +.

[ `project.lock.json` ](#projectlockjson) Souboru (popsaný níže) se také používá v projektech nasazení `project.json`.

`project.json`má následující základní strukturu, kde každý z čtyři nejvyšší úrovně objektů může mít libovolný počet podřízených objektů:

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>Závislosti

Uvádí závislosti balíčků NuGet projektu v následující podobě:

```json
"PackageID" : "version_constraint"
```

Příklad:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

`dependencies` Část je, kde dialogové okno Správce balíčků NuGet přidá k projektu závislosti balíčků.

Id balíčku, který odpovídá id balíčku v nuget.org, stejná jako číslo id použité v konzole Správce balíčků: `Install-Package Microsoft.NETCore`.

Při obnovování balíčků, omezení verze `"5.0.0"` znamená `>= 5.0.0`. To znamená pokud 5.0.0 není k dispozici na serveru, ale je – 5.0.1, nainstaluje – 5.0.1 NuGet a upozorňuje na upgrade. Jinak NuGet vybere nejnižší možné verze na serveru odpovídající omezení.

V tématu [řešení závislostí](../consume-packages/dependency-resolution.md) další podrobnosti o pravidel řešení.

### <a name="managing-dependency-assets"></a>Správa závislostí prostředky

Jaké prostředky z závislosti toku do nejvyšší úrovně projektu je řízena zadáním sadu značky v oddělených čárkou `include` a `exclude` vlastnosti závislý odkaz. Zadané značky jsou uvedeny v následující tabulce:

| Zahrnutí a vyloučení značky | Ovlivněné složky cíle |
| --- | --- |
| contentFiles | Obsah  |
| modul runtime | Modul runtime, prostředky a FrameworkAssemblies  |
| compile | lib |
| sestavení | sestavení (MSBuild props a cíle) |
| nativní | nativní |
| žádná | Žádné složky |
| všechny | Všechny složky |

Značky s `exclude` mají přednost před uvedenými s `include`. Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.

Chcete-li například zahrnout `build` a `native` složky závislost, použijte následující:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

Vyloučit `content` a `build` složky závislost, použijte tento příkaz:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>rozhraní

Uvádí rozhraní, které spouští projektu, například `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

V je povolen pouze jeden záznam `frameworks` oddílu. (Výjimkou je `project.json` soubory pro projekty ASP.NET, které jsou sestavení s nepoužívané sada DNX, který umožňuje více cílů.)

## <a name="runtimes"></a>Moduly runtime

Obsahuje operační systémy a architektury, které běží vaše aplikace, jako například `win10-arm`, `win8-x64`, `win8-x86`.

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

Balíček obsahující PCL, který můžete spustit na jakékoli runtime nebude muset zadat modulu runtime. Toto musí být také platí všechny závislosti, v opačném případě je nutné zadat moduly runtime.


## <a name="supports"></a>Podporuje

Definuje sadu kontroluje pro závislosti balíčků. Můžete definovat, kdy očekáváte PCL nebo aplikace spustit. Definice nejsou omezující, jak váš kód pravděpodobně bude moci spustit jinde. Ale zadání těchto kontrol provádí NuGet, zkontrolujte, že jsou splněny všechny závislosti na uvedené TxMs. Příklady hodnot pro tyto: `net46.app`, `uwp.10.0.app`atd.

V této části by měl naplněny automaticky, když vyberete položku v dialogovém okně knihovny přenosných tříd cíle.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importy

Importy jsou navržené tak, aby balíčky, které používají `dotnet` TxM pracovat s balíčky, které nejsou deklarovat dotnet TxM. Pokud je váš projekt pomocí `dotnet` TxM pak všechny balíčky, které závisí na musí také mít `dotnet` TxM, pokud přidejte následující vaše `project.json` umožňující bez `dotnet` platformy, aby byl kompatibilní s `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Pokud používáte `dotnet` TxM pak systém projektu PCL přidá odpovídající `imports` příkaz na základě podporované cílů.

## <a name="differences-from-portable-apps-and-web-projects"></a>Rozdíl oproti přenosné aplikace a webové projekty

`project.json` Soubor používaný NuGet je podmnožinou který nalézt projektů ASP.NET Core. V ASP.NET Core `project.json` se používá pro projekt metadata, kompilace informace a závislosti. Pokud se použije v ostatních systémech projektu, jsou tyto tři věci rozdělit do samostatných souborů a `project.json` menší informacemi. Významné rozdíly patří:

- Může existovat pouze jedna framework v `frameworks` oddílu.

- Soubor nemůže obsahovat závislosti, možnosti kompilace, atd., které se zobrazí v DNX `project.json` soubory. Vzhledem k tomu, že může existovat jenom jeden framework nemá smysl zadat závislosti konkrétní rozhraní.

- Kompilace se zpracovává souborem MSBuild tak kompilace možnosti preprocesoru definuje atd., jsou všechny součástí soubor projektu nástroje MSBuild a není `project.json`.

V NuGet 3 + vývojáři neočekává se ručně upravit, pokud `project.json`, protože uživatelské rozhraní Správce balíčků v sadě Visual Studio zpracovává obsah. Ale nutné dodat, jistě můžete upravit soubor, ale musí sestavte projekt a spusťte obnovení balíčků nebo vyvolat obnovení jiným způsobem. V tématu [obnovení balíčků](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

`project.lock.json` Soubor je generován právě probíhá obnovení balíčků NuGet v projektech, které používají `project.json`. Drží snímek všechny informace, které jsou generovány jako provede grafu balíčků NuGet a zahrnuje verze, obsah a závislých součástí pro všechny balíčky v projektu. Systém sestavení pomocí to balíčky z globální umístění, které jsou relevantní při sestavování projektu místo v závislosti na složku místní balíčky v projektu. Výsledkem je vyšší výkon sestavení vzhledem k tomu, že je potřeba jen pro čtení `project.lock.json` místo mnoho oddělení `.nuspec` soubory.

`project.lock.json`se automaticky vygeneroval na obnovení balíčků, tak ho lze vynechat od správy zdrojového kódu, přidejte je do `.gitignore` a `.tfignore` soubory (viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md). Ale pokud zahrnete ji do správy zdrojového kódu, historii změn zobrazuje změny v závislosti přeložit v čase.
