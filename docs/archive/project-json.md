---
title: project.jsodkaz na soubor pro NuGet
description: V některých typech projektů project.jszachovává seznam balíčků NuGet použitých v projektu.
author: JonDouglas
ms.author: jodou
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 6665f4f3e688cb4a3989216c8c8f1a8655b61ed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775201"
---
# <a name="projectjson-reference"></a>project.jsna referenci

*NuGet 3. x +*

`project.json`Soubor uchovává seznam balíčků použitých v projektu, označovaných jako formát správy balíčků. Nahrazuje, `packages.config` ale je zase nahrazen [PackageReferenceem](../consume-packages/package-references-in-project-files.md) s NuGet 4.0 +.

[`project.lock.json`](#projectlockjson)Soubor (popsaný níže) se používá také v projektech, které používají `project.json` .

`project.json` má následující základní strukturu, kde každý ze čtyř objektů nejvyšší úrovně může mít libovolný počet podřízených objektů:

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

Zobrazí seznam závislostí balíčku NuGet v projektu v následujícím tvaru:

```json
"PackageID" : "version_constraint"
```

Například:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

V tomto `dependencies` oddílu se v dialogovém okně Správce balíčků NuGet do projektu přidají závislosti balíčků.

ID balíčku odpovídá ID balíčku v nuget.org, stejné jako ID použité v konzole správce balíčků: `Install-Package Microsoft.NETCore` .

Při obnovování balíčků má omezení verze `"5.0.0"` implikuje `>= 5.0.0` . To znamená, že pokud 5.0.0 není na serveru k dispozici, ale 5.0.1 je, NuGet nainstaluje 5.0.1 a upozorní vás na upgrade. NuGet v opačném případě vybere nejnižší možnou verzi serveru, který odpovídá omezení.

Další podrobnosti o pravidlech řešení najdete v tématu věnovaném [řešení závislostí](../concepts/dependency-resolution.md) .

### <a name="managing-dependency-assets"></a>Správa prostředků závislosti

Které prostředky ze závislostí toků do projektu nejvyšší úrovně jsou kontrolovány zadáním sady značek oddělených čárkami ve `include` `exclude` vlastnostech a odkazu na závislost. Značky jsou uvedeny v následující tabulce:

| Značka include/Exclude | Ovlivněné složky v cíli |
| --- | --- |
| contentFiles | Content  |
| modul runtime | Modul runtime, prostředky a FrameworkAssemblies  |
| kompilovat | Knihovna |
| sestavení | Build (MSBuild props and targets) |
| nativní | nativní |
| žádné | Žádné složky |
| Vše | Všechny složky |

Zadané značky s `exclude` prioritou mají přednost před hodnotami určenými pomocí `include` . Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"` .

Pokud například chcete zahrnout `build` složky a pro `native` závislost, použijte následující:

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

Pokud chcete vyloučit `content` složky a v `build` závislosti, použijte následující:

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

Obsahuje seznam rozhraní, na kterých je projekt spuštěn, například `net45` , `netcoreapp` , `netstandard` .

```json
"frameworks": {
    "netcore50": {}
    }
 ```

V části je povolená jenom jedna položka `frameworks` . (Výjimkou jsou `project.json` soubory pro projekty ASP.NET, které jsou sestaveny pomocí zastaralého řetězce nástroje DNX, který umožňuje více cílů.)

## <a name="runtimes"></a>Moduly runtime

Obsahuje seznam operačních systémů a architektur, na kterých běží vaše aplikace, jako je například, `win10-arm` `win8-x64` `win8-x86` .

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

Balíček obsahující PCL, který může běžet v jakémkoli modulu runtime, nemusí určovat modul runtime. Tato hodnota musí být také pravdivá pro jakékoli závislosti, jinak musíte zadat moduly runtime.


## <a name="supports"></a>Podporuje

Definuje sadu kontrol pro závislosti balíčku. Můžete definovat, kde očekáváte, že se má jazyk PCL nebo aplikace spustit. Definice nejsou omezující, protože váš kód může být možné spustit jinde. Ale zadáním těchto kontrol vrátí NuGet kontrolu nad tím, že všechny závislosti jsou splněné na uvedených TxMs. Příklady hodnot pro tyto hodnoty jsou: `net46.app` , `uwp.10.0.app` , atd.

Tato část by měla být naplněna automaticky při výběru položky v dialogovém okně cíle knihovny tříd.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Objem

Importy jsou navržené tak, aby umožňovaly balíčkům, které používají `dotnet` TxM k práci s balíčky, které nedeklarují dotnet TxM. Pokud váš projekt používá `dotnet` TxM, pak všechny balíčky, na kterých závisí, musí mít také `dotnet` TxM, pokud do své služby nepřidáte následující, aby bylo možné `project.json` `dotnet` nekompatibilní s platformou `dotnet` :

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Pokud používáte `dotnet` TxM, pak systém projektu PCL přidá příslušný `imports` příkaz na základě podporovaných cílů.

## <a name="differences-from-portable-apps-and-web-projects"></a>Rozdíly mezi přenosnými aplikacemi a webovými projekty

`project.json`Soubor používaný NuGet je podmnožina nástroje, která se nachází v ASP.NET Corech projektech. V ASP.NET Core `project.json` se používá pro metadata projektu, informace o kompilaci a závislosti. Při použití v jiných systémech projektů jsou tyto tři věci rozděleny do samostatných souborů a `project.json` obsahují méně informací. Mezi významné rozdíly patří:

- V části může být pouze jedna architektura `frameworks` .

- Soubor nemůže obsahovat závislosti, možnosti kompilace atd., které vidíte v `project.json` souborech DNX. Vzhledem k tomu, že může existovat pouze jeden rámec, nemá smysl zadat závislosti specifické pro rozhraní.

- Kompilace je zpracována nástrojem MSBuild, takže možnosti kompilace, definice preprocesoru atd. jsou všechny součástí souboru projektu MSBuild a nikoli `project.json` .

V NuGet 3 + se vývojáři neočekávají ruční úpravou `project.json` , protože uživatelské rozhraní Správce balíčků v aplikaci Visual Studio pracuje s obsahem. V takovém případě můžete soubor upravovat, ale je nutné sestavit projekt, aby bylo možné spustit obnovení balíčku nebo vyvolat obnovení jiným způsobem. Viz [obnovení balíčku](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.jsna

`project.lock.json`Soubor se vygeneruje v procesu obnovení balíčků NuGet v projektech, které používají `project.json` . Obsahuje snímek všech informací, které jsou generovány s tím, že NuGet projde graf balíčků a obsahuje verzi, obsah a závislosti všech balíčků v projektu. Systém sestavení používá tuto možnost k výběru balíčků z globálního umístění, které je relevantní při sestavování projektu, nikoli v závislosti na místní složce balíčků v samotném projektu. Výsledkem je rychlejší sestavování výkonu, protože je nutné číst pouze `project.lock.json` místo mnoha samostatných `.nuspec` souborů.

`project.lock.json` se automaticky generuje při obnovení balíčku, takže ho můžete vypustit ze správy zdrojového kódu, a to tak, že ho přidáte do `.gitignore` `.tfignore` souborů a (viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md). Pokud však zahrnete je do správy zdrojového kódu, zobrazí se v historii změn v průběhu času změny v závislostech.
