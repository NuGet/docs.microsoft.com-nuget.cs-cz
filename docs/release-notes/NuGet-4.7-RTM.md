---
title: Zpráva k vydání verze NuGet 4.7 RTM
description: Zpráva k vydání verze pro NuGet 4.7.0 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 79be74f9c54e27bf2c08e83c7adf81d1f96ce79a
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508160"
---
# <a name="nuget-47-rtm-release-notes"></a>Zpráva k vydání verze NuGet 4.7 RTM

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) součástí [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Souhrn: Novinky v této verzi

* Budeme mít vylepšila povolit podepisování balíčků [úložiště podepsané balíčky](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* S Visual Studio verze 15.7, zavedli jsme možnost [migrovat existující projekty, které používají formát souboru packages.config na PackageReference použít](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) místo.

## <a name="known-issues"></a>Známé problémy

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` Možnost není k dispozici v místní nabídce klikněte pravým tlačítkem na

#### <a name="issue"></a>Problém

Při prvním otevření projektu NuGet nemusí mít inicializace, dokud se provádí operace NuGet. To způsobí, že není uveden v místní nabídce klikněte pravým tlačítkem na možnost migrace `packages.config` nebo `References`.

#### <a name="workaround"></a>Alternativní řešení

Proveďte některou z následujících akcí NuGet:
* Otevřít uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem na `References` a vyberte `Manage NuGet Packages...`
* Otevřete konzolu Správce balíčků pro - ze `Tools > NuGet Package Manager`vyberte `Package Manager Console`
* Spuštění obnovení NuGet – klikněte pravým tlačítkem na uzel řešení v Průzkumníku řešení a vyberte `Restore NuGet Packages`
* Sestavte projekt, který také aktivuje obnovení NuGet

Teď by měl být vidět možnost migrace. Všimněte si, že tato možnost není podporována a nezobrazí se pro typy projektů ASP.NET a C++.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET Standard 2.0 pomocí rozhraní .NET Framework a NuGet

.NET standard a jeho nástroje je navržená tak, že projekty cílené na rozhraní .NET Framework 4.6.1 může spotřebovat balíčky NuGet & projekty cílené na .NET Standard 2.0 nebo dřívější. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře plánu pro účely řešení a alternativní řešení můžete nasadit s dnešní stavu nástrojů.

## <a name="top-issues-fixed-in-this-release"></a>Nejzávažnější chyby opravené v této verzi

### <a name="bugs"></a>Chyby

* NuGet systémem do zablokování v.Net Core project (nový regrese). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Balíček: PackagePath je správně vytvořena Pokud TfmSpecificPackageFile se používá s cestami podpory zástupných znaků - [#6726](https://github.com/NuGet/Home/issues/6726)
* Balíček: projektem webového rozhraní api nelze vytvořit balíček, pokud ispackable explicitně nastavena. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS uživatelského rozhraní a konzolu PMC trvat 30 minut, chcete-li zobrazit nový balíček (nuget.exe uvidí ho hned) - [#6657](https://github.com/NuGet/Home/issues/6657)
* Podepisování: SignatureUtility.GetCertificateChain(...) nekontroluje všechny stavy řetězce - [#6565](https://github.com/NuGet/Home/issues/6565)
* Podepisování: zlepšení zpracování DER GeneralizedTime – [#6564](https://github.com/NuGet/Home/issues/6564)
* Podepisování: VS nezobrazuje NU3002 chyby při instalaci balíčku zmanipulovanou - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary rozlišuje velikost písmen – [#6500](https://github.com/NuGet/Home/issues/6500)
* Instalace nebo aktualizace obnovit kódu a cesty kódu obnovení nejsou konzistentní - [#3471](https://github.com/NuGet/Home/issues/3471)
* Řešení PackageManager verze – pole se seznamem můžete vybrat oddělovač prostřednictvím klávesnice - [#2606](https://github.com/NuGet/Home/issues/2606)
* Nepovedlo se načíst index služby pro zdroj `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: stavový kód odpovědi neoznačuje Úspěch: 403 (zakázáno) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Chcete

* Záhlaví vygeneruje X-NuGet-Session-Id pro korelaci mezi požadavky [funkce návrh] - [#5330](https://github.com/NuGet/Home/issues/5330)
* Zveřejněte cestu pro čekání na spuštění operace obnovení pro spuštění v sadě Visual Studio prostřednictvím rozhraní API a vektory IV. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe - NoServiceEndpoint se vyhnout přidávání adresa url služby přípona - [#6586](https://github.com/NuGet/Home/issues/6586)
* Přidat informační verze – hodnota hash zápisu [#6492](https://github.com/NuGet/Home/issues/6492)
* Podepisování: povolení odebrání potvrzovací podpis úložiště/podpis - [#6646](https://github.com/NuGet/Home/issues/6646)
* Podepisování: Rozhraní API pro odstranění signatura a potvrzovací podpis úložiště- [#6589](https://github.com/NuGet/Home/issues/6589)
* Protokolovat informace o zdroji v sadě Visual Studio – [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtrovat /tools na pouze TFM a identifikátorů RID, takže nastavení XML mohou být umístěny ve složce /tools - [#6197](https://github.com/NuGet/Home/issues/6197)
* Upozornit, pokud příkaz Pack vyloučí soubor, který začíná.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Seznam všech problémů, které jsou opravené v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
