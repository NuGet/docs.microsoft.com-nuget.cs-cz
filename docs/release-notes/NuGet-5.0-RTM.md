---
title: Zpráva k vydání verze NuGet 5.0 RTM
description: Zpráva k vydání verze NuGet 5.0, včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921582"
---
# <a name="nuget-50-release-notes"></a>Zpráva k vydání verze 5.0 verze NuGet

Distribuce vozidel NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v rozhraní .NET SDK, pomocí kterých|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>nainstalované s Visual Studio 2019 se sadou .NET Core 

<sup>2</sup>dostupné jako volitelná instalace s Visual Studio 2019 se sadou .NET Core

## <a name="summary-whats-new-in-50"></a>Shrnutí: Co je nového v 5.0

* Podpora pro obnovení [filtrované řešení](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) v aplikaci Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` složka umožňuje balíčky přechodně přispívat cíle/props do projektu hostitel - [#6091](https://github.com/NuGet/Home/issues/6091)
* Lepší podpora pro scénáře PackageReference v rozhraní API vektory IV NuGet – [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` se už nepoužívá - [#7928](https://github.com/NuGet/Home/issues/7928)
* Modul plugin poskytovatele přihlašovacích údajů 1. generace bylo nahrazeno [2. generace](https://aka.ms/nuget-cross-platform-authentication-plugin) a bude brzy přestanou používat - [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chyby**

* Vyhněte se při obnovení NoOp, *. dgspec.json zápis v adresáři obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* Oprávnění u souborů, které vytvářejí ~/.nuget jsou příliš open - [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` nebude fungovat u jiných zdrojů, které je třeba ověřování - [#7605](https://github.com/NuGet/Home/issues/7605)

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

* `nuget.exe /?` zveřejnit msbuild správná verze – [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): Chyba: Nelze najít část cesty "/ tmp/NuGetScratch – v mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* obnovení zbytečně zobrazí obsah odkazovaný balíček v mezipaměti machine - všechny verze [#7639](https://github.com/NuGet/Home/issues/7639)

* Automatické zjišťování MSBuild vždy vybere 16.0 po instalaci a 2019 ve verzi Preview - [#7621](https://github.com/NuGet/Home/issues/7621)

* DotNet seznamu balíčku v řešení výstupy duplicitní položky framework – [#7607](https://github.com/NuGet/Home/issues/7607)

* Výjimka "prázdnou cestu název není platný" při volání IVsPackageInstaller.InstallPackage na staré projekty a balíčky složka neexistuje. - [#5936](https://github.com/NuGet/Home/issues/5936)

* minimální podrobnost nástroje MSBuild/t: Restore by měl být minimálnější - [#4695](https://github.com/NuGet/Home/issues/4695)

* VS pro 16.0 NuGet uživatelského rozhraní obsahuje nečitelná karty z důvodu problémů s barva - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt vyjasnění - [#7629](https://github.com/NuGet/Home/issues/7629)

* Složka globální balíčku obnovení zbytečně zobrazí při pokusu určit typ - [#7596](https://github.com/NuGet/Home/issues/7596)

* Chyby z vynucení soubor zámku se měla zobrazit v okně Seznam chyb - [#7429](https://github.com/NuGet/Home/issues/7429)

* Oprava problémů NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Přizpůsobit jeho instalace aktualizace nástroje MSBuild místo – [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack by měl být vývojovou závislost - [#7249](https://github.com/NuGet/Home/issues/7249)

* Přidat balíček rozšiřovacím bodem pro včetně symboly – ladění [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` mělo zachovat rozsah verzí závislosti v vytvořený soubor nupkg (i když je použita verze s plovoucí desetinnou čárkou) - [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` selže na ověřeného zdroje při individuální konfigurace má také zdroj - [#7209](https://github.com/NuGet/Home/issues/7209)

* Balíček by nemělo omezit sadu BuildActions souborů obsahu – [#7155](https://github.com/NuGet/Home/issues/7155)

* Pomocí ProjectReference, který vyžaduje AssetTargetFallback úspěšné, by měla upozornění. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Zablokování kvůli problémy s tvorbou vláken při volání do prohlášení CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` nepoužívá přihlašovacích údajů z globální konfigurace pro zadaný v místních konfiguračních - zdroj [#6935](https://github.com/NuGet/Home/issues/6935)

* Problémy s tvorbou vláken MEF, že se volá asynchronní kód cesty - [#6771](https://github.com/NuGet/Home/issues/6771)

* Podepisování: hlášená dvakrát a bez zásobník volání – chyba [#6455](https://github.com/NuGet/Home/issues/6455)

* Instalace pomocí nedůvěryhodného podpisový certifikát podepsaný balíček by se zobrazit chyba – [#6318](https://github.com/NuGet/Home/issues/6318)

* Obnovení NuGet nesprávně chová jako operace NoOp při 2 projekty jsou sdílení directory obj – [#6114](https://github.com/NuGet/Home/issues/6114)

* Nelze použít token PAT s `dotnet restore` v Linuxu pomocí balíčků z ověřené informační kanál – [#5651](https://github.com/NuGet/Home/issues/5651)

* DotNet restore nezdaří z důvodu široké zakázané počítač kanál – [#5410](https://github.com/NuGet/Home/issues/5410)

**Chcete**

* Upozornit budoucí odebrání "project.json balíčku dotnet" - [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Přidat upozornění na vyřazení pro modul plug-in credential Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Podpis: Povolené úložiště tak, aby vyžadovala ověření klienta z každého balíčku jako úložiště podepsán--přes RepositorySignatures/5.0.0 prostředek - [#7759](https://github.com/NuGet/Home/issues/7759)

* omezit požadavek http na zdroji pomocí souboru NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet zaměřit Net472 (usnadní vyčištění 16,0 sestavení VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Odebrat příkaz OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)

* Zkontrolujte mapování NetCoreApp 3.0 NetStandard 2.1 – [#7762](https://github.com/NuGet/Home/issues/7762)

* Přidání podpory netstandard2.0 NuGet.* balíčků - [#6516](https://github.com/NuGet/Home/issues/6516)

* Umožnil autorům balíčků k definování sestavení prostředky přenosné chování - [#6091](https://github.com/NuGet/Home/issues/6091)

* Podpora funkce filtru řešení VS 2019. Podporuje také projekt není v řešení nebo uvolněné projekty. Třeba obnovit tak získají kompletní řešení (prostřednictvím rozhraní příkazového řádku nebo VS) first – [#5820](https://github.com/NuGet/Home/issues/5820)

* NuGet 5.0 sestavení tak, aby vyžadovala .NET 4.7.2 (prostřednictvím změnit TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData z NuGet.Packaging by měl být veřejným typem. Aktualizujte metadata licence ingestována z spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Odebrat zastaralé nastavení rozhraní API – [#7294](https://github.com/NuGet/Home/issues/7294)

* Alternativní řešení obnovení vypršení časového limitu v systémech s 1 cpu – [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet upřednostňuje ověřování NTLM, i když nejsou přihlašovací údaje do souboru NuGet.config – přidání možností konfigurace k filtrování typů ověřování pro přihlašovací údaje – [#5286](https://github.com/NuGet/Home/issues/5286)

* Povolit EmbedInteropTypes pro PackageReference (odpovídající souboru Packages.Config schopnost) - [#2365](https://github.com/NuGet/Home/issues/2365)

**[Seznam všech problémů, které jsou opravené v této verzi - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a>Známé problémy

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problém
Při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu. To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.<br>
#### <a name="workaround"></a>Alternativní řešení
Zakázat používání složky pro použití náhradní lokality tak, že nastavíte `RestoreAdditionalProjectSources` Nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Jak balíčky, které se obnoví ze záložní složky budou nyní stáhnout z webu NuGet.org, použijte tento fragment se upozornění.
