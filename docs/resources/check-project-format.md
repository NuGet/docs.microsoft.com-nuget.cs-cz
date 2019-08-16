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
# <a name="identify-the-project-format"></a><span data-ttu-id="cc928-103">Určení formátu projektu</span><span class="sxs-lookup"><span data-stu-id="cc928-103">Identify the project format</span></span>

<span data-ttu-id="cc928-104">NuGet funguje se všemi projekty .NET.</span><span class="sxs-lookup"><span data-stu-id="cc928-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="cc928-105">Formát projektu (styl sady SDK nebo sada SDK bez sady SDK) však určuje některé z nástrojů a metod, které je třeba použít ke zpracování a vytváření balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="cc928-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="cc928-106">Projekty ve stylu sady SDK používají [atribut SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="cc928-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="cc928-107">Je důležité identifikovat typ projektu, protože metody a nástroje, které používáte pro využívání a vytváření balíčků NuGet, jsou závislé na formátu projektu.</span><span class="sxs-lookup"><span data-stu-id="cc928-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="cc928-108">Pro projekty, které nejsou v sadě SDK, jsou metody a nástroje závislé také na tom, zda byl projekt migrován do `PackageReference` formátu.</span><span class="sxs-lookup"><span data-stu-id="cc928-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="cc928-109">Zda je projekt ve stylu sady SDK nebo není závislý na metodě použité k vytvoření projektu.</span><span class="sxs-lookup"><span data-stu-id="cc928-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="cc928-110">Následující tabulka ukazuje výchozí formát projektu a přidružený nástroj rozhraní příkazového řádku pro váš projekt při jeho vytváření pomocí sady Visual Studio 2017 a novějších verzí.</span><span class="sxs-lookup"><span data-stu-id="cc928-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="cc928-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="cc928-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="cc928-112">Výchozí formát projektu</span><span class="sxs-lookup"><span data-stu-id="cc928-112">Default project format</span></span> | <span data-ttu-id="cc928-113">CLI – nástroj&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="cc928-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="cc928-114">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cc928-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="cc928-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="cc928-115">.NET Standard</span></span> | <span data-ttu-id="cc928-116">Styl sady SDK</span><span class="sxs-lookup"><span data-stu-id="cc928-116">SDK-style</span></span> | [<span data-ttu-id="cc928-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="cc928-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="cc928-118">Projekty vytvořené před sadou Visual Studio 2017 jsou ve stylu bez sady SDK.</span><span class="sxs-lookup"><span data-stu-id="cc928-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="cc928-119">Použijte `nuget.exe` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="cc928-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="cc928-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="cc928-120">.NET Core</span></span> | <span data-ttu-id="cc928-121">Styl sady SDK</span><span class="sxs-lookup"><span data-stu-id="cc928-121">SDK-style</span></span> | [<span data-ttu-id="cc928-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="cc928-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="cc928-123">Projekty vytvořené před sadou Visual Studio 2017 jsou ve stylu bez sady SDK.</span><span class="sxs-lookup"><span data-stu-id="cc928-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="cc928-124">Použijte `nuget.exe` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="cc928-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="cc928-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="cc928-125">.NET Framework</span></span> | <span data-ttu-id="cc928-126">Styl jiný než SDK</span><span class="sxs-lookup"><span data-stu-id="cc928-126">Non-SDK-style</span></span> | [<span data-ttu-id="cc928-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="cc928-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="cc928-128">Projekty .NET Framework vytvořené pomocí jiných metod mohou být projekty ve stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="cc928-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="cc928-129">Pro ty použijte místo toho příkaz [DOTNET CLI](../install-nuget-client-tools.md#dotnetexe-cli) .</span><span class="sxs-lookup"><span data-stu-id="cc928-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="cc928-130">[Migrovaný](../consume-packages/migrate-packages-config-to-package-reference.md) projekt .NET</span><span class="sxs-lookup"><span data-stu-id="cc928-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="cc928-131">Styl jiný než SDK</span><span class="sxs-lookup"><span data-stu-id="cc928-131">Non-SDK-style</span></span>| <span data-ttu-id="cc928-132">Pro vytváření balíčků použijte [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) k vytvoření balíčků.</span><span class="sxs-lookup"><span data-stu-id="cc928-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="cc928-133">Pro vytváření balíčků `msbuild -t:pack` se doporučuje.</span><span class="sxs-lookup"><span data-stu-id="cc928-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="cc928-134">V opačném případě použijte rozhraní příkazového [řádku dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="cc928-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="cc928-135">Migrované projekty nejsou projekty ve stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="cc928-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="cc928-136">Ověřte formát projektu.</span><span class="sxs-lookup"><span data-stu-id="cc928-136">Check the project format</span></span>

<span data-ttu-id="cc928-137">Pokud si nejste jistí, jestli je projekt ve formátu sady SDK nebo ne, vyhledejte atribut SDK v `<Project>` elementu v souboru projektu (pro C#je to soubor \*. csproj).</span><span class="sxs-lookup"><span data-stu-id="cc928-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="cc928-138">Pokud je k dispozici, projekt je projekt ve stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="cc928-138">If it is present, the project is an SDK-style project.</span></span>

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

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="cc928-139">Podívejte se na formát projektu v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc928-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="cc928-140">Pokud pracujete v aplikaci Visual Studio, můžete rychle kontrolovat formát projektu pomocí jedné z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="cc928-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="cc928-141">Klikněte pravým tlačítkem na projekt v Průzkumník řešení a vyberte **Upravit MyProjectName. csproj**.</span><span class="sxs-lookup"><span data-stu-id="cc928-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="cc928-142">Tato možnost je k dispozici pouze od začátku v sadě Visual Studio 2017 pro projekty, které používají atribut Style sady SDK.</span><span class="sxs-lookup"><span data-stu-id="cc928-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="cc928-143">V opačném případě použijte jinou metodu.</span><span class="sxs-lookup"><span data-stu-id="cc928-143">Otherwise, use the other method.</span></span>

   ![Upravit soubor projektu](media/edit-project-file.png)

   <span data-ttu-id="cc928-145">Projekt ve stylu sady SDK zobrazuje [atribut sady SDK](/dotnet/core/tools/csproj#additions) v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="cc928-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="cc928-146">V nabídce **projekt** klikněte na příkaz **Uvolnit projekt** (nebo klikněte pravým tlačítkem myši na projekt a vyberte možnost **Uvolnit projekt**).</span><span class="sxs-lookup"><span data-stu-id="cc928-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="cc928-147">Tento projekt nebude obsahovat atribut sady SDK v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="cc928-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="cc928-148">Nejedná se o projekt ve stylu sady SDK.</span><span class="sxs-lookup"><span data-stu-id="cc928-148">It is not an SDK-style project.</span></span>

   ![Uvolnit projekt](media/unload-project.png)

   <span data-ttu-id="cc928-150">Pak klikněte pravým tlačítkem na uvolněný projekt a zvolte **Upravit MyProjectName. csproj**.</span><span class="sxs-lookup"><span data-stu-id="cc928-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="cc928-151">Viz také:</span><span class="sxs-lookup"><span data-stu-id="cc928-151">See also</span></span>

- [<span data-ttu-id="cc928-152">Vytváření balíčků .NET Standard pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="cc928-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="cc928-153">Vytváření balíčků .NET Standard pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc928-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="cc928-154">Vytvoření a publikování .NET Framework balíčku (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cc928-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="cc928-155">Sada NuGet Pack a obnovení jako cíle MSBuild</span><span class="sxs-lookup"><span data-stu-id="cc928-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
