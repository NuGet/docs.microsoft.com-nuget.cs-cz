---
title: Poznámky k verzi RC NuGet 4.0 | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Poznámky k verzi pro NuGet 4.0 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
keywords: NuGet 4.0 RTM poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 75ce757c209afd74f8d4f45d58d4e13a23b3b743
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-40-rtm-release-notes"></a>Poznámky k verzi 4.0 RTM NuGet

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s 4.0 NuGet, který přidává podporu pro .NET Core, má spoustu kvalita opravy a zvyšuje výkon. Tato verze přináší také několik vylepšení, jako je podpora pro PackageReference, příkazy pro balíčky NuGet jako MSBuild cíle, pozadí balíček obnovení a další.

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

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně, zkuste odstranit `project.lock.json` a opakujte obnovení.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>Pokud v projektech .NET Core použijete balíček, který obsahuje sestavení s neplatným podpisem, můžete uvíznout v nekonečné smyčce obnovování

#### <a name="issue"></a>Problém

Když použijete balíček, který obsahuje sestavení s neplatným obsahem, nebo když se verze balíčku nastaví pomocí časovače DateTime, automatické obnovení balíčku běží v nekonečné smyčce. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nelze zobrazit, přidat nebo aktualizovat DotNetCLITools pomocí Správce balíčků Nuget

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

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>Když projekt, který cílí na .NET461, odkazuje na jiný projekt, který cílí na .NETStandard, příkaz msbuild /t:restore nebude úspěšný

#### <a name="issue"></a>Problém

Když projekt založený na PackageReference, který cílí na .NET461, odkazuje na jiný projekt založený na PackageReference, který cílí na .NETStandard, příkaz msbuild /t:restore nebude úspěšný.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Chyby v období NuGet 4.0 RTM

[Poznámky k verzi RC 4.0 NuGet](../release-notes/nuget-4.0-RC.md) -jsou uvedené všechny problémy opravě pro NuGet 4.0 RC

### <a name="features"></a>Funkce

- Lokalizace řetězců v NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)

- Vynutí Nuget načíst projekty webových aplikací v režimu dolní limit - [#4258](https://github.com/NuGet/Home/issues/4258)

- Podpora AutoReferenced PackageReference bloku verzi změny v uživatelském rozhraní pro balíčky "sdk nainstalován" - [#4044](https://github.com/NuGet/Home/issues/4044)

- Správně komunikovat PackageSpec.Version pro všechny závislosti projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)

- Podpora pro odebírání odkazů do `.csproj` z commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)

- Podpora obnovení pro projekty PackageReference (normální a xplat) a zatížení řešení Lightweight - [#4003](https://github.com/NuGet/Home/issues/4003)

- Podpora pro přidání odkazů do `.csproj` z commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)

- Podpora pro zatížení Lightweight řešení pro obnovení NuGet `packages.config` nebo `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- contentFiles podporují v souboru cíle nuget generované - [#3683](https://github.com/NuGet/Home/issues/3683)

- Vytvoření Mono CI pro ověření nuget.exe v systému Mac pomocí nástroje MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)

- Přesunout z v2 NuGet.Core závislosti - NuGet [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Chyby

- Obnovení NuGet v sadě Visual Studio nerespektuje PackageId vlastnost projekty - [#4586](https://github.com/NuGet/Home/issues/4586)

- Chyba NuGet ProjectSystemCache při přidání balíčku do balíčku vsix - [#4545](https://github.com/NuGet/Home/issues/4545)

- Pack vyvolá výjimku, pokud se používá v projektu s více TFMs - IncludeSource [#4536](https://github.com/NuGet/Home/issues/4536)

- Balíček správy - VS 2017 RC3 havárií na použití aktualizace z celé řešení [#4474](https://github.com/NuGet/Home/issues/4474)

- Nelze odinstalovat, nově nainstalovaný balíček - [#4435](https://github.com/NuGet/Home/issues/4435)

- Při migraci PackageRef, hybridní řešení mají obnovení neobvyklé chování - [#4433](https://github.com/NuGet/Home/issues/4433)

- Vytváření krátce po spuštění NuGet operace (instalace, update, obnovení), může způsobit VS k zablokování - [#4420](https://github.com/NuGet/Home/issues/4420)

- Zablokování uživatelského rozhraní – zablokování inicializace NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- Přidejte balíček příkaz má přidat verze jako atribut místo element - [#4325](https://github.com/NuGet/Home/issues/4325)

- Obnovení DotNet foo.sln – selže, pokud konfigurace v SLN – způsobit duplicitní (ale konfigurace rozdílové) projekty v grafu obnovení – [#4316](https://github.com/NuGet/Home/issues/4316)

- Obsahu pouze balíčky - [#3668](https://github.com/NuGet/Home/issues/3668)

- Ve výchozím nastavení vyjádření výslovného nesouhlasu s možností pro výběr formátu balíček - [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: CreateUAP_CSharp_VS.01.1.Create projekt znovu zahrnut Duration_TotalElapsedTime podle 3,153.570 ms (149.1 %). Základní 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: ManagedLangs_CS_DDRIT.0300.Rebuild řešení který poklesl Duration_TotalElapsedTime podle 1,5 sekundu. Základní 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Navrženém selže v projektech více TFM - [#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: WebForms_DDRIT.1200.Close řešení který poklesl VM_ImagesInMemory_Total_devenv podle počtu 3.000 (0,5 %). Základní 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - Pack upozornění při cílení na netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)

- PathTooLongException při pokusu o přidání balíčku NuGet do prázdné webové aplikace ASP.NET Core - [#4391](https://github.com/NuGet/Home/issues/4391)

- Pack spouští příliš často – dotnet pack nepodaří a dojde k dispozici je cyklická závislost cílové závislosti grafu zahrnující cílové "Pack" - [#4381](https://github.com/NuGet/Home/issues/4381)

- Pack spouští příliš často – balíček NuGet generovat neobsahuje všechny konfigurace - [#4380](https://github.com/NuGet/Home/issues/4380)

- Přidání nuget NullReferenceException s packageref v projektu C++ - [#4378](https://github.com/NuGet/Home/issues/4378)

- Usnadnění: Předčítání není mluvený komentář zaškrtávací políčko Vybrat projekty, které chcete nainstalovat balíček - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 k selhání připojení k VSO nebo služby VSTS kanály - 365798 chyb VS - [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles získat výstup do nesprávného umístění, pokud PackagePath Určuje cestu jako "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)

- Cíl Pack připojí PackageVersion vlastnost s VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)

- Zadat cestu k balíčku nefunguje s aktualizací Service pack dotnet - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet výstupy bunch upozornění o duplicitní importy během obnovení - [#4304](https://github.com/NuGet/Home/issues/4304)

- Zvolte vypadá chybný pod tmavý motiv – dialogové okno "Správce balíčků NuGet Format" [#4300](https://github.com/NuGet/Home/issues/4300)

- VS dojít k chybě při obnovení sestavení - [#4298](https://github.com/NuGet/Home/issues/4298)

- Visual Studio zablokování Pokud přidáte TFM v targetframeworks, uložte a sestavení. 10 % času - [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget pack není výstup zprávu o úspěchu na balení projektu úspěšně - [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask nezdaří z důvodu System.IO.Compression 4.1 nebude nalezen – [#4290](https://github.com/NuGet/Home/issues/4290)

- Pack spouští příliš často – PackTask často selže s konfliktu přístupu k souboru - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet otevře ve výstupním okně během obnovení pozadí - [#4274](https://github.com/NuGet/Home/issues/4274)

- Vyloučit položku ServiceProvider jako nebezpečná kódování vzor, (který může způsobit zablokování) - [#4268](https://github.com/NuGet/Home/issues/4268)

- Výkonu nebo UIHang - zlepšení DownloadTimeoutStream čtení - [#4266](https://github.com/NuGet/Home/issues/4266)

- Visual Studio zablokování, když zkusíte zavřít projekt dokončil obnovení NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)

- Problémy s PackTask a okolních `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Nelze vyřešit balíčků nuget v novém projektu (vyžaduje restartování sady visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] "Verze" rozevírací nabídky, které zobrazuje verze balíčku k dispozici, prohry zůstane synchronizovaná s balíček vybrané nuGet... - [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client měli použít třída JoinableTaskFactory CPS při interakci s CPS zablokování - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 není rozbalování `.targets` z balíčku - [#4171](https://github.com/NuGet/Home/issues/4171)

- DotNet pack nepodporuje název v `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package výsledkem dialogové okno chyby v VS2017 RC – [#4127](https://github.com/NuGet/Home/issues/4127)

- Aktualizace balíčku pro rozhraní .net core projekt se nebude fungovat, jako uživatelské rozhraní není sám aktualizace prohlášení CPS nominate. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Zlepšení nerozpoznaný odkaz upozornění - [#3955](https://github.com/NuGet/Home/issues/3955)

- DotNet pack - ProjectReference ztratí informace o verzi - [#3953](https://github.com/NuGet/Home/issues/3953)

- Vytvoření aplikace pro UPW & Vytvořit projekt znovu sestavit Celkem uběhlý čas regresí - [#3873](https://github.com/NuGet/Home/issues/3873)

- Úspěšné obnovení zpráva se zobrazí i po chybě. během obnovení. - [#3799](https://github.com/NuGet/Home/issues/3799)

- znovu publikovat Nuget.CommandLine 3.4.4 k Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- Na migraci, změňte projekty z `project.json` k `.csproj` , se nezdaří obnovení - [#4297](https://github.com/NuGet/Home/issues/4297)

- Selhání obnovení na nově vytvořený xunit testovacího projektu - [#4296](https://github.com/NuGet/Home/issues/4296)

- Základní projekty můžete zablokuje, zamčení uživatelského rozhraní při otevření - [#4269](https://github.com/NuGet/Home/issues/4269)

- Opravte soubor cíle pro úlohy sestavení – [#4267](https://github.com/NuGet/Home/issues/4267)

- Seznam chyb obsahuje chybu po sestavení řešení, které uvolnit odkazované projekt – [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: Cíl "_GenerateRestoreGraphProjectEntry" v projektu neexistuje. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: Když vyberete všechny projekty - dojde k chybě uživatelského rozhraní správce nuget pro řešení [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath selže, když je koncové lomítko - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: obnovení NuGet poskytnout několik upozornění odkaz na projekt pro projekt LinqToTwitter – [#4156](https://github.com/NuGet/Home/issues/4156)

- Pack z `.csproj` neobsahuje atribut minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll dodaný zpoždění přihlášení VS2017 (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: Obnovení selže z projektu VS 2015 vygeneroval s CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Chybám při obnovení mohou skrývat podrobnější chybové zprávy, které může poskytnout sestavení - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Při obnovování balíčků NuGet pro projekt webové stránky došlo k chybě: hodnota nemůže být null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Migrace vyvolá "Objekt odkaz výjimky" v NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)

- DotNet pack by měla pack nástrojů s verzemi, které balíčku byl sestaven s - [#4063](https://github.com/NuGet/Home/issues/4063)

- Nové pozadí obnovení zapisuje milisekund na stavovém řádku při trvá sekund obnovit - [#4036](https://github.com/NuGet/Home/issues/4036)

- Máte překlep v Nepodařilo se vyřešit všechny odkazy na - projektu [#4018](https://github.com/NuGet/Home/issues/4018)

- Povolte PCM pracovní postupy ve scénářích odkaz na balíček - [#4016](https://github.com/NuGet/Home/issues/4016)

- Nelze najít nainstalované balíčky v balíčku správci uživatelské rozhraní – [#4015](https://github.com/NuGet/Home/issues/4015)

- DotNet pack selže, když je prázdná - PackagePath [#3993](https://github.com/NuGet/Home/issues/3993)

- Obnovení selže úkol ve scénáři s více uživateli - [#3897](https://github.com/NuGet/Home/issues/3897)

- Nelze změnit typ obsahu, když balení pomocí úlohy Pack NuGet- [#3895](https://github.com/NuGet/Home/issues/3895)

- Výchozí kopie ContentFiles jsou nesprávná pro MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)

- Obnovení balíčku instalace dvojité protokoly obnovení balíčků zpráva – [#3785](https://github.com/NuGet/Home/issues/3785)

- Odebrat ochranného zábradlí – obnovení "moduly runtime" oddílu použít pouze na aktuální projekt – [#3768](https://github.com/NuGet/Home/issues/3768)

- Úloha sady převádí soubory obsahu v obou se obsah nebo ' a ' contentFiles nebo '- [#3718](https://github.com/NuGet/Home/issues/3718)

- DotNet pack3 velmi značky rozdělení - [#3701](https://github.com/NuGet/Home/issues/3701)

- DotNet pack: balení projekty s balíčkem odkazuje má za následek upozornění duplicitní import - [#3665](https://github.com/NuGet/Home/issues/3665)

- Obnovení protokolování v sadě VS není vždy zobrazovat - [#3633](https://github.com/NuGet/Home/issues/3633)

- text nápovědy místní hodnoty – nuget uvedených stále balíčky mezipaměti - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 páry v odstupu PackageReferences s TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget vybere neočekávanou verzí nástroje MSBuild v sadě VS "15" Preview 4 účelem příkazový řádek - [#3408](https://github.com/NuGet/Home/issues/3408)

- Vypsat soubory cíle nebo props při obnovení se nezdařilo - [#3399](https://github.com/NuGet/Home/issues/3399)

- NuGet během obnovení nerespektuje stejné překrytí compat jako MSBuild při spuštění v příkazovém řádku VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)

- Znovu povolit PackFromProjectWithDevelopmentDependencySet pro VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)

- Inovativně problémy s NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)

- Integrovat 4.0.0.2067 do rozhraní příkazového řádku a sady SDK úložiště pro odeslání s RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)

- VS zablokování, když vytvoříte nové základní konzolovou aplikaci, zavřete řešení, otevřete řešení a zavřít řešení - [#4008](https://github.com/NuGet/Home/issues/4008)

- Stiskne zablokování otevření projektu proti d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)

- Opravte dotnet/nuget.exe místní hodnoty – zpráva doc/help – [#3919](https://github.com/NuGet/Home/issues/3919)

- Zkontrolujte PackTask pro problémy se službou koncové nebo počáteční prázdné znaky - [#3906](https://github.com/NuGet/Home/issues/3906)

- DotNet pack je balení z obj není bin - [#3880](https://github.com/NuGet/Home/issues/3880)

- DotNet pack vždy zdá se, že nastavte ProjectReference verzi 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- DotNet pack se nezdaří s odkazy na projekt a <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException v ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)

- Oříznout mezery z hodnoty vlastnosti nástroje MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)

- Proveďte konsolidaci událostí dvě projektu vyvolá při načítání projektu - [#3759](https://github.com/NuGet/Home/issues/3759)

- Knihovny P2P v `project.assets.json` soubor mít nesprávné verze - [#3748](https://github.com/NuGet/Home/issues/3748)

- Obnovení havárií kvůli reagovat informační kanál a není k dispozici balíčku - [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe může přestat reagovat na velké množství výstupní chyba nástroje MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)

- Obnovení na sestavení pro Blend selže prvním úspěšné podruhé (VS scénář pevné) - [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCRs

- migrovat vsix ze v2 vsix v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet by měl mít mechanismus pro získání cesty k souboru zámku v nástroji MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)

- Přidat prostředky sestavení do TFM kompatibility kontroly a prostředky souboru - [#3296](https://github.com/NuGet/Home/issues/3296)

- Definovat nové ProjectCapability "Pack" sadě cíle pro povolení balíček související možnosti – [#4146](https://github.com/NuGet/Home/issues/4146)

- Spustit Pack jako metodu POST směřující sestavení cíl záleží na vlastnosti "GeneratePackageOnBuild" MSBuild - [#4145](https://github.com/NuGet/Home/issues/4145)

- Vlastnost NuGet RestoreProjectStyle použít k vytvoření konkrétní NuGet projektu - [#4134](https://github.com/NuGet/Home/issues/4134)

- Přizpůsobit obnovení přenositelné odkazy na projekt změn - [#4076](https://github.com/NuGet/Home/issues/4076)

- Přidání vlastností NuGet v cílový soubor pro projekty bez UWP - [#4030](https://github.com/NuGet/Home/issues/4030)

- Podpora UWP TargetPlatformVersion - [#3923](https://github.com/NuGet/Home/issues/3923)

- Komunikaci projekt odkazuje na metadata do systému NuGet projektu - [#3922](https://github.com/NuGet/Home/issues/3922)

- Přidání uživatelského rozhraní pro balení režim – [#3921](https://github.com/NuGet/Home/issues/3921)

- Starší verze `.csproj` potřebuje NugetTargetMoniker a RuntimeIdentifiers nastavit v proj/cíle - [#3854](https://github.com/NuGet/Home/issues/3854)

- Instalace balíčku se mohou překrývat s automatického obnovení - [#3836](https://github.com/NuGet/Home/issues/3836)

- Kontextové nabídky QueryStatus nedojde, pokud není načtena VSPackage – [#3835](https://github.com/NuGet/Home/issues/3835)

- Obnovení řešení a sestavení obnovení stále zobrazit dialogová okna - [#3789](https://github.com/NuGet/Home/issues/3789)

- Izolovat VSSDK verze sestavení řešení NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Odkazy na Githubu chyby v RTM
[Seznam problémů 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[Seznam problémů 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[Seznam problémů 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[Seznam problémů 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[Seznam problémů 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
