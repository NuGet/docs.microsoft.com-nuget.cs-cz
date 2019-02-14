---
title: Poznámky k verzi 5.0 preview NuGet
description: Zpráva k vydání verze NuGet 5.0 verzí Preview, včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247656"
---
# <a name="nuget-50-preview-release-notes"></a>Zpráva k vydání verze NuGet 5.0 ve verzi Preview

## <a name="nuget-50-preview-releases"></a>NuGet 5.0 předběžné verze

* 13. února 2019 - [NuGet 5.0 ve verzi Preview 3](#summary-whats-new-in-50-preview-3)
* Od 23. května 2019 - [NuGet 5.0 ve verzi Preview 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-3"></a>Shrnutí: Co je nového ve verzi Preview 3 NuGet 5.0

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi 

**Chyby:**

* nuget.exe /? zveřejnit msbuild správná verze – [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): Chyba: Nelze najít část cesty "/ tmp/NuGetScratch – v mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* obnovení zbytečně zobrazí obsah odkazovaný balíček v mezipaměti machine - všechny verze [#7639](https://github.com/NuGet/Home/issues/7639)

* Automatické zjišťování MSBuild vždy vybere 16.0 po instalaci a 2019 ve verzi Preview - [#7621](https://github.com/NuGet/Home/issues/7621)

* DotNet seznamu balíčku v řešení výstupy duplicitní položky framework – [#7607](https://github.com/NuGet/Home/issues/7607)

* Výjimka "prázdnou cestu název není platný" při volání IVsPackageInstaller.InstallPackage na staré projekty a balíčky složka neexistuje. - [#5936](https://github.com/NuGet/Home/issues/5936)

* minimální podrobnost nástroje MSBuild/t: Restore by měl být minimálnější - [#4695](https://github.com/NuGet/Home/issues/4695)

**Chcete**

* Umožnil autorům balíčků k definování sestavení prostředky přenosné chování - [#6091](https://github.com/NuGet/Home/issues/6091)

* Povolit obnovení v sadě Visual Studio úspěšná, když projekt není součástí řešení nebo není načten, ale se dříve obnovila - [#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>Shrnutí: Co je nového ve verzi 5.0 Preview 2

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chyby:**

* VS pro 16.0 NuGet uživatelského rozhraní obsahuje nečitelná karty z důvodu problémů s barva - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt vyjasnění - [#7629](https://github.com/NuGet/Home/issues/7629)

* Složka globální balíčku obnovení zbytečně zobrazí při pokusu určit typ - [#7596](https://github.com/NuGet/Home/issues/7596)

* Chyby z vynucení soubor zámku se měla zobrazit v okně Seznam chyb - [#7429](https://github.com/NuGet/Home/issues/7429)

* Oprava problémů NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Přizpůsobení nástroje MSBuild aktualizace v umístění instalace.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack by měl být vývojovou závislost - [#7249](https://github.com/NuGet/Home/issues/7249)

* Přidat balíček rozšiřovacím bodem pro včetně symboly – ladění [#7234](https://github.com/NuGet/Home/issues/7234)

* balíčku DotNet mělo zachovat rozsah verzí závislosti v vytvořený soubor nupkg. (i když je použita verze s plovoucí desetinnou čárkou) - [#7232](https://github.com/NuGet/Home/issues/7232)

* DotNet restore selže ověřeného zdroje, pokud uživatelské úrovni konfigurace má také zdroj - [#7209](https://github.com/NuGet/Home/issues/7209)

* Balíček by nemělo omezit sadu BuildActions souborů obsahu – [#7155](https://github.com/NuGet/Home/issues/7155)

* Pomocí projectreference, který vyžaduje AssetTargetFallback úspěšné, by měla upozornění. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Zablokování kvůli problémy s tvorbou vláken při volání do prohlášení CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* příkaz DotNet add balíček nebude používat přihlašovací údaje z globální konfigurace zdroje zadaného v místním souboru config - [#6935](https://github.com/NuGet/Home/issues/6935)

* Práce s vlákny problémy s MEF se volalo asynchronní cest v kódu – [#6771](https://github.com/NuGet/Home/issues/6771)

* Podepisování: hlášená dvakrát a bez zásobník volání – chyba [#6455](https://github.com/NuGet/Home/issues/6455)

* Instalace pomocí nedůvěryhodného podpisový certifikát podepsaný balíček by se zobrazit chyba – [#6318](https://github.com/NuGet/Home/issues/6318)

* Obnovení NuGet nesprávně chová jako operace NoOp při 2 projekty jsou sdílení directory obj – [#6114](https://github.com/NuGet/Home/issues/6114)

* Nelze použít token PAT s dotnet restore v Linuxu pomocí balíčků z ověřené informační kanál – [#5651](https://github.com/NuGet/Home/issues/5651)

* DotNet restore nezdaří z důvodu široké zakázané počítač kanál – [#5410](https://github.com/NuGet/Home/issues/5410)

**Chcete**

* NuGet 5.0 sestavení tak, aby vyžadovala .NET 4.7.2 (prostřednictvím změnit TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData z NuGet.Packaging by měl být veřejným typem. Aktualizujte metadata licence ingestována z spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Odebrat zastaralé nastavení rozhraní API – [#7294](https://github.com/NuGet/Home/issues/7294)

* Alternativní řešení obnovení vypršení časového limitu v systémech s 1 cpu – [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet upřednostňuje ověřování NTLM, i když nejsou přihlašovací údaje do souboru NuGet.config – přidání možností konfigurace k filtrování typů ověřování pro přihlašovací údaje – [#5286](https://github.com/NuGet/Home/issues/5286)

* Povolit EmbedInteropTypes pro PackageReference (odpovídající souboru Packages.Config schopnost) - [#2365](https://github.com/NuGet/Home/issues/2365)

[Seznam všech chyby opravené v této verzi 5.0.0-preview2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>Známé problémy

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>DotNet nuget příkaz push--interaktivní vrátí chybu v systému Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)
**Problém** `--interactive` argument není předávaná pomocí rozhraní příkazového řádku dotnet, jejichž výsledkem chyba `error: Missing value for option 'interactive'` 
 **řešení** spuštění další příkaz dotnet pomocí interaktivní možnosti, jako je například `dotnet restore --interactive` a provést ověření. Ověřování potom může do mezipaměti podle poskytovatele přihlašovacích údajů. Potom spusťte `dotnet nuget push`.

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)
**Problém** při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu. To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.
**Alternativní řešení** využití záložní složky zakázat nastavením `RestoreAdditionalProjectSources` na hodnotu nothing. `<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.
