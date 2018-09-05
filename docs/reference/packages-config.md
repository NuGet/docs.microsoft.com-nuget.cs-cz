---
title: Odkaz na soubor packages.config NuGet
description: V některých typech projektů souboru packages.config udržuje seznam balíčky NuGet používané v projektu.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 18566671b611899b28fcc8542cf53935f5ee2dfd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551767"
---
# <a name="packagesconfig-reference"></a>odkaz na soubor Packages.config

`packages.config` Soubor je používán v některých typech projektů pro zachování seznam balíčků, které jsou odkazované projektem. To umožňuje snadno obnovit projektu závislosti balíčků NuGet při projekt tak, aby přenést k jinému počítači, jako je například server sestavení, aniž by tyto balíčky.

Pokud použijete, `packages.config` se obvykle nachází v kořenovém adresáři projektu. Je vytvořeno automaticky při spuštění první operace NuGet, ale můžete také vytvořit ručně před spuštěním libovolné příkazy, jako `nuget restore`.

Projekty, které používají [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nepoužívejte `packages.config`.

## <a name="schema"></a>Schéma

Schéma je jednoduchý: následující standardní záhlaví XML je jedinou `<packages>` uzel, který obsahuje jeden nebo více `<package>` prvky, jeden pro každý odkaz. Každý `<package>` prvek může mít následující atributy:

| Atribut | Požadováno | Popis |
| --- | --- | --- |
| id | Ano | Identifikátor balíčku, jako je například Newtonsoft.json nebo Microsoft.AspNet.Mvc. | 
| verze | Ano | Přesné verze balíčku k instalaci, jako je například 3.1.1 nebo 4.2.5.11-beta. Řetězec verze musí mít aspoň tří čísel. čtvrtý je volitelný, protože je příponu předběžné verze. Rozsahy nejsou povolené. | 
| targetFramework | Ne | [Cílit na moniker rozhraní (TFM)](target-frameworks.md) použít při instalaci balíčku. To je zpočátku nastaven k cíli projektu při instalaci balíčku. Jako výsledek různých `<package>` prvky mohou mít různé Tfm. Například pokud vytvoříte projekt cílí na .NET 4.5.2, balíčky nainstalované v tomto okamžiku bude používat TFM net452. Pokud jste; později změnit cílení projektů pro .NET 4.6 a přidat další balíčky, ty budou používat TFM net46. Neshoda mezi cílového projektu a `targetFramework` atributy vygeneruje upozornění, v takovém případě můžete znovu nainstalovat ovlivněné balíčky. | 
| Hodnota allowedVersions | Ne | Rozsah povolených verzí pro tento balíček použít při aktualizaci balíčku (viz [verze k upgradu Constraining](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Provádí *není* ovlivňují, jaké balíček nainstaluje při instalaci nebo operace obnovení. Zobrazit [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) syntaxi. Uživatelské rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah. | 
| DevelopmentDependency | Ne | Pokud používání vlastní projekt vytvoří balíček NuGet, nastavíte tuto možnost na `true` pro závislosti brání tento balíček nebudou zahrnuty při používání balíčku. Výchozí hodnota je `false`. | 

## <a name="examples"></a>Příklady

Následující `packages.config` odkazuje na dvě závislosti:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Následující `packages.config` odkazuje na devět balíčků, ale `Microsoft.Net.Compilers` nebudou zahrnuty při sestavování z důvodu spotřebitelskou balíčku `developmentDependency` atribut. Odkaz na Newtonsoft.Json také povoluje aktualizace pouze 8.x a 9.x verze.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
