---
title: Určení formátu projektu
description: Popisuje způsob, jak identity formátovat projekt
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488482"
---
# <a name="identify-the-project-format"></a>Určení formátu projektu

NuGet funguje se všemi projekty .NET. Formát projektu (styl sady SDK nebo sada SDK bez sady SDK) však určuje některé z nástrojů a metod, které je třeba použít ke zpracování a vytváření balíčků NuGet. Projekty ve stylu sady SDK používají [atribut SDK](/dotnet/core/tools/csproj#additions). Je důležité identifikovat typ projektu, protože metody a nástroje, které používáte pro využívání a vytváření balíčků NuGet, jsou závislé na formátu projektu. Pro projekty, které nejsou v sadě SDK, jsou metody a nástroje závislé také na tom, zda byl projekt migrován do `PackageReference` formátu.

Zda je projekt ve stylu sady SDK nebo není závislý na metodě použité k vytvoření projektu. Následující tabulka ukazuje výchozí formát projektu a přidružený nástroj rozhraní příkazového řádku pro váš projekt při jeho vytváření pomocí sady Visual Studio 2017 a novějších verzí.

| Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Výchozí formát projektu | CLI – nástroj&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Poznámky |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | Styl sady SDK | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty vytvořené před sadou Visual Studio 2017 jsou ve stylu bez sady SDK. Použijte `nuget.exe` rozhraní příkazového řádku. |
| .NET Core | Styl sady SDK | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty vytvořené před sadou Visual Studio 2017 jsou ve stylu bez sady SDK. Použijte `nuget.exe` rozhraní příkazového řádku. |
| .NET Framework | Styl jiný než SDK | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | Projekty .NET Framework vytvořené pomocí jiných metod mohou být projekty ve stylu sady SDK. Pro ty použijte místo toho příkaz [DOTNET CLI](../install-nuget-client-tools.md#dotnetexe-cli) . |
| [Migrovaný](../consume-packages/migrate-packages-config-to-package-reference.md) projekt .NET | Styl jiný než SDK| Pro vytváření balíčků použijte [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) k vytvoření balíčků. | Pro vytváření balíčků `msbuild -t:pack` se doporučuje. V opačném případě použijte rozhraní příkazového [řádku dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Migrované projekty nejsou projekty ve stylu sady SDK. |

## <a name="check-the-project-format"></a>Ověřte formát projektu.

Pokud si nejste jistí, jestli je projekt ve formátu sady SDK nebo ne, vyhledejte atribut SDK v `<Project>` elementu v souboru projektu (pro C#je to soubor *. csproj). Pokud je k dispozici, projekt je projekt ve stylu sady SDK.

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

## <a name="check-the-project-format-in-visual-studio"></a>Podívejte se na formát projektu v aplikaci Visual Studio.

Pokud pracujete v aplikaci Visual Studio, můžete rychle kontrolovat formát projektu pomocí jedné z následujících metod:

- Klikněte pravým tlačítkem na projekt v Průzkumník řešení a vyberte **Upravit MyProjectName. csproj**.

   Tato možnost je k dispozici pouze od začátku v sadě Visual Studio 2017 pro projekty, které používají atribut Style sady SDK. V opačném případě použijte jinou metodu.

   ![Upravit soubor projektu](media/edit-project-file.png)

   Projekt ve stylu sady SDK zobrazuje [atribut sady SDK](/dotnet/core/tools/csproj#additions) v souboru projektu.
   
- V nabídce **projekt** klikněte na příkaz **Uvolnit projekt** (nebo klikněte pravým tlačítkem myši na projekt a vyberte možnost **Uvolnit projekt**).

   Tento projekt nebude obsahovat atribut sady SDK v souboru projektu. Nejedná se o projekt ve stylu sady SDK.

   ![Uvolnit projekt](media/unload-project.png)

   Pak klikněte pravým tlačítkem na uvolněný projekt a zvolte **Upravit MyProjectName. csproj**.

## <a name="see-also"></a>Viz také:

- [Vytváření balíčků .NET Standard pomocí rozhraní příkazového řádku dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Vytváření balíčků .NET Standard pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Vytvoření a publikování .NET Framework balíčku (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Sada NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md)
