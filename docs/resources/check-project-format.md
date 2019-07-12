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
# <a name="identify-the-project-format"></a><span data-ttu-id="b8fbb-103">Určit formát projektu</span><span class="sxs-lookup"><span data-stu-id="b8fbb-103">Identify the project format</span></span>

<span data-ttu-id="b8fbb-104">NuGet funguje s všechny projekty .NET.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="b8fbb-105">Formát projektu (sada SDK – vizuální styl nebo sady SDK styl) určuje však některé nástroje a metody, které je třeba použít využívat a vytvářet balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="b8fbb-106">Použít projekty založenými na sadu SDK [SDK atribut](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="b8fbb-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="b8fbb-107">Je důležité identifikovat typ projektu, protože metody a nástrojů, které používáte, využívat a vytvářet balíčky NuGet jsou závislé na formát projektu.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="b8fbb-108">Pro projekty SDK styl, metody a nástroje jsou také závislé na Určuje, jestli se migroval projekt do `PackageReference` formátu.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="b8fbb-109">Určuje, zda váš projekt je sada SDK – vizuální styl, nebo Ne, závisí na metodu použitou k vytvoření projektu.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="b8fbb-110">Následující tabulka uvádí výchozí formát projektu a související nástroje rozhraní příkazového řádku pro váš projekt, když vytvoříte pomocí sady Visual Studio 2017 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="b8fbb-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="b8fbb-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="b8fbb-112">Výchozí formát projektu</span><span class="sxs-lookup"><span data-stu-id="b8fbb-112">Default project format</span></span> | <span data-ttu-id="b8fbb-113">Nástroj příkazového řádku&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="b8fbb-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="b8fbb-114">Poznámky</span><span class="sxs-lookup"><span data-stu-id="b8fbb-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="b8fbb-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="b8fbb-115">.NET Standard</span></span> | <span data-ttu-id="b8fbb-116">SDK-style</span><span class="sxs-lookup"><span data-stu-id="b8fbb-116">SDK-style</span></span> | [<span data-ttu-id="b8fbb-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="b8fbb-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="b8fbb-118">Projekty vytvořené před Visual Studio 2017 jsou mimo SDK-style.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="b8fbb-119">Použití `nuget.exe` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="b8fbb-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b8fbb-120">.NET Core</span></span> | <span data-ttu-id="b8fbb-121">SDK-style</span><span class="sxs-lookup"><span data-stu-id="b8fbb-121">SDK-style</span></span> | [<span data-ttu-id="b8fbb-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="b8fbb-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="b8fbb-123">Projekty vytvořené před Visual Studio 2017 jsou mimo SDK-style.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="b8fbb-124">Použití `nuget.exe` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="b8fbb-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="b8fbb-125">.NET Framework</span></span> | <span data-ttu-id="b8fbb-126">Non-SDK-style</span><span class="sxs-lookup"><span data-stu-id="b8fbb-126">Non-SDK-style</span></span> | [<span data-ttu-id="b8fbb-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="b8fbb-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="b8fbb-128">Rozhraní .NET framework projekty vytvořené pomocí jiných metod může být projekty založenými na sadě SDK.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="b8fbb-129">Pro ty, použijte [rozhraní příkazového řádku dotnet](../install-nuget-client-tools.md#dotnetexe-cli) místo.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="b8fbb-130">[Migrovat](../reference/migrate-packages-config-to-package-reference.md) projektu .NET</span><span class="sxs-lookup"><span data-stu-id="b8fbb-130">[Migrated](../reference/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="b8fbb-131">Non-SDK-style</span><span class="sxs-lookup"><span data-stu-id="b8fbb-131">Non-SDK-style</span></span>| <span data-ttu-id="b8fbb-132">Chcete-li vytvořit balíčky, použijte [msbuild - t: pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) k vytváření balíčků.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-132">To create packages, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="b8fbb-133">Vytvořit balíčky, `msbuild -t:pack` se doporučuje.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="b8fbb-134">Jinak použijte [rozhraní příkazového řádku dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="b8fbb-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="b8fbb-135">Migrované projekty nejsou projekty založenými na sadě SDK.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="b8fbb-136">Zkontrolujte formát projektu</span><span class="sxs-lookup"><span data-stu-id="b8fbb-136">Check the project format</span></span>

<span data-ttu-id="b8fbb-137">Pokud si nejste jisti, zda projekt používá formát SDK – vizuální styl nebo Ne, vyhledejte atribut sady SDK v aplikaci `<Project>` element v souboru projektu (pro C#, jedná se o soubor \*.csproj).</span><span class="sxs-lookup"><span data-stu-id="b8fbb-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="b8fbb-138">Pokud je k dispozici, projekt je projekt SDK-style.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-138">If it is present, the project is an SDK-style project.</span></span>

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

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="b8fbb-139">Zkontrolujte formát projektu v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8fbb-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="b8fbb-140">Pokud pracujete v sadě Visual Studio, můžete rychle zkontrolovat formát projektu pomocí jedné z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="b8fbb-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="b8fbb-141">Klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **upravit myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="b8fbb-142">Tato možnost je pouze k dispozici pro projekty, které používají atribut SDK – vizuální styl od v sadě Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="b8fbb-143">Jinak použijte jinou metodu.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-143">Otherwise, use the other method.</span></span>

   ![Úprava souboru projektu](media/edit-project-file.png)

   <span data-ttu-id="b8fbb-145">Ukazuje, projekt SDK-style [SDK atribut](/dotnet/core/tools/csproj#additions) v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="b8fbb-146">Z **projektu** nabídce zvolte **uvolnit projekt** (nebo klikněte pravým tlačítkem na projekt a zvolte **uvolnit projekt**).</span><span class="sxs-lookup"><span data-stu-id="b8fbb-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="b8fbb-147">Tento projekt nebude obsahovat atribut sady SDK v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="b8fbb-148">Není SDK styl projektu.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-148">It is not an SDK-style project.</span></span>

   ![Uvolněte projekt](media/unload-project.png)

   <span data-ttu-id="b8fbb-150">Potom klikněte pravým tlačítkem na projekt uvolněn a zvolte **upravit myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="b8fbb-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="b8fbb-151">Viz také:</span><span class="sxs-lookup"><span data-stu-id="b8fbb-151">See also</span></span>

- [<span data-ttu-id="b8fbb-152">Vytvoření standardních balíčků .NET pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="b8fbb-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="b8fbb-153">Vytvořit standardní balíčky .NET pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8fbb-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="b8fbb-154">Vytvoření a publikování balíčku .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b8fbb-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="b8fbb-155">Balíček NuGet a obnovení jako cílů MSBuild</span><span class="sxs-lookup"><span data-stu-id="b8fbb-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
