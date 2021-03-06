---
title: Poznámky k verzi NuGet 4,7 RTM
description: Poznámky k verzi pro NuGet 4.7.0, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 143781cf0a95c6a156d4afcd83ad277f3e227711
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780158"
---
# <a name="nuget-47-release-notes"></a>Zpráva k vydání verze NuGet 4,7

[Visual Studio 2017 15,7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) přináší [4.7.0 NuGet](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Shrnutí: co je nového v 4.7.0

* Pro povolení [balíčků podepsaných úložištěm](https://github.com/NuGet/Home/wiki/Repository-Signatures) jsme vylepšili rozšíření balíčku.

* V rámci sady Visual Studio verze 15,7 jsme zavedli možnost [migrovat existující projekty, které používají formát packages.config pro místo toho použití PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md) .

## <a name="summary-whats-new-in-472"></a>Shrnutí: co je nového v 4.7.2

* Oprava zabezpečení: oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) .

## <a name="summary-whats-new-in-473"></a>Shrnutí: co je nového v 4.7.3

* Oprava zabezpečení: soubory uvnitř NUPKGs můžou mít relativní cestu nad [#7906](https://github.com/NuGet/Home/issues/7906) ADRESÁŘem nupkg.

## <a name="known-issues"></a>Známé problémy

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Tato `Migrate packages.config to PackageReference...` možnost není k dispozici v místní nabídce kliknutím pravým tlačítkem myši.

#### <a name="issue"></a>Problém

Při prvním otevření projektu se nemusí NuGet inicializovat, dokud se neprovede operace NuGet. To způsobí, že se možnost migrace nebude zobrazovat v místní nabídce klikněte pravým tlačítkem myši na `packages.config` nebo `References` .

#### <a name="workaround"></a>Alternativní řešení

Proveďte jednu z následujících akcí NuGet:
* Otevřete uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem na `References` a vyberte `Manage NuGet Packages...`
* Otevřete konzolu Správce balíčků – v `Tools > NuGet Package Manager` Vyberte `Package Manager Console`
* Spustit obnovení NuGet – pravým tlačítkem myši klikněte na uzel řešení v Průzkumník řešení a vyberte `Restore NuGet Packages`
* Sestavení projektu, který také aktivuje obnovení NuGet

Nyní byste měli být schopni zobrazit možnost migrace. Všimněte si, že tato možnost není podporovaná a nebude se zobrazovat pro typy projektů ASP.NET a C++.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET Standard 2,0 s .NET Framework & NuGet

.NET Standard & jeho nástrojů bylo navrženo tak, aby projekty, které cílí na .NET Framework 4.6.1, mohly využívat balíčky NuGet & projektech cílících na .NET Standard 2,0 nebo starší. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy v tomto scénáři, plán pro jejich adresování a alternativní řešení, která můžete nasadit s dnešním stavem nástrojů.

## <a name="top-issues-fixed-in-this-release"></a>Hlavní problémy opravené v této verzi

### <a name="bugs"></a>Chyby

* NuGet běží na zablokování v .Net Core systém projektů (nová regrese). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pack: PackagePath se nesprávně vytvoří, pokud se TfmSpecificPackageFile používá s cestami k expanzi. [#6726](https://github.com/NuGet/Home/issues/6726)
* Balíček: projekt webového rozhraní API nemůže vytvořit balíček, pokud není explicitně nastavená žádná sada. - [#6156](https://github.com/NuGet/Home/issues/6156)
* Uživatelské rozhraní VS a PMC převezmou 30min, že se zobrazí nový balíček (nuget.exe hned hned) – [#6657](https://github.com/NuGet/Home/issues/6657)
* Podepisování: SignatureUtility. GetCertificateChain (...) nekontroluje všechny stavy řetězu – [#6565](https://github.com/NuGet/Home/issues/6565)
* Podepisování: vylepšení zpracování GeneralizedTime DER – [#6564](https://github.com/NuGet/Home/issues/6564)
* Podepisování: VS nezobrazuje NU3002 chybu při instalaci úmyslného balíčku – [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile. getlibrary rozlišuje velká a malá písmena – [#6500](https://github.com/NuGet/Home/issues/6500)
* Instalace/aktualizace kód obnovení a cesty kódu obnovení nejsou konzistentní – [#3471](https://github.com/NuGet/Home/issues/3471)
* Pole PackageManager verze řešení může vybrat oddělovač pomocí klávesnice – [#2606](https://github.com/NuGet/Home/issues/2606)
* Nepovedlo se načíst index služby pro zdroj `https://www.myget.org/F/<id>` ---> System .NET. http. HttpRequestException: stavový kód odpovědi neindikuje úspěch: 403 (zakázáno) – [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Chcete odeslat obecnou

* Generovat hlavičku X-NuGet-Session-ID pro korelaci mezi požadavky [návrh funkcí]- [#5330](https://github.com/NuGet/Home/issues/5330)
* Vystavte si způsob, jak počkat na spuštění operace obnovení běžící v aplikaci Visual Studio prostřednictvím rozhraní Ideographic API. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe – služba ServiceEndpoint se nepřipojí k příponě adresy URL služby – [#6586](https://github.com/NuGet/Home/issues/6586)
* Přidat potvrzení hodnoty hash do informační verze – [#6492](https://github.com/NuGet/Home/issues/6492)
* Podepisování: povolení odebrání signatury úložiště/potvrzovací podpis- [#6646](https://github.com/NuGet/Home/issues/6646)
* Podepisování: rozhraní API pro odstranění podpisu úložiště/potvrzovací podpis- [#6589](https://github.com/NuGet/Home/issues/6589)
* Protokolovat informace o zdroji v VS- [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtrujte/Tools jenom na TFM a RID, takže nastavení XML se dá vložit do složky/Tools – [#6197](https://github.com/NuGet/Home/issues/6197)
* Upozornit, pokud příkaz Pack vyloučí soubor, který začíná.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Seznam všech problémů opravených v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
