---
title: Poznámky k verzi 5.0 preview NuGet
description: Zpráva k vydání verze NuGet 5.0 verzí Preview, včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 57b66b347ac47a3d05907a4bb237002de8981ecc
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196197"
---
# <a name="nuget-50-preview-release-notes"></a>Zpráva k vydání verze NuGet 5.0 ve verzi Preview

## <a name="nuget-50-preview-releases"></a>NuGet 5.0 předběžné verze

* 27. únoru 2010 - [NuGet 5.0 ve verzi Preview 4](#summary-whats-new-in-50-preview-4)
* 13. února 2019 - [NuGet 5.0 ve verzi Preview 3](#summary-whats-new-in-50-preview-3)
* Od 23. května 2019 - [NuGet 5.0 ve verzi Preview 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-4"></a>Shrnutí: Co je nového ve verzi Preview 4 NuGet 5.0

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chyby:**

* NuGet.VisualStudio.IVsPackageInstaller - volání na projektu se žádný balíček odkazuje vždy používá soubor packages.config, i v případě, že ve výchozím nastavení je na PackageReference – [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Package v delisted balíčky přeinstalujete selže ("Nepodařilo se najít balíček"). - [#7268](https://github.com/NuGet/Home/issues/7268)

* Přidat oznámení třetích stran v našem úložišti a VSIX – [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage měli nainstalovat nejnovější verzi, pokud žádné verzi uvedenou - [#7493](https://github.com/NuGet/Home/issues/7493)

* --interaktivní podporu pro dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* Při obnovování se soubor zámku, by neměla být vyvolána NU1603 upozornění. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet by neměl tisk cesta k projektu během obnovení s minimálním protokolováním - [#7647](https://github.com/NuGet/Home/issues/7647)

* --interaktivní podporu pro dotnet odebrat balíček - [#7727](https://github.com/NuGet/Home/issues/7727)

* Přidat zpět NuGet.Packaging.Core s TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache potřebuje kratší cestu fungovat dobře - [#7770](https://github.com/NuGet/Home/issues/7770)

* Dáváte přednost cestu k msbuild zjišťování, pokud uživatel nežádali verze konkrétní msbuild - [#7786](https://github.com/NuGet/Home/issues/7786)

**Chcete:**

* omezit požadavek http na zdroji pomocí souboru NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet zaměřit Net472 (usnadní vyčištění 16,0 sestavení VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Odebrat příkaz OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)

* Zkontrolujte mapování NetCoreApp 3.0 NetStandard 2.1 – [#7762](https://github.com/NuGet/Home/issues/7762)

* Přidání podpory netstandard2.0 NuGet.* balíčků - [#6516](https://github.com/NuGet/Home/issues/6516)


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

**Chcete:**

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

**Chcete:**

* NuGet 5.0 sestavení tak, aby vyžadovala .NET 4.7.2 (prostřednictvím změnit TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData z NuGet.Packaging by měl být veřejným typem. Aktualizujte metadata licence ingestována z spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Odebrat zastaralé nastavení rozhraní API – [#7294](https://github.com/NuGet/Home/issues/7294)

* Alternativní řešení obnovení vypršení časového limitu v systémech s 1 cpu – [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet upřednostňuje ověřování NTLM, i když nejsou přihlašovací údaje do souboru NuGet.config – přidání možností konfigurace k filtrování typů ověřování pro přihlašovací údaje – [#5286](https://github.com/NuGet/Home/issues/5286)

* Povolit EmbedInteropTypes pro PackageReference (odpovídající souboru Packages.Config schopnost) - [#2365](https://github.com/NuGet/Home/issues/2365)

[Seznam všech chyby opravené v této verzi 5.0.0-preview2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>Známé problémy

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)
**Problém** při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu. To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.
**Alternativní řešení** využití záložní složky zakázat nastavením `RestoreAdditionalProjectSources` na hodnotu nothing. `<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.
