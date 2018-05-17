---
title: Poznámky k verzi 4.7 RTM NuGet
description: Poznámky k verzi pro včetně NuGet 4.7.0 – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: a37b7fd9cb44d485250deb18d7630d47c68e0517
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="nuget-47-rtm-release-notes"></a>Poznámky k verzi 4.7 RTM NuGet

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Souhrn: Novinky v této verzi

* Máme balíček augemented podepisování povolit [podepsané úložiště balíčků](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* S 15.7 verze Visual Studio, jsme zavedli schopnost [migrovat existující projekty, které používají formát souboru packages.config používat PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) místo.

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET standardní 2.0 pomocí rozhraní .NET Framework & NuGet

.NET standard & jeho nástrojů je navržené tak, aby projektech zacílených na rozhraní .NET Framework 4.6.1 může využívat balíčky NuGet & projektech zacílených na standardní rozhraní .NET 2.0 nebo dřívější. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tento scénář, plán pro adresování a alternativní řešení můžete nasadit s je aktuální stav nástrojů.

## <a name="top-issues-fixed-in-this-release"></a>Horní chyby v této verzi

### <a name="bugs"></a>Chyby

* NuGet systémem do vzájemné zablokování v rozhraní .net Core projektu (nové regrese). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Sada: PackagePath sestavený nesprávně Pokud TfmSpecificPackageFile používá s expanze názvů cest - [#6726](https://github.com/NuGet/Home/issues/6726)
* Sada: projekt webového rozhraní api nelze vytvořit balíček, pokud ispackable explicitně nastaven. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS uživatelského rozhraní a pomocí PMC trvat 30min zobrazíte nový balíček (nuget.exe uvidí ho hned) - [#6657](https://github.com/NuGet/Home/issues/6657)
* Podpis: SignatureUtility.GetCertificateChain(...) nekontroluje všechny stavy řetězu - [#6565](https://github.com/NuGet/Home/issues/6565)
* Podpis: zlepšení zpracování DER GeneralizedTime - [#6564](https://github.com/NuGet/Home/issues/6564)
* Podpis: VS nezobrazuje NU3002 chyby při instalaci balíčku zmanipulovanou - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary je velká a malá písmena - [#6500](https://github.com/NuGet/Home/issues/6500)
* Instalovat nebo aktualizovat obnovení kódu a cesty kódu obnovení nejsou konzistentní - [#3471](https://github.com/NuGet/Home/issues/3471)
* ComboBox – verze PackageManager řešení můžete vybrat oddělovače z klávesnice - [#2606](https://github.com/NuGet/Home/issues/2606)
* Nelze načíst index služby pro zdroj `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: stavový kód odpovědi neindikuje Úspěch: 403 (zakázáno) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Chcete

* Hlavička vysílat X-NuGet-Session-Id ke korelaci napříč požadavky [funkce návrh] - [#5330](https://github.com/NuGet/Home/issues/5330)
* Zveřejnění způsobu čekat na spuštění operace obnovení provozu v sadě Visual Studio prostřednictvím rozhraní API inicializační vektory. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe - NoServiceEndpoint zabrání připojování adresa url služby příponu - [#6586](https://github.com/NuGet/Home/issues/6586)
* Přidejte hodnotu hash potvrzení do informační verze - [#6492](https://github.com/NuGet/Home/issues/6492)
* Podpis: povolení odebrání úložiště podpis/potvrzovací podpis - [#6646](https://github.com/NuGet/Home/issues/6646)
* Podpis: Rozhraní API pro odstraňování podpis úložiště nebo potvrzovací podpis- [#6589](https://github.com/NuGet/Home/issues/6589)
* Informace o zdroji přihlásit VS - [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtrovat /tools na pouze TFM a identifikátorů RID, takže nastavení XML mohou být umístěny ve složce /tools - [#6197](https://github.com/NuGet/Home/issues/6197)
* Upozornit, když příkaz Pack vyloučí soubor, který začíná.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Seznam všechny chyby v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
