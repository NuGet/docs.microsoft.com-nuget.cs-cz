---
title: Nastavení typu balíčku NuGet
description: Popisuje typy balíčků k označení zamýšleného použití balíčku.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067272"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="a5961-103">Nastavení typu balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="a5961-103">Set a NuGet package type</span></span>

<span data-ttu-id="a5961-104">Balíčky lze označit dalšími dalšími *typy balíčků* k označení zamýšleného použití.</span><span class="sxs-lookup"><span data-stu-id="a5961-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="a5961-105">Známé typy balíčků</span><span class="sxs-lookup"><span data-stu-id="a5961-105">Known package types</span></span>

- <span data-ttu-id="a5961-106">`Dependency` balíčky typů přidávají prostředky pro sestavení nebo spuštění do knihoven a aplikací a mohou být nainstalovány v jakémkoli typu projektu (za předpokladu, že jsou kompatibilní).</span><span class="sxs-lookup"><span data-stu-id="a5961-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="a5961-107">`DotnetTool` balíčky typů jsou nástroje .NET, které lze nainstalovat pomocí rozhraní příkazového [řádku dotnet](/dotnet/articles/core/tools/index).</span><span class="sxs-lookup"><span data-stu-id="a5961-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="a5961-108">`Template` balíčky typů poskytují [vlastní šablony](/dotnet/core/tools/custom-templates) , které lze použít k vytvoření souborů nebo projektů, jako jsou aplikace, služby, nástroje nebo knihovny tříd.</span><span class="sxs-lookup"><span data-stu-id="a5961-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="a5961-109">Balíčky, které nejsou označeny typem, včetně všech balíčků vytvořených v dřívějších verzích NuGet, jsou ve výchozím nastavení `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="a5961-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="a5961-110">Do NuGet 3,5 se přidala podpora pro typy balíčků.</span><span class="sxs-lookup"><span data-stu-id="a5961-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="a5961-111">Pokud nepotřebujete vlastní typ balíčku, je *vhodné explicitně nastavit* typ balíčku.</span><span class="sxs-lookup"><span data-stu-id="a5961-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="a5961-112">Výchozí hodnota pro NuGet je `Dependency` typ, pokud není zadán žádný typ.</span><span class="sxs-lookup"><span data-stu-id="a5961-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="a5961-113">Vlastní typy balíčků</span><span class="sxs-lookup"><span data-stu-id="a5961-113">Custom package types</span></span>

<span data-ttu-id="a5961-114">Balíček můžete označit jedním nebo více vlastními typy balíčků, pokud jeho použití nevyhovuje [známým typům balíčků](#known-package-types).</span><span class="sxs-lookup"><span data-stu-id="a5961-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="a5961-115">Představte si například, že zákazníci `Contoso` aplikace mohou instalovat rozšíření.</span><span class="sxs-lookup"><span data-stu-id="a5961-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="a5961-116">Aplikace by mohla vyžadovat, aby autoři rozšíření používali vlastní typ balíčku `ContosoExtension` k identifikaci svých balíčků jako správných rozšíření, která následují podle požadovaných konvencí.</span><span class="sxs-lookup"><span data-stu-id="a5961-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="a5961-117">Balíček s vlastním typem balíčku nejde nainstalovat pomocí sady Visual Studio ani nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="a5961-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="a5961-118">Další informace najdete v tématu [NuGet/Home # 10468](https://github.com/NuGet/Home/issues/10468) .</span><span class="sxs-lookup"><span data-stu-id="a5961-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="a5961-119">Použití rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="a5961-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="a5961-120">Typy balíčků lze nastavit v souboru projektu ( `.csproj` ):</span><span class="sxs-lookup"><span data-stu-id="a5961-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="a5961-121">Balíčky s více zamýšlenými použitími se dají označit pomocí oddělovače s více typy balíčků `;` :</span><span class="sxs-lookup"><span data-stu-id="a5961-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="a5961-122">Typy balíčků se dají odlišit pomocí `,` oddělovače mezi typem balíčku a jeho [`Version`](/dotnet/api/system.version) řetězcem:</span><span class="sxs-lookup"><span data-stu-id="a5961-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="a5961-123">Použití nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a5961-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="a5961-124">Typy balíčků jsou nastaveny v `.nuspec` souboru v `packageTypes\packageType` uzlu pod `<metadata>` prvkem:</span><span class="sxs-lookup"><span data-stu-id="a5961-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="a5961-125">Balíčky s více zamýšlenými použitími mohou být označeny více typy balíčků:</span><span class="sxs-lookup"><span data-stu-id="a5961-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="a5961-126">Typy balíčků se dají používat ve verzi [`Version`](/dotnet/api/system.version) String:</span><span class="sxs-lookup"><span data-stu-id="a5961-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="a5961-127">Formát řetězce typu balíčku je přesně stejný jako ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="a5961-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="a5961-128">To znamená, že typ balíčku je řetězec nerozlišující malá a velká písmena, který odpovídá regulárnímu výrazu, který `^\w+([_.-]\w+)*$` má alespoň jeden znak a nejvíce 100 znaků.</span><span class="sxs-lookup"><span data-stu-id="a5961-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="a5961-129">Je-li zadána, je verze typu balíčku [`Version`](/dotnet/api/system.version) řetězec.</span><span class="sxs-lookup"><span data-stu-id="a5961-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="a5961-130">Verze typu balíčku je volitelná a výchozí hodnota je `0.0` .</span><span class="sxs-lookup"><span data-stu-id="a5961-130">The package type version is optional and defaults to `0.0`.</span></span>
