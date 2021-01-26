---
title: Poznámky k verzi NuGet 4,0 RTM
description: Poznámky k verzi pro NuGet 4,0 RTM, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c3ec5c20e5175edd315de20ca98c7a106c51809e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776275"
---
# <a name="nuget-40-rtm-release-notes"></a>Poznámky k verzi NuGet 4,0 RTM

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) obsahuje NuGet 4,0, který přidává podporu pro .NET Core, má spoustu kvalitních oprav a zvyšuje výkon. Tato verze také přináší několik vylepšení, jako je podpora PackageReference, příkazů NuGet jako cílů MSBuild, obnovení balíčku na pozadí a další.

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

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně zkuste `project.lock.json` obnovení a znovu obnovit.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>Pokud v projektech .NET Core použijete balíček, který obsahuje sestavení s neplatným podpisem, můžete uvíznout v nekonečné smyčce obnovování

#### <a name="issue"></a>Problém

Když použijete balíček, který obsahuje sestavení s neplatným obsahem, nebo když se verze balíčku nastaví pomocí časovače DateTime, automatické obnovení balíčku běží v nekonečné smyčce. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Pomocí Správce balíčků NuGet nemůžete zobrazit, přidat ani aktualizovat DotNetCLITools.

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

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problémy opravené v časovém rámci NuGet 4,0 RTM

[Poznámky k verzi nuget 4,0 RC](../release-notes/nuget-4.0-RC.md) – seznam všech problémů opravených pro NUGET 4,0 RC

### <a name="features"></a>Funkce

- Lokalizace řetězců v NuGet. Core. sln – [#2041](https://github.com/NuGet/Home/issues/2041)

- NuGet nutí načíst projekty webové aplikace v režimu LSL – [#4258](https://github.com/NuGet/Home/issues/4258)

- Podpora autoreference PackageReference k blokování změn verze v uživatelském rozhraní pro balíčky nainstalované sadou SDK – [#4044](https://github.com/NuGet/Home/issues/4044)

- Správně komunikovat PackageSpec. Version pro všechny závislosti projektu (PackageRef) – [#3902](https://github.com/NuGet/Home/issues/3902)

- Podpora pro odebrání odkazů na `.csproj` z příkazového řádku (s) – [#4101](https://github.com/NuGet/Home/issues/4101)

- Podpora obnovení pro projekty PackageReference (normální a xplat) a zjednodušené načtení řešení – [#4003](https://github.com/NuGet/Home/issues/4003)

- Podpora přidávání odkazů do `.csproj` příkazového řádku (CommandLine) – [#3751](https://github.com/NuGet/Home/issues/3751)

- Podpora obnovení NuGet pro zjednodušené načtení řešení pro `packages.config` nebo `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- Podpora contentFiles v souboru NuGet generovaných cíli – [#3683](https://github.com/NuGet/Home/issues/3683)

- Vytvoření mono CI pro nuget.exe ověřování na Macu pomocí MSBuild- [#3646](https://github.com/NuGet/Home/issues/3646)

- Přesune NuGet z verze V2 NuGet. základní závislosti – [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Chyby

- Obnovení NuGet v aplikaci Visual Studio nerespektuje vlastnost PackageId projektů – [#4586](https://github.com/NuGet/Home/issues/4586)

- Při přidávání balíčku do balíčku VSIX došlo k chybě ProjectSystemCache NuGet – [#4545](https://github.com/NuGet/Home/issues/4545)

- Sada vyvolá výjimku, pokud se v projektu používá IncludeSource s více TFM- [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3 selhání při použití aktualizace ze správy balíčků na úrovni řešení – [#4474](https://github.com/NuGet/Home/issues/4474)

- Nelze odinstalovat nově nainstalovaný balíček – [#4435](https://github.com/NuGet/Home/issues/4435)

- Při migraci na PackageRef mají hybridní řešení nezvyklé chování při obnovení – [#4433](https://github.com/NuGet/Home/issues/4433)

- Sestavování po spuštění operace NuGet (instalace, aktualizace, obnovení) může způsobit, že systém přestane reagovat [#4420](https://github.com/NuGet/Home/issues/4420)

- Uživatelské rozhraní přestane zablokovat inicializaci NuGet. SolutionRestoreManager. RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- příkaz pro přidání balíčku by měl přidat verzi jako atribut namísto prvku [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo. sln – neúspěšná, když konfigurace v SLN způsobují duplicitní projekty (ale rozdílové konfigurace) v grafu obnovit – [#4316](https://github.com/NuGet/Home/issues/4316)

- Balíčky pouze s obsahem – [#3668](https://github.com/NuGet/Home/issues/3668)

- Ve výchozím nastavení se z možnosti selektor formátu balíčku odsouhlasí – [#4468](https://github.com/NuGet/Home/issues/4468)

- Výkon: CreateUAP_CSharp_VS. 01.1. Create Project Duration_TotalElapsedTime by 3 153,570 MS (149,1%). Směrný plán 26129,02 – [#4452](https://github.com/NuGet/Home/issues/4452)

- Výkon: ManagedLangs_CS_DDRIT .0300. znovu sestavit řešení Duration_TotalElapsedTime o 1,5 sec. Směrný plán 26105 – [#4441](https://github.com/NuGet/Home/issues/4441)

- V projektech s více TFM se nezdařila její jmenování – [#4419](https://github.com/NuGet/Home/issues/4419)

- Výkon: WebForms_DDRIT .1200. zavřít řešení VM_ImagesInMemory_Total_devenv podle 3,000ho počtu (0,5%). Směrný plán 26123,04 – [#4408](https://github.com/NuGet/Home/issues/4408)

- Upozornění vsfeedback-Pack při cílení na netcoreapp 1.1 – [#4397](https://github.com/NuGet/Home/issues/4397)

- PathTooLongException při pokusu o přidání balíčku NuGet do prázdné ASP.NET Core webové aplikace – [#4391](https://github.com/NuGet/Home/issues/4391)

- Sada se spouští příliš často – dotnet.
  - sada dotnetcore Pack se nezdařila s cyklickými závislostmi v grafu závislosti cíle zahrnující cílovou sadu "Pack" – [#4381](https://github.com/NuGet/Home/issues/4381)

- Sada se spouští příliš často – vygeneruje se balíček NuGet nezahrnuje všechny konfigurace – [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceException přidání nugetu s packageref v projektu C++ – [#4378](https://github.com/NuGet/Home/issues/4378)

- Usnadnění: Předčítání nepopisuje políčko pro výběr projektů pro instalaci balíčku do [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 se neúspěšně připojuje k kanálům VSO/VSTS – VS chyba 365798- [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles načíst výstup do špatného umístění, pokud PackagePath Určuje cestu jako "contentFiles" – [#4348](https://github.com/NuGet/Home/issues/4348)

- Cílová sada připojí vlastnost PackageVersion pomocí VersionSuffix- [#4324](https://github.com/NuGet/Home/issues/4324)

- Zadání cesty k balíčku nefunguje se sadou dotnet Pack – [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet výstupuje spoustu upozornění o duplicitních importech během obnovení- [#4304](https://github.com/NuGet/Home/issues/4304)

- Volba "formát správce balíčků NuGet" v dialogovém okně vypadá špatný motiv – [#4300](https://github.com/NuGet/Home/issues/4300)

- Chyba VS při obnovení buildu – [#4298](https://github.com/NuGet/Home/issues/4298)

- Zablokování sady Visual Studio Pokud přidáte TFM v targetFramework, uložte a pak sestavíte. 10% času – [#4295](https://github.com/NuGet/Home/issues/4295)

- sada NuGet Pack neúspěšně zavedla výstup zprávy o úspěchu při vybalení projektu [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask se nepovedlo kvůli chybě System. IO. Compression 4,1 – [#4290](https://github.com/NuGet/Home/issues/4290)

- Sada se spouští příliš často – PackTask se často nedaří a je to konflikt přístupu k souboru – [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet otevře okno výstup během obnovení na pozadí – [#4274](https://github.com/NuGet/Home/issues/4274)

- Eliminujte ServiceProvider jako nebezpečný vzor kódování (což může způsobit zablokování) – [#4268](https://github.com/NuGet/Home/issues/4268)

- Výkon a UIHang – zlepšení čtení DownloadTimeoutStream – [#4266](https://github.com/NuGet/Home/issues/4266)

- Zablokování sady Visual Studio při pokusu zavřít projekt před dokončením obnovení NuGet – [#4257](https://github.com/NuGet/Home/issues/4257)

- Problémy s PackTask a balícími `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Balíčky NuGet se nedají přeložit v novém projektu (musí se restartovat Visual Studio) – [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] Rozevírací seznam verze, který zobrazuje dostupné verze balíčku, potýká a zůstane v synchronizaci s vybraným balíčkem nuGet...- [#4198](https://github.com/NuGet/Home/issues/4198)

- NuGet. klient by měl používat JoinableTaskFactory CPS při interakci se serverem CPS, aby se zabránilo zablokování – [#4185](https://github.com/NuGet/Home/issues/4185)

- 3.5.0 NuGet se nebalí `.targets` z balíčku – [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - dotnetcore Pack nepodporuje nadpis v `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package má za následek chybovou dialog v VS2017 RC – [#4127](https://github.com/NuGet/Home/issues/4127)

- Aktualizace balíčku pro projekt .NET Core vypadá jako nefunguje, protože uživatelské rozhraní nezíská aktualizaci CPS z jeho jmenovaného. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Vylepšit nevyřešené upozornění na odkaz – [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore Pack – ProjectReference ztratí informace o verzi – [#3953](https://github.com/NuGet/Home/issues/3953)

- Vytvoření aplikace UWP vytvoření projektu & opětovného sestavení celkových uplynulých časových regresí – [#3873](https://github.com/NuGet/Home/issues/3873)

- Zpráva o úspěšném obnovení se zobrazí i po chybě při obnovení. - [#3799](https://github.com/NuGet/Home/issues/3799)

- Opětovné publikování NuGet. CommandLine 3.4.4 do Nuget.org- [#2931](https://github.com/NuGet/Home/issues/2931)

- Při migraci se projekty mění z `project.json` na a---obnovení se nepovede. `.csproj` [#4297](https://github.com/NuGet/Home/issues/4297)

- Neúspěšné obnovení při nově vytvořeném projektu xUnit test- [#4296](https://github.com/NuGet/Home/issues/4296)

- Základní projekty můžou zablokovat, uzamknout uživatelské rozhraní při otevření [#4269](https://github.com/NuGet/Home/issues/4269)

- Oprava souboru cílů pro úlohy sestavení – [#4267](https://github.com/NuGet/Home/issues/4267)

- Seznam chyb obsahuje chybu po sestavení řešení, které uvolní odkazovaný projekt – [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: cíl "_GenerateRestoreGraphProjectEntry" v projektu neexistuje. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: uživatelské rozhraní správce NuGet pro zhroucení řešení při výběru všech projektů – [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe MSBuildPath v případě, že dojde k koncovému lomítku – [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: obnovení NuGetu udělit několik upozornění na projekt pro projekt LinqToTwitter – [#4156](https://github.com/NuGet/Home/issues/4156)

- Sada `.csproj` nezahrnuje atribut minClientVersion- [#4135](https://github.com/NuGet/Home/issues/4135) .

- NuGet.Build.Tasks.Pack.dll zaslané zpoždění podepsané v VS2017 (d15rel 26014,00) – [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: obnovení selhalo pro projekt VS 2015 generovaný s CMake 3.7.1- [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Restore Errors může skrývat více kompletních chybových zpráv, které může sestavení poskytnout – [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Při obnovování balíčků NuGet pro webový projekt došlo k chybě: hodnota nemůže být null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Migrace vyvolá výjimku "Object Reference Exception" v NuGet. PackageManagement. VisualStudio. SolutionRestoreWorker- [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - sada dotnetcore Pack by měla zabalit nástroje s verzemi, na které byl balíček sestaven – [#4063](https://github.com/NuGet/Home/issues/4063)

- Nové obnovení na pozadí: zapisuje milisekundy do stavového řádku, když trvá obnovení s [#4036](https://github.com/NuGet/Home/issues/4036)

- Překlepy při pokusu o vyřešení všech odkazů na projekt – [#4018](https://github.com/NuGet/Home/issues/4018)

- Povolit pracovní postupy PCM v referenčních scénářích balíčku – [#4016](https://github.com/NuGet/Home/issues/4016)

- Nelze nalézt nainstalované balíčky v uživatelském rozhraní Správce balíčků – [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - sada dotnetcore Pack se nezdařila, pokud je PackagePath prázdné – [#3993](https://github.com/NuGet/Home/issues/3993)

- Úloha obnovení se ve scénáři více uživatelů nezdařila – [#3897](https://github.com/NuGet/Home/issues/3897)

- Nelze změnit typ obsahu při balení pomocí úlohy NuGet Pack Task- [#3895](https://github.com/NuGet/Home/issues/3895)

- Výchozí kopie ContentFiles nejsou správné pro MsBuild/t: Pack- [#3894](https://github.com/NuGet/Home/issues/3894)

- Nainstalovat balíček obnovení dvojitým protokolem zpráva obnovení balíčků – [#3785](https://github.com/NuGet/Home/issues/3785)

- Remove Guardrails – obnovení oddílu runtimes by mělo platit jenom pro aktuální projekt – [#3768](https://github.com/NuGet/Home/issues/3768)

- Úloha balíčku vloží soubory obsahu v obsahu/a contentFiles/- [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore Pack3 má dodatečné rozdělení značek – [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore Pack: při balení projektů s odkazy na balíčky dojde k duplicitnímu upozornění importu – [#3665](https://github.com/NuGet/Home/issues/3665)

- Obnovit protokolování VS nezobrazuje se vždy [#3633](https://github.com/NuGet/Home/issues/3633)

- text v nápovědě pro místní prostředí NuGet se pořád zmiňují balíčky v mezipaměti – [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 Couples PackageReferences s TargetFramework. - [#3504](https://github.com/NuGet/Home/issues/3504)

- NuGet vybere neočekávanou verzi nástroje MSBuild v sadě VS "15" Preview 4 – vývoj. příkazový řádek – [#3408](https://github.com/NuGet/Home/issues/3408)

- Při neúspěšném obnovení se zapisují soubory targets/props- [#3399](https://github.com/NuGet/Home/issues/3399)

- NuGet během obnovování nerespektuje stejné překrytí popisovačem, když běží v sadě VS 15 Command Prompt – [#3387](https://github.com/NuGet/Home/issues/3387)

- Opětovné povolení PackFromProjectWithDevelopmentDependencySet pro VS15- [#3272](https://github.com/NuGet/Home/issues/3272)

- Problémy s Blendem s využitím NuGet – [#4043](https://github.com/NuGet/Home/issues/4043)

- Integrace 4.0.0.2067 do úložišť CLI a sady SDK k dodávání pomocí RC2- [#4029](https://github.com/NuGet/Home/issues/4029)

- VS přestane reagovat při vytváření nové základní aplikace konzoly, uzavření řešení, otevření řešení a zavření řešení – [#4008](https://github.com/NuGet/Home/issues/4008)

- Zablokování zablokuje otevírání projektu proti d15prerel. 25916.01- [#3982](https://github.com/NuGet/Home/issues/3982)

- Oprava příkazu dotnet/nuget.exeho dokumentu nebo zprávy o nápovědě – [#3919](https://github.com/NuGet/Home/issues/3919)

- Prozkoumejte PackTask a vyhledejte problémy s koncovým nebo úvodním [#3906](https://github.com/NuGet/Home/issues/3906) prázdných znaků.

- dotnet
  - dotnetcore Pack je balení z obj, nikoli z přihrádky – [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - sada dotnetcore Pack vždy ukazuje, jak nastavit verzi ProjectReference na 1.0.0- [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - sada dotnetcore Pack se nezdařila s odkazy na projekt a <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException v ProjectSystemCache. TryGetProjectNameByShortName- [#3861](https://github.com/NuGet/Home/issues/3861)

- Oříznout prázdné znaky z vlastností MSBuild – [#3819](https://github.com/NuGet/Home/issues/3819)

- Konsolidovat dvě události projektu, které byly vyvolány při načtení projektu – [#3759](https://github.com/NuGet/Home/issues/3759)

- Knihovny P2P v `project.assets.json` souboru mají nesprávnou verzi [#3748](https://github.com/NuGet/Home/issues/3748)

- Selhání obnovení kvůli nereagující kanálu a nedostupnému balíčku- [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe může reagovat na velké množství chybového výstupu nástroje MSBuild – [#3572](https://github.com/NuGet/Home/issues/3572)

- Obnovení na buildu pro Blend selže poprvé, úspěšná podruhé (v případě pevného scénáře VS) – [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>Chcete odeslat obecnou

- migrace souboru VSIX z VSIX VSIX na V3 VSIX – [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet by měl mít mechanismus pro získání cesty k souboru zámku v MSBuild- [#3351](https://github.com/NuGet/Home/issues/3351)

- Přidat assety sestavení do TFM kontroly kompatibility a souboru prostředků Asset- [#3296](https://github.com/NuGet/Home/issues/3296)

- Definování nové ProjectCapability "balíčku" v cílech balíčku pro povolení funkcí souvisejících s balíčky – [#4146](https://github.com/NuGet/Home/issues/4146)

- Spustit balíček jako cíl po sestavení s podmínkou pro vlastnost MSBuild GeneratePackageOnBuild- [#4145](https://github.com/NuGet/Home/issues/4145)

- K vytvoření konkrétního projektu NuGet použijte RestoreProjectStyle vlastnosti NuGet – [#4134](https://github.com/NuGet/Home/issues/4134)

- Přizpůsobit obnovení pro změny odkazů na přenositelné projekty – [#4076](https://github.com/NuGet/Home/issues/4076)

- Přidání vlastností NuGet do cílového souboru pro projekty jiné než UWP – [#4030](https://github.com/NuGet/Home/issues/4030)

- Podpora UWP TargetPlatformVersion – [#3923](https://github.com/NuGet/Home/issues/3923)

- Oznamovat metadata odkazů projektu na systém projektů NuGet – [#3922](https://github.com/NuGet/Home/issues/3922)

- Přidat uživatelské rozhraní pro režim balení – [#3921](https://github.com/NuGet/Home/issues/3921)

- Starší verze `.csproj` potřebuje NugetTargetMoniker a RuntimeIdentifiers nastavené v proj/targets – [#3854](https://github.com/NuGet/Home/issues/3854)

- Instalační balíček se může překrývat s automatickým obnovením – [#3836](https://github.com/NuGet/Home/issues/3836)

- QueryStatus místní nabídky se nestane, když VSPackage není načten – [#3835](https://github.com/NuGet/Home/issues/3835)

- Obnovení řešení a obnovení buildu se pořád zobrazují dialogy – [#3789](https://github.com/NuGet/Home/issues/3789)

- Izolace verze VSSDK v NuGet. buildy řešení klientů – [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Odkazy na problémy GitHubu opravené ve verzi RTM
[Seznam problémů 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Seznam problémů 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Seznam problémů 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Seznam problémů 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Seznam problémů 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
