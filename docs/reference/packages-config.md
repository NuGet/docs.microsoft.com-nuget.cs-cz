---
title: Referenční dokumentace souboru Packages. config balíčků NuGet
description: V některých typech projektů soubor Packages. config udržuje seznam balíčků NuGet použitých v projektu.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 2fd1640295ca35304358565808a89d752cfd8abf
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488641"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="926dd-103">odkaz na soubor Packages. config</span><span class="sxs-lookup"><span data-stu-id="926dd-103">packages.config reference</span></span>

<span data-ttu-id="926dd-104">`packages.config` Soubor se používá v některých typech projektů k údržbě seznamu balíčků, na které se odkazuje v projektu.</span><span class="sxs-lookup"><span data-stu-id="926dd-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="926dd-105">To umožňuje, aby NuGet snadno obnovil závislosti projektu, když se projekt přepravuje na jiný počítač, jako je například server sestavení, bez všech těchto balíčků.</span><span class="sxs-lookup"><span data-stu-id="926dd-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="926dd-106">Pokud je použit `packages.config` , je obvykle umístěn v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="926dd-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="926dd-107">Automaticky se vytvoří při spuštění první operace NuGet, ale je možné ji také vytvořit ručně před spuštěním příkazů, jako je `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="926dd-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="926dd-108">Projekty, které používají [PackageReference](../consume-packages/Package-References-in-Project-Files.md) , nepoužívají `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="926dd-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="926dd-109">Schéma</span><span class="sxs-lookup"><span data-stu-id="926dd-109">Schema</span></span>

<span data-ttu-id="926dd-110">Schéma je jednoduché: za standardní hlavičkou XML je `<packages>` jeden uzel, který obsahuje jeden nebo více `<package>` elementů, jeden pro každý odkaz.</span><span class="sxs-lookup"><span data-stu-id="926dd-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="926dd-111">Každý `<package>` prvek může mít následující atributy:</span><span class="sxs-lookup"><span data-stu-id="926dd-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="926dd-112">Atribut</span><span class="sxs-lookup"><span data-stu-id="926dd-112">Attribute</span></span> | <span data-ttu-id="926dd-113">Požadováno</span><span class="sxs-lookup"><span data-stu-id="926dd-113">Required</span></span> | <span data-ttu-id="926dd-114">Popis</span><span class="sxs-lookup"><span data-stu-id="926dd-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="926dd-115">id</span><span class="sxs-lookup"><span data-stu-id="926dd-115">id</span></span> | <span data-ttu-id="926dd-116">Ano</span><span class="sxs-lookup"><span data-stu-id="926dd-116">Yes</span></span> | <span data-ttu-id="926dd-117">Identifikátor balíčku, jako je například Newtonsoft. JSON nebo Microsoft. AspNet. Mvc.</span><span class="sxs-lookup"><span data-stu-id="926dd-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="926dd-118">verze</span><span class="sxs-lookup"><span data-stu-id="926dd-118">version</span></span> | <span data-ttu-id="926dd-119">Ano</span><span class="sxs-lookup"><span data-stu-id="926dd-119">Yes</span></span> | <span data-ttu-id="926dd-120">Přesná verze balíčku, který se má nainstalovat, například 3.1.1 nebo 4.2.5.11-Beta.</span><span class="sxs-lookup"><span data-stu-id="926dd-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="926dd-121">Řetězec verze musí mít alespoň tři čísla; Čtvrtá je volitelná, stejně jako přípona předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="926dd-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="926dd-122">Rozsahy nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="926dd-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="926dd-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="926dd-123">targetFramework</span></span> | <span data-ttu-id="926dd-124">Ne</span><span class="sxs-lookup"><span data-stu-id="926dd-124">No</span></span> | <span data-ttu-id="926dd-125">[Moniker cílového rozhraní (TFM)](target-frameworks.md) , který se má použít při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="926dd-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="926dd-126">Tato nastavení se zpočátku nastaví na cíl projektu při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="926dd-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="926dd-127">V důsledku toho mohou mít `<package>` různé prvky různé TFM.</span><span class="sxs-lookup"><span data-stu-id="926dd-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="926dd-128">Například pokud vytvoříte projekt, který cílí na .NET 4.5.2, balíčky nainstalované v tomto okamžiku budou používat TFM net452.</span><span class="sxs-lookup"><span data-stu-id="926dd-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="926dd-129">Pokud budete, později přecílíte projekt na rozhraní .NET 4,6 a přidáte další balíčky, budou použity TFM z net46.</span><span class="sxs-lookup"><span data-stu-id="926dd-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="926dd-130">Neshoda mezi cílovou a `targetFramework` atributovou vlastností projektu vygeneruje upozornění. v takovém případě můžete ovlivněné balíčky přeinstalovat.</span><span class="sxs-lookup"><span data-stu-id="926dd-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="926dd-131">Hodnota allowedversions</span><span class="sxs-lookup"><span data-stu-id="926dd-131">allowedVersions</span></span> | <span data-ttu-id="926dd-132">Ne</span><span class="sxs-lookup"><span data-stu-id="926dd-132">No</span></span> | <span data-ttu-id="926dd-133">Rozsah povolených verzí pro tento balíček byl použit během aktualizace balíčku (viz téma [omezení verzí upgradu](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="926dd-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="926dd-134">Neovlivňuje , ke které balíčku se nainstaluje během operace instalace nebo obnovení.</span><span class="sxs-lookup"><span data-stu-id="926dd-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="926dd-135">Syntaxe se zobrazuje v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges-and-wildcards) .</span><span class="sxs-lookup"><span data-stu-id="926dd-135">See [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="926dd-136">Uživatelské rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah.</span><span class="sxs-lookup"><span data-stu-id="926dd-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="926dd-137">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="926dd-137">developmentDependency</span></span> | <span data-ttu-id="926dd-138">Ne</span><span class="sxs-lookup"><span data-stu-id="926dd-138">No</span></span> | <span data-ttu-id="926dd-139">Pokud samotný projekt vytvoří balíček NuGet, jeho nastavení na `true` hodnotu pro závislost zabraňuje tomu, aby tento balíček byl zahrnutý při vytvoření balíčku, který je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="926dd-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="926dd-140">Výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="926dd-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="926dd-141">Příklady</span><span class="sxs-lookup"><span data-stu-id="926dd-141">Examples</span></span>

<span data-ttu-id="926dd-142">Následující `packages.config` odkazy odkazují na dvě závislosti:</span><span class="sxs-lookup"><span data-stu-id="926dd-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="926dd-143">Následující `packages.config` odkazy odkazují na devět balíčků, ale `Microsoft.Net.Compilers` nebudou zahrnuty při sestavování `developmentDependency` nenáročného balíčku z důvodu atributu.</span><span class="sxs-lookup"><span data-stu-id="926dd-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="926dd-144">Odkaz na Newtonsoft. JSON taky omezuje aktualizace jenom na 8. x a 9. verze x.</span><span class="sxs-lookup"><span data-stu-id="926dd-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
