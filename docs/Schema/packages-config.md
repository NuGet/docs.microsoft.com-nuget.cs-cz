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
# <a name="packagesconfig-reference"></a><span data-ttu-id="99ba2-104">odkaz na soubor Packages.config</span><span class="sxs-lookup"><span data-stu-id="99ba2-104">packages.config reference</span></span>

<span data-ttu-id="99ba2-105">`packages.config` Soubor se používá v některé typy projektů k údržbě seznamu balíčků odkazuje projektu.</span><span class="sxs-lookup"><span data-stu-id="99ba2-105">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="99ba2-106">To umožňuje správci balíčků NuGet snadno obnovte závislosti projektu při projekt, který má být přenosu na jiný počítač, například server sestavení bez tyto balíčky.</span><span class="sxs-lookup"><span data-stu-id="99ba2-106">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="99ba2-107">Schéma</span><span class="sxs-lookup"><span data-stu-id="99ba2-107">Schema</span></span>

<span data-ttu-id="99ba2-108">Schéma je jednoduchý: následující standardní hlavičku XML je jediný `<packages>` uzlu, který obsahuje jeden nebo více `<package>` prvky, jednu pro každý odkaz.</span><span class="sxs-lookup"><span data-stu-id="99ba2-108">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="99ba2-109">Každý `<package>` element může obsahovat následující atributy:</span><span class="sxs-lookup"><span data-stu-id="99ba2-109">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="99ba2-110">Atribut</span><span class="sxs-lookup"><span data-stu-id="99ba2-110">Attribute</span></span> | <span data-ttu-id="99ba2-111">Požadováno</span><span class="sxs-lookup"><span data-stu-id="99ba2-111">Required</span></span> | <span data-ttu-id="99ba2-112">Popis</span><span class="sxs-lookup"><span data-stu-id="99ba2-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99ba2-113">id</span><span class="sxs-lookup"><span data-stu-id="99ba2-113">id</span></span> | <span data-ttu-id="99ba2-114">Ano</span><span class="sxs-lookup"><span data-stu-id="99ba2-114">Yes</span></span> | <span data-ttu-id="99ba2-115">Identifikátor balíčku, například Newtonsoft.json nebo Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="99ba2-115">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="99ba2-116">verze</span><span class="sxs-lookup"><span data-stu-id="99ba2-116">version</span></span> | <span data-ttu-id="99ba2-117">Ano</span><span class="sxs-lookup"><span data-stu-id="99ba2-117">Yes</span></span> | <span data-ttu-id="99ba2-118">Přesné verze balíčku, který má nainstalovat, jako je například 3.1.1 nebo 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="99ba2-118">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="99ba2-119">Řetězec verze o musí mít alespoň tří čísel. čtvrtý je volitelný, jako je příponu předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="99ba2-119">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="99ba2-120">Rozsahy nejsou povolené.</span><span class="sxs-lookup"><span data-stu-id="99ba2-120">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="99ba2-121">targetFramework</span><span class="sxs-lookup"><span data-stu-id="99ba2-121">targetFramework</span></span> | <span data-ttu-id="99ba2-122">Ne</span><span class="sxs-lookup"><span data-stu-id="99ba2-122">No</span></span> | <span data-ttu-id="99ba2-123">[Cíle Přezdívka framework (TFM)](Target-Frameworks.md) použít při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="99ba2-123">The [target framework moniker (TFM)](Target-Frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="99ba2-124">To je původně nastavení projektu cíl při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="99ba2-124">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="99ba2-125">V důsledku různých `<package>` elementy může mít různé TFMs.</span><span class="sxs-lookup"><span data-stu-id="99ba2-125">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="99ba2-126">Například pokud vytvoříte projekt cílení na rozhraní .NET 4.5.2, balíčky nainstalované v tomto bodě použije TFM net452.</span><span class="sxs-lookup"><span data-stu-id="99ba2-126">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="99ba2-127">Pokud jste; později změnit cílový projektu na .NET 4.6 a přidat další balíčky těch, které budou používat TFM net46.</span><span class="sxs-lookup"><span data-stu-id="99ba2-127">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="99ba2-128">Neshoda mezi cíle projektu a `targetFramework` atributy, vydá upozornění, v takovém případě můžete přeinstalovat, ovlivněných balíčků.</span><span class="sxs-lookup"><span data-stu-id="99ba2-128">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="99ba2-129">Hodnota allowedVersions</span><span class="sxs-lookup"><span data-stu-id="99ba2-129">allowedVersions</span></span> | <span data-ttu-id="99ba2-130">Ne</span><span class="sxs-lookup"><span data-stu-id="99ba2-130">No</span></span> | <span data-ttu-id="99ba2-131">Rozsah povolených verzí pro tento balíček použít při aktualizaci balíčku (viz [Constraining upgradu verze](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="99ba2-131">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="99ba2-132">Provede *není* ovlivnit jakém jsou balíčku je nainstalován během instalace nebo obnovení.</span><span class="sxs-lookup"><span data-stu-id="99ba2-132">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="99ba2-133">V tématu [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="99ba2-133">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="99ba2-134">Rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah.</span><span class="sxs-lookup"><span data-stu-id="99ba2-134">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="99ba2-135">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="99ba2-135">developmentDependency</span></span> | <span data-ttu-id="99ba2-136">Ne</span><span class="sxs-lookup"><span data-stu-id="99ba2-136">No</span></span> | <span data-ttu-id="99ba2-137">Pokud využívání projektu samotné vytvoří balíček NuGet, nastavíte jako `true` pro závislost zabraňuje zahrnutí při využívání balíček je vytvořen tento balíček.</span><span class="sxs-lookup"><span data-stu-id="99ba2-137">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="99ba2-138">Výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="99ba2-138">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="99ba2-139">Příklady</span><span class="sxs-lookup"><span data-stu-id="99ba2-139">Examples</span></span>

<span data-ttu-id="99ba2-140">Následující `packages.config` odkazuje na dva závislosti:</span><span class="sxs-lookup"><span data-stu-id="99ba2-140">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="99ba2-141">Následující `packages.config` odkazuje na devět balíčků, ale `Microsoft.Net.Compilers` nebudou zahrnuty při sestavování náročné balíček z důvodu `developmentDependency` atribut.</span><span class="sxs-lookup"><span data-stu-id="99ba2-141">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="99ba2-142">Odkaz na Newtonsoft.Json také omezuje aktualizace na 8.x a 9.x verze.</span><span class="sxs-lookup"><span data-stu-id="99ba2-142">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
