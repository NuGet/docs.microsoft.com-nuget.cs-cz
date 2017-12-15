---
title: Odkaz na soubor packages.config NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 207b9547-4558-41dc-9f3f-4bbdfb1d74e3
description: "V některých typů projektu souboru packages.config udržuje seznam balíčky NuGet použité v projektu."
keywords: "Soubor packages.config NuGet, odkazů na balíček NuGet se závislostí NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d851a09fad45ca25edc95ecee496bbf399f5e255
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="packagesconfig-reference"></a>odkaz na soubor Packages.config

`packages.config` Soubor se používá v některé typy projektů k údržbě seznamu balíčků odkazuje projektu. To umožňuje správci balíčků NuGet snadno obnovte závislosti projektu při projekt, který má být přenosu na jiný počítač, například server sestavení bez tyto balíčky.

## <a name="schema"></a>Schéma

Schéma je jednoduchý: následující standardní hlavičku XML je jediný `<packages>` uzlu, který obsahuje jeden nebo více `<package>` prvky, jednu pro každý odkaz. Každý `<package>` element může obsahovat následující atributy:

| Atribut | Požadováno | Popis |
| --- | --- | --- |
| id | Ano | Identifikátor balíčku, například Newtonsoft.json nebo Microsoft.AspNet.Mvc. | 
| verze | Ano | Přesné verze balíčku, který má nainstalovat, jako je například 3.1.1 nebo 4.2.5.11-beta. Řetězec verze o musí mít alespoň tří čísel. čtvrtý je volitelný, jako je příponu předběžné verze. Rozsahy nejsou povolené. | 
| targetFramework | Ne | [Cíle Přezdívka framework (TFM)](Target-Frameworks.md) použít při instalaci balíčku. To je původně nastavení projektu cíl při instalaci balíčku. V důsledku různých `<package>` elementy může mít různé TFMs. Například pokud vytvoříte projekt cílení na rozhraní .NET 4.5.2, balíčky nainstalované v tomto bodě použije TFM net452. Pokud jste; později změnit cílový projektu na .NET 4.6 a přidat další balíčky těch, které budou používat TFM net46. Neshoda mezi cíle projektu a `targetFramework` atributy, vydá upozornění, v takovém případě můžete přeinstalovat, ovlivněných balíčků. | 
| Hodnota allowedVersions | Ne | Rozsah povolených verzí pro tento balíček použít při aktualizaci balíčku (viz [Constraining upgradu verze](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Provede *není* ovlivnit jakém jsou balíčku je nainstalován během instalace nebo obnovení. V tématu [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards) syntaxe. Rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah. | 
| DevelopmentDependency | Ne | Pokud využívání projektu samotné vytvoří balíček NuGet, nastavíte jako `true` pro závislost zabraňuje zahrnutí při využívání balíček je vytvořen tento balíček. Výchozí hodnota je `false`. | 

## <a name="examples"></a>Příklady

Následující `packages.config` odkazuje na dva závislosti:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Následující `packages.config` odkazuje na devět balíčků, ale `Microsoft.Net.Compilers` nebudou zahrnuty při sestavování náročné balíček z důvodu `developmentDependency` atribut. Odkaz na Newtonsoft.Json také omezuje aktualizace na 8.x a 9.x verze.

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
