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
# <a name="identify-the-project-format"></a><span data-ttu-id="f50f7-103">Identifikace formátu projektu</span><span class="sxs-lookup"><span data-stu-id="f50f7-103">Identify the project format</span></span>

<span data-ttu-id="f50f7-104">NuGet pracuje se všemi projekty .NET.</span><span class="sxs-lookup"><span data-stu-id="f50f7-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="f50f7-105">Formát projektu (sdk styl nebo non-SDK styl) určuje některé nástroje a metody, které je třeba použít ke spotřebě a vytváření balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="f50f7-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="f50f7-106">Projekty ve stylu sady SDK používají [atribut SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="f50f7-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="f50f7-107">Je důležité identifikovat typ projektu, protože metody a nástroje, které používáte ke spotřebování a vytváření balíčků NuGet, jsou závislé na formátu projektu.</span><span class="sxs-lookup"><span data-stu-id="f50f7-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="f50f7-108">U projektů, které nejsou ve stylu sady SDK, jsou metody a nástroje `PackageReference` také závislé na tom, zda byl projekt migrován do formátu.</span><span class="sxs-lookup"><span data-stu-id="f50f7-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="f50f7-109">Zda je projekt ve stylu sady SDK nebo ne, závisí na metodě použité k vytvoření projektu.</span><span class="sxs-lookup"><span data-stu-id="f50f7-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="f50f7-110">V následující tabulce je uveden výchozí formát projektu a přidružený nástroj příkazového příkazu k příkazu pro váš projekt při jeho vytvoření pomocí sady Visual Studio 2017 a novějších verzí.</span><span class="sxs-lookup"><span data-stu-id="f50f7-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="f50f7-111">Projektu&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="f50f7-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="f50f7-112">Výchozí formát projektu</span><span class="sxs-lookup"><span data-stu-id="f50f7-112">Default project format</span></span> | <span data-ttu-id="f50f7-113">Nástroj CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="f50f7-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="f50f7-114">Poznámky</span><span class="sxs-lookup"><span data-stu-id="f50f7-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="f50f7-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="f50f7-115">.NET Standard</span></span> | <span data-ttu-id="f50f7-116">Ve stylu Sady SDK</span><span class="sxs-lookup"><span data-stu-id="f50f7-116">SDK-style</span></span> | [<span data-ttu-id="f50f7-117">Rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="f50f7-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="f50f7-118">Projekty vytvořené před Visual Studio 2017 jsou ve stylu sdk.</span><span class="sxs-lookup"><span data-stu-id="f50f7-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="f50f7-119">Použijte `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="f50f7-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="f50f7-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f50f7-120">.NET Core</span></span> | <span data-ttu-id="f50f7-121">Ve stylu Sady SDK</span><span class="sxs-lookup"><span data-stu-id="f50f7-121">SDK-style</span></span> | [<span data-ttu-id="f50f7-122">Rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="f50f7-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="f50f7-123">Projekty vytvořené před Visual Studio 2017 jsou ve stylu sdk.</span><span class="sxs-lookup"><span data-stu-id="f50f7-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="f50f7-124">Použijte `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="f50f7-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="f50f7-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f50f7-125">.NET Framework</span></span> | <span data-ttu-id="f50f7-126">Ve stylu sady SDK</span><span class="sxs-lookup"><span data-stu-id="f50f7-126">Non-SDK-style</span></span> | [<span data-ttu-id="f50f7-127">Rozhraní příkazového řádku nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f50f7-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="f50f7-128">Projekty rozhraní .NET Framework vytvořené pomocí jiných metod mohou být projekty ve stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="f50f7-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="f50f7-129">Pro tyto místo použijte [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) místo.</span><span class="sxs-lookup"><span data-stu-id="f50f7-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="f50f7-130">[Migrovaný](../consume-packages/migrate-packages-config-to-package-reference.md) projekt .NET</span><span class="sxs-lookup"><span data-stu-id="f50f7-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="f50f7-131">Ve stylu sady SDK</span><span class="sxs-lookup"><span data-stu-id="f50f7-131">Non-SDK-style</span></span>| <span data-ttu-id="f50f7-132">Chcete-li vytvořit [balíčky, použijte msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) k vytvoření balíčků.</span><span class="sxs-lookup"><span data-stu-id="f50f7-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="f50f7-133">Chcete-li `msbuild -t:pack` vytvořit balíčky, je doporučeno.</span><span class="sxs-lookup"><span data-stu-id="f50f7-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="f50f7-134">V opačném případě použijte [rozhraní SEkat dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="f50f7-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="f50f7-135">Migrované projekty nejsou projekty ve stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="f50f7-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="f50f7-136">Kontrola formátu projektu</span><span class="sxs-lookup"><span data-stu-id="f50f7-136">Check the project format</span></span>

<span data-ttu-id="f50f7-137">Pokud si nejste jisti, zda je projekt ve formátu sdk nebo ne, `<Project>` vyhledejte atribut SDK v elementu v souboru projektu (Pro C#, toto je soubor \*.csproj).</span><span class="sxs-lookup"><span data-stu-id="f50f7-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="f50f7-138">Pokud je k dispozici, projekt je projekt ve stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="f50f7-138">If it is present, the project is an SDK-style project.</span></span>

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

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="f50f7-139">Kontrola formátu projektu v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f50f7-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="f50f7-140">Pokud pracujete v sadě Visual Studio, můžete rychle zkontrolovat formát projektu pomocí jedné z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="f50f7-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="f50f7-141">Klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte **upravit název_projektu.csproj**.</span><span class="sxs-lookup"><span data-stu-id="f50f7-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="f50f7-142">Tato možnost je k dispozici pouze od visual studia 2017 pro projekty, které používají atribut stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="f50f7-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="f50f7-143">V opačném případě použijte jinou metodu.</span><span class="sxs-lookup"><span data-stu-id="f50f7-143">Otherwise, use the other method.</span></span>

   ![Úprava souboru projektu](media/edit-project-file.png)

   <span data-ttu-id="f50f7-145">Projekt ve stylu sady SDK zobrazuje [atribut SDK](/dotnet/core/tools/csproj#additions) v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="f50f7-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="f50f7-146">V nabídce **Projekt** zvolte **Unload Project** (nebo klikněte pravým tlačítkem myši na projekt a zvolte **Uvolnit projekt).**</span><span class="sxs-lookup"><span data-stu-id="f50f7-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="f50f7-147">Tento projekt nebude obsahovat atribut SDK v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="f50f7-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="f50f7-148">Nejedná se o projekt ve stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="f50f7-148">It is not an SDK-style project.</span></span>

   ![Uvolnění projektu](media/unload-project.png)

   <span data-ttu-id="f50f7-150">Potom klepněte pravým tlačítkem myši na nezatížený projekt a zvolte **Upravit název_projektu.csproj**.</span><span class="sxs-lookup"><span data-stu-id="f50f7-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="f50f7-151">Viz také</span><span class="sxs-lookup"><span data-stu-id="f50f7-151">See also</span></span>

- [<span data-ttu-id="f50f7-152">Vytvořit standardní balíčky rozhraní .NET pomocí rozhraní se síťovým rozhraním DOTNET</span><span class="sxs-lookup"><span data-stu-id="f50f7-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="f50f7-153">Vytvoření standardních balíčků rozhraní .NET pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f50f7-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="f50f7-154">Vytvoření a publikování balíčku rozhraní .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f50f7-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="f50f7-155">NuGet pack a obnovení jako cíle MSBuild</span><span class="sxs-lookup"><span data-stu-id="f50f7-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
