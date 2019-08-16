---
title: Poznámky k verzi NuGet 4,7 RTM
description: Poznámky k verzi pro NuGet 4.7.0, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: fe769f95e3eda4bc07db4369544472c00b35363d
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488656"
---
# <a name="nuget-47-release-notes"></a>Zpráva k vydání verze NuGet 4,7

[Visual Studio 2017 15,7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) přináší [4.7.0 NuGet](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Shrnut Co je nového v 4.7.0

* Pro povolení [balíčků podepsaných úložištěm](https://github.com/NuGet/Home/wiki/Repository-Signatures) jsme vylepšili rozšíření balíčku.

* V rámci sady Visual Studio verze 15,7 jsme zavedli možnost [migrovat existující projekty, které používají formát Packages. config, aby](https://docs.microsoft.com/en-us/nuget/consume-packages/migrate-packages-config-to-package-reference) místo toho používaly PackageReference.

## <a name="summary-whats-new-in-472"></a>Shrnut Co je nového v 4.7.2

* Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) .

## <a name="summary-whats-new-in-473"></a>Shrnut Co je nového v 4.7.3

* Oprava zabezpečení: Soubory uvnitř NUPKGs můžou mít relativní cestu nad [#7906](https://github.com/NuGet/Home/issues/7906) ADRESÁŘem nupkg.

## <a name="known-issues"></a>Známé problémy

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Tato `Migrate packages.config to PackageReference...` možnost není k dispozici v místní nabídce kliknutím pravým tlačítkem myši.

#### <a name="issue"></a>Problém

Při prvním otevření projektu se nemusí NuGet inicializovat, dokud se neprovede operace NuGet. To způsobí, že se možnost migrace nebude zobrazovat v místní nabídce klikněte pravým tlačítkem myši `packages.config` na `References`nebo.

#### <a name="workaround"></a>Alternativní řešení

Proveďte jednu z následujících akcí NuGet:
* Otevřete uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem `References` na a vyberte`Manage NuGet Packages...`
* Otevřete konzolu Správce balíčků – v `Tools > NuGet Package Manager`vyberte`Package Manager Console`
* Spustit obnovení NuGet – pravým tlačítkem myši klikněte na uzel řešení v Průzkumník řešení a vyberte`Restore NuGet Packages`
* Sestavení projektu, který také aktivuje obnovení NuGet

Nyní byste měli být schopni zobrazit možnost migrace. Všimněte si, že tato možnost není podporovaná a nebude se zobrazovat pro ASP.NET C++ a typy projektů.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET Standard 2,0 s .NET Framework & NuGet

.NET Standard & jeho nástrojů bylo navrženo tak, aby projekty, které cílí na .NET Framework 4.6.1, mohly využívat balíčky NuGet & projektech cílících na .NET Standard 2,0 nebo starší. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy v tomto scénáři, plán pro jejich adresování a alternativní řešení, která můžete nasadit s dnešním stavem nástrojů.

## <a name="top-issues-fixed-in-this-release"></a>Hlavní problémy opravené v této verzi

### <a name="bugs"></a>Chyby

* NuGet běží na zablokování v .Net Core systém projektů (nová regrese). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Jazykové PackagePath je nesprávně vytvořená, pokud se TfmSpecificPackageFile používá s cestami expanze. [#6726](https://github.com/NuGet/Home/issues/6726)
* Balíček: projekt webového rozhraní API nemůže vytvořit balíček, pokud není explicitně nastavená žádná sada. - [#6156](https://github.com/NuGet/Home/issues/6156)
* Uživatelské rozhraní VS a PMC přebírají 30min, aby se zobrazil nový balíček (NuGet. exe ho hned vidí) – [#6657](https://github.com/NuGet/Home/issues/6657)
* Hlašuje  SignatureUtility. GetCertificateChain (...) nekontroluje všechny stavy řetězu – [#6565](https://github.com/NuGet/Home/issues/6565)
* Podepisování: vylepšení zpracování GeneralizedTime DER – [#6564](https://github.com/NuGet/Home/issues/6564)
* Hlašuje VS při instalaci zfalšována balíčku nezobrazuje NU3002ou chybu – [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile. getlibrary rozlišuje velká a malá písmena – [#6500](https://github.com/NuGet/Home/issues/6500)
* Instalace/aktualizace kód obnovení a cesty kódu obnovení nejsou konzistentní – [#3471](https://github.com/NuGet/Home/issues/3471)
* Pole PackageManager verze řešení může vybrat oddělovač pomocí klávesnice – [#2606](https://github.com/NuGet/Home/issues/2606)
* Nepovedlo se načíst index služby pro `https://www.myget.org/F/<id>` zdroj---> System .NET. http. HttpRequestException: Stavový kód odpovědi neoznačuje úspěch: 403 (zakázáno) – [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Chcete odeslat obecnou

* Generovat hlavičku X-NuGet-Session-ID pro korelaci mezi požadavky [návrh funkcí]- [#5330](https://github.com/NuGet/Home/issues/5330)
* Vystavte si způsob, jak počkat na spuštění operace obnovení běžící v aplikaci Visual Studio prostřednictvím rozhraní Ideographic API. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet. exe – a v ServiceEndpoint se nepřipojí přípona adresy URL služby – [#6586](https://github.com/NuGet/Home/issues/6586)
* Přidat potvrzení hodnoty hash do informační verze – [#6492](https://github.com/NuGet/Home/issues/6492)
* Podepisování: povolení odebrání signatury úložiště/potvrzovací podpis- [#6646](https://github.com/NuGet/Home/issues/6646)
* Hlašuje  Rozhraní API pro odstranění podpisu úložiště/potvrzovací podpis- [#6589](https://github.com/NuGet/Home/issues/6589)
* Protokolovat informace o zdroji v VS- [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtrujte/Tools jenom na TFM a RID, takže nastavení XML se dá vložit do složky/Tools – [#6197](https://github.com/NuGet/Home/issues/6197)
* Upozornit, pokud příkaz Pack vyloučí soubor, který začíná.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Seznam všech problémů opravených v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
