---
title: Přehled ekosystému NuGet
description: Komplexní prostředky v ekosystému NuGet včetně zdrojů NuGet, projektů, nástrojů a školicích materiálů od jiných výrobců než Microsoftu.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 57fa8e5683e687aab3022ebc77d7e69a61615877
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775610"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Přehled ekosystému NuGet

Vzhledem k tomu, že je Úvod do 2010, NuGet má skvělou možnost zlepšit a automatizovat různé aspekty vývojových procesů.

Vzhledem k tomu, že NuGet je open source v rámci opravňující [licence Apache v2](http://choosealicense.com/licenses/apache/), můžou další projekty využít NuGet a společnosti, které pro něj můžou ve svých produktech vytvořit podporu. Bez ohledu na to, jestli pro open source projekty nebo pro vývoj podnikových aplikací, NuGet a další aplikace založené na a kolem NuGet přináší širokou škálu nástrojů pro zlepšení procesu vývoje softwaru.

Všechny tyto projekty jsou schopné inovovat z důvodu příspěvků vývojářů. Stejně jako přispějete k samotnému NuGet, můžete také přispět k těmto projektům prostřednictvím hlášení vad a nových nápadů na funkce, poskytování zpětné vazby, psaní dokumentace a přispívání kódu tam, kde je to možné.

## <a name="net-foundation-projects"></a>Projekty .NET Foundation

NuGet poskytuje bezplatný open source systém správy balíčků pro vývojovou platformu Microsoftu. Skládá se z několika klientských nástrojů a také ze sady služeb, které tvoří [oficiální galerii NuGet](http://www.nuget.org). V kombinaci těchto formulářů se jedná o projekt NuGet, který se řídí [.NET Foundation](http://www.dotnetfoundation.org/).

Organizace NuGet obsahuje různá úložiště na GitHubu. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) poskytuje přehled o všech úložištích a o tom, kde najít různé komponenty NuGet.

## <a name="microsoft-projects"></a>Projekty společnosti Microsoft

Společnost Microsoft přispěla k rozsáhlému vývoji NuGet. Všechny příspěvky, které provedli zaměstnanci Microsoftu, jsou také open source a jsou v rámci .NET Foundation darovány (včetně autorských práv).

## <a name="non-microsoft-projects"></a>Projekty jiných společností než Microsoft

Mnoho dalších jednotlivců a společností významně přispělo k ekosystému NuGet. Každý projekt, který je zde uveden, může mít jinou licenci než základní komponenty NuGet, takže si před použitím ověřte, zda jsou licenční podmínky přijatelné:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [Reostřejšíer JetBrains](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (nebo NuGet-as-a-Service)](http://www.myget.org/)
- [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [Server NuGet](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin a MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Další nástroje založené na NuGet

Jedná se o nástroje a pomůcky založené na NuGetu:

- [Rozšíření nakoukněte](http://getglimpse.com/Packages) (moduly plug-in jsou balíčky)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Sadu](http://www.orchardproject.net/) (moduly CMS se načítají z datového kanálu NuGet v1 hostovaného v galerii sad)
- [Implementace serveru NuGet v jazyce Java](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitter – nové publikace balíčku)
- [DefinitelyTyped](http://definitelytyped.org/) ([Automatické](https://github.com/DefinitelyTyped/NugetAutomation/) definice typu TypeScript [publikované do NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Školicí materiály a odkazy

Použití nového nástroje nebo technologie obvykle přináší výukovou křivku. Donovanovo NuGet nemá žádnou výukovou křivku strmé. Ve skutečnosti může kdokoli [začít spotřebovávat balíčky](../quickstart/install-and-use-a-package-in-visual-studio.md) rychle.

Tyto postupy, vytváření balíčků a zejména dobré balíčky – spolu s přechodu NuGet v procesech automatizovaného sestavování a nasazování vyžaduje více času s následujícími zdroji o něco delší dobu:

- [Blog NuGet](http://blog.nuget.org/)
- [Tým NuGet na Twitteru, @nuget](http://twitter.com/nuget)
- Příruček
  - [Apress pro NuGet](http://bit.ly/ProNuGet)
  - [Základy NuGet 2](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Dokumentace pro jednotlivé balíčky

[NuDoq](http://nudoq.org) poskytuje přímý přístup a aktualizace a dokumentaci pro balíčky NuGet.

NuDoq pravidelně dotazuje Server Galerie nuget.org na nejnovější aktualizace balíčků, rozbalí a zpracuje soubory dokumentace ke knihovně a aktualizuje web odpovídajícím způsobem.

## <a name="adding-your-project"></a>Přidání projektu

Pokud máte projekt ekosystému NuGet, který by byl užitečným doplňkem na tuto stránku, odešlete prosím na tuto stránku žádost o přijetí změn s úpravami.