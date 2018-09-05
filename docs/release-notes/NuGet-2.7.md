---
title: Zpráva k vydání verze 2.7 NuGet
description: Zpráva k vydání verze pro NuGet 2.7 včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550962"
---
# <a name="nuget-27-release-notes"></a>Zpráva k vydání verze 2.7 NuGet

[NuGet 2.6.1 pro WebMatrix poznámky](../release-notes/nuget-2.6.1-for-webmatrix.md) | [zpráva k vydání verze NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

22. srpna 2013 byla vydána NuGet 2.7.

## <a name="acknowledgements"></a>Potvrzení

Rádi bychom vám chceme poděkovat následující externí přispěvatele pro své důležité příspěvky 2.7 NuGet:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Zobrazit adresu url licence při podrobný výpis balíčky a podrobností.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) – přidání atributu developmentDependency `packages.config` a použít v příkazu balíčku obsahovat pouze balíčky runtime
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Vyhněte se duplicitním klíčem vlastnosti v příkazu pack nuget.exe.
4. [Robert Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -zvětšete velikost mezipaměti počítače na 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) – dialogové okno vyřešit NuGet zobrazující aktualizace v kartě nesprávný
    - Oprava Project.TargetFramework může mít hodnotu null v Vedoucí_projektu
    - [#3248](http://nuget.codeplex.com/workitem/3248) – oprava FindPackage/FindPackagesById SharedPackageRepository selže na neexistující ID balíčku
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) – povolení podpory pro Nomad projektu
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) – oprava nabízených příkaz selže s ukončovacím kódu 0, pokud soubor neexistuje.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -opravit chybu pomocí příkazu Add-BindingRedirect při projekt odkazuje na databázový projekt.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) – oprava chyb nuget.pack nesprávně parsování zástupných znaků v atributu "vyloučit".
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) – oprava chyb `NuGet.targets` nepředá $(Platform) nuget.exe při obnovování balíčků.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) – oprava chyby v příkazu nuget.exe balíček, který by umožnilo přidávání souborů se stejným názvem, ale jinou velikostí písmen, eventuálně výjimka "Položka už existuje".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) – vlastnost přidání verze do NetPortableProfile třídy.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) – oprava chyby NullReferenceException Pokud requireApiKey = true, ale hlavičku X-NUGET-APIKEY není k dispozici
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) – opravy NuGet.Build cíle do souboru, který bude fungovat správně v MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Výkon příkaz Restore zvýšením paralelizace

## <a name="notable-features-in-the-release"></a>Důležité funkce ve verzi

### <a name="package-restore-by-default-with-implicit-consent"></a>Obnovení balíčků ve výchozím nastavení (s implicitní souhlas)

Zavádí nový přístup k obnovení balíčků NuGet 2.7 a také na překonává hlavní mezní: souhlas obnovení balíčků je nyní ve výchozím! Kombinace nový přístup a implicitní souhlasu výrazně zjednodušuje scénáře obnovení balíčku.

#### <a name="implicit-consent"></a>Implicitní souhlas

S verzí 2.0, 2.1, 2.2, 2.5 a 2.6 NuGet uživatelé museli explicitně umožnit správci balíčků NuGet stáhnout chybějící balíčky během vytváření. Pokud svůj souhlas není explicitně dostali, a řešení, které bylo povoleno obnovení balíčku selže k sestavení, dokud uživatel měl udělení souhlasu.

Od verze NuGet 2.7, souhlasu obnovení balíčku dále ve výchozím nastavení je zároveň umožní uživatelům explicitně *Odhlásit se totiž* balíček obnovení v případě potřeby pomocí zaškrtávacího políčka v nastavení NuGet v sadě Visual Studio. Tato změna pro implicitní souhlasu ovlivní NuGet v následujících prostředích:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Nástroj příkazového řádku nuget.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Balíček automatické obnovení v sadě Visual Studio

Od verze NuGet 2.7, NuGet se automaticky stáhnout chybějící balíčky během sestavování v sadě Visual Studio, i v případě obnovení balíčku nebyla povolena explicitně pro řešení. Toto automatické obnovení balíčku se stane v sadě Visual Studio, při sestavování projektu nebo řešení, ale před vyvoláním MSBuild. To poskytuje několik významné výhody:

1. Dál budete muset použít gesto "Povolit obnovení balíčků NuGet" ve vašem řešení
1. Projekty není nutné upravovat a NuGet nebudou měnit projekt tak, aby Ujistěte se, že je povoleno obnovení balíčku
1. Obnoví všechny balíčky NuGet, včetně těch, které zahrnuté MSBuild importy pro soubory props/cíle *před* MSBuild je vyvolána, zajištění tyto vlastnosti a cíle jsou správně rozpoznány během sestavení

Chcete-li použít automatické obnovení balíčku v sadě Visual Studio, stačí provést jednu (akci palce):

1. Nezaregistrují, platí vaše `packages` složky

Existuje několik způsobů, jak vynechat, nechte vaše `packages` složky ze správy zdrojového kódu. Další informace najdete v tématu [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) tématu.

Všichni uživatelé jsou implicitně přihlášení ke službě Automatické obnovení balíčku souhlasu, můžete jednoduše odhlásit prostřednictvím nastavení Správce balíčků v sadě Visual Studio.

![Nastavení správce balíčků](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Obnovení balíčku zjednodušené z příkazového řádku

NuGet 2.7 představuje novou funkci pro nuget.exe: `nuget.exe restore`

Tento nový příkaz Obnovit umožňuje snadno obnovit všechny balíčky pro řešení pomocí jediného příkazu přijetím řešení soubor nebo složku jako argument. Kromě toho tento argument je vyjádřena, když pouze jedno řešení v aktuální složce. To znamená, že všechny následující fungovat ze složky, která obsahuje soubor řešení (MySolution.sln):

1. obnovení nuget.exe MySolution.sln
1. nuget.exe obnovení.
1. obnovení nuget.exe

Příkaz Restore bude otevřete soubor řešení a najít všechny projekty v řešení. Odtud najde `packages.config` soubory pro jednotlivé projekty a obnovení všech balíčků nalezen. Také obnoví balíčků řešení na úrovni součástí `.nuget\packages.config` souboru. Další informace o nový příkaz obnovení najdete v [Reference k příkazovému řádku](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Nový pracovní postup obnovení balíčku

S potěšením o tyto změny k obnovení balíčků, protože zavádí nový pracovní postup. Pokud chcete vynechat, nechte své balíčky ze správy zdrojových kódů jednoduše není potvrzení `packages` složky. Visual Studio, kteří otevřít a sestavit řešení se zobrazí balíčky automaticky obnoví. Pro sestavení příkazového řádku, jednoduše vyvolat `nuget.exe restore` před vyvoláním `msbuild`. Už nemusíte nezapomeňte použít gesto "Povolit obnovení balíčků NuGet" na své řešení a jsme už budete potřebovat k úpravě vaše projekty ke změně sestavení. A to také poskytuje mnohem lepší prostředí pro balíčky, které zahrnují MSBuild importy, zejména pro importy přidané prostřednictvím Nugetu pro nejnovější funkce [automatickým importem props/cíle soubory](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) ze složky \build.

Kromě práce, kterou jsme udělali sami také spolupracujeme se některé důležité partnerům zaokrouhlí tento nový přístup. Konkrétní časové osy pro některé z těchto zatím nemáme, ale je také, jak jsme se o nový přístup jednotlivých partnerů.

* Team Foundation Service - funkčnost integrace volání `nuget.exe restore` do výchozí sestavení scénáře.
* Windows Azure Web Sites – pracují aby bylo možné posunout svůj projekt do Azure a mají `nuget.exe restore` volá předtím, než vaše webová stránka je sestaven.
* TeamCity – aktualizují jejich instalačního programu NuGet modulu plug-in pro TeamCity 8.x
* AppHarbor - pracují a umožňuje tak push úložišti AppHarbor a mít `nuget.exe restore` voláno před provedením vaše řešení je sestavení.

S každou z výše uvedených partnerů by používají vlastní kopii nuget.exe a nebude potřeba provádět nuget.exe ve vašem řešení.

#### <a name="known-issues"></a>Známé problémy

Existují dva známé problémy s nuget.exe obnovení s počáteční verze 2.7, ale nebudou opraveny 9/6/2013 s aktualizací [NuGet.CommandLine balíčku](http://www.nuget.org/packages/NuGet.CommandLine/).  Tato aktualizace je také k dispozici na [stránku pro stažení NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) na webu CodePlex.  Spuštění `nuget.exe update -self` aktualizuje na nejnovější verzi.

Pevné byly:

1. [Nový balíček obnovení nebude fungovat v Mono, při použití souboru SLN](https://nuget.codeplex.com/workitem/3596)
1. [Nové obnovení balíčků nefunguje s projekty Wix](https://nuget.codeplex.com/workitem/3598)

Je také známý problém s nový pracovní postup obnovení balíčku důvěryhodných [automatické obnovení balíčků nefunguje pro projekty v rámci složky řešení](https://nuget.codeplex.com/workitem/3625). Tento problém byl vyřešen v NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Chyby a upozornění sestavení projektu mění se cílení a Upgrade

V mnoha případech po Přeorientovat nebo upgrade projektu, pro vás, nejsou některé balíčky NuGet funguje správně. Bohužel neexistuje žádná zpráva o této a nejsou k dispozici žádné pokyny o tom, jak řešit. V rámci NuGet 2.7 využíváme teď některé události aplikace Visual Studio rozpoznat jste změnilo nebo upgradovat projekt způsobem, který má vliv na nainstalované balíčky NuGet.

Pokud je zjištěno, že některý z balíčků byly ovlivněny Přeorientovat nebo upgrade, vytváříme budete okamžitě sestavení chyby s oznámením. Kromě chybě okamžité sestavení jsme také zachovat `requireReinstallation="true"` příznak ve vaší `packages.config` souboru pro všechny balíčky, které nebyly ovlivněné podle mění se cílení a každý další sestavení v sadě Visual Studio vyvolá upozornění sestavení pro tyto balíčky.

NuGet nelze provést automatickou akci k přeinstalování ovlivněné balíčky, Věříme, že toto označení a upozornění vás provedou nápovědy je zjistit, kdy je potřeba znovu nainstaluje balíčky. Pracujeme také na [balíček přeinstalace doprovodných materiálech](../consume-packages/reinstalling-and-updating-packages.md) , že tyto chybové zprávy směrovat na.

### <a name="nuget-configuration-defaults"></a>Výchozí konfigurace NuGet

Mnoho společností NuGet používají interně, ale měli obtížné provést potřebnými svého vývojáře nahrazujícím balíčku interní zdroje nuget.org. NuGet 2.7 představuje výchozí konfigurační hodnoty funkci, která umožňuje nastavit pro celý počítač výchozí hodnota:

1. Povolenému zdroji balíčků
1. Zaregistrované, ale zdroji balíčků
1. Výchozí zdroj nuget.exe nabízených oznámení

Každý z nich se teď dá nakonfigurovat v souboru umístěného v `%ProgramData%\NuGet\NuGetDefaults.Config`. Pokud tento konfigurační soubor Určuje zdroje balíčků, pak výchozí zdroj balíčku nuget.org se automaticky nezaregistruje a v `NuGetDefaults.Config` místo něj se zaregistruje.

Přestože se nevyžaduje použití této funkce, Očekáváme, že společnosti nasadit `NuGetDefaults.Config` soubory pomocí zásad skupiny.

*Všimněte si, že tato funkce se nikdy nezpůsobí zdroj balíčku, který má být odebrán z nastavení NuGet pro vývojáře. To znamená, že pokud se už používá NuGet vývojář a proto má zdroj balíčku nuget.org zaregistrovali, se neodstraní po vytvoření `NuGetDefaults.Config` souboru.*

Zobrazit [výchozí konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) Další informace o této funkci.

### <a name="renaming-the-default-package-source"></a>Přejmenování výchozí zdroj balíčku

NuGet má vždy zaregistrovaný zdroj balíčku výchozím názvem "Oficiální zdroj balíčku NuGet", který odkazuje na nuget.org. Tento název jste podrobné a je také neurčili, nevložily kde ve skutečnosti odkazuje. Pro vyřešení těchto problémů dvou, My jste přejmenovali zdroje tohoto balíčku do jednoduše "nuget.org" v uživatelském rozhraní. Adresa URL zdroje balíčku byl také změněn na zahrnují "www". Předpona. Po použití NuGet 2.7, vaše existující "oficiální zdroj balíčku NuGet" se automaticky aktualizují na "nuget.org" jako název a "<https://www.nuget.org/api/v2/>" jako její adresu URL.

### <a name="performance-improvements"></a>Zvýšení výkonu

Provedli jsme některá vylepšení výkonu v 2.7, který poskytne menší nároky na paměť, méně využití disku a rychlejší instalace balíčku. Také jsme provedli inteligentnější dotazy na informační kanály založených na protokolu OData, které se sníží celkové datové části.

### <a name="new-extensibility-apis"></a>Nové rozhraní API pro rozšiřitelnost

Jsme přidali několik nových rozhraní API pro naše služby rozšíření k vyplnění mezer chybějící funkce v předchozích verzích.

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

### <a name="development-only-dependencies"></a>Závislosti jen pro vývoj

Tato funkce byla přispěla [Adam Ralph](https://twitter.com/adamralph) a umožňuje autorům balíčků pro deklaraci závislosti, které byly použity jen na vývoj čas a nevyžadují závislosti balíčků. Přidáním `developmentDependency="true"` atribut balíčku v `packages.config`, `nuget.exe pack` bude již obsahovat tento balíček jako závislost.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Odebrat podporu pro Visual Studio 2010 Express pro Windows Phone

Nový model obnovení balíčku v 2.7 implementují nové VSPackage, která se liší od hlavního balíčku NuGet VSPackage. Kvůli technickému problému, tento nový VSPackage nebude fungovat správně v *Visual Studio 2010 Express pro Windows Phone* SKU Jaro stejného základu kódu s ostatními nepodporuje produktová SKU sady Visual Studio. Proto od verze NuGet 2.7, jsme se vyřazení podpory pro *Visual Studio 2010 Express pro Windows Phone* z publikovaných rozšíření. Podpora pro *Visual Studio 2010 Express for Web* je však stále součástí primární linka publikována do Galerie rozšíření Visual Studio.

Protože jsme nejste jistí, jak mnoho vývojářů v této verzi nebo edici sady Visual Studio stále používají NuGet, Snažíme se publikování používat samostatné rozšíření sady Visual Studio speciálně pro tyto uživatele a jeho publikování na webu CodePlex (spíše než Galerie rozšíření sady Visual Studio) . Plánujeme není nadále spravovat rozšíření, ale pokud se vás tato změna týká dejte nám vědět, můžete založením problému na webu CodePlex.

Správce balíčků NuGet stáhnout (pro Visual Studio 2010 Express pro Windows Phone), najdete v tématu [stáhne 2.7 NuGet](https://nuget.codeplex.com/releases/view/107605) stránky.

### <a name="bug-fixes"></a>Opravy chyb

Kromě těchto funkcí tato verze NuGet obsahuje také mnoho ostatní opravy chyb. Došlo k 97 celkový problémy zákazníky a vyřešené ve verzi. Úplný seznam pracovních položek opravených NuGet 2.7 prosím zobrazení [NuGet sledování problémů pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
