---
title: Předběžné verze v balíčků NuGet
description: Pokyny pro vytváření předběžné verze balíčků
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 498509e03a794878eeeadd46d499521d19415600
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818370"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="cbfb9-103">Vytváření předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="cbfb9-103">Building pre-release packages</span></span>

<span data-ttu-id="cbfb9-104">Vždy, když uvolnění aktualizovaný balíček s nové číslo verze se považuje za NuGet než jako "nejnovější stabilní verze" jak je vidět, třeba v uživatelském rozhraní Správce balíčků ve Visual Studiu:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Uživatelského rozhraní Správce balíčků zobrazující nejnovější stabilní verze](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="cbfb9-106">Stabilní verze je ten, který je považován za dostatečně spolehlivé, který se má použít v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="cbfb9-107">Nejnovější stabilní verze je také ten, který se nainstaluje jako aktualizace balíčku nebo při obnovování balíčků (vztahují omezení, jak je popsáno v [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="cbfb9-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="cbfb9-108">Pro podporu životního cyklu verze softwaru, NuGet 1.6 nebo novější umožňuje distribuci předběžné verze balíčků, kde se číslo verze obsahuje příponu sémantické verze, jako `-alpha`, `-beta`, nebo `-rc`.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="cbfb9-109">Další informace najdete v tématu [Správa verzí balíčku](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="cbfb9-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="cbfb9-110">Tyto verze můžete určit dvěma způsoby:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-110">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="cbfb9-111">`.nuspec` soubor: zahrnují příponou sémantickou verzi v `version` element:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="cbfb9-112">Atributů sestavení: při vytváření balíčků z projektu sady Visual Studio (`.csproj` nebo `.vbproj`), použijte `AssemblyInformationalVersionAttribute` k určení verze:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-112">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="cbfb9-113">NuGet převezme tuto hodnotu namísto verze zadaná v `AssemblyVersion` atribut, který nepodporuje sémantické verze.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-113">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="cbfb9-114">Až budete připraveni k uvolnění stabilní verze, právě odeberte příponu a balíček má přednost před všechny předprodejní verze.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-114">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="cbfb9-115">Znovu, najdete v části [Správa verzí balíčku](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="cbfb9-115">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="cbfb9-116">Instalace a aktualizace předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="cbfb9-116">Installing and updating pre-release packages</span></span>

<span data-ttu-id="cbfb9-117">Ve výchozím nastavení NuGet nezahrnuje předprodejní verze při práci s balíčky, ale toto chování lze změnit takto:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-117">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="cbfb9-118">**Správce balíčků uživatelského rozhraní v sadě Visual Studio**: V **spravovat balíčky NuGet** uživatelského rozhraní, zkontrolujte **zahrnout předběžné verze** pole:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-118">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Políčko zahrnout předběžné verze v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="cbfb9-120">Nastavení nebo zrušíte zaškrtnutí tohoto políčka se aktualizuje uživatelské rozhraní Správce balíčků a seznam dostupných verzí, které můžete instalovat.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-120">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="cbfb9-121">**Konzola správce balíčků**: použití `-IncludePrerelease` přepínač s `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, a `Update-Package` příkazy.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-121">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="cbfb9-122">Odkazovat [referenční informace prostředí PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="cbfb9-122">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="cbfb9-123">**Rozhraní příkazového řádku NuGet**: použití `-prerelease` přepínač s `install`, `update`, `delete`, a `mirror` příkazy.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-123">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="cbfb9-124">Odkazovat [odkaz NuGet rozhraní příkazového řádku](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="cbfb9-124">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="cbfb9-125">Sémantické verze</span><span class="sxs-lookup"><span data-stu-id="cbfb9-125">Semantic versioning</span></span>

<span data-ttu-id="cbfb9-126">[Sémantické verze nebo SemVer konvence](http://semver.org/spec/v1.0.0.html) popisuje, jak využívat řetězců v čísla verzí pro vyjádření jejich význam kódu.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-126">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="cbfb9-127">V touto konvencí, každá verze má tři části `Major.Minor.Patch`, s následující význam:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-127">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="cbfb9-128">`Major`: Nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="cbfb9-128">`Major`: Breaking changes</span></span>
- <span data-ttu-id="cbfb9-129">`Minor`: Nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="cbfb9-129">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="cbfb9-130">`Patch`: Zpětné opravy pouze kompatibilní chyb</span><span class="sxs-lookup"><span data-stu-id="cbfb9-130">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="cbfb9-131">Předběžné verze jsou pak odlišené připojování řetězec a pomlčka po číslo opravy.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-131">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="cbfb9-132">Technicky platí, že můžete použít * žádné * řetězec po pomlčku a NuGet bude považovat za balíček předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-132">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="cbfb9-133">Číslo plnou verzi NuGet pak zobrazí v uživatelském rozhraní použít, a spotřebitelé interpretovat význam sami.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-133">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="cbfb9-134">Myslete na to je obvykle dobrou sledovat rozpoznaný zásady vytváření názvů jako je například následující:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-134">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="cbfb9-135">`-alpha`: Alfa verze, obvykle se používá pro práce v průběhu a experimentování</span><span class="sxs-lookup"><span data-stu-id="cbfb9-135">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="cbfb9-136">`-beta`: Beta verze, obvykle ten, který je funkce dokončení další plánované verze, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-136">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="cbfb9-137">`-rc`: Release candidate, obvykle verzi, která je potenciálně konečné (stable), pokud vznikat významné chyby.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-137">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="cbfb9-138">Podporuje NuGet 4.3.0+ [sémantické verze v2.0.0](http://semver.org/spec/v2.0.0.html), který podporuje předběžné verze čísla s zápisu s tečkou, jako v `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-138">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="cbfb9-139">Verze NuGet před 4.3.0 nepodporuje zápisu s tečkou.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-139">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="cbfb9-140">V dřívějších verzích systému NuGet, můžete použít formuláře jako `1.0.1-build23` ale vždycky to považovaná předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-140">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="cbfb9-141">Ať přípony, které používáte, ale NuGet získáte jejich prioritu ve vzestupném abecedním pořadí:</span><span class="sxs-lookup"><span data-stu-id="cbfb9-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="cbfb9-142">Jak je znázorněno, verze bez žádné přípony bude vždy přednost předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="cbfb9-143">Všimněte si také, že pokud používáte číselné přípony s předběžné verze značky, které můžou používat dvoumístných čísel (nebo více), použít úvodní nuly jako beta01 a beta05 zajistit, že budou řadit správně při získání větší čísla.</span><span class="sxs-lookup"><span data-stu-id="cbfb9-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
