---
title: NuGet 4.0 RC poznámky k verzi
description: Poznámky k verzi pro NuGet 4.0 RTM včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496608"
---
# <a name="nuget-40-rtm-release-notes"></a>Poznámky k verzi NuGet 4.0 RTM

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) je dodáván s NuGet 4.0, který přidává podporu pro .NET Core, má spoustu oprav kvality a zlepšuje výkon. Tato verze také přináší několik vylepšení, jako je podpora PackageReference, NuGet příkazy jako MSBuild cíle, obnovení balíčku na pozadí a další.

## <a name="known-issues"></a>Známé problémy

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Když máte několik projektů, které se odkazují na jiný projekt v řešení, může selhat obnovení NuGet

#### <a name="issue"></a>Problém

Pokud v řešení máte odkazy na stejný projekt s jinou velikostí písmen nebo s jinými relativními cestami, obnovení NuGet nemusí fungovat. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Alternativní řešení

Opravte velikost písmen nebo relativní cesty tak, aby pro všechny odkazy na projekt byly stejné.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně zkuste znovu smažit `project.lock.json` a obnovit.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>Pokud v projektech .NET Core použijete balíček, který obsahuje sestavení s neplatným podpisem, můžete uvíznout v nekonečné smyčce obnovování

#### <a name="issue"></a>Problém

Když použijete balíček, který obsahuje sestavení s neplatným obsahem, nebo když se verze balíčku nastaví pomocí časovače DateTime, automatické obnovení balíčku běží v nekonečné smyčce. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Pomocí Nástroje pro balení Nuget nelze zobrazit, přidat nebo aktualizovat nástroje DotNetCLITools.

#### <a name="issue"></a>Problém

Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Alternativní řešení

V souboru projektu se musí ručně upravit DotNetCLIToolReferences.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>Když pro projekty nastavíte vlastnost PackageId, obnovení NuGet se nepovede

#### <a name="issue"></a>Problém

Obnovení NuGet v sadě Visual Studio nerespektuje pro projekty .NET Core vlastnost projektů PackageId. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Alternativní řešení

Spusťte obnovení pomocí příkazového řádku.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Pokud váš projekt nemá složku obj, nemusí se povést obnovit balíček

#### <a name="issue"></a>Problém

Pokud se odstraní složka obj, sadě Visual Studio se nepovede obnovit PackageReferences. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Alternativní řešení

Vytvořte složku obj ručně a obnovení by mělo fungovat.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Ruční aktualizace balíčků pomocí Update-Package v konzole může selhat

#### <a name="issue"></a>Problém

Ruční použití Update-Package v konzole funguje pro projekty, které se právě převedly, jenom jednou. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>Když projekt, který cílí na .NET461, odkazuje na jiný projekt, který cílí na .NETStandard, příkaz msbuild /t:restore nebude úspěšný

#### <a name="issue"></a>Problém

Když projekt založený na PackageReference, který cílí na .NET461, odkazuje na jiný projekt založený na PackageReference, který cílí na .NETStandard, příkaz msbuild /t:restore nebude úspěšný.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problémy opravené v časovém rámci NuGet 4.0 RTM

[NuGet 4.0 RC Poznámky k verzi](../release-notes/nuget-4.0-RC.md) - Seznam všech problémů opravených pro NuGet 4.0 RC

### <a name="features"></a>Funkce

- Lokalizovat řetězce v NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget vynutí načtení projektů webových aplikací v režimu LSL - [#4258](https://github.com/NuGet/Home/issues/4258)

- Podpora aplikace AutoReferenced PackageReference pro blokování změn verzí v ui pro balíčky s nainstalovanou sadou SDK – [#4044](https://github.com/NuGet/Home/issues/4044)

- Správně komunikovat PackageSpec.Version pro všechny závislosti projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)

- podpora pro odstranění `.csproj` odkazů z příkazové čáry ( příkazů) - [#4101](https://github.com/NuGet/Home/issues/4101)

- Podpora obnovení pro packagereference projekty (normální a xplat) a zjednodušené zatížení řešení - [#4003](https://github.com/NuGet/Home/issues/4003)

- podpora přidávání odkazů `.csproj` z příkazových řádků - [#3751](https://github.com/NuGet/Home/issues/3751)

- Podpora NuGet obnovení pro `packages.config` zjednodušené zatížení řešení pro nebo `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- contentFiles podpora v nuget generované cíle soubor - [#3683](https://github.com/NuGet/Home/issues/3683)

- Vytvoření mono CI pro nuget.exe ověření na Macu pomocí MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)

- Přesunout NuGet z v2 NuGet.Core závislosti - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Chyby

- NuGet obnovení v sadě Visual Studio nerespektuje PackageId vlastnost projektů – [#4586](https://github.com/NuGet/Home/issues/4586)

- Chyba NuGet ProjectSystemCache při přidávání balíčku v balíčku vsix - [#4545](https://github.com/NuGet/Home/issues/4545)

- Pack vyvolá výjimku, pokud IncludeSource se používá v projektu s více TFM - [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3 havaruje při použití aktualizace ze správy balíčků pro celé řešení - [#4474](https://github.com/NuGet/Home/issues/4474)

- Nelze odinstalovat nově nainstalovaný balíček - [#4435](https://github.com/NuGet/Home/issues/4435)

- Při migraci na PackageRef, hybridní řešení mají podivné chování obnovení - [#4433](https://github.com/NuGet/Home/issues/4433)

- Vytváření brzy po spuštění operace NuGet (instalace, aktualizace, obnovení), může způsobit VS zavěsit - [#4420](https://github.com/NuGet/Home/issues/4420)

- Zablokování ui - zablokování inicializace NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- příkaz add package by měl přidat verzi jako atribut namísto elementu - [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo.sln -- selže, když konfigurace v SLN způsobit duplicitní (ale diff config) projekty v grafu obnovení - [#4316](https://github.com/NuGet/Home/issues/4316)

- Pouze balíčky obsahu - [#3668](https://github.com/NuGet/Home/issues/3668)

- Ve výchozím nastavení odhlásit možnost výběru formátu balíčku - [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: CreateUAP_CSharp_VS.01.1.Vytvořit projekt regresní Duration_TotalElapsedTime o 3,153.570 ms (149.1%). Výchozí hodnota 26129,02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: ManagedLangs_CS_DDRIT.0300.Rebuild řešení regressed Duration_TotalElapsedTime o 1,5 s. Výchozí hodnota 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Nominace se nezdaří v projektech multi-TFM - [#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: WebForms_DDRIT.1200.Zavřít řešení regressed VM_ImagesInMemory_Total_devenv o 3.000 Počet (0,5%). Výchozí hodnota 26123,04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - Pack upozornění při cílení netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)

- PathTooLongException při pokusu o přidání balíčku NuGet do prázdné webové aplikace ASP.NET Core - [#4391](https://github.com/NuGet/Home/issues/4391)

- Balení běží příliš často -- dotnet
  - dotnetcore pack selže s Existuje cyklická závislost v grafu cílové závislosti zahrnující cíl "Pack" - [#4381](https://github.com/NuGet/Home/issues/4381)

- Pack běží příliš často -- Generovat balíček NuGet neobsahuje všechny konfigurace - [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceException přidání nuget s packageref v projektu C++ - [#4378](https://github.com/NuGet/Home/issues/4378)

- Usnadnění přístupu : Předčítání nerozejde políčko a vybere projekty, do kterých chcete balíček nainstalovat – [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 sporadicky selže připojení k vojínům VSO/VSTS - Chyba VS 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles získat výstup do nesprávného umístění, pokud PackagePath určuje cestu jako "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)

- Pack target připojí vlastnost PackageVersion s versionsuffix - [#4324](https://github.com/NuGet/Home/issues/4324)

- Určení cesty balíčku nefunguje s balíčkem dotnet - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet výstupy spoustu upozornění o duplicitní importy během obnovení - [#4304](https://github.com/NuGet/Home/issues/4304)

- Zvolte "NuGet Package Manager Format" dialog vypadá špatně pod tmavým tématem - [#4300](https://github.com/NuGet/Home/issues/4300)

- VS selhání na obnovení sestavení - [#4298](https://github.com/NuGet/Home/issues/4298)

- Visual Studio zablokování, pokud přidáte TFM v targetframeworks, uložit, pak sestavení. 10% času - [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget pack nevydává zprávu o úspěchu při úspěšném balení projektu - [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask selže z důvodu System.IO.Compression 4.1 nebyl nalezen - [#4290](https://github.com/NuGet/Home/issues/4290)

- Pack běží příliš často -- PackTask často selže s konfliktem přístupu k souborům - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet otevře výstupní okno během obnovení pozadí - [#4274](https://github.com/NuGet/Home/issues/4274)

- Eliminovat ServiceProvider jako nebezpečný kódovací vzor (což může způsobit zablokování) - [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf/UIHang - Zlepšit DownloadTimeoutStream čte - [#4266](https://github.com/NuGet/Home/issues/4266)

- Visual Studio zablokování, pokud se pokusíte zavřít projekt před dokončením obnovení NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)

- Problémy s PackTask a balení `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Nelze vyřešit nuget ové balíčky v novém projektu (je třeba restartovat visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] Rozbalovací balíček "Version", který zobrazuje dostupné verze balíčků, se snaží zůstat v synchronizaci s vybraným balíčkem nuGet... - [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client by měl používat CPS JoinableTaskFactory při interakci s CPS, aby se zabránilo zablokování - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 není `.targets` vybalování z balení - [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - Dotnetcore Pack nepodporuje `.csproj`  - titul v [#4150](https://github.com/NuGet/Home/issues/4150)

- Výsledky instalačního balíčku v chybovém dialogu ve VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)

- Aktualizace balíčku pro základní projekt .net se zdá nefunguje, protože uI nezíská aktualizaci CPS z nominovaného. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Zlepšit nevyřešené upozornění na reference - [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore pack - ProjectReference ztratí informace o verzi - [#3953](https://github.com/NuGet/Home/issues/3953)

- Vytvoření aplikace UPW vytvořit projekt & znovu sestavit celkový počet časregresí - [#3873](https://github.com/NuGet/Home/issues/3873)

- Zpráva o úspěšném obnovení se zobrazí i po chybě během obnovení. - [#3799](https://github.com/NuGet/Home/issues/3799)

- znovu publikovat Nuget.CommandLine 3.4.4 na Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- Při migraci se `project.json` `.csproj` projekty změní z na --- obnovení se nezdaří – [#4297](https://github.com/NuGet/Home/issues/4297)

- Obnovení se lhl na nově vytvořený projekt xunit Test - [#4296](https://github.com/NuGet/Home/issues/4296)

- Základní projekty mohou zavěsit, zamknout uI na open - [#4269](https://github.com/NuGet/Home/issues/4269)

- oprava souboru cílů pro úlohy sestavení – [#4267](https://github.com/NuGet/Home/issues/4267)

- Seznam chyb obsahuje chybu po sestavení řešení, které uvolnit odkazovaný projekt - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: Cíl "_GenerateRestoreGraphProjectEntry" neexistuje v projektu. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: nuget manager ui pro řešení dojde k chybě při výběru všech projektů - [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath selže, pokud je koncové lomítko - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: NuGet obnovení dát několik upozornění odkaz na projekt LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)

- Balíček `.csproj` z neobsahuje atribut minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll dodané zpoždění podepsáno v VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: Obnovení se nezdaří pro projekt VS 2015 generovaný pomocí CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Chyby obnovení může zakrýt úplnější chybové zprávy, které sestavení může dát - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Při obnovení balíčků NuGet pro projekt webu došlo k chybě: Hodnota nemůže být null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Migrace vyvolá "Výjimku odkazu na objekt" v NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - dotnetcore pack by měl zabalit nástroje s verzemi, proti kterým byl balíček postaven - [#4063](https://github.com/NuGet/Home/issues/4063)

- Nové obnovení pozadí zapíše milisekundy na stavový řádek, když trvá několik sekund k obnovení - [#4036](https://github.com/NuGet/Home/issues/4036)

- Překlep na nepodařilo vyřešit všechny odkazy na projekt - [#4018](https://github.com/NuGet/Home/issues/4018)

- Povolení pracovních postupů PCM v referenčních scénářích balíčku – [#4016](https://github.com/NuGet/Home/issues/4016)

- Nelze najít nainstalované balíčky v ui správce balíčků - [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - Dotnetcore Pack se nezdaří, když PackagePath je prázdný - [#3993](https://github.com/NuGet/Home/issues/3993)

- Obnovení úlohy se nezdaří ve scénáři pro více uživatelů – [#3897](https://github.com/NuGet/Home/issues/3897)

- Typ obsahu nelze změnit při balení pomocí úlohy sady NuGet Pack – [#3895](https://github.com/NuGet/Home/issues/3895)

- Výchozí kopie ContentFiles jsou nesprávné pro MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)

- Instalace balíčku obnovit dvojité protokoly obnovení balíčků zprávy - [#3785](https://github.com/NuGet/Home/issues/3785)

- Odebrat svodidla - Obnovení části "runtimes" by se mělo vztahovat pouze na aktuální projekt - [#3768](https://github.com/NuGet/Home/issues/3768)

- Pack úkol umístí obsah souborů v 'obsah/' a 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore pack3 dělá extra tag rozdělení - [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore pack: balení projektů s odkazy na balíky vede k upozornění na duplicitní import - [#3665](https://github.com/NuGet/Home/issues/3665)

- Obnovení protokolování ve VS se ne vždy zobrazuje - [#3633](https://github.com/NuGet/Home/issues/3633)

- nuget locals pomáhají text stále zmiňované balíčky cache - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 páry PackageReferences s TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget vybere neočekávanou verzi MSBuild v VS "15" Preview 4 dev. příkazový řádek - [#3408](https://github.com/NuGet/Home/issues/3408)

- Zapsat cíle /rekvizity soubory na neúspěšné obnovení - [#3399](https://github.com/NuGet/Home/issues/3399)

- NuGet během obnovení nerespektuje stejné komituční podložky jako MSBuild při spuštění v příkazovém řádku VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)

- Znovu povolit PackFromProjectWithDevelopmentDependencySet pro VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)

- Blend problémy s NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)

- Integrace 4.0.0.2067 do repo polí CLI a reposad SDK pro odeslání s RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)

- VS přestane reagovat při vytváření nové aplikace Core Console, zavřít řešení, otevřené řešení a zavřít řešení - [#4008](https://github.com/NuGet/Home/issues/4008)

- Bít hang otevření projektu proti d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)

- Oprava dotnet/nuget.exe místní chudou/nápověda - [#3919](https://github.com/NuGet/Home/issues/3919)

- Zkontrolujte PackTask problémy s koncové nebo úvodní prázdné znaky - [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore pack je balení z obj ne bin - [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - Dotnetcore pack vždy zdá nastavit ProjectReference verze 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - Dotnetcore Pack selže s <TargetFramework>  - odkazy na projekt a [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException v aplikaci ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)

- Oříznutí mezer z vlastností MSBuild – [#3819](https://github.com/NuGet/Home/issues/3819)

- Konsolidovat dvě události projektu vyvolané při zatížení projektu - [#3759](https://github.com/NuGet/Home/issues/3759)

- P2P knihovny `project.assets.json` v souboru mají nesprávnou verzi - [#3748](https://github.com/NuGet/Home/issues/3748)

- Obnovení selhání z důvodu nereagujícího kanálu a nedostupného balíčku - [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe může zavěsit na velké množství výstupu chyby MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)

- Obnovení na sestavení pro blend selže poprvé, úspěšné podruhé (VS scénář opraven) - [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>Řadiče domény

- migrovat vsix z v2 vsix na v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet by měl mít mechanismus pro získání cesty k souboru zámku v MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)

- Přidání datových zdrojů sestavení do souboru kontroly kompatibility TFM a souboru datových zdrojů – [#3296](https://github.com/NuGet/Home/issues/3296)

- Definujte nový ProjectCapability "Pack" v cíli pack pro povolení balíček související choré - [#4146](https://github.com/NuGet/Home/issues/4146)

- Spustit balíček jako cíl sestavení příspěvku podmíněno vlastností "GeneratePackageOnBuild" MSBuild - [#4145](https://github.com/NuGet/Home/issues/4145)

- Použití vlastnosti NuGet RestoreProjectStyle k vytvoření konkrétního projektu NuGet - [#4134](https://github.com/NuGet/Home/issues/4134)

- Přizpůsobit obnovení pro změny odkazů na přenositelné projekty – [#4076](https://github.com/NuGet/Home/issues/4076)

- Přidání vlastností NuGet do cílového souboru pro projekty bez UPW - [#4030](https://github.com/NuGet/Home/issues/4030)

- Podpora UWP TargetPlatformVersion - [#3923](https://github.com/NuGet/Home/issues/3923)

- Komunikovat metadata odkazu projektu do systému projektu NuGet - [#3922](https://github.com/NuGet/Home/issues/3922)

- Přidat uI pro režim balení - [#3921](https://github.com/NuGet/Home/issues/3921)

- Starší `.csproj` verze potřebuje NugetTargetMoniker a RuntimeIdentifiers nastavené v proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)

- Instalační balíček se může překrývat s automatickým obnovením - [#3836](https://github.com/NuGet/Home/issues/3836)

- Kontextová nabídka QueryStatus se nestane, když Není načten VSPackage - [#3835](https://github.com/NuGet/Home/issues/3835)

- Obnovení a obnovení sestavení řešení stále zobrazují dialogová okna – [#3789](https://github.com/NuGet/Home/issues/3789)

- Izolovat verzi VSSDK v sestavení řešení NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Odkazy na problémy GitHubu opravené v RTM
[Seznam problémů 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Seznam problémů 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Seznam problémů 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Seznam problémů 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Seznam problémů 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
