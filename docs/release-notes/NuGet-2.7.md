---
title: Zpráva k vydání verze NuGet 2,7
description: Poznámky k verzi pro NuGet 2,7, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 70600e3c563e357663b4a2f24139d2fc25f75fdf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780398"
---
# <a name="nuget-27-release-notes"></a>Zpráva k vydání verze NuGet 2,7

[2.6.1 NuGet pro poznámky k verzi WebMatrixu](../release-notes/nuget-2.6.1-for-webmatrix.md)  |  [Poznámky k verzi NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2,7 byl vydán 22. srpna 2013.

## <a name="acknowledgements"></a>Poděkování

Rádi bychom pro své významné příspěvky k NuGet 2,7 měli Děkujeme za tyto externí přispěvatele:

1. [Mike Skořepa](http://www.codeplex.com/site/users/view/mxrss) ( [@mxrss](https://twitter.com/mxrss) )
    - Zobrazit adresu URL licence při výpisu balíčků a podrobné podrobnosti
2. [Adam petrpo](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#1956](http://nuget.codeplex.com/workitem/1956) – přidat atribut developmentDependency do `packages.config` a použít ho v balení příkazu, aby zahrnoval jenom balíčky za běhu
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ( [@tkrafael](https://twitter.com/tkrafael) )
    - Vyhněte se duplicitnímu klíči vlastností v příkazu sady nuget.exe Pack.
4. [Robert Phegan](http://www.codeplex.com/site/users/view/benphegan) ( [@BenPhegan](https://twitter.com/benphegan) )
    - [#2610](http://nuget.codeplex.com/workitem/2610) – zvyšte velikost mezipaměti počítače na 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ( [@derigel](https://twitter.com/derigel) )
    - Dialogové okno [#3217](http://nuget.codeplex.com/workitem/3217) – opravit NuGet zobrazující aktualizace na nesprávné kartě
    - Oprava projektu. TargetFramework může mít hodnotu null v ProjectManager
    - [#3248](http://nuget.codeplex.com/workitem/3248) -Fix SharedPackageRepository FindPackage/FindPackagesById selže v neexistujícím packageId
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ( [@kevfromireland](https://twitter.com/kevfromireland) )
    - [#3234](http://nuget.codeplex.com/workitem/3234) – povolit podporu pro projekt Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ( [@corinblaikie](https://twitter.com/corinblaikie) )
    - [#3252](http://nuget.codeplex.com/workitem/3252) – oprava příkazu push se nezdařila s ukončovacím kódem 0, pokud soubor neexistuje.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) – opravit chybu pomocí příkazu Add-BindingRedirect, když projekt odkazuje na projekt databáze.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - [#2891](http://nuget.codeplex.com/workitem/2891) -opravit chybu souboru NuGet. Pack pro analýzu zástupného znaku v atributu Exclude nesprávně.
10. [Justin vážený](http://www.codeplex.com/site/users/view/zippy1981) ( [@zippy1981](https://twitter.com/zippy1981) )
     - [#3307](http://nuget.codeplex.com/workitem/3307) – Oprava chyby `NuGet.targets` neprojde $ (Platform) k nuget.exe při obnovování balíčků.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) – opravit chybu v příkazu nuget.exe balíčku, který umožňuje přidat soubory se stejným názvem, ale s různou velikostí písmen, a nakonec způsobit výjimku "položka již existuje".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ( [@kzu](https://twitter.com/kzu) )
     - [#2990](http://nuget.codeplex.com/workitem/2990) – přidejte vlastnost verze do třídy NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) – opravit chybu NullReferenceException, pokud requireApiKey = true, ale hlavička X-NUGET-APIKEY není k dispozici.
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ( [@friism](https://twitter.com/friism) )
     - [#3278](https://nuget.codeplex.com/workitem/3278) – opraví soubor s cíli sestavení NuGet. sestavení tak, aby fungovalo správně ve MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ( [@pranav_km](https://twitter.com/pranav_km) )
     - Zlepšení výkonu příkazu obnovit zvýšením paralelismu

## <a name="notable-features-in-the-release"></a>Významné funkce v této verzi

### <a name="package-restore-by-default-with-implicit-consent"></a>Obnovení balíčků ve výchozím nastavení (s implicitním souhlasem)

NuGet 2,7 zavádí nový přístup k obnovení balíčků a přináší také zásadní prahovou hodnotu: souhlas s obnovením balíčku je teď ve výchozím nastavení zapnutý. Kombinací nového přístupu a implicitního souhlasu se drasticky zjednoduší scénáře obnovení balíčků.

#### <a name="implicit-consent"></a>Implicitní souhlas

V případě NuGet verze 2,0, 2,1, 2,2, 2,5 a 2,6 mohou uživatelé, kteří mají explicitně možnost stáhnout chybějící balíčky během sestavení, výslovně dovolit NuGet. Pokud se tomuto souhlasu výslovně nedali, pak se sestavení s povoleným obnovením balíčku nepodaří sestavit, dokud uživatel neudělí souhlas.

Počínaje verzí NuGet 2,7 je souhlas balíčku pro obnovení ve výchozím nastavení zapnutý, ale pokud chcete, aby se uživatelé výslovně *odhlásili* z obnovení balíčků, pokud je to potřeba, použijte zaškrtávací políčko v nastavení NuGet v aplikaci Visual Studio. Tato změna implicitního souhlasu má vliv na NuGet v následujících prostředích:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Nástroj nuget.exe Command-Line

#### <a name="automatic-package-restore-in-visual-studio"></a>Automatické obnovení balíčků v aplikaci Visual Studio

Počínaje NuGet 2,7, NuGet automaticky stáhne chybějící balíčky během sestavování v aplikaci Visual Studio, i když není pro řešení explicitně zapnuté obnovení balíčku. K tomuto automatickému obnovení balíčku dojde v aplikaci Visual Studio při sestavení projektu nebo řešení, ale před vyvoláním nástroje MSBuild. To přináší několik významných výhod:

1. Ve vašem řešení už nemusíte používat gesto povolit obnovení balíčku NuGet.
1. Projekty není nutné upravovat a NuGet neprovede změny v projektu, aby bylo zajištěno, že je povoleno obnovení balíčku.
1. Všechny balíčky NuGet včetně těch, které zahrnovaly importy nástroje MSBuild pro soubory props/targets, budou obnoveny *před* vyvoláním nástroje MSBuild, čímž se zajistí, že tyto props/cíle budou během sestavení správně rozpoznány.

Chcete-li použít automatické obnovení balíčku v aplikaci Visual Studio, stačí provést jednu akci (v):

1. Nevracet se změnami `packages` složku

Existuje několik způsobů, jak složku vynechat `packages` ze správy zdrojového kódu. Další informace najdete v tématu [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) .

I když se všichni uživatelé implicitně zařadí do automatického souhlasu balíčku pro obnovení, můžete se snadno odhlásit prostřednictvím nastavení správce balíčků v aplikaci Visual Studio.

![Nastavení správce balíčků](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Zjednodušené obnovení balíčků z Command-Line

NuGet 2,7 zavádí novou funkci pro nuget.exe: `nuget.exe restore`

Tento nový příkaz pro obnovení umožňuje snadno obnovit všechny balíčky pro řešení jediným příkazem a přijmout soubor řešení nebo složku jako argument. Kromě toho je tento argument implicitní, pokud je v aktuální složce pouze jedno řešení. To znamená, že následující vše funguje ze složky, která obsahuje jeden soubor řešení (Mojereseni. sln):

1. nuget.exe obnovení Mojereseni. sln
1. nuget.exe obnovení.
1. nuget.exe obnovení

Příkaz Restore otevře soubor řešení a vyhledá všechny projekty v rámci řešení. Odtud vám nalezne `packages.config` soubory pro každý z projektů a obnoví všechny nalezené balíčky. Také obnoví balíčky na úrovni řešení nalezené v `.nuget\packages.config` souboru. Další informace o novém příkazu pro obnovení najdete v části Reference k [příkazovému řádku](../reference/cli-reference/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Nový pracovní postup pro obnovení balíčku

O těchto změnách zajímáme obnovení balíčku, protože zavádí nový pracovní postup. Pokud chcete balíčky vynechat ze správy zdrojového kódu, nebudete ji moct jednoduše potvrzovat `packages` . Uživatelé sady Visual Studio, kteří otevřou a sestavují řešení, budou zobrazovat balíčky automaticky. Pro sestavení příkazového řádku stačí vyvolat `nuget.exe restore` před vyvoláním `msbuild` . Už nemusíte používat gesto povolit obnovení balíčku NuGet ve vašem řešení a nebudete už muset upravovat vaše projekty pro změnu sestavení. A také poskytuje mnohem vylepšené prostředí pro balíčky, které zahrnují importy nástroje MSBuild, zejména pro importy přidané prostřednictvím nedávné funkce NuGet pro [Automatické importování souborů props/targets](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) ze složky \Build.

Kromě práce, kterou jsme dokončili dodržovali, pracujeme také s některými důležitými partnery k tomu, abyste tento nový postup zaokrouhlí. Pro žádné z nich ještě neexistují žádné konkrétní časové osy, ale každý partner se zajímá od nového přístupu.

* Team Foundation Service – pracují na integraci volání do `nuget.exe restore` do výchozích scénářů sestavení.
* Weby Windows Azure – fungují tak, aby vám umožnily nasdílet projekt do Azure a volat se `nuget.exe restore` před sestavením webu.
* TeamCity – aktualizuje se modul plug-in instalačního programu NuGet pro TeamCity 8. x
* AppHarbor – pracují na to, aby vám umožnily nasdílení úložiště do AppHarbor a bylo `nuget.exe restore` voláno před tím, než se vaše řešení sestaví.

Každý z výše uvedených partnerů by používal svoji vlastní kopii nuget.exe a nemusíte nuget.exe ve vašem řešení.

#### <a name="known-issues"></a>Známé problémy

Při nuget.exe obnovení s původní verzí 2,7 byly zjištěny dva známé problémy, ale byly opraveny na 9/6/2013 s aktualizací [balíčku NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Tato aktualizace je také k dispozici na [stránce pro stažení NuGet 2,7](https://nuget.codeplex.com/releases/view/107605) na webu CodePlex.  Spuštění `nuget.exe update -self` se aktualizuje na nejnovější verzi.

Opraveno:

1. [Nové obnovení balíčku nefunguje na mono při použití souboru SLN.](https://nuget.codeplex.com/workitem/3596)
1. [Nové obnovení balíčku nefunguje s projekty WIX](https://nuget.codeplex.com/workitem/3598)

Existuje taky známý problém s novým pracovním postupem pro obnovení balíčků, kdy [Automatické obnovení balíčku nefunguje pro projekty ve složce řešení](https://nuget.codeplex.com/workitem/3625). Tento problém byl opravený ve 2.7.1 NuGet.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Změny cílení projektu a upgrade chyb a upozornění buildu

V mnoha případech po provedení změny cílení nebo upgradu projektu zjistíte, že některé balíčky NuGet nefungují správně. Bohužel k tomu neexistují žádné informace a neexistují žádné pokyny k tomu, jak je řešit. S NuGet 2,7 teď používáme některé události sady Visual Studio k rozpoznávání, když jste změnili cílení nebo upgradovat projekt způsobem, který má vliv na nainstalované balíčky NuGet.

Pokud zjistíme, že všechny vaše balíčky byly ovlivněny změnou cíle nebo upgrade, vytvoříme okamžité chyby sestavení, abychom vám věděli. Kromě chyby okamžitého sestavení také uchovává `requireReinstallation="true"` příznak v `packages.config` souboru pro všechny balíčky ovlivněné změnou cíle a každé následné sestavení v aplikaci Visual Studio vyvolá upozornění sestavení pro tyto balíčky.

I když NuGet nemůže provést automatickou akci přeinstalovat ovlivněné balíčky, doufáme, že toto oznámení a upozornění vám pomůže zjistit, kdy potřebujete balíčky znovu nainstalovat. Pracujeme také na dokumentaci s [pokyny k přeinstalaci balíčku](../consume-packages/reinstalling-and-updating-packages.md) , na kterou vás tyto chybové zprávy přesměrují.

### <a name="nuget-configuration-defaults"></a>Výchozí hodnoty konfigurace NuGet

Mnohé společnosti používají NuGet interně, ale měly by mít čas od času, kdy vývojáři používají místo nuget.org interní zdroje balíčků. NuGet 2,7 zavádí funkci výchozích hodnot konfigurace, která umožňuje zadat výchozí nastavení pro všechny počítače:

1. Povolené zdroje balíčků
1. Zaregistrováno, ale zakázané zdroje balíčků
1. Výchozí nuget.exe zdroj nabízených oznámení

Každý z nich se teď dá nakonfigurovat v rámci souboru umístěného na `%ProgramData%\NuGet\NuGetDefaults.Config` . Pokud tento konfigurační soubor určuje zdroje balíčků, výchozí zdroj balíčku nuget.org nebude zaregistrován automaticky a `NuGetDefaults.Config` místo toho budou zaregistrovány.

I když není nutné používat tuto funkci, očekáváme, že společnosti nasadí `NuGetDefaults.Config` soubory pomocí Zásady skupiny.

*Všimněte si, že tato funkce nikdy nezpůsobí odebrání zdroje balíčku z nastavení NuGet vývojáře. To znamená, že pokud vývojář již použil NuGet, a proto má registrovaný zdroj balíčku nuget.org, po vytvoření souboru se neodstraní `NuGetDefaults.Config` .*

Další informace o této funkci najdete v tématu [výchozí hodnoty konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) .

### <a name="renaming-the-default-package-source"></a>Přejmenování výchozího zdroje balíčku

NuGet vždy zaregistroval výchozí zdroj balíčku nazvaný "oficiální zdroj balíčků NuGet", který odkazuje na nuget.org. Tento název byl podrobný a zároveň neurčil, kde byl skutečně ukázán. Abychom vyřešili tyto dva problémy, přejmenovali jsme tento zdroj balíčku na jednoduše "nuget.org" v uživatelském rozhraní. Změnila se taky adresa URL pro zdroj balíčku, aby obsahovala "www". „com.microsoft.intune.mam“. Po použití NuGet 2,7 se existující "oficiální zdroj balíčku NuGet" automaticky aktualizuje na "nuget.org" jako jeho název a <https://www.nuget.org/api/v2/> jako jeho adresa URL.

### <a name="performance-improvements"></a>Zvýšení výkonu

Provedli jsme vylepšení výkonu v 2,7, což bude mít za následek menší nároky na paměť, méně využití disku a rychlejší instalaci balíčku. Provedli jsme také inteligentnější dotazy na kanály založené na OData, které omezí celkovou datovou část.

### <a name="new-extensibility-apis"></a>Nová rozhraní API pro rozšiřitelnost

Do naší služby rozšiřitelnosti jsme přidali několik nových rozhraní API, která vyplní mezery chybějících funkcí v předchozích verzích.

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

### <a name="development-only-dependencies"></a>Development-Only závislosti

Tato funkce byla vyvinuta službou [Adam petrpo](https://twitter.com/adamralph) a umožňuje autorům balíčků deklarovat závislosti, které byly použity pouze v době vývoje a nevyžadují závislosti balíčků. Přidáním `developmentDependency="true"` atributu do balíčku v nástroji `packages.config` `nuget.exe pack` již nebude tento balíček zahrnovat jako závislost.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Odebrala se podpora pro Visual Studio 2010 Express for Windows Phone.

Nový model obnovení balíčků v 2,7 je implementován novým rozhraním VSPackage, které se liší od hlavního balíčku NuGet. Z důvodu technického problému tento nový produkt VSPackage nefunguje správně v rámci sady *Visual Studio 2010 Express for Windows Phone* SKU, protože sdílíme stejný základ kódu s ostatními podporovanými SKU sady Visual Studio. Počínaje verzí NuGet 2,7 proto vynecháváme podporu sady *Visual Studio 2010 Express for Windows Phone* z publikovaného rozšíření. Podpora pro *Visual Studio 2010 Express for Web* je stále zahrnutá v primárním rozšíření publikovaném v galerii rozšíření sady Visual Studio.

Vzhledem k tomu, že si nejste jistí, kolik vývojářů v této verzi nebo edici sady Visual Studio stále používá NuGet, publikujeme samostatné rozšíření sady Visual Studio, konkrétně pro tyto uživatele a publikování na webu CodePlex (nikoli v galerii rozšíření pro Visual Studio). Neplánujeme toto rozšíření dál spravovat, ale pokud se to bude informovat, dejte nám prosím na webu CodePlex problém.

Chcete-li stáhnout správce balíčků NuGet (pro Visual Studio 2010 Express for Windows Phone), navštivte stránku se [soubory ke stažení nuget 2,7](https://nuget.codeplex.com/releases/view/107605) .

### <a name="bug-fixes"></a>Opravy chyb

Kromě těchto funkcí obsahuje tato verze NuGet také mnoho dalších oprav chyb. V této verzi byly vyřešeny 97 celkové problémy. Úplný seznam pracovních položek opravených v NuGet 2,7 najdete v [přehledu problémů NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
