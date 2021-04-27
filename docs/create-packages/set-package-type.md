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
# <a name="set-a-nuget-package-type"></a>Nastavení typu balíčku NuGet

Balíčky lze označit dalšími dalšími *typy balíčků* k označení zamýšleného použití.

## <a name="known-package-types"></a>Známé typy balíčků

- `Dependency` balíčky typů přidávají prostředky pro sestavení nebo spuštění do knihoven a aplikací a mohou být nainstalovány v jakémkoli typu projektu (za předpokladu, že jsou kompatibilní).

- `DotnetTool` balíčky typů jsou nástroje .NET, které lze nainstalovat pomocí rozhraní příkazového [řádku dotnet](/dotnet/articles/core/tools/index).

- `Template` balíčky typů poskytují [vlastní šablony](/dotnet/core/tools/custom-templates) , které lze použít k vytvoření souborů nebo projektů, jako jsou aplikace, služby, nástroje nebo knihovny tříd.

Balíčky, které nejsou označeny typem, včetně všech balíčků vytvořených v dřívějších verzích NuGet, jsou ve výchozím nastavení `Dependency` typu.

> [!NOTE]
> Do NuGet 3,5 se přidala podpora pro typy balíčků.
> Pokud nepotřebujete vlastní typ balíčku, je *vhodné explicitně nastavit* typ balíčku.
> Výchozí hodnota pro NuGet je `Dependency` typ, pokud není zadán žádný typ.

## <a name="custom-package-types"></a>Vlastní typy balíčků

Balíček můžete označit jedním nebo více vlastními typy balíčků, pokud jeho použití nevyhovuje [známým typům balíčků](#known-package-types).

Představte si například, že zákazníci `Contoso` aplikace mohou instalovat rozšíření. Aplikace by mohla vyžadovat, aby autoři rozšíření používali vlastní typ balíčku `ContosoExtension` k identifikaci svých balíčků jako správných rozšíření, která následují podle požadovaných konvencí.

> [!WARNING]
> Balíček s vlastním typem balíčku nejde nainstalovat pomocí sady Visual Studio ani nuget.exe. Další informace najdete v tématu [NuGet/Home # 10468](https://github.com/NuGet/Home/issues/10468) .

# <a name="using-dotnet-cli"></a>[Použití rozhraní příkazového řádku dotnet](#tab/dotnet)

Typy balíčků lze nastavit v souboru projektu ( `.csproj` ):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

Balíčky s více zamýšlenými použitími se dají označit pomocí oddělovače s více typy balíčků `;` :

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

Typy balíčků se dají odlišit pomocí `,` oddělovače mezi typem balíčku a jeho [`Version`](/dotnet/api/system.version) řetězcem:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[Použití nuget.exe](#tab/nugetexe)

Typy balíčků jsou nastaveny v `.nuspec` souboru v `packageTypes\packageType` uzlu pod `<metadata>` prvkem:

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

Balíčky s více zamýšlenými použitími mohou být označeny více typy balíčků:

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

Typy balíčků se dají používat ve verzi [`Version`](/dotnet/api/system.version) String:

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

Formát řetězce typu balíčku je přesně stejný jako ID balíčku. To znamená, že typ balíčku je řetězec nerozlišující malá a velká písmena, který odpovídá regulárnímu výrazu, který `^\w+([_.-]\w+)*$` má alespoň jeden znak a nejvíce 100 znaků.

Je-li zadána, je verze typu balíčku [`Version`](/dotnet/api/system.version) řetězec. Verze typu balíčku je volitelná a výchozí hodnota je `0.0` .
