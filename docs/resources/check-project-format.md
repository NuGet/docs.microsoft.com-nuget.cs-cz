---
title: Určit formát projektu
description: Popisuje, jak na identitu formát projektu
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843518"
---
# <a name="identify-the-project-format"></a>Určit formát projektu

NuGet funguje s všechny projekty .NET. Formát projektu (sada SDK – vizuální styl nebo sady SDK styl) určuje však některé nástroje a metody, které je třeba použít využívat a vytvářet balíčky NuGet. Použít projekty založenými na sadu SDK [SDK atribut](/dotnet/core/tools/csproj#additions). Je důležité identifikovat typ projektu, protože metody a nástrojů, které používáte, využívat a vytvářet balíčky NuGet jsou závislé na formát projektu. Pro projekty SDK styl, metody a nástroje jsou také závislé na Určuje, jestli se migroval projekt do `PackageReference` formátu.

Určuje, zda váš projekt je sada SDK – vizuální styl, nebo Ne, závisí na metodu použitou k vytvoření projektu. Následující tabulka uvádí výchozí formát projektu a související nástroje rozhraní příkazového řádku pro váš projekt, když vytvoříte pomocí sady Visual Studio 2017 a novějších verzích.

| Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Výchozí formát projektu | Nástroj příkazového řádku&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Poznámky |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK-style | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty vytvořené před Visual Studio 2017 jsou mimo SDK-style. Použití `nuget.exe` rozhraní příkazového řádku. |
| .NET Core | SDK-style | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty vytvořené před Visual Studio 2017 jsou mimo SDK-style. Použití `nuget.exe` rozhraní příkazového řádku. |
| .NET Framework | Non-SDK-style | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | Rozhraní .NET framework projekty vytvořené pomocí jiných metod může být projekty založenými na sadě SDK. Pro ty, použijte [rozhraní příkazového řádku dotnet](../install-nuget-client-tools.md#dotnetexe-cli) místo. |
| [Migrovat](../reference/migrate-packages-config-to-package-reference.md) projektu .NET | Non-SDK-style| Chcete-li vytvořit balíčky, použijte [msbuild - t: pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) k vytváření balíčků. | Vytvořit balíčky, `msbuild -t:pack` se doporučuje. Jinak použijte [rozhraní příkazového řádku dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Migrované projekty nejsou projekty založenými na sadě SDK. |

## <a name="check-the-project-format"></a>Zkontrolujte formát projektu

Pokud si nejste jisti, zda projekt používá formát SDK – vizuální styl nebo Ne, vyhledejte atribut sady SDK v aplikaci `<Project>` element v souboru projektu (pro C#, jedná se o soubor *.csproj). Pokud je k dispozici, projekt je projekt SDK-style.

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

## <a name="check-the-project-format-in-visual-studio"></a>Zkontrolujte formát projektu v sadě Visual Studio

Pokud pracujete v sadě Visual Studio, můžete rychle zkontrolovat formát projektu pomocí jedné z následujících metod:

- Klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **upravit myprojectname.csproj**.

   Tato možnost je pouze k dispozici pro projekty, které používají atribut SDK – vizuální styl od v sadě Visual Studio 2017. Jinak použijte jinou metodu.

   ![Úprava souboru projektu](media/edit-project-file.png)

   Ukazuje, projekt SDK-style [SDK atribut](/dotnet/core/tools/csproj#additions) v souboru projektu.
   
- Z **projektu** nabídce zvolte **uvolnit projekt** (nebo klikněte pravým tlačítkem na projekt a zvolte **uvolnit projekt**).

   Tento projekt nebude obsahovat atribut sady SDK v souboru projektu. Není SDK styl projektu.

   ![Uvolněte projekt](media/unload-project.png)

   Potom klikněte pravým tlačítkem na projekt uvolněn a zvolte **upravit myprojectname.csproj**.

## <a name="see-also"></a>Viz také:

- [Vytvoření standardních balíčků .NET pomocí rozhraní příkazového řádku dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Vytvořit standardní balíčky .NET pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Vytvoření a publikování balíčku .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Balíček NuGet a obnovení jako cílů MSBuild](../reference/msbuild-targets.md)
