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
# <a name="packagesconfig-reference"></a><span data-ttu-id="06c63-103">odkaz na soubor Packages.config</span><span class="sxs-lookup"><span data-stu-id="06c63-103">packages.config reference</span></span>

<span data-ttu-id="06c63-104">`packages.config` Soubor je používán v některých typech projektů pro zachování seznam balíčků, které jsou odkazované projektem.</span><span class="sxs-lookup"><span data-stu-id="06c63-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="06c63-105">To umožňuje snadno obnovit projektu závislosti balíčků NuGet při projekt tak, aby přenést k jinému počítači, jako je například server sestavení, aniž by tyto balíčky.</span><span class="sxs-lookup"><span data-stu-id="06c63-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="06c63-106">Pokud použijete, `packages.config` se obvykle nachází v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="06c63-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="06c63-107">Je vytvořeno automaticky při spuštění první operace NuGet, ale můžete také vytvořit ručně před spuštěním libovolné příkazy, jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="06c63-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="06c63-108">Projekty, které používají [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nepoužívejte `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="06c63-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="06c63-109">Schéma</span><span class="sxs-lookup"><span data-stu-id="06c63-109">Schema</span></span>

<span data-ttu-id="06c63-110">Schéma je jednoduchý: následující standardní záhlaví XML je jedinou `<packages>` uzel, který obsahuje jeden nebo více `<package>` prvky, jeden pro každý odkaz.</span><span class="sxs-lookup"><span data-stu-id="06c63-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="06c63-111">Každý `<package>` prvek může mít následující atributy:</span><span class="sxs-lookup"><span data-stu-id="06c63-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="06c63-112">Atribut</span><span class="sxs-lookup"><span data-stu-id="06c63-112">Attribute</span></span> | <span data-ttu-id="06c63-113">Požadováno</span><span class="sxs-lookup"><span data-stu-id="06c63-113">Required</span></span> | <span data-ttu-id="06c63-114">Popis</span><span class="sxs-lookup"><span data-stu-id="06c63-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06c63-115">id</span><span class="sxs-lookup"><span data-stu-id="06c63-115">id</span></span> | <span data-ttu-id="06c63-116">Ano</span><span class="sxs-lookup"><span data-stu-id="06c63-116">Yes</span></span> | <span data-ttu-id="06c63-117">Identifikátor balíčku, jako je například Newtonsoft.json nebo Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="06c63-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="06c63-118">verze</span><span class="sxs-lookup"><span data-stu-id="06c63-118">version</span></span> | <span data-ttu-id="06c63-119">Ano</span><span class="sxs-lookup"><span data-stu-id="06c63-119">Yes</span></span> | <span data-ttu-id="06c63-120">Přesné verze balíčku k instalaci, jako je například 3.1.1 nebo 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="06c63-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="06c63-121">Řetězec verze musí mít aspoň tří čísel. čtvrtý je volitelný, protože je příponu předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="06c63-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="06c63-122">Rozsahy nejsou povolené.</span><span class="sxs-lookup"><span data-stu-id="06c63-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="06c63-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="06c63-123">targetFramework</span></span> | <span data-ttu-id="06c63-124">Ne</span><span class="sxs-lookup"><span data-stu-id="06c63-124">No</span></span> | <span data-ttu-id="06c63-125">[Cílit na moniker rozhraní (TFM)](target-frameworks.md) použít při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="06c63-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="06c63-126">To je zpočátku nastaven k cíli projektu při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="06c63-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="06c63-127">Jako výsledek různých `<package>` prvky mohou mít různé Tfm.</span><span class="sxs-lookup"><span data-stu-id="06c63-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="06c63-128">Například pokud vytvoříte projekt cílí na .NET 4.5.2, balíčky nainstalované v tomto okamžiku bude používat TFM net452.</span><span class="sxs-lookup"><span data-stu-id="06c63-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="06c63-129">Pokud jste; později změnit cílení projektů pro .NET 4.6 a přidat další balíčky, ty budou používat TFM net46.</span><span class="sxs-lookup"><span data-stu-id="06c63-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="06c63-130">Neshoda mezi cílového projektu a `targetFramework` atributy vygeneruje upozornění, v takovém případě můžete znovu nainstalovat ovlivněné balíčky.</span><span class="sxs-lookup"><span data-stu-id="06c63-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="06c63-131">Hodnota allowedVersions</span><span class="sxs-lookup"><span data-stu-id="06c63-131">allowedVersions</span></span> | <span data-ttu-id="06c63-132">Ne</span><span class="sxs-lookup"><span data-stu-id="06c63-132">No</span></span> | <span data-ttu-id="06c63-133">Rozsah povolených verzí pro tento balíček použít při aktualizaci balíčku (viz [verze k upgradu Constraining](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="06c63-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="06c63-134">Provádí *není* ovlivňují, jaké balíček nainstaluje při instalaci nebo operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="06c63-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="06c63-135">Zobrazit [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) syntaxi.</span><span class="sxs-lookup"><span data-stu-id="06c63-135">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="06c63-136">Uživatelské rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah.</span><span class="sxs-lookup"><span data-stu-id="06c63-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="06c63-137">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="06c63-137">developmentDependency</span></span> | <span data-ttu-id="06c63-138">Ne</span><span class="sxs-lookup"><span data-stu-id="06c63-138">No</span></span> | <span data-ttu-id="06c63-139">Pokud používání vlastní projekt vytvoří balíček NuGet, nastavíte tuto možnost na `true` pro závislosti brání tento balíček nebudou zahrnuty při používání balíčku.</span><span class="sxs-lookup"><span data-stu-id="06c63-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="06c63-140">Výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="06c63-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="06c63-141">Příklady</span><span class="sxs-lookup"><span data-stu-id="06c63-141">Examples</span></span>

<span data-ttu-id="06c63-142">Následující `packages.config` odkazuje na dvě závislosti:</span><span class="sxs-lookup"><span data-stu-id="06c63-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="06c63-143">Následující `packages.config` odkazuje na devět balíčků, ale `Microsoft.Net.Compilers` nebudou zahrnuty při sestavování z důvodu spotřebitelskou balíčku `developmentDependency` atribut.</span><span class="sxs-lookup"><span data-stu-id="06c63-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="06c63-144">Odkaz na Newtonsoft.Json také povoluje aktualizace pouze 8.x a 9.x verze.</span><span class="sxs-lookup"><span data-stu-id="06c63-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
