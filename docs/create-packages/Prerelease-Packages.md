---
title: Předběžné verze v balíčcích NuGet
description: Pokyny pro vytváření předprodejních balíčků
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610717"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="d891d-103">Vytváření předprodejních balíčků</span><span class="sxs-lookup"><span data-stu-id="d891d-103">Building pre-release packages</span></span>

<span data-ttu-id="d891d-104">Při každém vydání aktualizovaného balíčku s novým číslem verze, NuGet považuje tento jeden jako "nejnovější stabilní verze", jak je znázorněno, například v ui Správce balíčků v rámci sady Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d891d-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![UI Správce balíčků zobrazující nejnovější stabilní verzi](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="d891d-106">Stabilní verze je taková, která je považována za dostatečně spolehlivou pro použití ve výrobě.</span><span class="sxs-lookup"><span data-stu-id="d891d-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="d891d-107">Nejnovější stabilní verze je také ten, který bude nainstalován jako balíček aktualizace nebo během obnovení balíčku (s výhradou omezení, jak je popsáno v [přeinstalaci a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="d891d-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="d891d-108">Pro podporu životního cyklu vydání softwaru umožňuje aplikace NuGet 1.6 a novější distribuci předběžných balíčků, kde číslo verze `-alpha`obsahuje `-beta`sémantickou příponu správy verzí, například , , nebo `-rc`.</span><span class="sxs-lookup"><span data-stu-id="d891d-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="d891d-109">Další informace naleznete [v tématu Package versioning](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="d891d-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="d891d-110">Tyto verze můžete zadat jedním z následujících způsobů:</span><span class="sxs-lookup"><span data-stu-id="d891d-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="d891d-111">\*\*Pokud váš [`PackageReference`](../consume-packages/package-references-in-project-files.md)projekt používá \*\*: zahrnout sémantické `.csproj` verze [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) přípony v prvku souboru:</span><span class="sxs-lookup"><span data-stu-id="d891d-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="d891d-112">**Pokud má váš [`packages.config`](../reference/packages-config.md) projekt soubor:** zahrňte do [`.nuspec`](../reference/nuspec.md) [`version`](../reference/nuspec.md#version) prvku souboru příponu sémantické verze:</span><span class="sxs-lookup"><span data-stu-id="d891d-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="d891d-113">Až budete připraveni vydat stabilní verzi, stačí odebrat příponu a balíček má přednost před všemi předběžnými verzemi.</span><span class="sxs-lookup"><span data-stu-id="d891d-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="d891d-114">Znovu naleznete [v tématu Package versioning](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="d891d-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="d891d-115">Instalace a aktualizace předběžných verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="d891d-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="d891d-116">Ve výchozím nastavení NuGet neobsahuje předběžné verze při práci s balíčky, ale můžete změnit toto chování následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d891d-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="d891d-117">**UI Správce balíčků v sadě Visual Studio**: V **umělou spravovat nugetové balíčky** zaškrtněte políčko **Zahrnout předběžnou verzi:**</span><span class="sxs-lookup"><span data-stu-id="d891d-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Zaškrtávací políčko Zahrnout předběžnou verzi v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="d891d-119">Nastavením nebo zrušením zaškrtnutí tohoto pole se aktualizuje ui Správce balíčků a seznam dostupných verzí, které můžete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="d891d-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="d891d-120">**Konzola Správce**balíčků `-IncludePrerelease` : `Find-Package`Použijte `Get-Package` `Install-Package`přepínač `Sync-Package`s `Update-Package` příkazy , , , a příkazy.</span><span class="sxs-lookup"><span data-stu-id="d891d-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="d891d-121">Odkazovat na [odkaz prostředí PowerShell](../reference/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d891d-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="d891d-122">**NuGet CLI**: `-prerelease` Použijte `install`přepínač `update` `delete`s `mirror` příkazy , , a.</span><span class="sxs-lookup"><span data-stu-id="d891d-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="d891d-123">Odkazovat na [odkaz NuGet CLI](../reference/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="d891d-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="d891d-124">Sémantická správa verzí</span><span class="sxs-lookup"><span data-stu-id="d891d-124">Semantic versioning</span></span>

<span data-ttu-id="d891d-125">[Sémantické Versioning nebo SemVer konvence](https://semver.org/spec/v1.0.0.html) popisuje, jak využít řetězce v číslech verzí sdělit význam základního kódu.</span><span class="sxs-lookup"><span data-stu-id="d891d-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="d891d-126">V této úmluvě má každá `Major.Minor.Patch`verze tři části , s následujícím významem:</span><span class="sxs-lookup"><span data-stu-id="d891d-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="d891d-127">`Major`: Nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="d891d-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="d891d-128">`Minor`: Nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="d891d-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="d891d-129">`Patch`: Pouze opravy zpětně kompatibilních chyb</span><span class="sxs-lookup"><span data-stu-id="d891d-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="d891d-130">Předběžné verze jsou pak označeny připojením pomlčky a řetězce za číslo opravy.</span><span class="sxs-lookup"><span data-stu-id="d891d-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="d891d-131">Technicky vzato můžete použít *libovolný* řetězec po pomlčka a NuGet bude považovat balíček jako předběžnou verzi.</span><span class="sxs-lookup"><span data-stu-id="d891d-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="d891d-132">NuGet pak zobrazí číslo plné verze v příslušném ui, takže spotřebitelé interpretovat význam pro sebe.</span><span class="sxs-lookup"><span data-stu-id="d891d-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="d891d-133">S ohledem na to je obecně dobré dodržovat uznávané konvence pojmenování, například následující:</span><span class="sxs-lookup"><span data-stu-id="d891d-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="d891d-134">`-alpha`: Alfa verze, obvykle používaná pro nedokončenou práci a experimentování</span><span class="sxs-lookup"><span data-stu-id="d891d-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="d891d-135">`-beta`: Beta verze, obvykle taková, která je dokončena pro další plánovanou verzi, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="d891d-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="d891d-136">`-rc`: Release candidate, obvykle vydání, které je potenciálně konečné (stabilní), pokud se neobjeví významné chyby.</span><span class="sxs-lookup"><span data-stu-id="d891d-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="d891d-137">NuGet 4.3.0+ podporuje [sémantické versioning v2.0.0](https://semver.org/spec/v2.0.0.html), který podporuje pre-release čísla s tečkou zápisu, jako v `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="d891d-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="d891d-138">Dot notace není podporována s Verzemi NuGet před 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="d891d-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="d891d-139">V dřívějších verzích NuGet můžete použít `1.0.1-build23` formulář, jako je, ale to bylo vždy považováno za předběžnou verzi.</span><span class="sxs-lookup"><span data-stu-id="d891d-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="d891d-140">Bez ohledu na přípony, které používáte, však NuGet jim dá přednost v obráceném abecedním pořadí:</span><span class="sxs-lookup"><span data-stu-id="d891d-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="d891d-141">Jak je znázorněno, verze bez přípony bude mít vždy přednost před předběžnými verzemi.</span><span class="sxs-lookup"><span data-stu-id="d891d-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="d891d-142">Úvodní 0s nejsou potřeba s semver2, ale jsou se schématem staré verze.</span><span class="sxs-lookup"><span data-stu-id="d891d-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="d891d-143">Pokud používáte číselné přípony s předprodejními značkami, které mohou používat dvouciferná čísla (nebo více), použijte úvodní nuly jako v beta.01 a beta.05, abyste zajistili, že se správně seřadí, když se čísla zvětší.</span><span class="sxs-lookup"><span data-stu-id="d891d-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="d891d-144">Toto doporučení platí pouze pro schéma staré verze.</span><span class="sxs-lookup"><span data-stu-id="d891d-144">This recommendation only applies to the old version schema.</span></span>
