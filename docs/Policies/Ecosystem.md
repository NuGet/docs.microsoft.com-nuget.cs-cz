---
title: "Přehled ekosystému NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Komplexní prostředky v ekosystému NuGet, včetně zdroje NuGet, Microsoft NuGet projekty, nástrojů a školicích materiálů."
keywords: "NuGet ekosystém, projekty Microsoft NuGet, NuGet s otevřeným zdrojem, nástroje NuGet, NuGet školicí materiály"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c1e457c034f239fbea4e75f24851ea38182a294
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Přehled ekosystému NuGet

Vzhledem k tomu, že je Úvod v 2010, má NuGet zobrazí skvělé příležitosti pro zlepšení a automatizaci různých aspektů procesy vývoje.

Protože NuGet je open source v rámci projektovou [licence v2 Apache](http://choosealicense.com/licenses/apache/), ostatní projekty mohou využívat NuGet a společností můžete vytvořit podporu pro něj v jejich produkty. Pro projekty open-source nebo vývoj aplikací enterprise, NuGet a další aplikace založené na a kolem NuGet poskytují řadou nástrojů pro zlepšení vývojových procesech softwaru.

Všechny tyto projekty jsou moct inovacemi. Zajistěte kvůli vývojáře příspěvky. Stejně jako podílet se na NuGet sám sebe, udělat příspěvku na tyto projekty také pomocí sestav defekty a nové funkce nápady, poskytnutí zpětné vazby, zápis dokumentaci a přidání kódu, kde je to možné.

## <a name="net-foundation-projects"></a>Projekty foundation rozhraní .NET

NuGet poskytuje bezplatný systém správy balíčků pro vývoj pro platformu Microsoft. Skládá se z několika nástrojích klienta a také na sadu služeb, které tvoří [oficiální Galerie NuGet](http://www.nuget.org). V kombinaci, tyto formuláři NuGet projektu, která se řídí [.NET Foundation](http://www.dotnetfoundation.org/).

Organizace NuGet obsahuje různé úložiště na Githubu. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) poskytuje přehled o všech úložiště a kde najít různé součásti NuGet.

## <a name="microsoft-projects"></a>Microsoft projekty

Microsoft má hojně podílí na vývoji jejích NuGet. Všechny příspěvky provedené zaměstnanců společnosti Microsoft jsou také otevřít zdroj a jsou věnován (včetně autorských práv) na rozhraní .NET Foundation.

## <a name="non-microsoft-projects"></a>Projekty od jiných výrobců

Mnoho jednotlivce a společností významně přispěli k ekosystému NuGet. Každý projekt tady může mít licenci jinou než základní součásti NuGet, tak ověřte, jestli jsou před použít přípustné s licenčními podmínkami:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (or NuGet-as-a-service)](http://www.myget.org/)
- [Balíček NuGet Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin a MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Další nástroje na základě NuGet

Jsou to nástrojů a pomůcek založený na NuGet:

- [Rozšíření balíčku glimpse](http://getglimpse.com/Packages) (moduly plug-in jsou balíčky)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (V1 NuGet kanálu hostované v galerii Orchard CMS moduly načtené)
- [Implementace Java serveru NuGet](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitter robota klientské nový balíček publikace)
- [DefinitelyTyped](http://definitelytyped.org/) ([automatické](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript typ [definice publikovaná NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Výukové materiály a odkazy

Pomocí nového nástroje nebo technologie obvykle dodává s křivku. Naštěstí, má NuGet žádné zvládnutí learning všechny křivka! Ve skutečnosti bylo možné [Začínáme využívání balíčky](../quickstart/use-a-package.md) rychle.

Ale nutné dodat, vytváření balíčků – a zvlášť vhodné balíčky – společně s osvojují NuGet v automatizované procesy sestavení a nasazení, vyžaduje výdaje trochu delší dobu se v následujících zdrojích informací:

- [NuGet Blog](http://blog.nuget.org/)
- [NuGet týmu na Twitteru,@nuget](http://twitter.com/nuget)
- Knihy:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [Essentials NuGet 2](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Dokumentace pro jednotlivé balíčky

[NuDoq](http://nudoq.org) poskytuje snadný přístup, aktualizace a dokumentace pro balíčky NuGet.

NuDoq pravidelně dotazuje serveru Galerie nuget.org nejnovější balíček aktualizace, rozbalí a zpracovává soubory knihovny dokumentace a příslušným způsobem aktualizuje webu.

## <a name="adding-your-project"></a>Přidání projektu

Pokud máte projekt ekosystém NuGet, které by cenné přidání na tuto stránku, odešlete prosím žádost o přijetí změn s upravíte na tuto stránku.
