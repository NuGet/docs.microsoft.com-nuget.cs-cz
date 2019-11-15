---
title: Zastaralé balíčky na nuget.org
description: Podrobný popis procesu zastaralých balíčků a způsobu, jakým klienti tyto informace zobrazují
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096887"
---
# <a name="deprecating-packages"></a><span data-ttu-id="b15b7-103">Zastaralé balíčky</span><span class="sxs-lookup"><span data-stu-id="b15b7-103">Deprecating packages</span></span>

<span data-ttu-id="b15b7-104">Pokud už balíček neuchováváte, nebo pokud chcete, aby se příjemci balíčku mohli přesunout na jiný balíček, můžete ho zařadit do zastaralého.</span><span class="sxs-lookup"><span data-stu-id="b15b7-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="b15b7-105">Vyřazení balíčku se **liší od** odbalení balíčku, jak je vysvětleno níže:</span><span class="sxs-lookup"><span data-stu-id="b15b7-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="b15b7-106">Odhlášení balíčku brání jeho zjištění, protože je ve výsledcích hledání skryté.</span><span class="sxs-lookup"><span data-stu-id="b15b7-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="b15b7-107">Když zařadíte **balíček,** umožníte stávajícím příjemcům balíčku zjistit, jestli mají nainstalované nebo používané ve svých projektech.</span><span class="sxs-lookup"><span data-stu-id="b15b7-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="b15b7-108">Také jim umožňuje zjistit důvod vyřazení a alternativní doporučený balíček, který jste určili (Vydavatel balíčku).</span><span class="sxs-lookup"><span data-stu-id="b15b7-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="b15b7-109">Zastaralost balíčku neodstraní balíček.</span><span class="sxs-lookup"><span data-stu-id="b15b7-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="b15b7-110">Jako vydavatel se můžete rozhodnout, jak odpisovat, tak i jako zastaralé balíčky.</span><span class="sxs-lookup"><span data-stu-id="b15b7-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="b15b7-111">Pracovní postup vyřazení</span><span class="sxs-lookup"><span data-stu-id="b15b7-111">Deprecation workflow</span></span>
1. <span data-ttu-id="b15b7-112">Pokud chcete balíček zařadit **, klikněte**na **Spravovat balíčky** a vyberte vyřazení:</span><span class="sxs-lookup"><span data-stu-id="b15b7-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Možnost přejít na nepoužívaného balíčku](media/deprecation-select-option.png)

2. <span data-ttu-id="b15b7-114">Vyberte verzi, kterou chcete vyřadit jako nevybranou.</span><span class="sxs-lookup"><span data-stu-id="b15b7-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="b15b7-115">Pokud chcete vyřadit všechny verze, zvolte možnost **Vybrat všechny verze** .</span><span class="sxs-lookup"><span data-stu-id="b15b7-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Vybrat verze balíčku k vyřazení](media/deprecation-select-version.png)

3. <span data-ttu-id="b15b7-117">Vyberte důvod pro vyřazení.</span><span class="sxs-lookup"><span data-stu-id="b15b7-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="b15b7-118">Pokud se balíček již neuchovává, vyberte možnost **starší verze** .</span><span class="sxs-lookup"><span data-stu-id="b15b7-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="b15b7-119">Pokud má konkrétní verze kritickou chybu, vyberte možnost **má kritické chyby** .</span><span class="sxs-lookup"><span data-stu-id="b15b7-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="b15b7-120">Z jakéhokoli jiného důvodu vyberte **jiný**.</span><span class="sxs-lookup"><span data-stu-id="b15b7-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="b15b7-121">Pro vlastníky můžete vždy zadat alternativní doporučený balíček (a verzi) a vlastní zprávu.</span><span class="sxs-lookup"><span data-stu-id="b15b7-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Vyberte důvody alternativního balíčku doporučení a vlastní zpráva.](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="b15b7-123">Vlastní zpráva se zobrazuje jenom na nuget.org, ale ne z klientů.</span><span class="sxs-lookup"><span data-stu-id="b15b7-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="b15b7-124">V současné době klienti, jako je `dotnet.exe` a správce balíčků NuGet, nezobrazují vlastní zprávu.</span><span class="sxs-lookup"><span data-stu-id="b15b7-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="b15b7-125">Prostředí klienta pro zastaralé balíčky</span><span class="sxs-lookup"><span data-stu-id="b15b7-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="b15b7-126">Jakmile je balíček zastaralý, jeho příjemci se o tom dozví v následujících způsobech (v závislosti na použitém klientovi).</span><span class="sxs-lookup"><span data-stu-id="b15b7-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="b15b7-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b15b7-127">Visual Studio</span></span> 
<span data-ttu-id="b15b7-128">*K dispozici počínaje verzí Visual Studio 2019 16,3*</span><span class="sxs-lookup"><span data-stu-id="b15b7-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="b15b7-129">Sada Visual Studio upozorňuje na použití zastaralého balíčku na kartě `Installed`. Zobrazí se upozornění pro balíček a informace o jeho zastaralosti (včetně důvodu, že byl zastaralý a místo toho alternativního balíčku, pokud je k dispozici).</span><span class="sxs-lookup"><span data-stu-id="b15b7-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Zastaralé balíčky na kartě nainstalované sady Visual Studio Správce balíčků](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="b15b7-131">dotnet. exe</span><span class="sxs-lookup"><span data-stu-id="b15b7-131">dotnet.exe</span></span>
<span data-ttu-id="b15b7-132">*K dispozici od .NET SDK 3,0*</span><span class="sxs-lookup"><span data-stu-id="b15b7-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="b15b7-133">Pokud používáte dotnet. exe, můžete spustit příkaz `dotnet list package --deprecated` ve složce řešení nebo projektu a získat tak seznam zastaralých balíčků spolu s informacemi o vyřazení:</span><span class="sxs-lookup"><span data-stu-id="b15b7-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
