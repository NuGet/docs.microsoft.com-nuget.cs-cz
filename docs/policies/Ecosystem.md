---
title: Přehled ekosystému NuGet
description: Ucelené materiály v ekosystému NuGet zdroje NuGet, Microsoft NuGet projektů, nástroje a školicích materiálů.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548141"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Přehled ekosystému NuGet

Protože je úvod 2010, má skvělé příležitosti pro zlepšení a automatizaci různých aspektů vývojové procesy uvedené NuGet.

Vzhledem k tomu, že Správce balíčků NuGet je open source v rámci povolující [licence Apache verze 2](http://choosealicense.com/licenses/apache/), ostatní projekty mohou využívat NuGet a díky tomu společnosti podporu do vlastních produktů. Pro open source projektů nebo vývoji podnikových aplikací, poskytují NuGet a jiných aplikací vytvořených a kolem NuGet pro řadu nástrojů pro zlepšení procesu vývoje softwaru.

Všechny tyto projekty budou moct inovace kvůli příspěvků pro vývojáře. Stejně jako jste mohli přispívat na NuGet samotného, také díky příspěvek do těchto projektů pro hlášení chyb a nové nápady týkající se funkcí, poskytování zpětné vazby, píšete dokumentaci a přispívání ke kódu tam, kde je to možné.

## <a name="net-foundation-projects"></a>Projekty .NET foundation

NuGet poskytuje zdarma, open source systém pro správu balíčků pro vývojovou platformu Microsoft. Skládá se z několika klientských nástrojů i sadu služeb, které tvoří [oficiální Galerie NuGet](http://www.nuget.org). V kombinaci, vytvářejí projektu NuGet, které se vztahují [.NET Foundation](http://www.dotnetfoundation.org/).

Organizace NuGet obsahuje různých úložištích na Githubu. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) poskytuje přehled o všechna úložiště a kde najít různé součásti NuGet.

## <a name="microsoft-projects"></a>Projekty Microsoft

Microsoft přidal často k vývoji NuGet. Zaměstnanci Microsoftu všechny příspěvky jsou také otevřít zdroj a je poskytnuto (včetně autorských práv) pro .NET Foundation.

## <a name="non-microsoft-projects"></a>Projekty jiné společnosti než Microsoft

Mnoho dalších jednotlivce a společnosti významně přispěli k ekosystému NuGet. Každý projekt zde uvedené může mít jiné licenční než součásti core NuGet, proto ověřte, zda jsou přijatelné před použít licenční podmínky:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (nebo NuGet-as-a-service)](http://www.myget.org/)
- [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin a MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Další nástroje založená na Nugetu

Toto jsou nástroje, které jsou vytvořené na webu NuGet:

- [Nakoukněte rozšíření](http://getglimpse.com/Packages) (moduly plug-in jsou balíčky)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (z v1 informačního kanálu NuGet hostované ve galerii Orchard CMS moduly načtené)
- [Java provádění NuGet Server](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitteru bot klientské nový balíček publikace)
- [DefinitelyTyped](http://definitelytyped.org/) ([automatické](https://github.com/DefinitelyTyped/NugetAutomation/) typů TypeScript [definice se publikují do NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Výukové materiály a odkazy

Pomocí nového nástroje nebo technologie obvykle obsahuje učení křivky. Naštěstí vám, nemá NuGet bez strmé učení křivky všechno! Ve skutečnosti bylo možné [Začínáme využívání balíčků](../quickstart/use-a-package.md) rychle.

Který ale nutné dodat, vytváření balíčků – a hlavně kvalitní balíčky – spolu s středu NuGet v automatizované procesy sestavení a nasazení, vyžaduje útraty trochu více času na následujících odkazech:

- [NuGet Blog](http://blog.nuget.org/)
- [NuGet týmu na Twitteru, @nuget](http://twitter.com/nuget)
- Knihy:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [Základy NuGet 2](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Dokumentace pro jednotlivé balíčky

[NuDoq](http://nudoq.org) poskytuje jednoduchý přístup, aktualizace a dokumentaci pro balíčky NuGet.

NuDoq pravidelně dotazuje serveru Galerie nuget.org nejnovější balíček aktualizace, rozbalí a zpracovává soubory knihovny dokumentace a odpovídajícím způsobem aktualizuje webu.

## <a name="adding-your-project"></a>Přidání projektu

Pokud máte projekt ekosystému NuGet, která by byla záležitostí cenné na tuto stránku, odešlete prosím žádost o přijetí změn s úpravy na tuto stránku.
