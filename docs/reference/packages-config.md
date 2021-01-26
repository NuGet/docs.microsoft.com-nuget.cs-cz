---
title: Odkaz na soubor packages.config NuGet
description: V některých typech projektů packages.config udržuje seznam balíčků NuGet použitých v projektu.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3e5db779f735cd42aa331f9f8a93496d32c8df54
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777625"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="f9b23-103">Odkaz na packages.config</span><span class="sxs-lookup"><span data-stu-id="f9b23-103">packages.config reference</span></span>

<span data-ttu-id="f9b23-104">`packages.config`Soubor se používá v některých typech projektů k údržbě seznamu balíčků, na které se odkazuje v projektu.</span><span class="sxs-lookup"><span data-stu-id="f9b23-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="f9b23-105">To umožňuje, aby NuGet snadno obnovil závislosti projektu, když se projekt přepravuje na jiný počítač, jako je například server sestavení, bez všech těchto balíčků.</span><span class="sxs-lookup"><span data-stu-id="f9b23-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="f9b23-106">Pokud je použit, `packages.config` je obvykle umístěn v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="f9b23-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="f9b23-107">Automaticky se vytvoří při spuštění první operace NuGet, ale je možné ji také vytvořit ručně před spuštěním příkazů, jako je `nuget restore` .</span><span class="sxs-lookup"><span data-stu-id="f9b23-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="f9b23-108">Projekty, které používají [PackageReference](../consume-packages/Package-References-in-Project-Files.md) , nepoužívají `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="f9b23-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="f9b23-109">Schéma</span><span class="sxs-lookup"><span data-stu-id="f9b23-109">Schema</span></span>

<span data-ttu-id="f9b23-110">Schéma je jednoduché: za standardní hlavičkou XML je jeden `<packages>` uzel, který obsahuje jeden nebo více `<package>` elementů, jeden pro každý odkaz.</span><span class="sxs-lookup"><span data-stu-id="f9b23-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="f9b23-111">Každý `<package>` prvek může mít následující atributy:</span><span class="sxs-lookup"><span data-stu-id="f9b23-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="f9b23-112">Atribut</span><span class="sxs-lookup"><span data-stu-id="f9b23-112">Attribute</span></span> | <span data-ttu-id="f9b23-113">Povinné</span><span class="sxs-lookup"><span data-stu-id="f9b23-113">Required</span></span> | <span data-ttu-id="f9b23-114">Popis</span><span class="sxs-lookup"><span data-stu-id="f9b23-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9b23-115">id</span><span class="sxs-lookup"><span data-stu-id="f9b23-115">id</span></span> | <span data-ttu-id="f9b23-116">Ano</span><span class="sxs-lookup"><span data-stu-id="f9b23-116">Yes</span></span> | <span data-ttu-id="f9b23-117">Identifikátor balíčku, například Newtonsoft.jsna nebo Microsoft. AspNet. Mvc.</span><span class="sxs-lookup"><span data-stu-id="f9b23-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="f9b23-118">verze</span><span class="sxs-lookup"><span data-stu-id="f9b23-118">version</span></span> | <span data-ttu-id="f9b23-119">Ano</span><span class="sxs-lookup"><span data-stu-id="f9b23-119">Yes</span></span> | <span data-ttu-id="f9b23-120">Přesná verze balíčku, který se má nainstalovat, například 3.1.1 nebo 4.2.5.11-Beta.</span><span class="sxs-lookup"><span data-stu-id="f9b23-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="f9b23-121">Řetězec verze musí mít alespoň tři čísla; Čtvrtá je volitelná, stejně jako přípona předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="f9b23-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="f9b23-122">Rozsahy nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="f9b23-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="f9b23-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="f9b23-123">targetFramework</span></span> | <span data-ttu-id="f9b23-124">No</span><span class="sxs-lookup"><span data-stu-id="f9b23-124">No</span></span> | <span data-ttu-id="f9b23-125">[Moniker cílového rozhraní (TFM)](target-frameworks.md) , který se má použít při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="f9b23-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="f9b23-126">Tato nastavení se zpočátku nastaví na cíl projektu při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="f9b23-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="f9b23-127">V důsledku toho `<package>` mohou mít různé prvky různé TFM.</span><span class="sxs-lookup"><span data-stu-id="f9b23-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="f9b23-128">Například pokud vytvoříte projekt, který cílí na .NET 4.5.2, balíčky nainstalované v tomto okamžiku budou používat TFM net452.</span><span class="sxs-lookup"><span data-stu-id="f9b23-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="f9b23-129">Pokud budete, později přecílíte projekt na rozhraní .NET 4,6 a přidáte další balíčky, budou použity TFM z net46.</span><span class="sxs-lookup"><span data-stu-id="f9b23-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="f9b23-130">Neshoda mezi cílovou a `targetFramework` atributovou vlastností projektu vygeneruje upozornění. v takovém případě můžete ovlivněné balíčky přeinstalovat.</span><span class="sxs-lookup"><span data-stu-id="f9b23-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="f9b23-131">Hodnota allowedversions</span><span class="sxs-lookup"><span data-stu-id="f9b23-131">allowedVersions</span></span> | <span data-ttu-id="f9b23-132">No</span><span class="sxs-lookup"><span data-stu-id="f9b23-132">No</span></span> | <span data-ttu-id="f9b23-133">Rozsah povolených verzí pro tento balíček byl použit během aktualizace balíčku (viz téma [omezení verzí upgradu](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="f9b23-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="f9b23-134">Neovlivňuje *,* ke které balíčku se nainstaluje během operace instalace nebo obnovení.</span><span class="sxs-lookup"><span data-stu-id="f9b23-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="f9b23-135">Syntaxe se zobrazuje v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges) .</span><span class="sxs-lookup"><span data-stu-id="f9b23-135">See [Package versioning](../concepts/package-versioning.md#version-ranges) for syntax.</span></span> <span data-ttu-id="f9b23-136">Uživatelské rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah.</span><span class="sxs-lookup"><span data-stu-id="f9b23-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="f9b23-137">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="f9b23-137">developmentDependency</span></span> | <span data-ttu-id="f9b23-138">No</span><span class="sxs-lookup"><span data-stu-id="f9b23-138">No</span></span> | <span data-ttu-id="f9b23-139">Pokud samotný projekt vytvoří balíček NuGet, jeho nastavení na `true` hodnotu pro závislost zabraňuje tomu, aby tento balíček byl zahrnutý při vytvoření balíčku, který je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="f9b23-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="f9b23-140">Výchozí formát je `false`.</span><span class="sxs-lookup"><span data-stu-id="f9b23-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="f9b23-141">Příklady</span><span class="sxs-lookup"><span data-stu-id="f9b23-141">Examples</span></span>

<span data-ttu-id="f9b23-142">Následující odkazy `packages.config` odkazují na dvě závislosti:</span><span class="sxs-lookup"><span data-stu-id="f9b23-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="f9b23-143">Následující odkazy `packages.config` odkazují na devět balíčků, ale nebudou `Microsoft.Net.Compilers` zahrnuty při sestavování nenáročného balíčku z důvodu `developmentDependency` atributu.</span><span class="sxs-lookup"><span data-stu-id="f9b23-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="f9b23-144">Odkaz na Newtonsoft.Jstaké omezuje aktualizace pouze na verze 8. x a 9. x.</span><span class="sxs-lookup"><span data-stu-id="f9b23-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
