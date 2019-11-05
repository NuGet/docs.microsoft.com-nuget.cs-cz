---
title: Poznámky k verzi NuGet 5,0 RTM
description: Poznámky k verzi pro NuGet 5,0, včetně známých problémů, oprav chyb, nových funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 52c71c6fe1a1854d5aed229abf2ce7ddc2685ae9
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611340"
---
# <a name="nuget-50-release-notes"></a>Zpráva k vydání verze NuGet 5,0

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v sadě .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core 

<sup>2</sup> . K dispozici jako volitelná instalace se sadou Visual Studio 2019 s úlohou .NET Core

## <a name="summary-whats-new-in-50"></a>Shrnutí: Novinky v 5,0

* Podpora pro obnovení [filtrovaných řešení](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019) v aplikaci Visual Studio 2019 – [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` složka umožňuje balíčkům průjezdně přispívat cíle/props do projektu hostitele – [#6091](https://github.com/NuGet/Home/issues/6091)
* Lepší podpora scénářů PackageReference v rozhraní NuGet Ideographic API [](https://github.com/NuGet/Home/issues/7005)– #7005 [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` se už nepoužívá – [#7928](https://github.com/NuGet/Home/issues/7928)
* Modul plug-in zprostředkovatele přihlašovacích údajů pro Gen 1 byl nahrazen [2. Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) a bude brzy zastaralý – [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Štěnic**

* Při obnovení NoOp Vyhněte se zápisu do adresáře obj pomocí *. argument dgspec. JSON – [#7854](https://github.com/NuGet/Home/issues/7854)

* Oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená – [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` nefunguje se zdroji, které potřebují auth- [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet. VisualStudio. IVsPackageInstaller-volání na projekt bez odkazů na balíčky vždycky používá Packages. config, i když je výchozí hodnota nastavená na PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005) .

* PMC: Update-Package REINSTALL-Package se nezdařil ("nelze nalézt balíček") na delistované balíčky. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Přidání oznámení třetí strany do našeho úložiště a VSIX – [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet. VisualStudio. IVsPackageInstaller. InstallPackage by měl nainstalovat nejnovější verzi, pokud není zadána žádná verze- [#7493](https://github.com/NuGet/Home/issues/7493)

* --Interaktivní podpora pro příkaz dotnet NuGet push- [#7519](https://github.com/NuGet/Home/issues/7519)

* Při obnovení pomocí souboru zámku by se nemělo vystavit upozornění NU1603. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet by neměl tisknout cestu projektu během obnovení s minimálním protokolováním – [#7647](https://github.com/NuGet/Home/issues/7647)

* --Interaktivní podpora pro příkaz dotnet Remove Package- [#7727](https://github.com/NuGet/Home/issues/7727)

* Přidejte zpět NuGet. balení. Core pomocí TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache potřebuje pro správnou práci [#7770](https://github.com/NuGet/Home/issues/7770) kratší cestu.

* Preferovat cestu pro zjišťování nástroje MSBuild, pokud uživatel nepožádal o konkrétní verzi nástroje MSBuild – [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` by měl vypsat správné verze nástroje MSBuild – [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet. TARGETS (498; 5): Chyba: nepovedlo se najít část cesty/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793) .

* Při obnovení se nenutně vytvoří výčet obsahu všech verzí odkazovaného balíčku v mezipaměti počítače – [#7639](https://github.com/NuGet/Home/issues/7639)

* Automatické zjišťování MSBuild vždy vybere 16,0 po instalaci VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)

* příkaz dotnet list na řešení má na výstupu duplicitní položky pro architekturu – [#7607](https://github.com/NuGet/Home/issues/7607)

* Výjimka "prázdný název cesty není platný" při volání IVsPackageInstaller. InstallPackage u starých projektů a složky balíčků neexistuje. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: Obnova minimální podrobností by měla být větší minimální [#4695](https://github.com/NuGet/Home/issues/4695)

* Uživatelské rozhraní NuGet 16.0 sady VS má nečitelný tabulátory z důvodu problémů s barvou – [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & NuGet. clients. txt License. txt – [#7629](https://github.com/NuGet/Home/issues/7629)

* Při pokusu o určení typu [#7596](https://github.com/NuGet/Home/issues/7596) se nenutně vytvoří výčet složky globálního balíčku.

* Chyby z vynucení zámků souborů by se měly zobrazit v Seznam chyb okně – [#7429](https://github.com/NuGet/Home/issues/7429)

* Oprava NuGet. problémy s konfigurací – [#7326](https://github.com/NuGet/Home/issues/7326)

* Přizpůsobit k aktualizaci MSBuild umístění instalace – [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet. Build. Tasks. Pack by měla být vývojová závislost – [#7249](https://github.com/NuGet/Home/issues/7249)

* Přidat bod rozšíření balíčku pro zahrnutí symbolů ladění – [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` by měl zachovat rozsah verzí závislosti ve vytvořeném nupkg (i když se používá plovoucí verze) – [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` se na ověřeném zdroji nezdařila, pokud má konfigurace na úrovni uživatele také [#7209](https://github.com/NuGet/Home/issues/7209) source-level

* Sada BuildActions by neměla omezovat sadu souborů obsahu – [#7155](https://github.com/NuGet/Home/issues/7155)

* Použití ProjectReference, které vyžaduje, aby AssetTargetFallback bylo úspěšné, by mělo upozorňovat. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Zablokování kvůli problémům s vlákny při volání do CPS (CommonProjectSystem) – [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` nepoužívá přihlašovací údaje z globální konfigurace pro zdroj zadaný v místní konfiguraci. [#6935](https://github.com/NuGet/Home/issues/6935)

* Problémy s vlákny s rozhraním MEF volanou v případě asynchronních cest kódu – [#6771](https://github.com/NuGet/Home/issues/6771)

* Podepisování: Chyba nahlášená dvakrát a bez zásobníku volání- [#6455](https://github.com/NuGet/Home/issues/6455)

* Při instalaci podepsaného balíčku s nedůvěryhodným podpisovým certifikátem by se měla zobrazit chyba [#6318](https://github.com/NuGet/Home/issues/6318)

* Obnovení NuGet je nesprávně NoOpsé, když 2 projekty sdílí adresář obj – [#6114](https://github.com/NuGet/Home/issues/6114)

* Nelze použít PAT s `dotnet restore` v systému Linux s balíčky z ověřeného informačního kanálu – [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore se nepovedlo kvůli zakázanému kanálu pro nejrůznější počítače – [#5410](https://github.com/NuGet/Home/issues/5410)

**Chcete odeslat obecnou**

* Upozornění na budoucí odebrání příkazu "dotnet Pack Project. JSON" – [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Přidání upozornění na zastaralost pro modul plug-in Gen1 přihlašovacích údajů – [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Podepisování: povolené úložiště, které vyžaduje ověření klienta každého balíčku jako úložiště pomocí RepositorySignatures/5.0.0 Resource- [#7759](https://github.com/NuGet/Home/issues/7759)

* Omezte číslo požadavku HTTP na zdroj prostřednictvím NuGet. config- [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet by měl cílit na Net472 (aby bylo možné vyčistit 16,0 sestavení VSIX) – [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Odebrat příkaz OpenPackagePage- [#7384](https://github.com/NuGet/Home/issues/7384)

* Vytvoření mapy NetCoreApp 3,0 na NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)

* Přidat podporu netstandard 2.0 do NuGet. * Packages – [#6516](https://github.com/NuGet/Home/issues/6516)

* Umožňuje autorům balíčků definovat přenosné chování prostředků sestavení – [#6091](https://github.com/NuGet/Home/issues/6091)

* Podporuje funkci filtru řešení VS 2019. Podporuje také projekt, který není v řešení, nebo uvolněné projekty. Je nutné obnovit kompletní řešení (přes CLI nebo VS) první [#5820](https://github.com/NuGet/Home/issues/5820)

* Sestavení NuGet 5,0, která vyžadují .NET 4.7.2 (prostřednictvím TFM změny) – [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData z NuGetu. balení musí být veřejný typ. Aktualizuje metadata licencí z spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Odebrat zastaralá rozhraní API pro nastavení – [#7294](https://github.com/NuGet/Home/issues/7294)

* Časový limit obnovení v systémech s 1 procesorem [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet dává přednost ověřování NTLM i v případě, že v souboru NuGet. config existují přihlašovací údaje, které filtrují typy ověřování pro přihlašovací údaje – [#5286](https://github.com/NuGet/Home/issues/5286)

* Povolit EmbedInteropTypes pro PackageReference (vyhovující možnosti Packages. config) – [#2365](https://github.com/NuGet/Home/issues/2365)

**[Seznam všech problémů opravených v této verzi – 5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Shrnutí: co je nového v 5.0.2

* Zabezpečení (při spuštění prostřednictvím příkazu dotnet. exe nebo mono. exe) – složka obj by měla být vytvořena se správnými oprávněními [#7908](https://github.com/NuGet/Home/issues/7908)

* NuGet. exe Restore on mono/MacOS se nezdařil s vlastními balíčky NuGet. config a `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Známé problémy

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Balíčky v FallbackFolders nainstalované pomocí .NET Core SDK jsou vlastní instalace a ověření podpisu při selhání. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problém
Při použití příkazu dotnet. exe 2. x k obnovení projektu, který má více cílů netcoreapp 1. x a netcoreapp 2. x, se záložní složka považuje za informační kanál souboru. To znamená, že při obnovení NuGet vybere balíček ze záložní složky a pokusí se ho nainstalovat do složky globálních balíčků a provede běžné ověřování podpisů, které selže.<br>
#### <a name="workaround"></a>Alternativní řešení
Zakažte použití záložní složky nastavením `RestoreAdditionalProjectSources` na hodnotu Nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Používejte je opatrně, protože balíčky, které by se obnovily ze záložní složky, se teď stáhnou z NuGet.org.
