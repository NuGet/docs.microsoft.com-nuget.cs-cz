---
title: Referenční dokumentace souboru Packages. config balíčků NuGet
description: V některých typech projektů soubor Packages. config udržuje seznam balíčků NuGet použitých v projektu.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3665989d35d7362b30a106cf6b4ed0210619efee
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230561"
---
# <a name="packagesconfig-reference"></a>odkaz na soubor Packages. config

`packages.config` soubor se používá v některých typech projektů k údržbě seznamu balíčků, na které se odkazuje v projektu. To umožňuje, aby NuGet snadno obnovil závislosti projektu, když se projekt přepravuje na jiný počítač, jako je například server sestavení, bez všech těchto balíčků.

Je-li použito, `packages.config` obvykle umístěn v kořenovém adresáři projektu. Automaticky se vytvoří při spuštění první operace NuGet, ale je možné ji také vytvořit ručně, než spustíte jakékoli příkazy, jako je `nuget restore`.

Projekty, které používají [PackageReference](../consume-packages/Package-References-in-Project-Files.md) , nepoužívají `packages.config`.

## <a name="schema"></a>Schéma

Schéma je jednoduché: za standardní hlavičkou XML je jeden `<packages>` uzel, který obsahuje jeden nebo více `<package>` prvků, jeden pro každý odkaz. Každý prvek `<package>` může mít následující atributy:

| Atribut | Požadováno | Popis |
| --- | --- | --- |
| id | Ano | Identifikátor balíčku, jako je například Newtonsoft. JSON nebo Microsoft. AspNet. Mvc. | 
| Verze nástroje  | Ano | Přesná verze balíčku, který se má nainstalovat, například 3.1.1 nebo 4.2.5.11-Beta. Řetězec verze musí mít alespoň tři čísla; Čtvrtá je volitelná, stejně jako přípona předběžné verze. Rozsahy nejsou povoleny. | 
| targetFramework | Ne | [Moniker cílového rozhraní (TFM)](target-frameworks.md) , který se má použít při instalaci balíčku. Tato nastavení se zpočátku nastaví na cíl projektu při instalaci balíčku. V důsledku toho mohou mít různé prvky `<package>` různé TFM. Například pokud vytvoříte projekt, který cílí na .NET 4.5.2, balíčky nainstalované v tomto okamžiku budou používat TFM net452. Pokud budete, později přecílíte projekt na rozhraní .NET 4,6 a přidáte další balíčky, budou použity TFM z net46. Neshoda mezi cílovým a `targetFramework` atributem projektu vygeneruje upozornění. v takovém případě můžete ovlivněné balíčky přeinstalovat. | 
| Hodnota allowedversions | Ne | Rozsah povolených verzí pro tento balíček byl použit během aktualizace balíčku (viz téma [omezení verzí upgradu](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Neovlivňuje *,* ke které balíčku se nainstaluje během operace instalace nebo obnovení. Syntaxe se zobrazuje v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges) . Uživatelské rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah. | 
| DevelopmentDependency | Ne | Pokud samotný projekt vytvoří balíček NuGet, nastavení této `true` pro závislost zabrání zahrnutí tohoto balíčku při vytvoření nenáročného balíčku. Výchozí formát je `false`. | 

## <a name="examples"></a>Příklady

Následující `packages.config` odkazují na dvě závislosti:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Následující `packages.config` odkazuje devět balíčků, ale `Microsoft.Net.Compilers` nebudou zahrnuty při sestavování nenáročného balíčku z důvodu atributu `developmentDependency`. Odkaz na Newtonsoft. JSON taky omezuje aktualizace jenom na 8. x a 9. verze x.

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
