---
title: project.json File Reference pro NuGet
description: V některých typech projektu project.json udržuje seznam balíčků NuGet použitých v projektu.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488285"
---
# <a name="projectjson-reference"></a>odkaz na project.json

*NuGet 3.x+*

Soubor `project.json` udržuje seznam balíčků používaných v projektu, známý jako formát správy balíčků. Nahrazuje, `packages.config` ale je zase nahrazen [PackageReference](../consume-packages/package-references-in-project-files.md) s NuGet 4.0 +.

Soubor [`project.lock.json`](#projectlockjson) (popsaný níže) se také používá `project.json`v projektech využívajících .

`project.json`má následující základní strukturu, kde každý ze čtyř objektů nejvyšší úrovně může mít libovolný počet podřízených objektů:

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

Zobrazí seznam závislostí balíčku NuGet projektu v následujícím formuláři:

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

Část `dependencies` je, kde dialogové okno NuGet Package Manager přidá závislosti balíčků do projektu.

ID balíčku odpovídá id balíčku na nuget.org , stejné jako id použité v `Install-Package Microsoft.NETCore`konzole správce balíčků: .

Při obnovování balíčků, verze `"5.0.0"` `>= 5.0.0`omezení implikuje . To znamená, že pokud 5.0.0 není k dispozici na serveru, ale 5.0.1 je, NuGet nainstaluje 5.0.1 a upozorní vás na upgrade. NuGet jinak vybere nejnižší možnou verzi na serveru odpovídající omezení.

Další podrobnosti o pravidlech řešení problémů najdete v [tématu Řešení závislostí.](../concepts/dependency-resolution.md)

### <a name="managing-dependency-assets"></a>Správa prostředků závislostí

Prostředky ze závislostí toku do projektu nejvyšší úrovně je řízen a zadáním čárka oddělené sadu značek v `include` a `exclude` vlastnosti odkazu na závislost. Značky jsou uvedeny v následující tabulce:

| Značka Zahrnout/vyloučit | Ovlivněné složky cíle |
| --- | --- |
| contentFiles | Obsah  |
| modul runtime | Runtime, prostředky a frameworkassemblies  |
| kompilovat | Lib |
| sestavení | sestavení (rekvizity a cíle MSBuild) |
| nativní | nativní |
| Žádná | Žádné složky |
| Vše | Všechny složky |

Značky `exclude` zadané s předností `include`před těmi, které jsou zadány s . Například `include="runtime, compile" exclude="compile"` je stejný `include="runtime"`jako .

Chcete-li například `build` `native` zahrnout složky a závislost, použijte následující:

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

Chcete-li `content` `build` vyloučit složky a závislost, použijte následující:

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

Uvádí architektury, na kterých je `net45`projekt `netcoreapp` `netstandard`spuštěn, například , .

```json
"frameworks": {
    "netcore50": {}
    }
 ```

V `frameworks` sekci je povolena pouze jedna položka. (Výjimkou jsou `project.json` soubory pro ASP.NET projekty, které jsou vytvářeny se zastaralou řetězcem nástrojů DNX, která umožňuje více cílů.)

## <a name="runtimes"></a>Runtime

Uvádí seznam operačních systémů a architektur, na `win10-arm` `win8-x64`kterých vaše aplikace běží, například , . `win8-x86`

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

Balíček obsahující PCL, který lze spustit v libovolném běhu, nemusí zadávat za běhu. To musí být také true všech závislostí, jinak je nutné zadat runtimes.


## <a name="supports"></a>Podporuje

Definuje sadu kontrol pro závislosti balíčků. Můžete definovat, kde očekáváte spuštění pcl nebo aplikace. Definice nejsou omezující, protože váš kód může být možné spustit jinde. Ale zadání těchto kontrol způsobí, že NuGet zkontrolovat, že všechny závislosti jsou splněny na uvedených TxMs. Příklady hodnot pro `net46.app`tojsou: `uwp.10.0.app`, , atd.

Tato část by měla být vyplněna automaticky, když vyberete položku v dialogovém okně Cíle knihovny přenosných tříd.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Dovoz

Importy jsou navrženy tak, `dotnet` aby balíčky, které používají TxM pracovat s balíčky, které nedeklarují dotnet TxM. Pokud váš projekt `dotnet` používá TxM, pak všechny balíčky, `dotnet` na kterých jste závislí, `project.json` musí `dotnet` mít také TxM, pokud nepřidáte následující do vašeho, abyste umožnili kompatibilitu s neplatformami `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Pokud používáte `dotnet` TxM, pak pcl projektový `imports` systém přidá příslušný příkaz založený na podporovaných cílech.

## <a name="differences-from-portable-apps-and-web-projects"></a>Rozdíly od přenosných aplikací a webových projektů

Soubor `project.json` používaný NuGet je podmnožinou, která se nachází v ASP.NET základní projekty. V ASP.NET `project.json` Jádro se používá pro metadata projektu, informace kompilace a závislosti. Při použití v jiných projektových systémech jsou tyto `project.json` tři věci rozděleny do samostatných souborů a obsahují méně informací. Mezi významné rozdíly patří:

- V `frameworks` sekci může být pouze jeden rámec.

- Soubor nemůže obsahovat závislosti, možnosti kompilace atd., `project.json` které vidíte v souborech DNX. Vzhledem k tomu, že může existovat pouze jeden rámec nemá smysl zadávat závislosti specifické pro architekturu.

- Kompilace je zpracována MSBuild, takže možnosti kompilace, preprocesor definuje, atd. `project.json`

V NuGet 3+ vývojáři se neočekává, `project.json`že ručně upravit , jako správce balíčků ujhává s obsahem. To znamená, že můžete určitě upravit soubor, ale musíte vytvořit projekt pro spuštění obnovení balíčku nebo vyvolání obnovení jiným způsobem. Viz [Obnovení balíčku](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

Soubor `project.lock.json` je generován v procesu obnovení NuGet balíčky `project.json`v projektech, které používají . Obsahuje snímek všechny informace, které jsou generovány jako NuGet procházky grafu balíčků a zahrnuje verzi, obsah a závislosti všech balíčků v projektu. Systém sestavení používá k výběru balíčků z globálního umístění, které jsou relevantní při vytváření projektu namísto v závislosti na místní složky balíčků v samotném projektu. To má za následek rychlejší výkon sestavení, `project.lock.json` protože je `.nuspec` nutné číst pouze namísto mnoha samostatných souborů.

`project.lock.json`je automaticky generovánpři obnovení balíčku, takže jej lze vynechat ze `.gitignore` `.tfignore` správy zdrojového kódu přidáním a souborů (viz [Balíčky a správa zdrojového kódu](../consume-packages/packages-and-source-control.md). Pokud jej však zahrnete do správy zdrojového kódu, historie změn zobrazí změny v závislostech vyřešených v průběhu času.
