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
# <a name="packagesconfig-reference"></a><span data-ttu-id="5d33d-103">odkaz na soubor Packages. config</span><span class="sxs-lookup"><span data-stu-id="5d33d-103">packages.config reference</span></span>

<span data-ttu-id="5d33d-104">`packages.config` soubor se používá v některých typech projektů k údržbě seznamu balíčků, na které se odkazuje v projektu.</span><span class="sxs-lookup"><span data-stu-id="5d33d-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="5d33d-105">To umožňuje, aby NuGet snadno obnovil závislosti projektu, když se projekt přepravuje na jiný počítač, jako je například server sestavení, bez všech těchto balíčků.</span><span class="sxs-lookup"><span data-stu-id="5d33d-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="5d33d-106">Je-li použito, `packages.config` obvykle umístěn v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="5d33d-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="5d33d-107">Automaticky se vytvoří při spuštění první operace NuGet, ale je možné ji také vytvořit ručně, než spustíte jakékoli příkazy, jako je `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="5d33d-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="5d33d-108">Projekty, které používají [PackageReference](../consume-packages/Package-References-in-Project-Files.md) , nepoužívají `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5d33d-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="5d33d-109">Schéma</span><span class="sxs-lookup"><span data-stu-id="5d33d-109">Schema</span></span>

<span data-ttu-id="5d33d-110">Schéma je jednoduché: za standardní hlavičkou XML je jeden `<packages>` uzel, který obsahuje jeden nebo více `<package>` prvků, jeden pro každý odkaz.</span><span class="sxs-lookup"><span data-stu-id="5d33d-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="5d33d-111">Každý prvek `<package>` může mít následující atributy:</span><span class="sxs-lookup"><span data-stu-id="5d33d-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="5d33d-112">Atribut</span><span class="sxs-lookup"><span data-stu-id="5d33d-112">Attribute</span></span> | <span data-ttu-id="5d33d-113">Požadováno</span><span class="sxs-lookup"><span data-stu-id="5d33d-113">Required</span></span> | <span data-ttu-id="5d33d-114">Popis</span><span class="sxs-lookup"><span data-stu-id="5d33d-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d33d-115">id</span><span class="sxs-lookup"><span data-stu-id="5d33d-115">id</span></span> | <span data-ttu-id="5d33d-116">Ano</span><span class="sxs-lookup"><span data-stu-id="5d33d-116">Yes</span></span> | <span data-ttu-id="5d33d-117">Identifikátor balíčku, jako je například Newtonsoft. JSON nebo Microsoft. AspNet. Mvc.</span><span class="sxs-lookup"><span data-stu-id="5d33d-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="5d33d-118">Verze nástroje </span><span class="sxs-lookup"><span data-stu-id="5d33d-118">version</span></span> | <span data-ttu-id="5d33d-119">Ano</span><span class="sxs-lookup"><span data-stu-id="5d33d-119">Yes</span></span> | <span data-ttu-id="5d33d-120">Přesná verze balíčku, který se má nainstalovat, například 3.1.1 nebo 4.2.5.11-Beta.</span><span class="sxs-lookup"><span data-stu-id="5d33d-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="5d33d-121">Řetězec verze musí mít alespoň tři čísla; Čtvrtá je volitelná, stejně jako přípona předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="5d33d-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="5d33d-122">Rozsahy nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="5d33d-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="5d33d-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="5d33d-123">targetFramework</span></span> | <span data-ttu-id="5d33d-124">Ne</span><span class="sxs-lookup"><span data-stu-id="5d33d-124">No</span></span> | <span data-ttu-id="5d33d-125">[Moniker cílového rozhraní (TFM)](target-frameworks.md) , který se má použít při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d33d-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="5d33d-126">Tato nastavení se zpočátku nastaví na cíl projektu při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d33d-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="5d33d-127">V důsledku toho mohou mít různé prvky `<package>` různé TFM.</span><span class="sxs-lookup"><span data-stu-id="5d33d-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="5d33d-128">Například pokud vytvoříte projekt, který cílí na .NET 4.5.2, balíčky nainstalované v tomto okamžiku budou používat TFM net452.</span><span class="sxs-lookup"><span data-stu-id="5d33d-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="5d33d-129">Pokud budete, později přecílíte projekt na rozhraní .NET 4,6 a přidáte další balíčky, budou použity TFM z net46.</span><span class="sxs-lookup"><span data-stu-id="5d33d-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="5d33d-130">Neshoda mezi cílovým a `targetFramework` atributem projektu vygeneruje upozornění. v takovém případě můžete ovlivněné balíčky přeinstalovat.</span><span class="sxs-lookup"><span data-stu-id="5d33d-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="5d33d-131">Hodnota allowedversions</span><span class="sxs-lookup"><span data-stu-id="5d33d-131">allowedVersions</span></span> | <span data-ttu-id="5d33d-132">Ne</span><span class="sxs-lookup"><span data-stu-id="5d33d-132">No</span></span> | <span data-ttu-id="5d33d-133">Rozsah povolených verzí pro tento balíček byl použit během aktualizace balíčku (viz téma [omezení verzí upgradu](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="5d33d-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="5d33d-134">Neovlivňuje *,* ke které balíčku se nainstaluje během operace instalace nebo obnovení.</span><span class="sxs-lookup"><span data-stu-id="5d33d-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="5d33d-135">Syntaxe se zobrazuje v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges) .</span><span class="sxs-lookup"><span data-stu-id="5d33d-135">See [Package versioning](../concepts/package-versioning.md#version-ranges) for syntax.</span></span> <span data-ttu-id="5d33d-136">Uživatelské rozhraní PackageManager také zakáže všechny verze mimo povolený rozsah.</span><span class="sxs-lookup"><span data-stu-id="5d33d-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="5d33d-137">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="5d33d-137">developmentDependency</span></span> | <span data-ttu-id="5d33d-138">Ne</span><span class="sxs-lookup"><span data-stu-id="5d33d-138">No</span></span> | <span data-ttu-id="5d33d-139">Pokud samotný projekt vytvoří balíček NuGet, nastavení této `true` pro závislost zabrání zahrnutí tohoto balíčku při vytvoření nenáročného balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d33d-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="5d33d-140">Výchozí formát je `false`.</span><span class="sxs-lookup"><span data-stu-id="5d33d-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="5d33d-141">Příklady</span><span class="sxs-lookup"><span data-stu-id="5d33d-141">Examples</span></span>

<span data-ttu-id="5d33d-142">Následující `packages.config` odkazují na dvě závislosti:</span><span class="sxs-lookup"><span data-stu-id="5d33d-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="5d33d-143">Následující `packages.config` odkazuje devět balíčků, ale `Microsoft.Net.Compilers` nebudou zahrnuty při sestavování nenáročného balíčku z důvodu atributu `developmentDependency`.</span><span class="sxs-lookup"><span data-stu-id="5d33d-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="5d33d-144">Odkaz na Newtonsoft. JSON taky omezuje aktualizace jenom na 8. x a 9. verze x.</span><span class="sxs-lookup"><span data-stu-id="5d33d-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
