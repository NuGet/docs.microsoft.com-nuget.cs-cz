---
title: NuGet 4.7 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.7.0 včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 2290025d42dcd5704b6b019c17346201fe6a990d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813790"
---
# <a name="nuget-47-release-notes"></a>NuGet 4.7 Poznámky k verzi

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) přichází s [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Shrnutí: Co je nového v 4.7.0

* Máme rozšířené podepisování balíčků, [abychom povolili balíčky podepsané úložištěm](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* S Visual Studio verze 15.7 jsme zavedli možnost [migrovat existující projekty, které používají formát packages.config použít PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md) místo.

## <a name="summary-whats-new-in-472"></a>Shrnutí: Co je nového v 4.7.2

* Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>Shrnutí: Co je nového v 4.7.3

* Oprava zabezpečení: Soubory uvnitř NUPKGs mohou mít relativní cestu nad adresářem NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Známé problémy

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Tato `Migrate packages.config to PackageReference...` možnost není k dispozici v kontextové nabídce po kliknutí pravým tlačítkem myši.

#### <a name="issue"></a>Problém

Při prvním otevření projektu NuGet nemusí mít inicializována, dokud není provedena operace NuGet. To způsobí, že možnost migrace se nezobrazí v `packages.config` `References`místní nabídce pravým tlačítkem myši na nebo .

#### <a name="workaround"></a>Alternativní řešení

Proveďte některou z následujících akcí NuGet:
* Otevřete ui Správce balíčků – `References` klikněte pravým tlačítkem myši a vyberte`Manage NuGet Packages...`
* Otevřete konzolu Správce `Tools > NuGet Package Manager`balíčků – od , vyberte`Package Manager Console`
* Spuštění obnovení NuGet – klikněte pravým tlačítkem myši na uzel řešení v Průzkumníku řešení a vyberte`Restore NuGet Packages`
* Sestavení projektu, který také aktivuje obnovení NuGet

Nyní byste měli mít možnost zobrazit možnost migrace. Všimněte si, že tato možnost není podporována a nezobrazí se pro typy projektů ASP.NET a C++.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s rozhraním .NET Standard 2.0 s rozhraním .NET Framework & NuGet

.NET Standard & jeho nástroje byly navrženy tak, že projekty zaměřené na rozhraní .NET Framework 4.6.1 mohou využívat balíčky NuGet & projekty zaměřené na standard .NET Standard 2.0 nebo starší. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře, plán pro jejich řešení a řešení, která můžete nasadit s dnešním stavem nástrojů.

## <a name="top-issues-fixed-in-this-release"></a>Hlavní problémy opravené v této verzi

### <a name="bugs"></a>Chyby

* NuGet běží do zablokování v systému .Net Core projektu (nová regrese). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pack: PackagePath je vytvořen nesprávně, pokud TfmSpecificPackageFile se používá s globbing cesty - [#6726](https://github.com/NuGet/Home/issues/6726)
* Pack: web api projekt nelze vytvořit balíček, pokud ispackable je explicitně nastavena. - [#6156](https://github.com/NuGet/Home/issues/6156)
* VS UI a PMC trvat 30min vidět nový balíček (nuget.exe vidí to hned) - [#6657](https://github.com/NuGet/Home/issues/6657)
* Podepisování: SignatureUtility.GetCertificateChain(...) nekontroluje všechny stavy řetězu - [#6565](https://github.com/NuGet/Home/issues/6565)
* Podepisování: zlepšit zpracování DER GeneralizedTime - [#6564](https://github.com/NuGet/Home/issues/6564)
* Podepisování: VS nezobrazuje chybu NU3002 při instalaci zfalšovaného balíčku - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary rozlišuje malá a velká [písmena](https://github.com/NuGet/Home/issues/6500) - #6500
* Instalace nebo aktualizace kódu obnovení a cesty obnovení kódu nejsou konzistentní - [#3471](https://github.com/NuGet/Home/issues/3471)
* Řešení PackageManager verze ComboBox můžete vybrat oddělovač pomocí klávesnice - [#2606](https://github.com/NuGet/Home/issues/2606)
* Nelze načíst index služby pro zdrojový `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: Stavový kód odpovědi neznamená úspěch: 403 (Zakázáno) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Řadiče domény

* Vyzařovat hlavičku X-NuGet-Session-Id ke korelaci mezi požadavky [návrh funkce] - [#5330](https://github.com/NuGet/Home/issues/5330)
* Vystavit způsob, jak čekat na spuštění operace obnovení spuštěna v sadě Visual Studio přes IVs apis. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe -NoServiceEndpoint se vyhne připojení adresy URL služby - [#6586](https://github.com/NuGet/Home/issues/6586)
* přidat hash potvrzení do informační verze - [#6492](https://github.com/NuGet/Home/issues/6492)
* Podepisování: povolit odebrání podpisu/protipodpisu úložiště - [#6646](https://github.com/NuGet/Home/issues/6646)
* Podepisování: API pro odstranění podpisu/protipodpisu úložiště - [#6589](https://github.com/NuGet/Home/issues/6589)
* Informace o zdroji protokolu ve VS - [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtrovat /tools pouze na TFM a RID, takže nastavení XML lze umístit do /tools složky - [#6197](https://github.com/NuGet/Home/issues/6197)
* Upozornit, když příkaz Pack vyloučí soubor začínající písmenem .  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Seznam všech problémů opravených v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
