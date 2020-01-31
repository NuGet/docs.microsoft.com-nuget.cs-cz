---
title: Poznámky k verzi NuGet 4,8 RTM
description: Poznámky k verzi pro NuGet 4.8.1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813764"
---
# <a name="nuget-48-release-notes"></a>Zpráva k vydání verze NuGet 4,8

[Visual Studio 2017 15,8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) přináší funkce NuGet 4,8.


K dispozici jsou také verze příkazového řádku stejných funkcí:
* NuGet. exe 4,8 – [NuGet.org/downloads](https://nuget.org/downloads)
* DotNet. exe – [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>Shrnutí: co je nového v 4.8.0
* NuGet. exe teď podporuje LONGFILENAMES ve Windows 10 – [#6937](https://github.com/NuGet/Home/issues/6937)
* Moduly plug-in pro ověřování teď fungují napříč nástroji MsBuild, DotNet. exe, NuGet. exe a Visual Studio, včetně různých platforem. První generace modulů plug-in pro ověřování se v nástroji MsBuild, DotNet. exe nepodporuje. Poznámka: buildy VS 2017 15,9 Preview mají zahrnutý modul plug-in VSTS Authentication. [#6486](https://github.com/NuGet/Home/issues/6486)
* Překladač SDK pro MsBuild se teď vytváří jako součást NuGet a instaluje se s nástroji NuGet pro VS. Zabráníte tak tomu, aby se verze synchronizoval. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference nyní podporuje DevelopmentDependency metadata – [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Shrnutí: co je nového v 4.8.2

* Oprava zabezpečení: oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) .

## <a name="known-issues"></a>Známé problémy
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Instalace podepsaných balíčků na počítači CI nebo v offline prostředí trvá déle než obvykle.

#### <a name="issue"></a>Problém
Pokud počítač omezil přístup k Internetu (například počítač sestavení ve scénáři CI/CD), zobrazí se při instalaci nebo obnovení podepsaného balíčku NuGet upozornění ([NU3028](../reference/errors-and-warnings/nu3028.md)), protože servery pro odvolání nejsou dostupné. To je očekávané chování. V některých případech ale může mít neúmyslná concequences, jako je například instalace nebo obnovení balíčku trvá déle než obvykle.

#### <a name="workaround"></a>Alternativní řešení
Aktualizujte na Visual Studio 15.8.4 a NuGet. exe 4.8.1, kde jsme zavedli proměnnou prostředí pro přepnutí do režimu kontroly odvolání.
Nastavení proměnné prostředí `NUGET_CERT_REVOCATION_MODE` na `offline` vynutí NuGet, aby zkontroloval stav odvolání certifikátu pouze proti seznamu odvolaných certifikátů v mezipaměti a NuGet se nebude pokoušet o přístup k serverům pro odvolání. Je-li režim kontroly odvolání nastaven na hodnotu `offline`, bude upozornění sníženo na informaci.

> [!Warning]
> V normálním cirumstances se nedoporučuje přepnout režim kontroly odvolání na offline. To způsobí, že NuGet skočí kontrolu online odvolání a provede jenom kontrolu odvolání offline proti seznamu odvolaných certifikátů v mezipaměti, který může být zastaralý. To znamená, že balíčky, ve kterých se podpisový certifikát mohl odvolat, bude pokračovat v instalaci nebo obnovení, což by jinak znamenalo neúspěšnou kontrolu odvolání a nenainstalovalo se.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Možnost `Migrate packages.config to PackageReference...` není k dispozici v místní nabídce kliknutím pravým tlačítkem myši.

#### <a name="issue"></a>Problém

Při prvním otevření projektu se nemusí NuGet inicializovat, dokud se neprovede operace NuGet. To způsobí, že se možnost migrace nebude zobrazovat v místní nabídce `packages.config` nebo `References`kliknutím pravým tlačítkem myši.

#### <a name="workaround"></a>Alternativní řešení

Proveďte jednu z následujících akcí NuGet:
* Otevřete uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem na `References` a vyberte `Manage NuGet Packages...`
* Otevřete konzolu Správce balíčků – z `Tools > NuGet Package Manager`vyberte `Package Manager Console`
* Spustit obnovení NuGet – pravým tlačítkem myši klikněte na uzel řešení v Průzkumník řešení a vyberte `Restore NuGet Packages`
* Sestavení projektu, který také aktivuje obnovení NuGet

Nyní byste měli být schopni zobrazit možnost migrace. Všimněte si, že tato možnost není podporovaná a nebude se zobrazovat pro ASP.NET C++ a typy projektů.
Poznámka: Tento problém byl opraven ve VS 2017 15,9 Preview 3

## <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

### <a name="bugs"></a>Chyby
#### <a name="signing"></a>Hlašuje
* Podepisování: instalace podepsaného balíčku v prostředí offline [#7008](https://github.com/NuGet/Home/issues/7008) --opraveno v 4.8.1
* Podepisování: nesprávná kontrolní adresa URL – [#7174](https://github.com/NuGet/Home/issues/7174)
* Podepisování: Kontrola integrity balíčku v RepositorySignatureVerifier, když je balíček podepsaný podpisem úložiště – [#6926](https://github.com/NuGet/Home/issues/6926)
* Kontrola integrity balíčku se nezdařila. musí mít ID balíčku ve zprávě (a kód chyby) – [#6944](https://github.com/NuGet/Home/issues/6944)
* Ověření balíčku podepsaného úložiště povoluje balíčky podepsané jiným certifikátem- [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet-podepisování – adresa URL časového razítka nemůže být https://á? - [#6871](https://github.com/NuGet/Home/issues/6871)
* NeNullRef ve scénáři balení NuSpec, Vylepšete taky možnosti – [#6866](https://github.com/NuGet/Home/issues/6866)
* Při aktualizaci přihlašovacích údajů při přidávání časového razítka do potvrzovací podpis- [#6840](https://github.com/NuGet/Home/issues/6840) je paměť neplatná.
* Podepisování: odebrání výjimek CTL – [#6794](https://github.com/NuGet/Home/issues/6794)
* Podepisování: contentUrl musí být HTTPS- [#6777](https://github.com/NuGet/Home/issues/6777)
* Podepisování: SignedPackageVerifierSettings. VSClientDefaultPolicy je nepoužitelné – [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Komprimovat
* Při použití příkazu dotnet. exe k balení nuspec- [#6866](https://github.com/NuGet/Home/issues/6866) by nemělo být nutné obnovení a sestavení.
* Povolení prázdných náhradních tokenů v NuspecProperties- [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask vyvolá NullReferenceException při zadání NuspecProperties- [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Usnadnění
* Přístup Hodnota řetězec "předprodej" pod tlačítkem Package je pokrytá popisem balíčku v uživatelském rozhraní PM – [#4504](https://github.com/NuGet/Home/issues/4504)
* Přístup Při výběru Microsoft Visual Studio offline balíčků v uživatelském rozhraní PM se zkrátilo tlačítko pro vyřazení a nastavení zdroje balíčku. [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Konzola pro správu prostředí PowerShell (PMC)
* `Update-Package` ignoruje rozsah verze PackageReference – [#6775](https://github.com/NuGet/Home/issues/6775)
* problém s `Update-Package -reinstall`em v nejrůznějším řešení – [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` přeinstaluje všechny balíčky místo pouze pojmenovaného [#737](https://github.com/NuGet/Home/issues/737)
* Může aktualizovat balíček NuGet v neuvedeném seznamu z konzoly Správce balíčků – [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Různé
* Oprava `NuGet update self` NuGet. příkaz CommandLine nupkg by neměl být semver 2.0 – [#7116](https://github.com/NuGet/Home/issues/7116)
* Zlepšení prostředí při selhání instalace NU1107 – [#7107](https://github.com/NuGet/Home/issues/7107)
* Serializace GetAuthenticationCredentialRequest je nesprávná – [#6983](https://github.com/NuGet/Home/issues/6983)
* AsyncPackage sady NuGet sady Visual Studio se nepovede načíst, když se inicializuje z vlákna uživatelského rozhraní – [#6976](https://github.com/NuGet/Home/issues/6976)
* Obnovení oznamuje zprávy zavádějící chyby informující o tom, že je Project. JSON nutný – [#6959](https://github.com/NuGet/Home/issues/6959)
* UI správce balíčků: náhled změn, tlačítko OK nefunguje automaticky pomocí klávesnice – [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources se pro projekt s odkazy na P2P ignorují – [#6776](https://github.com/NuGet/Home/issues/6776)
* Při vytváření projektu testů jednotek pomocí šablony .NET Framework se otevře starší model projektu s balíčky. config- [#6736](https://github.com/NuGet/Home/issues/6736)
* umožnit odkaz na projekt přepsat závislost balíčku – [#6536](https://github.com/NuGet/Home/issues/6536)
* Vystavení NoDefaultExcludes v úloze MSBuild – [#6450](https://github.com/NuGet/Home/issues/6450)
* Stavová zpráva pro "vymazání všech mezipaměti NuGet" může být při změně velikosti okna skryta – [#5938](https://github.com/NuGet/Home/issues/5938)


[Seznam všech problémů opravených v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
