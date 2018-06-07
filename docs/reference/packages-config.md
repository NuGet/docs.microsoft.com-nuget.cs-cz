---
title: Odkaz na soubor packages.config NuGet
description: V některých typů projektu souboru packages.config udržuje seznam balíčky NuGet použité v projektu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 2019ce5961a8237fbda855cd7d5b42948808be3a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817830"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="adcf2-103">odkaz na soubor Packages.config</span><span class="sxs-lookup"><span data-stu-id="adcf2-103">packages.config reference</span></span>

<span data-ttu-id="adcf2-104">`packages.config` Soubor se používá v některé typy projektů k údržbě seznamu balíčků odkazuje projektu.</span><span class="sxs-lookup"><span data-stu-id="adcf2-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="adcf2-105">To umožňuje správci balíčků NuGet snadno obnovte závislosti projektu při projekt, který má být přenosu na jiný počítač, například server sestavení bez tyto balíčky.</span><span class="sxs-lookup"><span data-stu-id="adcf2-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="adcf2-106">Pokud se používá, `packages.config` se obvykle nachází v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="adcf2-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="adcf2-107">Je vytvořeno automaticky při spuštění první NuGet operaci, ale můžete také vytvořit ručně před spuštěním žádné příkazy, jako například `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="adcf2-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="adcf2-108">Projekty využívající [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nepoužívejte `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="adcf2-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="adcf2-109">Schéma</span><span class="sxs-lookup"><span data-stu-id="adcf2-109">Schema</span></span>

<span data-ttu-id="adcf2-110">Schéma je jednoduchý: následující standardní hlavičku XML je jediný `<packages>` uzlu, který obsahuje jeden nebo více `<package>` prvky, jednu pro každý odkaz.</span><span class="sxs-lookup"><span data-stu-id="adcf2-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="adcf2-111">Každý `<package>` element může obsahovat následující atributy:</span><span class="sxs-lookup"><span data-stu-id="adcf2-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="adcf2-112">Atribut</span><span class="sxs-lookup"><span data-stu-id="adcf2-112">Attribute</span></span> | <span data-ttu-id="adcf2-113">Požadováno</span><span class="sxs-lookup"><span data-stu-id="adcf2-113">Required</span></span> | <span data-ttu-id="adcf2-114">Popis</span><span class="sxs-lookup"><span data-stu-id="adcf2-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="adcf2-115">id</span><span class="sxs-lookup"><span data-stu-id="adcf2-115">id</span></span> | <span data-ttu-id="adcf2-116">Ano</span><span class="sxs-lookup"><span data-stu-id="adcf2-116">Yes</span></span> | <span data-ttu-id="adcf2-117">Identifikátor balíčku, například Newtonsoft.json nebo Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="adcf2-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="adcf2-118">verze</span><span class="sxs-lookup"><span data-stu-id="adcf2-118">version</span></span> | <span data-ttu-id="adcf2-119">Ano</span><span class="sxs-lookup"><span data-stu-id="adcf2-119">Yes</span></span> | <span data-ttu-id="adcf2-120">Přesné verze balíčku, který má nainstalovat, jako je například 3.1.1 nebo 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="adcf2-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="adcf2-121">Řetězec verze o musí mít alespoň tří čísel. čtvrtý je volitelný, jako je příponu předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="adcf2-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="adcf2-122">Rozsahy nejsou povolené.</span><span class="sxs-lookup"><span data-stu-id="adcf2-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="adcf2-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="adcf2-123">targetFramework</span></span> | <span data-ttu-id="adcf2-124">Ne</span><span class="sxs-lookup"><span data-stu-id="adcf2-124">No</span></span> | <span data-ttu-id="adcf2-125">[Cíle Přezdívka framework (TFM)](target-frameworks.md) použít při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="adcf2-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="adcf2-126">To je původně nastavení projektu cíl při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="adcf2-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="adcf2-127">V důsledku různých `<package>` elementy může mít různé TFMs.</span><span class="sxs-lookup"><span data-stu-id="adcf2-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="adcf2-128">Například pokud vytvoříte projekt cílení na rozhraní .NET 4.5.2, balíčky nainstalované v tomto bodě použije TFM net452.</span><span class="sxs-lookup"><span data-stu-id="adcf2-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="adcf2-129">Pokud jste; později změnit cílový projektu na .NET 4.6 a přidat další balíčky těch, které budou používat TFM net46.</span><span class="sxs-lookup"><span data-stu-id="adcf2-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="adcf2-130">Neshoda mezi cíle projektu a `targetFramework` atributy, vydá upozornění, v takovém případě můžete přeinstalovat, ovlivněných balíčků.</span><span class="sxs-lookup"><span data-stu-id="adcf2-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="adcf2-131">Hodnota allowedVersions</span><span class="sxs-lookup"><span data-stu-id="adcf2-131">allowedVersions</span></span> | <span data-ttu-id="adcf2-132">Ne</span><span class="sxs-lookup"><span data-stu-id="adcf2-132">No</span></span> | <span data-ttu-id="adcf2-133">Rozsah povolených verzí pro tento balíček použít při aktualizaci balíčku (viz [Constraining upgradu verze](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="adcf2-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="adcf2-134">Provede *není* ovlivnit jakém jsou balíčku je nainstalován během instalace nebo obnovení.</span><span class="sxs-lookup"><span data-stu-id="adcf2-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="adcf2-135">V tématu [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="adcf2-135">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="adcf2-136">Rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah.</span><span class="sxs-lookup"><span data-stu-id="adcf2-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="adcf2-137">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="adcf2-137">developmentDependency</span></span> | <span data-ttu-id="adcf2-138">Ne</span><span class="sxs-lookup"><span data-stu-id="adcf2-138">No</span></span> | <span data-ttu-id="adcf2-139">Pokud využívání projektu samotné vytvoří balíček NuGet, nastavíte jako `true` pro závislost zabraňuje zahrnutí při využívání balíček je vytvořen tento balíček.</span><span class="sxs-lookup"><span data-stu-id="adcf2-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="adcf2-140">Výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="adcf2-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="adcf2-141">Příklady</span><span class="sxs-lookup"><span data-stu-id="adcf2-141">Examples</span></span>

<span data-ttu-id="adcf2-142">Následující `packages.config` odkazuje na dva závislosti:</span><span class="sxs-lookup"><span data-stu-id="adcf2-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="adcf2-143">Následující `packages.config` odkazuje na devět balíčků, ale `Microsoft.Net.Compilers` nebudou zahrnuty při sestavování náročné balíček z důvodu `developmentDependency` atribut.</span><span class="sxs-lookup"><span data-stu-id="adcf2-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="adcf2-144">Odkaz na Newtonsoft.Json také omezuje aktualizace na 8.x a 9.x verze.</span><span class="sxs-lookup"><span data-stu-id="adcf2-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
