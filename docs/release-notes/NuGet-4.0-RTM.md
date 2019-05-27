---
title: Zpráva k vydání verze NuGet 4.0 RC
description: Zpráva k vydání verze pro NuGet 4.0 RTM, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547758"
---
# <a name="nuget-40-rtm-release-notes"></a>Zpráva k vydání verze NuGet 4.0 RTM

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) obsahuje NuGet 4.0, který přidává podporu pro .NET Core, má spoustu opravy kvality a zvyšuje výkon. Tato verze také přináší několik vylepšení, jako je podpora pro PackageReference a příkazy pro balíčky NuGet jako MSBuild cíle, obnovení balíčku pozadí a další.

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

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Alternativně můžete zkusit odstranění `project.lock.json` a znovu ho obnovit.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>Pokud v projektech .NET Core použijete balíček, který obsahuje sestavení s neplatným podpisem, můžete uvíznout v nekonečné smyčce obnovování

#### <a name="issue"></a>Problém

Když použijete balíček, který obsahuje sestavení s neplatným obsahem, nebo když se verze balíčku nastaví pomocí časovače DateTime, automatické obnovení balíčku běží v nekonečné smyčce. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nejde zobrazit, přidat ani aktualizovat DotNetCLITools pomocí Správce balíčků Nuget

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

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Chyby opravené v určeném časovém rozmezí NuGet 4.0 RTM

[Zpráva k vydání verze NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) – zobrazí seznam všech problémů stanovené pro NuGet 4.0 RC

### <a name="features"></a>Funkce

- Lokalizace řetězců v NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget vynutí načíst projekty webových aplikací v režimu zjednodušeného načtení řešení - [#4258](https://github.com/NuGet/Home/issues/4258)

- AutoReferenced PackageReference podporu verze bloku sektorů změny v uživatelském rozhraní pro balíčky "nainstalované sady sdk" - [#4044](https://github.com/NuGet/Home/issues/4044)

- Pro všechny závislosti projektu (PackageRef) - správně komunikují PackageSpec.Version [#3902](https://github.com/NuGet/Home/issues/3902)

- Podpora pro odebrání odkazů do `.csproj` z commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)

- Podpora pro projekty PackageReference (normální a xplat) a zjednodušené načtení řešení – obnovení [#4003](https://github.com/NuGet/Home/issues/4003)

- Podpora pro přidání odkazů do `.csproj` z commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)

- Podpora obnovení NuGet pro zjednodušené načtení řešení pro `packages.config` nebo `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- contentFiles podporují v souboru cíle nuget vygeneruje - [#3683](https://github.com/NuGet/Home/issues/3683)

- Navázání Mono CI k ověření nuget.exe na počítači Mac pomocí nástroje MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)

- Přesunout NuGet z závislosti NuGet.Core v2 - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Chyby

- Obnovení NuGet v sadě Visual Studio nerespektuje vlastnost PackageId projekty – [#4586](https://github.com/NuGet/Home/issues/4586)

- Chyba NuGet ProjectSystemCache při přidání balíčku v balíčku souboru vsix – [#4545](https://github.com/NuGet/Home/issues/4545)

- Balíček vyvolá výjimku, pokud se používá v projektu s více Tfm – IncludeSource [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3 chyby týkající se použití aktualizace z celé řešení správy - balíčků [#4474](https://github.com/NuGet/Home/issues/4474)

- Nelze odinstalovat nově nainstalovaný balíček – [#4435](https://github.com/NuGet/Home/issues/4435)

- Při migraci do PackageRef, hybridní řešení mají obnovení neobvyklé chování - [#4433](https://github.com/NuGet/Home/issues/4433)

- Vytváření krátce po spuštění NuGet (instalace, aktualizace, obnovení), může způsobit, že VS pro zablokování - [#4420](https://github.com/NuGet/Home/issues/4420)

- Zablokování uživatelského rozhraní – zablokování inicializace NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- Přidání balíčku příkaz má přidat verze jako atribut namísto element - [#4325](https://github.com/NuGet/Home/issues/4325)

- DotNet
  - Obnovení foo.sln dotnetcore – selže, pokud konfigurace v SLN způsobit duplicitní (ale nakonfigurovat diff) projekty v grafu restore - [#4316](https://github.com/NuGet/Home/issues/4316)

- Obsah pouze balíčky - [#3668](https://github.com/NuGet/Home/issues/3668)

- Ve výchozím nastavení vyjádřit výslovný nesouhlas možnost selektor formátování balíčku - [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: Projekt CreateUAP_CSharp_VS.01.1.Create který poklesl Duration_TotalElapsedTime podle 3,153.570 ms (149.1 %). Směrný plán 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: Řešení ManagedLangs_CS_DDRIT.0300.Rebuild který poklesl Duration_TotalElapsedTime ve verzi 1.5 sekundu. Směrný plán 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Nominace selže v projektech multi TFM - [#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: Řešení WebForms_DDRIT.1200.Close který poklesl VM_ImagesInMemory_Total_devenv počtem 3.000 (0,5 %). Směrný plán 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - Pack upozornění při cílení na netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)

- PathTooLongException – při pokusu o přidání balíčku NuGet do prázdná webová aplikace ASP.NET Core – [#4391](https://github.com/NuGet/Home/issues/4391)

- Balíček spouští příliš často – dotnet
  - dotnetcore balíčku selže a zobrazí se zde je cyklická závislost v cílové závislosti grafu zahrnující cíl "Balíček" - [#4381](https://github.com/NuGet/Home/issues/4381)

- Balíček se spouští příliš často – balíček NuGet generovat neobsahuje všechny konfigurace - [#4380](https://github.com/NuGet/Home/issues/4380)

- Přidání nuget NullReferenceException s packageref v projektu jazyka C++ - [#4378](https://github.com/NuGet/Home/issues/4378)

- Usnadnění: Program Předčítání není vyprávění příběhu zaškrtávací políčko Vybrat projekty, které chcete nainstalovat balíček - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 nedojde selže připojuje k informačním kanálům VSO/VSTS - 365798 chyb VS - [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles získat výstup do nesprávného umístění, pokud Určuje cestu jako "contentFiles" - PackagePath [#4348](https://github.com/NuGet/Home/issues/4348)

- Cíl Pack připojí vlastnost PackageVersion s VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)

- Cesta k balíčku nefunguje při využití balíčku dotnet - zadání [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet výstupy spoustu upozornění na duplicitní importy během obnovení – [#4304](https://github.com/NuGet/Home/issues/4304)

- Zvolte možnost "Formát Správce balíčků NuGet" dialogové okno nevypadají v rámci tmavý motiv - [#4300](https://github.com/NuGet/Home/issues/4300)

- Při obnovení sestavení – chybě VS [#4298](https://github.com/NuGet/Home/issues/4298)

- Visual Studio zablokování Pokud chcete přidat TFM v targetframeworks, uložte a pak sestavení. 10 % doby - [#4295](https://github.com/NuGet/Home/issues/4295)

- balíček nuget není výstupní zpráva o úspěchu, o balicí projekt úspěšně - [#4294](https://github.com/NuGet/Home/issues/4294)

- Packtask se neposkytl se nezdaří z důvodu System.IO.Compression 4.1 nebyly nalezeny - [#4290](https://github.com/NuGet/Home/issues/4290)

- Balíček spouští příliš často – packtask se neposkytl často selže kvůli konfliktu přístup k souboru - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet otevře v okně výstupu se během obnovení na pozadí – [#4274](https://github.com/NuGet/Home/issues/4274)

- Vylučte poskytovatel služeb jako nebezpečné kódování vzor (který může způsobit zablokování) – [#4268](https://github.com/NuGet/Home/issues/4268)

- Výkon/UIHang – vylepšení DownloadTimeoutStream čtení - [#4266](https://github.com/NuGet/Home/issues/4266)

- Visual Studio zablokování při pokusu o zavření projektu před dokončením příkazu se obnovení NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)

- Problémy s packtask se neposkytl a balení `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Nejde přeložit balíčky nuget v novém projektu (musí se restartovat visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] "Verze" rozevírací nabídka, která zobrazuje verze k dispozici balíčku potýká zůstat synchronizované s balíčkem nuGet vybrané... – [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client by měl používat CPS JoinableTaskFactory při interakci s CPS zablokování - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 není při rozbalování `.targets` z balíčku - [#4171](https://github.com/NuGet/Home/issues/4171)

- DotNet
  - dotnetcore pack nepodporuje title v `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package má za následek chybové dialogové okno v VS2017 RC – [#4127](https://github.com/NuGet/Home/issues/4127)

- Aktualizace balíčku pro projekt .net core pravděpodobně nebude fungovat, jak rozhraní nezíská aktualizace CPS od nominate. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Zlepšení nepřeložený odkaz upozornění - [#3955](https://github.com/NuGet/Home/issues/3955)

- DotNet
  - pack dotnetcore – ProjectReference ztratí informace o verzi – [#3953](https://github.com/NuGet/Home/issues/3953)

- Vytvoření aplikace pro UPW vytvoření projektu a znovu sestavte regrese celkový uplynulý čas – [#3873](https://github.com/NuGet/Home/issues/3873)

- Během obnovení se zobrazí zpráva úspěšné obnovení po chybě. - [#3799](https://github.com/NuGet/Home/issues/3799)

- opakované publikování Nuget.CommandLine 3.4.4 na Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- Na migraci, změňte projekty z `project.json` k `.csproj` ---nezdaří obnovení – [#4297](https://github.com/NuGet/Home/issues/4297)

- Selhání obnovení na projekt testů xunit nově vytvořený - [#4296](https://github.com/NuGet/Home/issues/4296)

- Projekty Core můžete reagovat, uzamčení uživatelského rozhraní na open - [#4269](https://github.com/NuGet/Home/issues/4269)

- Opravte soubor cílů pro sestavení úkoly – [#4267](https://github.com/NuGet/Home/issues/4267)

- Seznam chyb obsahuje chybu po sestavení řešení, které uvolnit Odkazovaný projekt - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: Cíl "_GenerateRestoreGraphProjectEntry" v projektu neexistuje. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: Když vyberete všechny projekty - dojde k chybě uživatelského rozhraní správce nuget pro řešení [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath selže po koncové lomítko - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: obnovení NuGet poskytují několik upozornění odkaz projektu pro projekt LinqToTwitter – [#4156](https://github.com/NuGet/Home/issues/4156)

- Balíčku ze `.csproj` neobsahuje atribut minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll dodáno podepisováno v VS2017 (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: Obnovení se nezdaří pro projekt VS 2015 generuje s použitím CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Chyby obnovení může ztížit odhalení zjevného kompletní chybové zprávy, které může poskytnout sestavení - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Při obnovování balíčků NuGet pro projekt webu došlo k chybě: hodnota nemůže být null. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Migrace vyvolá "Odkaz na objekt výjimky" v NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)

- DotNet
  - dotnetcore pack by měl aktualizací Service pack nástroje s verzemi, které byla vytvořena balíčku - [#4063](https://github.com/NuGet/Home/issues/4063)

- Nové pozadí obnovení zapisuje milisekund do stavového řádku při trvá sekund obnovit - [#4036](https://github.com/NuGet/Home/issues/4036)

- Máte překlep v nepovedlo se vyřešit všechny odkazy – projektu [#4018](https://github.com/NuGet/Home/issues/4018)

- Povolte pracovní postupy PCM ve scénářích odkaz na balíček - [#4016](https://github.com/NuGet/Home/issues/4016)

- Nejde najít nainstalované balíčky v balíčku správce uživatelského rozhraní – [#4015](https://github.com/NuGet/Home/issues/4015)

- DotNet
  - dotnetcore balíčku selže, pokud je prázdný - PackagePath [#3993](https://github.com/NuGet/Home/issues/3993)

- Obnovení selže úkol ve scénáři s více uživateli - [#3897](https://github.com/NuGet/Home/issues/3897)

- Nelze změnit typ obsahu při balení pomocí úkolu pro balíček NuGet- [#3895](https://github.com/NuGet/Home/issues/3895)

- Výchozí kopie ContentFiles nesprávných MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)

- Obnovení balíčku instalace double zaznamená obnovení balíčků zprávu - [#3785](https://github.com/NuGet/Home/issues/3785)

- Odebrat ochranného zábradlí – obnovení v části "moduly runtime" by se měly používat jenom k aktuálnímu projektu – [#3768](https://github.com/NuGet/Home/issues/3768)

- Úloha sady umístí soubory obsahu v obou ' obsah / "a" contentFiles / "- [#3718](https://github.com/NuGet/Home/issues/3718)

- DotNet
  - dotnetcore pack3 velmi označit rozdělení - [#3701](https://github.com/NuGet/Home/issues/3701)

- DotNet
  - balíček dotnetcore: balení projektů v balíčku odkazuje na výsledky upozornění na duplicitní import - [#3665](https://github.com/NuGet/Home/issues/3665)

- Obnovení protokolování v sadě Visual Studio není vždy zobrazovat - [#3633](https://github.com/NuGet/Home/issues/3633)

- text nápovědy nuget locals stále uvedených mezipaměť balíčků - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 páry v odstupu PackageReferences s TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget vybere neočekávanou verzí nástroje MSBuild v sadě Visual Studio "15" Preview 4. odch. příkazový řádek – [#3408](https://github.com/NuGet/Home/issues/3408)

- Vypsat soubory cíle/props na selhání obnovení – [#3399](https://github.com/NuGet/Home/issues/3399)

- Během obnovení NuGet nerespektuje stejné překrytí compat jako MSBuild při spuštění v příkazovém řádku VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)

- Opětovné povolení PackFromProjectWithDevelopmentDependencySet pro VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)

- Blend problémy s NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)

- Integrace 4.0.0.2067 do příkazového řádku a sady SDK úložiště k odeslání RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)

- VS – zablokování při vytváření nové základní konzolovou aplikaci, Zavřít řešení, otevřete řešení a zavřít řešení - [#4008](https://github.com/NuGet/Home/issues/4008)

- Dosažení zablokování otevírání projektu proti d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)

- Oprava dotnet/nuget.exe lokální zprávy doc/help – [#3919](https://github.com/NuGet/Home/issues/3919)

- Kontrola problémů s koncové nebo počáteční mezery – packtask se neposkytl [#3906](https://github.com/NuGet/Home/issues/3906)

- DotNet
  - dotnetcore pack je balení z obj není bin - [#3880](https://github.com/NuGet/Home/issues/3880)

- DotNet
  - balíček dotnetcore vždy zdá se, že nastavení ProjectReference verze 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- DotNet
  - balíček dotnetcore selže s odkazy na projekt a <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException v ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)

- Oříznout mezery z hodnoty vlastnosti nástroje MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)

- Sloučit dva projektu události vyvolané při načtení projektu – [#3759](https://github.com/NuGet/Home/issues/3759)

- Knihovny P2P `project.assets.json` souboru mají nesprávnou verzi - [#3748](https://github.com/NuGet/Home/issues/3748)

- Obnovení při selhání z důvodu informačního kanálu poslána a není k dispozici balíček – [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe může reagovat na velké množství chybový výstup nástroje MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)

- Obnovení na sestavení pro Blend selže poprvé, bude úspěšné podruhé (VS scénář pevné) – [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>Chcete

- migrace vsix z v2 vsix na v3 vsix – [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet by měl mít mechanismus pro získání cesty k souboru zámku v nástroji MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)

- Přidat prostředky sestavení do TFM kompatibility kontrola a prostředky souboru - [#3296](https://github.com/NuGet/Home/issues/3296)

- Definovat nové ProjectCapability "Balíček" v sadě cílů pro povolení balíček související možnosti – [#4146](https://github.com/NuGet/Home/issues/4146)

- Spuštění balíčku jako příspěvek sestavení záleží na vlastnost MSBuild "GeneratePackageOnBuild" - target [#4145](https://github.com/NuGet/Home/issues/4145)

- Vlastnost NuGet RestoreProjectStyle použít k vytvoření určitého projektu NuGet - [#4134](https://github.com/NuGet/Home/issues/4134)

- Přizpůsobit obnovení u přenositelných odkazů projektu změnit - [#4076](https://github.com/NuGet/Home/issues/4076)

- Přidat NuGet vlastnosti v cílovém souboru pro projekty bez UPW – [#4030](https://github.com/NuGet/Home/issues/4030)

- Podpora UWP TargetPlatformVersion – [#3923](https://github.com/NuGet/Home/issues/3923)

- Komunikovat se projekt odkazuje na metadata do projektu systému NuGet - [#3922](https://github.com/NuGet/Home/issues/3922)

- Přidání uživatelského rozhraní pro režim balení – [#3921](https://github.com/NuGet/Home/issues/3921)

- Starší verze `.csproj` potřebuje NugetTargetMoniker a RuntimeIdentifiers nastavit na proj/zaměřuje - [#3854](https://github.com/NuGet/Home/issues/3854)

- Instalace balíčku se mohly překrývat s automatické obnovení – [#3836](https://github.com/NuGet/Home/issues/3836)

- Místní nabídka QueryStatus nestane při načtení není VSPackage - [#3835](https://github.com/NuGet/Home/issues/3835)

- Obnovení řešení a sestavení obnovení stále zobrazit dialogová okna - [#3789](https://github.com/NuGet/Home/issues/3789)

- Izoluje VSSDK verze sestavení řešení NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Odkazy na problémy Githubu Vyřešeno ve verzi RTM
[Seznam problémů 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Seznam problémů 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Seznam problémů 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Seznam problémů 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Seznam problémů 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
