---
title: "Poznámky k verzi NuGet 1.8 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: e694ee1a-fe4c-4397-8d0a-7336be4dfebe
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.8 NuGet."
keywords: "NuGet 1.8 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 350f0d9590c1e0ef1a843fd783203b158059efa7
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="0efe9-104">Poznámky k verzi 1,8 NuGet</span><span class="sxs-lookup"><span data-stu-id="0efe9-104">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="0efe9-105">[Poznámky k verzi NuGet 1.7](../release-notes/nuget-1.7.md) | [NuGet 2.0 poznámky k verzi](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="0efe9-105">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="0efe9-106">NuGet 1.8 byla vydána 23 květen 2012.</span><span class="sxs-lookup"><span data-stu-id="0efe9-106">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="0efe9-107">Instalace známý problém</span><span class="sxs-lookup"><span data-stu-id="0efe9-107">Known Installation Issue</span></span>
<span data-ttu-id="0efe9-108">Pokud používáte VS 2010 SP1, můžete spustit došlo k chybě instalace při pokusu o upgrade NuGet, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="0efe9-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="0efe9-109">Alternativní řešení je jednoduše odinstalovat NuGet a nainstalujte ji z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="0efe9-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="0efe9-110">V tématu [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Další informace, nebo [přejděte přímo na opravu hotfix VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="0efe9-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="0efe9-111">Poznámka: Pokud Visual Studio nebude možné odinstalovat rozšíření (k dispozici tlačítko Odinstalovat), bude pravděpodobně nutné restartujte Visual Studio pomocí "Spustit jako správce."</span><span class="sxs-lookup"><span data-stu-id="0efe9-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="0efe9-112">NuGet 1.8 kompatibilní se systémem Windows XP, opravy hotfix publikována</span><span class="sxs-lookup"><span data-stu-id="0efe9-112">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="0efe9-113">Krátce po vydání byl NuGet 1.8, zjistili jsme, že ke změně šifrování v 1.8 překročila uživatelé v systému Windows XP.</span><span class="sxs-lookup"><span data-stu-id="0efe9-113">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="0efe9-114">Protože Vydali jsme opravu hotfix, která řeší tento problém.</span><span class="sxs-lookup"><span data-stu-id="0efe9-114">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="0efe9-115">Při aktualizaci NuGet prostřednictvím Galerie rozšíření sady Visual Studio, zobrazí se tato oprava hotfix.</span><span class="sxs-lookup"><span data-stu-id="0efe9-115">By updating NuGet through the Visual Studio Extension Gallery, you will receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="0efe9-116">Funkce</span><span class="sxs-lookup"><span data-stu-id="0efe9-116">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="0efe9-117">Satelitní balíčky pro místní zdroje</span><span class="sxs-lookup"><span data-stu-id="0efe9-117">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="0efe9-118">NuGet 1.8 teď podporuje možnost vytvořit samostatné balíčky pro místní zdroje, podobně jako možnosti satelitní sestavení rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="0efe9-118">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="0efe9-119">Satelitní balíček je vytvořen stejným způsobem jako jakýkoli jiný balíček NuGet s přidáním systému několik konvence:</span><span class="sxs-lookup"><span data-stu-id="0efe9-119">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="0efe9-120">Satelitní balíček ID a název souboru by měla obsahovat příponu, která odpovídá jednomu z standardní [jazykovou verzi řetězců v rozhraní .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span><span class="sxs-lookup"><span data-stu-id="0efe9-120">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="0efe9-121">V jeho `.nuspec` souboru balíčku satelitní měli definovat element jazyka s do jednoho řetězce jazykovou verzi, která je použita v ID</span><span class="sxs-lookup"><span data-stu-id="0efe9-121">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="0efe9-122">Balíček satelitní měli definovat v závislosti na jeho `.nuspec` souboru do jeho základní balíčku, který je jednoduše balíček se stejným ID minus příponou jazyk.</span><span class="sxs-lookup"><span data-stu-id="0efe9-122">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="0efe9-123">Základní balíček musí být k dispozici v úložišti pro úspěšnou instalaci.</span><span class="sxs-lookup"><span data-stu-id="0efe9-123">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="0efe9-124">Chcete-li nainstalovat balíček s lokalizované prostředky, vývojář explicitně vybere lokalizované balíček z úložiště.</span><span class="sxs-lookup"><span data-stu-id="0efe9-124">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="0efe9-125">V současné době Galerie NuGet není poskytnuta jakýkoli druh zvláštní zacházení satelitní balíčků.</span><span class="sxs-lookup"><span data-stu-id="0efe9-125">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![Dialogové okno Správce balíčku se lokalizované pacakges](./media/dlg-w-loc-packs.png)

<span data-ttu-id="0efe9-127">Vzhledem k tomu, že balíček satelitní uvádí závislost na jeho základní balíček, jsou satelitní i základní balíčky vyžádat do složky balíčků NuGet a nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="0efe9-127">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![Složka balíčky s lokalizované balíčky](./media/fldr-loc-packs.png)

<span data-ttu-id="0efe9-129">Při instalaci balíčku satelit, navíc NuGet také rozpozná zásady vytváření názvů řetězce jazykovou verzi a pak zkopíruje lokalizovaný prostředek sestavení do správné podsložky v rámci balíčku jádra, takže mohou být zachyceny pomocí rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="0efe9-129">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![Základní složka balíčku s složku zkopírovaný prostředků](./media/fldr-copied-loc.png)

<span data-ttu-id="0efe9-131">Jeden existující chyby na mějte na paměti, satelitní balíčků je, že NuGet nekopíruje lokalizované prostředky k `bin` složku pro webové projekty.</span><span class="sxs-lookup"><span data-stu-id="0efe9-131">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="0efe9-132">Tento problém bude vyřešený v příští verzi balíčku nuget.</span><span class="sxs-lookup"><span data-stu-id="0efe9-132">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="0efe9-133">Kompletní příklad, který ukazuje, jak vytvořit a používat satelitní balíčky, najdete v části [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span><span class="sxs-lookup"><span data-stu-id="0efe9-133">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="0efe9-134">Balíček obnovení souhlasu</span><span class="sxs-lookup"><span data-stu-id="0efe9-134">Package Restore Consent</span></span>
<span data-ttu-id="0efe9-135">V NuGet 1.8 jsme umístěné základ pro podporu důležité omezení pro obnovení balíčků pro ochrany osobních údajů uživatele.</span><span class="sxs-lookup"><span data-stu-id="0efe9-135">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="0efe9-136">Toto omezení vyžaduje vývojářům vytvářet projekty a řešení, které používáte obnovení balíčků pro výslovně souhlasit s obnovení balíčků je přechod do režimu online na stahovat balíčky ze zdroje balíčků nakonfigurované.</span><span class="sxs-lookup"><span data-stu-id="0efe9-136">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="0efe9-137">Zadejte svůj souhlas 2 způsoby.</span><span class="sxs-lookup"><span data-stu-id="0efe9-137">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="0efe9-138">První naleznete v dialogu balíček Správce konfigurace jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="0efe9-138">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="0efe9-139">Tato metoda je primárně určený pro vývojáře počítače.</span><span class="sxs-lookup"><span data-stu-id="0efe9-139">This method is primarily intended for developer machines.</span></span>

![Dialogové okno Konfigurace správce balíčku](./media/pr-consent-configdlg.png)

<span data-ttu-id="0efe9-141">Druhý způsob je nastavení prostředí proměnné "EnableNuGetPackageRestore" na hodnotu "true".</span><span class="sxs-lookup"><span data-stu-id="0efe9-141">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="0efe9-142">Tato metoda je určena pro bezobslužné počítače, jako jsou třeba servery položky konfigurace nebo sestavení.</span><span class="sxs-lookup"><span data-stu-id="0efe9-142">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="0efe9-143">Nyní jak jsme uvedli výše, budeme mít pouze podle základ pro tuto funkci NuGet 1.8.</span><span class="sxs-lookup"><span data-stu-id="0efe9-143">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="0efe9-144">Prakticky to znamená, že když jsme přidali veškerou logiku k povolení této funkce, vynuceno není aktuálně v této verzi.</span><span class="sxs-lookup"><span data-stu-id="0efe9-144">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="0efe9-145">Bude povoleno, ale v příští verzi NuGet, takže jsme chtěli, aby vás upozornit je co nejdříve, aby správně nakonfigurovat vaše prostředí a proto nelze dopad jsme spouštění vynutit omezení souhlasu.</span><span class="sxs-lookup"><span data-stu-id="0efe9-145">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="0efe9-146">Další podrobnosti najdete v tématu [příspěvku na blogu týmu](http://blog.nuget.org/20120518/package-restore-and-consent.html) na tuto funkci.</span><span class="sxs-lookup"><span data-stu-id="0efe9-146">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="0efe9-147">Vylepšení výkonu nuget.exe</span><span class="sxs-lookup"><span data-stu-id="0efe9-147">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="0efe9-148">Změnou instalační příkaz stáhnout a nainstalovat balíčky současně přináší NuGet 1.8 výraznému zlepšení výkonu k nuget.exe – a obnovení balíčků rozšíření.</span><span class="sxs-lookup"><span data-stu-id="0efe9-148">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="0efe9-149">Vysoké úrovně testování ukazuje výkon pro instalaci 6 balíčky do projektu volbou asi 35 % v NuGet 1.8.</span><span class="sxs-lookup"><span data-stu-id="0efe9-149">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="0efe9-150">Zvýšením počtu balíčků, které mají 25 uvádí výkonnější o 60 %.</span><span class="sxs-lookup"><span data-stu-id="0efe9-150">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="0efe9-151">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="0efe9-151">Bug Fixes</span></span>
<span data-ttu-id="0efe9-152">NuGet 1.8 obsahuje několik oprav chyb s důrazem na konzole Správce balíčků a pracovní postup obnovení balíčku, zvlášť, protože se týká balíček obnovení souhlasu a integrace s Windows 8 Express.</span><span class="sxs-lookup"><span data-stu-id="0efe9-152">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="0efe9-153">Úplný seznam pracovní položky pevná ve NuGet 1.8 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="0efe9-153">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
