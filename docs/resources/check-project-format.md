---
title: Identifikace formátu projektu
description: Popisuje způsob identity formátu projektu.
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488482"
---
# <a name="identify-the-project-format"></a>Identifikace formátu projektu

NuGet pracuje se všemi projekty .NET. Formát projektu (sdk styl nebo non-SDK styl) určuje některé nástroje a metody, které je třeba použít ke spotřebě a vytváření balíčků NuGet. Projekty ve stylu sady SDK používají [atribut SDK](/dotnet/core/tools/csproj#additions). Je důležité identifikovat typ projektu, protože metody a nástroje, které používáte ke spotřebování a vytváření balíčků NuGet, jsou závislé na formátu projektu. U projektů, které nejsou ve stylu sady SDK, jsou metody a nástroje `PackageReference` také závislé na tom, zda byl projekt migrován do formátu.

Zda je projekt ve stylu sady SDK nebo ne, závisí na metodě použité k vytvoření projektu. V následující tabulce je uveden výchozí formát projektu a přidružený nástroj příkazového příkazu k příkazu pro váš projekt při jeho vytvoření pomocí sady Visual Studio 2017 a novějších verzí.

| Projektu&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Výchozí formát projektu | Nástroj CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Poznámky |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | Ve stylu Sady SDK | [Rozhraní příkazového řádku dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty vytvořené před Visual Studio 2017 jsou ve stylu sdk. Použijte `nuget.exe` CLI. |
| .NET Core | Ve stylu Sady SDK | [Rozhraní příkazového řádku dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty vytvořené před Visual Studio 2017 jsou ve stylu sdk. Použijte `nuget.exe` CLI. |
| .NET Framework | Ve stylu sady SDK | [Rozhraní příkazového řádku nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | Projekty rozhraní .NET Framework vytvořené pomocí jiných metod mohou být projekty ve stylu sady SDK. Pro tyto místo použijte [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) místo. |
| [Migrovaný](../consume-packages/migrate-packages-config-to-package-reference.md) projekt .NET | Ve stylu sady SDK| Chcete-li vytvořit [balíčky, použijte msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) k vytvoření balíčků. | Chcete-li `msbuild -t:pack` vytvořit balíčky, je doporučeno. V opačném případě použijte [rozhraní SEkat dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Migrované projekty nejsou projekty ve stylu sady SDK. |

## <a name="check-the-project-format"></a>Kontrola formátu projektu

Pokud si nejste jisti, zda je projekt ve formátu sdk nebo ne, `<Project>` vyhledejte atribut SDK v elementu v souboru projektu (Pro C#, toto je soubor *.csproj). Pokud je k dispozici, projekt je projekt ve stylu sady SDK.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Kontrola formátu projektu v sadě Visual Studio

Pokud pracujete v sadě Visual Studio, můžete rychle zkontrolovat formát projektu pomocí jedné z následujících metod:

- Klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte **upravit název_projektu.csproj**.

   Tato možnost je k dispozici pouze od visual studia 2017 pro projekty, které používají atribut stylu sady SDK. V opačném případě použijte jinou metodu.

   ![Úprava souboru projektu](media/edit-project-file.png)

   Projekt ve stylu sady SDK zobrazuje [atribut SDK](/dotnet/core/tools/csproj#additions) v souboru projektu.
   
- V nabídce **Projekt** zvolte **Unload Project** (nebo klikněte pravým tlačítkem myši na projekt a zvolte **Uvolnit projekt).**

   Tento projekt nebude obsahovat atribut SDK v souboru projektu. Nejedná se o projekt ve stylu sady SDK.

   ![Uvolnění projektu](media/unload-project.png)

   Potom klepněte pravým tlačítkem myši na nezatížený projekt a zvolte **Upravit název_projektu.csproj**.

## <a name="see-also"></a>Viz také

- [Vytvořit standardní balíčky rozhraní .NET pomocí rozhraní se síťovým rozhraním DOTNET](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Vytvoření standardních balíčků rozhraní .NET pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Vytvoření a publikování balíčku rozhraní .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [NuGet pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md)
