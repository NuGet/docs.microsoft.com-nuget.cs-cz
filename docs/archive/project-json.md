---
title: Odkaz na soubor Project.JSON pro NuGet
description: V některých typech projektů project.json udržuje seznam balíčky NuGet používané v projektu.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547781"
---
# <a name="projectjson-reference"></a>odkaz na Project.JSON

*NuGet 3.x+*

`project.json` Souboru udržuje seznam balíčků používá v projektu, označované jako formát správy balíčků. Tato Smlouva nahrazuje `packages.config` ale zase nahrazována [PackageReference](../consume-packages/package-references-in-project-files.md) nuget 4.0 +.

[ `project.lock.json` ](#projectlockjson) Souboru (popsaných níže) se také používá v projektech využívající `project.json`.

`project.json` má následující základní strukturou, kde každý z objektů čtyři nejvyšší úrovně může mít libovolný počet podřízených objektů:

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

Zobrazí seznam závislosti balíčku NuGet projektu v následujícím tvaru:

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

`dependencies` Je oddíl, kde dialogové okno Správce balíčků NuGet přidá závislosti balíčků do vašeho projektu.

Id balíčku, který odpovídá id balíčků na nuget.org, stejné jako id použít v konzole Správce balíčků: `Install-Package Microsoft.NETCore`.

Při obnovování balíčků, omezení verze `"5.0.0"` znamená `>= 5.0.0`. To znamená pokud 5.0.0 není k dispozici na serveru, ale je – 5.0.1, nainstaluje – 5.0.1 NuGet a upozorňuje na inovace. Jinak NuGet vybere nejnižší možné verze na serveru odpovídající omezení.

Zobrazit [řešení závislostí](../consume-packages/dependency-resolution.md) podrobné informace o řešení pravidla.

### <a name="managing-dependency-assets"></a>Správa závislostí prostředky

Které prostředky od závislostí tok do nejvyšší úrovně projektu je řízen tak, že zadáte sadu klíčových slov do oddělených čárkou `include` a `exclude` vlastnosti odkazu na závislost. Značky jsou uvedeny v následující tabulce:

| Zahrnutí a vyloučení značek | Ovlivněné složky cíle |
| --- | --- |
| contentFiles | Obsah  |
| modul runtime | Modul runtime, prostředky a FrameworkAssemblies  |
| Kompilace | lib |
| sestavení | sestavení (cíle a vlastnosti nástroje MSBuild) |
| nativní | nativní |
| žádná | Žádné složky |
| všechny | Všechny složky |

Značky s `exclude` přednost zadaným `include`. Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.

Například chcete zahrnout `build` a `native` složky závislosti, použijte následující:

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

Chcete-li vyloučit `content` a `build` složky závislosti, použijte následující:

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

## <a name="frameworks"></a>Rozhraní

Obsahuje seznam rozhraní projektu, na kterých běží, jako například `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Je povolena pouze jedna položka `frameworks` oddílu. (Výjimkou je `project.json` souborů pro projekty ASP.NET, které jsou sestavení s nepoužívané DNX nástroj řetězce, která umožňuje více cílů.)

## <a name="runtimes"></a>Moduly runtime

Obsahuje seznam operačních systémů a architektur, které vaše aplikace běží na serveru, jako například `win10-arm`, `win8-x64`, `win8-x86`.

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

Balíček, který obsahuje, můžete spustit na libovolné runtime PCL nepotřebuje k určení modulu runtime. Musí být také platí pro všechny závislosti, jinak je nutné zadat moduly runtime.


## <a name="supports"></a>Podporuje

Definuje sadu kontroluje pro závislosti balíčků. Můžete definovat, kdy očekáváte PCL nebo na spuštění aplikace. Definice nejsou omezující, jak váš kód může být možné spouštět jinde. Ale zadáte tyto kontroly díky NuGet, zkontrolujte, že jsou splněny všechny závislosti na uvedené TxMs. Příklady hodnot jsou: `net46.app`, `uwp.10.0.app`atd.

Tato část by měl vyplní automaticky, když vyberete položku v dialogovém okně knihovny přenosných tříd cíle.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importy

Importy jsou navržené tak, aby balíčky, které používají `dotnet` TxM pracovat s balíčky, které není deklarovat dotnet TxM. Pokud váš projekt používá `dotnet` TxM pak všechny balíčky, které závisí na musí mít také `dotnet` TxM, pokud přidejte následující text do vašeho `project.json` umožňující bez `dotnet` platformy se kvůli kompatibilitě s `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Pokud používáte `dotnet` TxM pak systém projektu PCL přidá odpovídající `imports` příkaz na základě podporovaných cílů.

## <a name="differences-from-portable-apps-and-web-projects"></a>Rozdíl oproti přenosné aplikace a webové projekty

`project.json` Soubor používaný NuGet je podmnožinou nalezeným v projektech ASP.NET Core. V ASP.NET Core `project.json` se používá pro metadata projektu, informace o kompilaci a závislosti. Při použití v jiných systémech projektu, jsou tyto tři věci rozdělit na samostatné soubory a `project.json` obsahuje méně informací. Významný rozdíl patří:

- Může existovat pouze jedno rozhraní v `frameworks` oddílu.

- Soubor nesmí obsahovat závislosti, možnosti kompilace, atd., které se zobrazí v DNX `project.json` soubory. Vzhledem k tomu, že může existovat pouze jeden rámec ho nemá smysl zadejte závislosti pro konkrétní rozhraní.

- Kompilace se zpracovává souborem MSBuild tak definuje možnosti kompilace, preprocesoru, atd. jsou všechny části souboru projektu MSBuild, ne `project.json`.

Ve Správci NuGet 3 +, vývojáři nepředpokládá ručně upravit `project.json`, protože uživatelské rozhraní Správce balíčků v sadě Visual Studio pracuje obsah. Ale nutné dodat, určitě můžete upravit soubor, ale musíte sestavit projekt ke spuštění obnovení balíčku nebo vyvolat obnovení jiným způsobem. Zobrazit [obnovení balíčku](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

`project.lock.json` Soubor se generuje Probíhá obnovování balíčků NuGet v projektech, které používají `project.json`. Obsahuje snímek všech informace, které jsou generovány podle vás grafu balíčky NuGet a obsahuje verze, obsah a všech balíčků závislostí ve vašem projektu. Systém sestavení používá toto vybrat balíčky z globálního místa, které jsou relevantní, při sestavování projektu namísto v závislosti na balíčky místní složky v projektu. Výsledkem je rychlejší výkon sestavení vzhledem k tomu je potřeba jen pro čtení `project.lock.json` místo mnoho oddělení `.nuspec` soubory.

`project.lock.json` není automaticky vygenerován při obnovování balíčků, tak ho lze vynechat ze správy zdrojového kódu tak, že ji přidáte `.gitignore` a `.tfignore` soubory (viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md). Ale pokud ho zahrnete ve správě zdrojového kódu, historii změn zobrazí změny v závislosti vyřešených v průběhu času.
