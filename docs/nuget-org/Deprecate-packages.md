---
title: Zastaralé balíčky na nuget.org
description: Podrobný popis procesu zavržení balíků a jak klienti tyto informace zobrazují
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096887"
---
# <a name="deprecating-packages"></a><span data-ttu-id="66ed9-103">Zastaralé balíčky</span><span class="sxs-lookup"><span data-stu-id="66ed9-103">Deprecating packages</span></span>

<span data-ttu-id="66ed9-104">Balíček můžete zamezit, pokud již nespravujete balíček nebo pokud chcete povzbudit spotřebitele balíčku, aby se přesunuli na jiný balíček.</span><span class="sxs-lookup"><span data-stu-id="66ed9-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="66ed9-105">Vyřazení balíčku se liší od **vyřazení balíčku,** jak je vysvětleno níže:</span><span class="sxs-lookup"><span data-stu-id="66ed9-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="66ed9-106">**Zrušení výpisu** balíčku zabrání jeho zjišťování, protože je skrytý ve výsledcích hledání.</span><span class="sxs-lookup"><span data-stu-id="66ed9-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="66ed9-107">**Zastaralá** balíček umožňuje existující příjemci balíčku zjistit, zda mají nainstalován nebo použit y ve svých projektech.</span><span class="sxs-lookup"><span data-stu-id="66ed9-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="66ed9-108">Také jim umožní znát důvod vyřazení a alternativní doporučený balíček, jak jste určili (vydavatel balíčku).</span><span class="sxs-lookup"><span data-stu-id="66ed9-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="66ed9-109">Zavržení balíček není zrušit seznam balíček.</span><span class="sxs-lookup"><span data-stu-id="66ed9-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="66ed9-110">Jako vydavatel se můžete rozhodnout zrušit seznam i zapojit meze balíčků.</span><span class="sxs-lookup"><span data-stu-id="66ed9-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="66ed9-111">Pracovní postup vyřazení</span><span class="sxs-lookup"><span data-stu-id="66ed9-111">Deprecation workflow</span></span>
1. <span data-ttu-id="66ed9-112">Chcete-li balíček zařadit, přejděte na **Spravovat balíčky** a vyberte **možnost Vyřazení**:</span><span class="sxs-lookup"><span data-stu-id="66ed9-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Přejít na možnost zavržení balíčku](media/deprecation-select-option.png)

2. <span data-ttu-id="66ed9-114">Vyberte verzi, kterou chcete zapřetat.</span><span class="sxs-lookup"><span data-stu-id="66ed9-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="66ed9-115">Pokud chcete zařadit všechny verze, zvolte **Vybrat všechny verze** možnost.</span><span class="sxs-lookup"><span data-stu-id="66ed9-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Vyberte verze balíčků, které chcete zakácet.](media/deprecation-select-version.png)

3. <span data-ttu-id="66ed9-117">Zvolte důvod pro vyřazení.</span><span class="sxs-lookup"><span data-stu-id="66ed9-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="66ed9-118">Pokud balíček již není udržován, zvolte možnost **Starší verze.**</span><span class="sxs-lookup"><span data-stu-id="66ed9-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="66ed9-119">Pokud konkrétní verze má kritickou chybu, zvolte možnost **má kritické chyby.**</span><span class="sxs-lookup"><span data-stu-id="66ed9-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="66ed9-120">Z jakéhokoli jiného důvodu vyberte **možnost Jiné**.</span><span class="sxs-lookup"><span data-stu-id="66ed9-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="66ed9-121">Vždy můžete zadat alternativní doporučený balíček (a verzi) a vlastní zprávu vlastníkům.</span><span class="sxs-lookup"><span data-stu-id="66ed9-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Výběr důvodů doporučení alternativního balíčku a vlastní zprávy](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="66ed9-123">Vlastní zpráva se zobrazí pouze na nuget.org, ale ne od klientů.</span><span class="sxs-lookup"><span data-stu-id="66ed9-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="66ed9-124">V současné době `dotnet.exe` klienti jako a NuGet Správce balíčků nezobrazují vlastní zprávu.</span><span class="sxs-lookup"><span data-stu-id="66ed9-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="66ed9-125">Zkušenosti s klientem pro zastaralé balíčky</span><span class="sxs-lookup"><span data-stu-id="66ed9-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="66ed9-126">Jakmile balíček byl zastaralá, jeho spotřebitelé jsou upozorněni na to následujícími způsoby (v závislosti na použitém klientem).</span><span class="sxs-lookup"><span data-stu-id="66ed9-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="66ed9-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66ed9-127">Visual Studio</span></span> 
<span data-ttu-id="66ed9-128">*K dispozici od visual studia 2019 verze 16.3*</span><span class="sxs-lookup"><span data-stu-id="66ed9-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="66ed9-129">Visual Studio varuje o zastaralé balíček použití `Installed` na kartě. Zobrazí upozornění pro balíček a jeho informace o vyřazení (včetně důvodu, že byl zastarala a alternativní balíček použít místo, pokud je k dispozici).</span><span class="sxs-lookup"><span data-stu-id="66ed9-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Zastaralé balíčky na kartě nainstalované aplikací Visual Studio správce balíčků](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="66ed9-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="66ed9-131">dotnet.exe</span></span>
<span data-ttu-id="66ed9-132">*K dispozici počínaje sadou .NET SDK 3.0*</span><span class="sxs-lookup"><span data-stu-id="66ed9-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="66ed9-133">Pokud používáte dotnet.exe, můžete `dotnet list package --deprecated` spustit příkaz na řešení nebo složky projektu získat seznam zastaralé balíčky spolu s informacemi vyřazení:</span><span class="sxs-lookup"><span data-stu-id="66ed9-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
