---
title: Odkaz na soubor packages.config NuGet
description: V některých typech projektů packages.config udržuje seznam balíčků NuGet použitých v projektu.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: da682197d4a156f9dff8ce169aab449a5392ef41
ms.sourcegitcommit: c19d398cecee3cad2d79a8b22650fc1988d41a3f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2021
ms.locfileid: "99260300"
---
# <a name="packagesconfig-reference"></a>Odkaz na packages.config

`packages.config`Soubor se používá v některých typech projektů k údržbě seznamu balíčků, na které se odkazuje v projektu. To umožňuje, aby NuGet snadno obnovil závislosti projektu, když se projekt přepravuje na jiný počítač, jako je například server sestavení, bez všech těchto balíčků.

Pokud je použit, `packages.config` je obvykle umístěn v kořenovém adresáři projektu. Automaticky se vytvoří při spuštění první operace NuGet, ale je možné ji také vytvořit ručně před spuštěním příkazů, jako je `nuget restore` .

Projekty, které používají [PackageReference](../consume-packages/Package-References-in-Project-Files.md) , nepoužívají `packages.config` .

## <a name="schema"></a>Schéma

Schéma je jednoduché: za standardní hlavičkou XML je jeden `<packages>` uzel, který obsahuje jeden nebo více `<package>` elementů, jeden pro každý odkaz. Každý `<package>` prvek může mít následující atributy:

| Atribut | Povinné | Popis |
| --- | --- | --- |
| id | Ano | Identifikátor balíčku, například Newtonsoft.jsna nebo Microsoft. AspNet. Mvc. | 
| verze | Ano | Přesná verze balíčku, který se má nainstalovat, například 3.1.1 nebo 4.2.5.11-Beta. Řetězec verze musí mít alespoň tři čísla; Čtvrtá je volitelná, stejně jako přípona předběžné verze. Rozsahy nejsou povoleny. | 
| targetFramework | Ne | [Moniker cílového rozhraní (TFM)](target-frameworks.md) , který se má použít při instalaci balíčku. Tato nastavení se zpočátku nastaví na cíl projektu při instalaci balíčku. V důsledku toho `<package>` mohou mít různé prvky různé TFM. Například pokud vytvoříte projekt, který cílí na .NET 4.5.2, balíčky nainstalované v tomto okamžiku budou používat TFM net452. Pokud budete, později přecílíte projekt na rozhraní .NET 4,6 a přidáte další balíčky, budou použity TFM z net46. Neshoda mezi cílovou a `targetFramework` atributovou vlastností projektu vygeneruje upozornění. v takovém případě můžete ovlivněné balíčky přeinstalovat. | 
| Hodnota allowedversions | Ne | Rozsah povolených verzí pro tento balíček byl použit během aktualizace balíčku (viz téma [omezení verzí upgradu](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Neovlivňuje *,* ke které balíčku se nainstaluje během operace instalace nebo obnovení. Syntaxe se zobrazuje v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges) . Uživatelské rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah. | 
| developmentDependency | Ne | Pokud samotný projekt vytvoří balíček NuGet, jeho nastavení na `true` hodnotu pro závislost zabraňuje tomu, aby tento balíček byl zahrnutý při vytvoření balíčku, který je k dispozici. Výchozí formát je `false`. | 

## <a name="examples"></a>Příklady

Následující odkazy `packages.config` odkazují na dvě závislosti:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Následující odkazy `packages.config` odkazují na devět balíčků, ale nebudou `Microsoft.Net.Compilers` zahrnuty při sestavování nenáročného balíčku z důvodu `developmentDependency` atributu. Odkaz na Newtonsoft.Jstaké omezuje aktualizace pouze na verze 8. x a 9. x.

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
