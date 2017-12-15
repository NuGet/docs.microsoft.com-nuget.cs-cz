---
title: "Poznámky k verzi NuGet 2.7 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba2edaad-4795-47a0-a572-d0e1716bd540
description: "Poznámky k verzi pro NuGet 2.7 včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.7 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 502cb5e68f905e9ad8f4003bb0690d3e676f6bb7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-27-release-notes"></a>Poznámky k verzi 2.7 NuGet

[Poznámky k verzi služby WebMatrix NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 poznámky k verzi](../release-notes/nuget-2.7.1.md)

NuGet 2.7 byla vydána 22 srpen 2013.

## <a name="acknowledgements"></a>Potvrzení

Rádi bychom se Děkujeme, že následující externí přispěvatele pro jejich významné příspěvky NuGet 2.7:

1. [Jan Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Zobrazí adresu url licence, když je podrobný výpis balíčky a podrobností.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -přidat atribut developmentDependency `packages.config` a použít ho v příkazu pack zahrnout pouze balíčky modulu runtime
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Vyhněte se duplicitní klíč vlastnosti v nuget.exe pack příkazu.
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -zvětšete velikost mezipaměti počítače na 200.
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) – dialogové okno vyřešit NuGet zobrazující aktualizace na kartě nesprávný
    - Oprava Project.TargetFramework může mít hodnotu null v Vedoucí_projektu
    - [#3248](http://nuget.codeplex.com/workitem/3248) -opravte SharedPackageRepository FindPackage/FindPackagesById na neexistující packageId selžou
1. [Kevina Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -povolit podporu pro projekt Nomad
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -oprava nabízené příkaz selže s ukončovacím kódu 0, pokud soubor neexistuje.
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -oprava chyb pomocí příkazu přidat BindingRedirect, když projekt odkazuje na projekt databáze.
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -oprava chyb z nuget.pack analýza zástupný znak v atribut 'vyloučení, nesprávně.
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -oprava chyb `NuGet.targets` nepředává $(Platform) do nuget.exe, když probíhá obnovení balíčků.
1. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -oprava chyb v příkazu nuget.exe balíček, který by umožnil přidávání souborů se stejným názvem, ale s jinou velká a malá písmena, eventuálně vyvolá výjimku "Položka už existuje".
1. [ADAM Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [#2990](http://nuget.codeplex.com/workitem/2990) -verze přidat vlastnost do třídy NetPortableProfile.
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) -oprava chyb NullReferenceException Pokud requireApiKey = true, ale záhlaví X-NUGET-APIKEY není přítomna
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -opravy NuGet.Build cíle do souboru, který bude správně fungovat na MonoDevelop
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - Výkon příkaz Restore zvýšením paralelizace

## <a name="notable-features-in-the-release"></a>Upozorňují na důležité funkce ve verzi

### <a name="package-restore-by-default-with-implicit-consent"></a>Obnovení balíčků ve výchozím nastavení (s implicitní souhlas)

Zavádí nový přístup k obnovení balíčků NuGet 2.7 a také překonává hlavní mezní: souhlasu obnovení balíčků je nyní ve výchozím! Kombinace nový přístup a implicitní souhlasu zásadně zjednoduší scénáře obnovení balíčku.

#### <a name="implicit-consent"></a>Implicitní souhlasu

S NuGet verze 2.0, 2.1, 2.2, 2.5 a 2.6 uživatelé museli výslovně povolit aplikaci NuGet stáhnout chybějící balíčky během sestavení. Pokud svůj souhlas měli není explicitně dostali, pak řešení, které měl povolit obnovení balíčků by nepovede dokud uživateli byl udělen souhlas.

Od verze NuGet 2.7, balíček obnovení souhlasu ON ve výchozím nastavení je současně uživatelům explicitně *chodit* balíček obnovení v případě potřeby pomocí políčka v nastavení NuGet v sadě Visual Studio. Tato změna pro implicitní souhlasu ovlivňuje NuGet v následujících prostředích:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Nástroj příkazového řádku nuget.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Balíček automatické obnovení v sadě Visual Studio

Od verze NuGet 2.7, NuGet bude automaticky stáhnout chybějící balíčky během vytváření sestavení v sadě Visual Studio, i v případě obnovení balíčku není explicitně povolená pro řešení. Toto automatické obnovení balíčků se stane v sadě Visual Studio, když vytváříte projekt nebo řešení, ale před vyvoláním MSBuild. Dostaneme několik významné výhody:

1. Žádné další nutné používat gesto "Povolit obnovení balíčků NuGet" v řešení
1. Projekty, nemusíte být upraven a NuGet nebude proveďte změny do projektu a zda je povoleno obnovení balíčků
1. Všechny balíčky NuGet, včetně těch, které zahrnuty MSBuild importy pro soubory props nebo cíle, bude obnovena *před* vyvolání MSBuild zajištění těchto props cíle jsou správně rozpoznány během sestavení

Pokud chcete používat automatické obnovení balíčků v sadě Visual Studio, stačí provést jednu (akci v):

1. Nekontrolovat vaší `packages` složky

Existuje několik způsobů vynechat vaší `packages` složky od správy zdrojového kódu. Další informace najdete v tématu [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) tématu.

Všichni uživatelé jsou implicitně zapojen do souhlasu automatické obnovení balíčků, můžete můžete snadno chodit prostřednictvím nastavení Správce balíčků v sadě Visual Studio.

![Nastavení správce balíčků](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Obnovení zjednodušené balíčku z příkazového řádku

NuGet 2.7 zavádí novou funkci pro nuget.exe:`nuget.exe restore`

Tento nový příkaz Obnovit umožňuje snadno obnovit všechny balíčky pro řešení pomocí jednoho příkazu, přijetím řešení souboru nebo složky jako argument. Kromě toho tento argument je zahrnuta, jestliže existuje pouze jeden řešení v aktuální složce. To znamená, že všechny následující fungovat ze složky, která obsahuje soubor jediném řešení (MySolution.sln):

1. obnovení nuget.exe MySolution.sln
1. nuget.exe obnovení.
1. obnovení nuget.exe

Příkaz Restore bude otevřete soubor řešení a najít všechny projekty v řešení. Z tohoto místa se najít `packages.config` soubory pro všechny projekty a obnovení všech balíčků nalezen. Také obnoví se nenašly v úrovni řešení balíčky `.nuget\packages.config` souboru. Další informace o nové příkazu Restore naleznete v [Reference k příkazovému řádku](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Nový pracovní postup obnovení balíčku

Snažíme se nadšení o těchto změnách obnovení balíčků, jako by to zavedlo nového pracovního postupu. Pokud chcete vynechat vlastních balíčků od správy zdrojového kódu jednoduše nemáte potvrzení `packages` složky. Visual Studio uživatele, kteří otevřete a sestavte řešení zobrazí balíčky automaticky obnoví. Pro sestavení příkazového řádku, jednoduše vyvolání `nuget.exe restore` před vyvoláním `msbuild`. Je potřeba už nezapomeňte použít gesto "Povolit obnovení balíčků NuGet" na řešení a už budeme potřebovat změnit projekty pro úpravu sestavení. A také dostaneme mnohem lepší prostředí pro balíčky, které zahrnují MSBuild importy, zejména pro importy přidány prostřednictvím NuGet nejnovější funkce pro [automaticky import props/cíle soubory](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) ze složky \build.

Kromě práci, kterou jsme jste si udělat také Pracujeme s zaokrouhlí tento nový přístup některé důležité partnery. Nemáme konkrétní časové osy pro některý z těchto ještě, ale každého partnera, je nadšení, protože jsme se o nový přístup.

* Team Foundation Service - pracují integrovat volání `nuget.exe restore` do výchozí sestavení scénáře.
* Windows Azure webové servery – pracují a umožní vám k uložení projektu do Azure a mají `nuget.exe restore` voláno před provedením vychází vašeho webu.
* TeamCity – aktualizují jejich instalačního programu NuGet modulu plug-in pro TeamCity 8.x
* AppHarbor - pracují a umožní vám nabízená vašeho úložiště AppHarbor a `nuget.exe restore` volat sestavení řešení.

S každou z výše uvedených partnerů jako v aplikaci vlastní kopii nuget.exe a nebude potřeba k provedení nuget.exe ve vašem řešení.

#### <a name="known-issues"></a>Známé problémy

Nebyly k dispozici dva známé problémy s obnovením nuget.exe s původním vydáním 2.7, ale jsme vyřešili na 9/6/2013 s aktualizací do [NuGet.CommandLine balíček](http://www.nuget.org/packages/NuGet.CommandLine/).  Tato aktualizace je také k dispozici na [stránky pro stažení NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) na webu CodePlex.  Spuštění `nuget.exe update -self` se aktualizuje na nejnovější verzi.

Pevné měla:

1. [Nové obnovení balíčků nefunguje na Mono při použití SLN – soubor](https://nuget.codeplex.com/workitem/3596)
1. [Nové obnovení balíčků nefunguje s Wix projekty](https://nuget.codeplex.com/workitem/3598)

Je také známý problém s nový pracovní postup obnovení balíčku které [automatické obnovení balíčků nefunguje pro projekty v řešení složce](https://nuget.codeplex.com/workitem/3625). Tento problém byl opraven v NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Změna orientace projektu a Upgrade sestavení chyby/varování

Kolikrát po Změna orientace nebo upgrade projektu, zjistíte, zda nejsou některé balíčky NuGet funguje správně. Bohužel neexistuje žádná informace o to a nejsou k dispozici žádné pokyny o tom, jak jej vyřešit. S NuGet 2.7 jsme teď použít některé události sady Visual Studio k rozpoznání během jste změnit cíl necílené nebo upgradovat projektu způsobem, který má vliv na vaše nainstalované balíčky NuGet.

Pokud je zjištěno, že některé z vašich balíčků situace měla vliv na Změna orientace nebo upgrade, jsme budete vytvořit chyby okamžitou sestavení s upozorněním. Kromě chyba okamžitou sestavení jsme také zachovat `requireReinstallation="true"` příznak ve vaší `packages.config` souboru pro všechny balíčky, které byly ovlivněných podle Změna orientace a každý další sestavení v sadě Visual Studio vyvolá upozornění sestavení pro tyto balíčky.

I když NuGet nelze provést automatickou akci k opětovné instalaci ovlivněné balíčky, Věříme, že tento údaj a upozornění budou Průvodce Nápověda zjistíte, když bude nutné přeinstalovat balíčky. Také pracujeme na [balíček přeinstalování pokyny dokumentace](../consume-packages/reinstalling-and-updating-packages.md) tyto chybové zprávy přímo vám.

### <a name="nuget-configuration-defaults"></a>Výchozí hodnoty konfigurace NuGet

Mnoho společností používají NuGet interně, ale předtím vedení svého vývojáře k použití zdroje interní balíčků místo nuget.org pevný čas. NuGet 2.7 zavádí funkce výchozí hodnoty konfigurace, která umožňuje zadat pro celý počítač výchozí hodnota:

1. Povolenému zdroji balíčků
1. Zdroje balíčků registrovaná, ale zakázané
1. Výchozí nuget.exe nabízené zdroj

Každá z těchto se teď dá nakonfigurovat v souboru nachází v `%ProgramData%\NuGet\NuGetDefaults.Config`. Pokud tento konfigurační soubor Určuje zdroje balíčků, pak výchozí zdroj balíčku nuget.org nebude registrována automaticky a v `NuGetDefaults.Config` místo níž bude zaregistrována.

Není požadováno k použití této funkce Očekáváme, že společnosti nasadit `NuGetDefaults.Config` souborů pomocí zásad skupiny.

*Všimněte si, že tato funkce může způsobit nikdy zdroj balíčku, který má být odebrán z nastavení NuGet pro vývojáře. To znamená, pokud vývojář již použit NuGet a proto má zdroj balíčku nuget.org registrován, nebude odebraný po vytvoření `NuGetDefaults.Config` souboru.*

V tématu [výchozí konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) Další informace o této funkci.

### <a name="renaming-the-default-package-source"></a>Přejmenování zdrojového balíčku výchozí

NuGet vždy zaregistrovala výchozí zdroj balíčku názvem "NuGet oficiální zdroj balíčku" odkazující na nuget.org. Tento název byl podrobné a je také nezadal kde ve skutečnosti odkazuje. Chcete-li vyřešit tyto dva problémy, jsme jste přejmenovat tohoto balíčku zdroje do jednoduše "nuget.org" v uživatelském rozhraní. Adresu URL pro zdroj balíčku se změní taky zahrnout "www". Předpona. Po použití NuGet 2.7, bude vaše stávající "NuGet oficiální zdroj balíčku" automaticky aktualizují na "nuget.org" jako její název a "https://www.nuget.org/api/v2/" jako jeho adresa URL.

### <a name="performance-improvements"></a>Zvýšení výkonu

Jsme provedli několik zlepšení výkonu v 2.7, která předá menší nároky na paměť, menší využití disku a rychlejší instalaci balíčku. Také jsme provedli chytřejší dotazy do informačních kanálů založené na protokolu OData, které se sníží celkový datové části.

### <a name="new-extensibility-apis"></a>Nové rozšíření rozhraní API

Jsme přidali některých nových rozhraní API našich služeb rozšiřitelnost mezeru chybějící funkce v předchozích verzích.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>Jenom pro vývojové závislosti

Tato funkce byla přispěli [Adam Ralph](https://twitter.com/adamralph) a umožňuje autorům balíček deklarovat závislosti, které byly použity pouze na vývoj čas a nevyžadují závislosti balíčků. Přidáním `developmentDependency="true"` atribut balíček v `packages.config`, `nuget.exe pack` budou už obsahovat tento balíček jako závislost.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Odebrat podporu pro Visual Studio 2010 Express pro Windows Phone

Nový model obnovení balíčku v 2.7 je implementováno modulem nové VSPackage, který se liší od hlavní NuGet VSPackage. Kvůli technickým problémem, tento nový VSPackage nebude fungovat správně v *Visual Studio 2010 Express pro Windows Phone* SKU, protože má stejný kód základní můžeme sdílet s jinými podporováno Visual Studio SKU. Proto od verze NuGet 2.7, jsme ztrácejí jsou podpora *Visual Studio 2010 Express pro Windows Phone* z publikovaných rozšíření. Podpora pro *Visual Studio 2010 Express pro Web* je stále součástí primární rozšíření, které jsou publikovány do Galerie rozšíření sady Visual Studio.

Vzhledem k tomu, že jsme nejste jistí, kolik vývojáři stále používají NuGet v této verzi nebo edici sady Visual Studio, jsme jsou publikování samostatné rozšíření sady Visual Studio speciálně pro tyto uživatele a publikování na webu CodePlex (nikoli Galerie rozšíření sady Visual Studio) . Plánujeme není nadále spravovat rozšíření, ale pokud to setkáte dejte nám vědět podle vyplnění problém na webu CodePlex.

Chcete-li Správce balíčků NuGet (pro Visual Studio 2010 Express pro Windows Phone), navštivte [NuGet 2.7 stáhne](https://nuget.codeplex.com/releases/view/107605) stránky.

### <a name="bug-fixes"></a>Opravy chyb

Kromě těchto funkcích tato verze NuGet také obsahuje mnoho ostatní opravy chyb. Nebyly 97 celkový problémy řešeny v verze. Úplný seznam pracovní položky pevná ve NuGet 2.7 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
