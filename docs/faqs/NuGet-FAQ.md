---
title: NuGet – nejčastější dotazy
description: Běžné otázky a odpovědi na příkazovém řádku a v sadě Visual Studio pomocí nástroje NuGet a práci v galerii NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 01/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1c838116f9737b01ea3f9ca17f5d5002f6548044
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196210"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet – nejčastější dotazy

**Co je potřeba spuštěním rozšíření NuGet?**

Všechny informace týkající se uživatelského rozhraní a nástroje příkazového řádku jsou k dispozici v [Instalační příručka](../install-nuget-client-tools.md).

**Podporuje NuGet Mono?**

Nástroj příkazového řádku `nuget.exe`, sestavení a běží pod Mono 3.2 + a můžete vytvořit balíčky v Mono.

I když `nuget.exe` funguje plně na Windows, dochází ke známým problémům v Linuxu a OS X. naleznete [Mono vydá](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na Githubu.

A [grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.

**Jak zjistím obsah balíčku a zda je stabilní a užitečné pro mé aplikace?**

Primární zdroj informací o balíčku je její stránce na nuget.org (nebo jiný privátní kanál). Každou stránku balíčků na nuget.org obsahuje popis balíčku, historie verzí a statistiky o využití. **Informace** oddíl na stránce balíček pro také obsahuje odkaz projekt webové stránky, kdy obvykle najít mnoho příkladů a další dokumentaci, která vám pomůže se naučit, jak se používá balíček.

Další informace najdete v tématu [hledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet v sadě Visual Studio

**Jak se v různých produktů Visual Studio podporuje NuGet?**

- Visual Studio na Windows podporuje [uživatelské rozhraní Správce balíčků](../tools/package-manager-ui.md) a [Konzola správce balíčků](../tools/package-manager-console.md).
- Visual Studio for Mac obsahuje integrované funkce NuGet, jak je popsáno na [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (všechny platformy) nemá žádné přímé integraci NuGet. Použití [rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md) nebo [rozhraní příkazového řádku dotnet](../tools/dotnet-commands.md).
- Poskytuje Azure DevOps [kroku sestavení pro obnovování balíčků NuGet](/vsts/build-release/tasks/package/nuget). Můžete také [privátní balíček NuGet hostitele kanálů na Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Jak můžu ověřit přesnou verzi, které jsou nainstalované nástroje NuGet?**

V sadě Visual Studio, použijte **Nápověda > o Microsoft Visual Studio** příkazů a podívejte se na verzi vedle položky **Správce balíčků NuGet**.

Alternativně spusťte konzolu Správce balíčků (**nástroje > Správce balíčků NuGet > Konzola správce balíčků**) a zadejte `$host` zobrazíte informace o systému NuGet, včetně verze.

**Jaké programovací jazyky podporují NuGet?**

NuGet obecně se dá použít pro jazyky .NET a je určený pro přenesení do projektu knihovny .NET. Vzhledem k tomu, že v některých typech projektů podporuje také automatizaci MSBuild a sadě Visual Studio, podporuje také dalších projektů a jazyky na různých úrovních.

Podporuje nejnovější verzi balíčku nuget C#, Visual Basic, F#, WiX a C++.

**Jaké šablony projektů podporuje NuGet?**

NuGet má plnou podporu pro širokou škálu šablony projektu, jako je Windows, Web, Cloud, SharePoint, Wix a tak dále.

**Jak můžu aktualizovat balíčky, které jsou součástí šablony sady Visual Studio?**

Přejděte na **aktualizace** kartu v Uživatelském rozhraní Správce balíčků a vyberte **Aktualizovat vše**, nebo použijte [ `Update-Package` příkaz](../tools/ps-ref-update-package.md) z konzoly Správce balíčků.

Pokud chcete aktualizovat samotné šablony, budete muset ručně aktualizovat úložiště šablon. Zobrazit [Xavier Decoster blogu](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) k tomuto tématu. Protože ruční aktualizace může dojít k poškození šablony Pokud nejnovější verze všechny závislosti nejsou navzájem kompatibilní, mějte na paměti, že to se provádí na vaše vlastní nebezpečí.

**Můžete použít balíček NuGet mimo sadu Visual Studio?**

Ano, NuGet pracuje přímo z příkazového řádku. Zobrazit [Instalační příručka](../install-nuget-client-tools.md) a [odkaz na rozhraní příkazového řádku](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>NuGet příkazového řádku

**Jak získat nejnovější verzi nástroje příkazového řádku NuGet?**

Zobrazit [Instalační příručka](../install-nuget-client-tools.md).

**Co je licence pro nuget.exe?**

Jste oprávněni nuget.exe podle podmínek licence MIT znovu distribuovat. Zodpovídáte za aktualizace a údržba všechny kopie nuget.exe, které chcete znovu distribuovat.

**Je možné rozšířit nástroje příkazového řádku NuGet?**

Ano, je možné přidat vlastní příkazy `nuget.exe`, jak je popsáno v [Rob Reynold příspěvek](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konzola správce balíčků NuGet (Visual Studio na Windows)

**Jak získat přístup k objektu DTE v konzole Správce balíčků**

Objekt nejvyšší úrovně v objektovém modelu automatizace sady Visual Studio se nazývá objekt DTE (Development Tools Environment). Konzole vám tohle všechno poskytuje prostřednictvím proměnné s názvem `$DTE`. Další informace najdete v tématu [přehled modelu automatizace](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci k rozšiřitelnosti sady Visual Studio.

**Můžu zkusit přetypovat $DTE proměnnou typu DTE2, ale se zobrazí chyba: Nelze převést hodnotu "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" typ "EnvDTE80.DTE2". Co je?**

Jde o známý problém s interakci Powershellu pomocí objektu COM. Vyzkoušejte následující postup:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` pomocná funkce přidal hostitele prostředí NuGet PowerShell.

## <a name="creating-and-publishing-packages"></a>Vytvoření a publikování balíčků

**Jak se seznam Můj balíček v informačním kanálu?**

Zobrazit [vytváření a publikování balíčku](../quickstart/create-and-publish-a-package.md).

**Mám k dispozici více verzí knihovny, které cílí různé verze rozhraní .NET Framework. Jak vytvořit jeden balíček, který to podporuje?**

Zobrazit [podporuje více verzí rozhraní .NET Framework a profily](../create-packages/supporting-multiple-target-frameworks.md).

**Nastavení vlastní úložiště nebo informačního kanálu**

Zobrazit [hostování balíčků přehled](../hosting-packages/overview.md).

**Jak můžete nahrát balíčky do mé NuGet kanálu hromadně?**

Zobrazit [hromadně publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Práce s balíčky

**Jaký je rozdíl mezi balíčkem na úrovni projektu a balíček řešení úrovni?**

Balíček řešení úrovni (NuGet 3.x+) se nainstaluje pouze jednou v řešení a je pak k dispozici pro všechny projekty v řešení. Na úrovni projektu balíček je nainstalován v každém projektu, která ji používá. Balíček úrovni řešení může být také nainstalovat nové příkazy, které může být volána z konzoly Správce balíčků.

**Je možné nainstalovat balíčky NuGet bez připojení k Internetu?**

Ano, najdete v příspěvku blogu Scotta Hanselmana [jak získat přístup k NuGet, když nuget.org je mimo provoz (nebo jste palubě)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Jak nainstalovat balíčky v jiném umístění z výchozí složku balíčků?**

Nastavte [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` pomocí `nuget config -set repositoryPath=<path>`.

**Jak se můžu vyhnout přidávání složce balíčků NuGet do správy zdrojových kódů?**

Nastavte [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) v `Nuget.Config` k `true`. Tento klíč funguje v řešení úrovni a proto je potřeba přidat do `$(Solutiondir)\.nuget\Nuget.Config` souboru. Povolení obnovení balíčku ze sady Visual Studio automaticky vytvoří tento soubor.

**Jak můžu vypnout obnovení balíčků?**

Zobrazit [povolení a zákaz obnovení balíčku](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Proč se zobrazí zpráva "Nelze přeložit došlo k chybě závislosti" při instalaci místního balíčku se vzdálených závislostí?**

Je nutné vybrat **všechny** zdroje při instalaci místního balíčku do projektu. To agreguje všechny kanály místo jen jeden. Důvod se zobrazí tato chyba je, že uživatelé z místního úložiště se často chcete zabránit náhodnému instalace vzdálených balíčků z důvodu firemní zásady.

**Mám několik projektů ve stejné složce, jak můžete použít soubory samostatného souboru packages.config pro každý projekt?**

Ve většině projektů, ve kterém live samostatné projekty do samostatné složky, to není problém protože identifikuje NuGet `packages.config` soubory v každém projektu. Nuget 3.3 + a více projektů ve stejné složce, můžete vložit název projektu do `packages.config` názvy souborů použijte vzor `packages.{project-name}.config`, a tento soubor používá NuGet.

To není problém při používání PackageReference, protože každý soubor projektu obsahuje vlastní seznam závislostí.

**Nevidím v seznamu úložišť v nuget.org, jak to můžu získat zpátky?**

- Přidat `https://api.nuget.org/v3/index.json` do seznamu zdrojů, nebo
- Odstranit `%appdata%\.nuget\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a nechat NuGet znovu vytvořit.

**Co jsou výchozí licenční podmínky Pokud balíček neobsahuje konkrétní informace o licencích?**

Každý balíček se řídí podmínkami, které jsou součástí balíčku. Přečtěte si před přístupem k, stahování nebo získání všechny balíčky, které příslušné podmínky. Na nuget.org, použijte **informace o licenci** odkaz na stránce balíček.

Pokud balíček neurčuje licenční podmínky, obraťte se přímo pomocí vlastníka balíčku **obraťte se na vlastníky** odkazu na stránce balíček pro nuget.org. Společnost Microsoft není licence duševního vlastnictví, od poskytovatelů třetích stran balíček a neodpovídá za informace, které jsou poskytovány třetími stranami.

## <a name="managing-packages-on-nugetorg"></a>Správa balíčků na NuGet.org

**Můžete upravit po je nahraná metadata balíčků?**

NuGet doporučuje podepsat všechny balíčky. Princip návrhu podpisu balíčku je, že je podepsaný balíček obsahu neměnný, což zahrnuje soubor nuspec. Úpravy metadat balíčku výsledkem změny do souboru nuspec, proto už není platná existující podpisy. Doporučujeme, abyste úpravy stávajících pracovních postupů, aby nebyl vyžadován upravovat metadata balíčku po vytvoření balíčku.

Všimněte si, že závislostí uvedených pro váš balíček se generují automaticky z balíčku samotného a nelze jej upravit.

Kromě toho nahrání balíčků [int.nugettest.org](https://int.nugettest.org) je skvělý způsob, jak otestovat a ověřit váš balíček přitom balíček k dispozici ve veřejné galerii. Koncový bod rozhraní API: https://apiint.nugettest.org/v3/index.json

**Můžete odstranit balíček publikovány na NuGet.org?**

Odstranění balíčku publikují do NuGet.org obecně nepodporujeme. Další informace o našich [zásady týkající se odstraněním balíčků](../policies/deleting-packages).

**Je možné rezervovat názvy balíčků, které se publikují v budoucnosti?**

Ano. ID můžete vyhradit pro balíčky na [nuget.org](https://www.nuget.org/) vyžádáním předponu ID balíčku pro váš účet. Aby bylo možné požádat o předponu ID balíčku, postupujte podle pokynů [dokumentaci](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Jak uplatním nárok na vlastnictví pro balíčky?**

Zobrazit [vlastníky Správa balíčků na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Jak zacházet s vlastníka balíčku, který porušuje licence na software**

Doporučujeme komunity NuGet spolupráce řešení všech sporů, které mohou vzniknout mezi vlastníky balíčku a vlastníci dalšího softwaru. Jsme vytvořený [spor proces překladu](../policies/dispute-resolution.md) dodržovat před položením správcům nuget.org intercede.

**Je doporučeno uložit Moje testovací balíčky nuget.org?**

Pro účely testování můžete použít [int.nugettest.org](https://int.nugettest.org), nebo jako alternativní veřejné servery NuGet [webu myget.org](https://myget.org) nebo [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Všimněte si, že nemusí být zachována balíčky nahráli do int.nugettest.org.

**Jaká je maximální velikost balíčky, které můžu nahrát do nuget.org?**

nuget.org umožňuje balíčky až 250MB, ale My doporučujeme udržování balíčky v části 1MB. Pokud je to možné a používání závislosti, které balíčky se propojují. Balíčky jako říci, obsahovat pouze jedno sestavení pro zabránění kolizím.

Stáhnout balíčky, takže větší balíčky mají vyšší pravděpodobnost selhání instalace, než menších NuGet pomocí protokolu HTTP.

Je možné sdílet závislosti mezi více balíčků zmenšit celková stahovaná velikost spotřebitelé vaše balíčky NuGet.

Závislosti jsou většinou statická a nikdy změnit. Pokud opravujete chybu v kódu, závislosti nemusí aktualizovat. Pokud seskupíte závislosti, skončíte reshipping pokaždé, když větší balíčky. Rozdělením balíčky NuGet na související závislosti jsou mnohem podrobnějšího pro spotřebitele balíčku upgradu.

## <a name="nugetorg-not-accessible"></a>není k dispozici nuget.org

**Proč nejde stáhnout balíčky z nebo nahrání balíčků na nuget.org?**

Nejprve ujistěte se, že používáte nejnovější verze nugetu. Pokud tuto verzi ani potom nedaří, [obraťte se na podporu](https://www.nuget.org/policies/Contact) a poskytují další připojení, řešení potíží s informací, včetně:

- Verze balíčku nuget, které používáte
- Zdroje balíčků, které používáte
- Obnovení protokolu s podrobnou úroveň podrobností
- MTR nebo trasování Fiddler (viz níže)
- Zeměpisné oblasti
- Určuje, zda váš počítač není za proxy nebo brány firewall?
- Je váš počítač umístěný v datovém centru poskytovatelů cloudu (Azure, AWS atd.)? Pokud ano, zadejte prosím název poskytovatele a oblast.

*K zachycení MTR:*

- Stáhněte si WinMTR z [http://winmtr.net/download/](http://winmtr.net/)
- Zadejte `api.nuget.org` jako název hostitele a klikněte na **Start**.
- Počkejte, dokud **odeslané** je sloupec > = 100.

    ![Zachytávání MTR](media/mtr.png)

- Zkopírování textu do schránky.

*K zachycení Fiddleru:*

- Nainstalujte nejnovější verzi [Fiddler](http://www.telerik.com/download/fiddler).
- Spusťte aplikaci Fiddler a zakázat zachytávání provozu pomocí **soubor > Capture Traffic** nabídky.
- Odebrat všechny relace (vybrat všechny položky v seznamu, stiskněte **odstranit** klíč).
- Konfigurace aplikace Fiddler k zachycení přenosy HTTPS tak, že zkontrolujete **přenosy HTTPS dešifrovat** v **HTTPS** karty **nástroje > Možnosti Fiddleru...**  nabídky.
- Zavřete Visual Studio.
- Povolit **soubor > Capture Traffic** nabídky.
- Spusťte Visual Studio nebo nuget.exe .exe a provádět akce, které nefungují. Přenosy generované tyto akce by měla objevoval ve Fiddleru.
- Po spuštění akce, které mají používat **soubor > Uložit > všechny relace** k uložení zaznamenané relace.

Poznámka: to může být nutné nastavit `HTTP_PROXY` proměnnou prostředí, aby `http://127.0.0.1:8888` za směrování přenosů NuGet pomocí Fiddleru.

Pokud se to nepodaří, zkuste [tipy uvedených v tomto příspěvku na StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="what-is-the-api-endpoint-for-nugetorg"></a>Co je koncový bod rozhraní API pro nuget.org?

Pokud chcete použít jako úložiště balíčků s klienty NuGet nuget.org, měli byste použít následující koncový bod rozhraní API V3: 

**`https://api.nuget.org/v3/index.json`**

Starší klienti stále může použít protokol V2 k dosažení nuget.org. Nicméně nezapomeňte prosím, že klienti NuGet 3.0 nebo vyšší budou mít nižší a méně spolehlivé služby pomocí protokolu V2:

`https://www.nuget.org/api/v2` (NEPOUŽÍVANÉ). **Poznámka:** použijte "www". pro nejlepší spolehlivost.

## <a name="nugetorg-account-management"></a>Správa účtů nuget.org

### <a name="how-to-create-a-new-nugetorg-account"></a>Jak vytvořit nový účet nuget.org?

Pokud chcete vytvořit účet nuget.org, potřebujete osobní účet Microsoft (MSA) nebo účet Azure Active Directory (AAD). Pokud nemáte, můžete si [vytvořit](https://signup.live.com) jeden. Pokud máte účet MSA nebo AAD, postupujte podle následujících kroků.
1. Přejděte [nuget.org přihlašovací stránku](https://www.nuget.org/users/account/LogOn).
1. Klikněte na **přihlásit se účtem Microsoft** tlačítko.
1. Zadejte podrobnosti o účtu MSA nebo AAD.
1. Přijměte prosím oprávnění k *NuGet.org* aplikace.
1. Budete přesměrováni na nuget.org a zobrazí výzva k registraci uživatelské jméno.
1. Zadejte uživatelské jméno do vstupního pole. Pamatujte, že uživatelské jméno **je** malá a velká citlivé a nedá se změnit nebo přejmenovat později.
1. Klikněte na **zaregistrovat** tlačítko.

Teď máte účet nuget.org. Můžete na operaci správy účtů [nastavení účtu](https://www.nuget.org/account) stránky.

### <a name="how-to-recover-nugetorg-password-login"></a>Jak obnovit heslo přihlášení nuget.org?

Pamatujte, že [nebyly vyřazeny nuget.org heslu](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) a jediný způsob, jak se přihlásit do nuget.org se pomocí osobního účtu Microsoft (MSA) nebo účet Azure Active Directory (AAD). Ale v případě, že nelze získat přístup k vaší přidružené účty MSA nebo AAD můžete potřebovat pro použití přihlášení k heslo pro obnovení účtu nuget.org. V takovém případě postupujte podle následujících kroků.
- **Požadavek:** Musíte mít přístup k e-mailu, který je přidružen k účtu, pro kterou je potřeba obnovit heslo.
- Přejděte [stránka zapomenuté heslo](https://www.nuget.org/account/ForgotPassword)
- Zadejte **e-mailu** adresu, která je přidružená k účtu nuget.org, které chcete obnovit.
- Klikněte na tlačítko **odeslat** tlačítko.
- Zobrazí se e-mailu pro účet zadané e-mailové adresy se odkaz na resetování hesla. Klikněte na tento odkaz a nastavte nové heslo. Pokud nemůžete najít e-mailu Zkontrolujte složku s "nevyžádanou poštou".
- Až budete hotovi, můžete teď přihlásit se pomocí uživatelského jména a hesla na webu NuGet.
- Chcete-li se přihlásit pomocí uživatelského jména a hesla, použijte **přihlaste pomocí účtu Nuget.org** odkaz na [nuget.org přihlašovací stránku](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Který účet Microsoft je propojený s účtem Moje nuget.org?

Pokud jste zapomněli účtu Microsoft, který je přidružen k vašemu účtu nuget.org, postupujte podle kroků níže a vyžádejte si pomoc.
1. Přejděte na [nuget.org přihlašovací stránku](https://www.nuget.org/users/account/LogOn) a klikněte na **potřebujete pomoc s přihlášením?** odkaz.
1. To se seznámíte místním dialogovém žádostí o pomoc. Postupujte podle kroků v tomto dialogovém pochopit přidružené účty Microsoft pro váš účet nuget.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Jak změnit účet Microsoft, které používám pro přihlášení nuget.org?
Pokud chcete změnit účet Microsoft pro uživatele nuget.org, použijte následující postup. Umožňuje Dejme tomu, že váš účet Microsoft s e-mailem `account1@outlook.com` souvisí s vaším účtem nuget.org s uživatelským jménem `MyNuGetAccount`. Chcete změnit přihlášení do jiného účtu Microsoft s e-mailem `account2@outlook.com`
1. Přihlaste se prosím pomocí **aktuálně přiřazen účet Microsoft** tedy `account1@outlook.com` na [přihlašovací stránku](https://www.nuget.org/users/account/LogOn) po kliknutí na tlačítko **přihlásit se účtem Microsoft**.
1. Po přihlášení, přejděte k vaší [nastavení účtu](https://www.nuget.org/account) stránky.
1. Rozbalte v části **přihlašovací účet**. Klikněte na **změnit účet** tlačítko.
1. Nyní budou přesměrováni na přihlašovací stránku Microsoftu. Přihlaste se prosím pomocí účtu, který chcete změnit přidružení tedy `account2@outlook.com`. **Poznámka:**: možná budete muset kliknout na **přihlásit na více instancí a přihlaste se pomocí jiného účtu** během tok pro přihlašování k nebudou moct přihlásit s jiným účtem Microsoft.
1. Pokud se zobrazí chyba podobná níže uvedenému příkladu naleznete v tématu [účet Microsoft je propojený s jiným účtem nuget.org](#microsoft-account-is-linked-with-another-nugetorg-account) další podrobnosti.
    >_Nepovedlo se aktualizovat účet Microsoft s "obchodní vztah 2 <account2@outlook.com>". K tomu může dojít, pokud je už propojený s jiným účtem NuGet. Další informace, obraťte se na podporu._

1. Až se úspěšně se pomocí svého druhého účtu, budete přesměrováni zpět na stránku nastavení účtu nuget.org a měli byste vidět nový účet Microsoft spojený jako přihlašovací účet. Do budoucna můžete používejte tento účet při přihlašování do nuget.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Účet Microsoft je propojený s jiným účtem nuget.org.

Pokud se při změně vaše přihlašovací údaje Microsoft viděli následující chyba:
> _Nepovedlo se aktualizovat účet Microsoft s "obchodní vztah 2 <account2@outlook.com>". K tomu může dojít, pokud je už propojený s jiným účtem NuGet. Další informace, obraťte se na podporu._

Dejme tomu, že jste se pokoušeli změnit Microsoft vám umožňuje účtu přihlášení z `account1@outlook.com` nuget.org uživatele s uživatelským jménem `MyNuGetAccount1` do jiného účtu Microsoft s e-mailem `account2@outlook.com`. A zobrazí výše uvedenou chybu.

**Co znamená výše uvedenou chybu?**

Znamená to, že je jiný účet nuget.org, který je přidružen k účtu Microsoft, že se pokoušíte změnit tak, tedy v nad příklad účet Microsoft s e-mailu `<account2@outlook.com>` je spojen s jiným účtem nuget.org se například uživatelské jméno `MyNuGetAccount2`.

Nelze změnit přidružený přihlášení pomocí účtu Microsoft, který je propojený s účtem různé nuget.org.

**Nemohu si vzpomenout, že jsem měl jiný účet nuget.org, jak zjistím účtu nuget.org, který se jedná?**

Přihlaste se pomocí druhého účtu Microsoft na [přihlašovací stránku](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "přihlašovací stránku"). To se můžete přihlásit na nuget.org účet, který je teď přidružená druhého účtu Microsoft. Pak můžete zobrazit nahrané balíčků a provádět správu účtu na tento účet.

**Můžu nezáleží na tento druhý účet nuget.org, chci změnit přihlašovací údaje pro první účet nuget.org pomocí druhého účtu Microsoft. Co mám dělat?**

Pokud budete chtít není záleží druhého účtu nuget.org a stále chcete znovu použít přidružený účet Microsoft s e-mailem `account2@outlook.com`. 

Přidružení účtu Microsoft a nuget.org účtu můžete uvolnit tak, že odstraníte účet nuget.org.
1. Uvedený postup [odstranit uživatele](#how-to-delete-my-nugetorg-account) druhého účtu nuget.org `MyNuGetAccount2`. 
1. Jakmile tento účet je odstraněn, můžete opakovat postup [změnit přihlášení k účtu Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Počkejte, nezajímá tento druhý účet příliš. Můžu nechcete přijít o tento účet ale změnit Moje přihlašovací jména k souvisejícím účtům pro první účet.**

Budete muset vytvořit/použít jiného účtu Microsoft, například s e-mailem `account3@outlook.com`. 
1. Nejdřív byste se měli přihlásit se pomocí svého druhého účtu Microsoft, `account2@outlook.com` na nuget.org. Postupujte podle výše uvedené kroky a změnit přidružené přihlašovací údaje a přidružit třetí účet Microsoft s tímto účtem nuget.org.
1. Až to bude hotové, druhý účtu Microsoft s e-mailem `account2@outlook.com` je zdarma chcete přidružit k účtu první nuget.org `MyNuGetAccount1`. Postupujte podle stejných kroků výše, chcete-li změnit přihlašovací údaje microsoft druhého účtu Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Přihlášení pomocí účtu Microsoft ukáže se, že synchronizuji si e-maily z je propojená s jiným účtem Microsoft
Pokud jste se pokusili přihlaste pomocí svého účtu Microsoft, například s e-mailem `account1@outlook.com` a zobrazit chyba podobná níže uvedenému příkladu:
> _Účet s e-mailu "account1@outlook.com" je propojený s jiným účtem microsoft._
>
> _Pokud chcete aktualizovat propojeným účtem Microsoft, že můžete tak učinit na stránce nastavení účtu._

**Co znamená výše uvedenou chybu?**

Při vytvoření účtu na nuget.org je přidružený k tomuto účtu komunikace e-mailovou adresu. To je obvykle stejné jako e-mailovou adresu, která slouží k souvisejícímu účtu Microsoft. Ale můžete se rozhodnout zadejte jinou e-mailovou adresu pro komunikaci. Proto technicky vzato můžete mít různé Microsoft account, Řekněme, že se `account2@outlook.com` , který je propojený s účtem nuget.org s komunikace e-mailovou adresu jako `account1@outlook.com`.

Takže výše uvedená chyba znamená, že už existuje účet nuget.org komunikace e-mailovou adresou `account1@outlook.com` je spojen s jiným účtem Microsoft s e-mailem, ale **, který není** `account1@outlook.com`.

**Jak zjistím, které společnost Microsoft k tomuto účtu nuget.org je propojený účet?**

Měli byste použít [přihlášení potřebujete pomoc](#which-microsoft-account-is-linked-to-my-nugetorg-account) toku můžete zjistit, který účet Microsoft je propojený s účtem nuget.org s e-mailovou adresu `account1@outlook.com`.

**Chcete přepsat tento účet pomocí účtu Microsoft**

Postupujte podle kroků v [nelze pro použití přihlášení k Microsoftu, jak obnovit svůj účet nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) části postupu přidružte svůj účet Microsoft s existujícím účtem nuget.org.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Nelze pro použití přihlášení k Microsoftu, jak obnovit svůj účet nuget.org?

Pokud jste se pokusili pomocí [přihlášení pomoc](#which-microsoft-account-is-linked-to-my-nugetorg-account) a nemáte přístup k účtu Microsoft, který je spojen s vaším účtem nuget.org, postupujte podle následujících kroků, abyste propojit nový účet Microsoft se svým účtem nuget.org.
1. **Požadavek**: Budete potřebovat přístup k účtu Microsoft (což není přidružené žádné existující účty nuget.org). Pokud nemáte, můžete si [vytvořit](https://signup.live.com) jeden.
2. Postupujte podle [postupů k obnovení vašeho hesla přihlášení](#how-to-recover-nugetorg-password-login), pokud jste nastavili heslo přihlášení, tento krok přeskočit.
3. [Přihlaste se k nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) pomocí přihlášení uživatelského jména a hesla.
4. Po přihlášení, zobrazí se dialogové okno automaticky otevírané okno zobrazit až podobná níže uvedenému příkladu. Toto je dialogové okno heslo přerušení.
5. **POZNÁMKA:**: Ignorujte podle pokynů k přihlášení pomocí zadaného účtu Microsoft. Teď můžete propojit účet nuget.org pro další přihlášení společnosti Microsoft.
6. Klikněte na tlačítko **přihlásit se účtem Microsoft** a přihlaste se pomocí účtu Microsoft, že máte přístup do, jak je uvedeno v kroku 1.
7. Váš účet bude nyní propojen nový účet Microsoft, který můžete použít k přihlášení do nuget.org do budoucna.

    ![Dialogové okno MSA odkaz](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Jak transformovat nuget.org účet organizace?

Pokud chcete transformovat váš účet organizace, a tento účet je již přidružen přihlašovací údaje účtu Microsoft, postupujte podle kroků uvedených v dokumentaci k [organizace v organizaci nuget](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org).

Pokud však nuget.org účtu není přidružené nebo propojených s účtem Microsoft, můžete podle následujících pokynů pro transformaci tento účet organizace.
1. **Požadavek**: Musíte mít samostatný účet prvním vytvoření na nuget.org se použije jako správce účtu organizace. Pokud nemáte, [vytvořit nový účet nuget.org](#how-to-create-a-nugetorg-account)
2. Postupujte podle [postupů k obnovení vašeho hesla přihlášení](#how-to-recover-nugetorg-password-login) pro váš účet nuget.org, pokud nemáte přihlašovací heslo pro něj, pokud, tento krok přeskočit.
3. [Přihlaste se k nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) pomocí přihlášení uživatelského jména a hesla.
4. Po přihlášení, zobrazí se dialogové okno automaticky otevírané okno zobrazit až podobná níže uvedenému příkladu. Toto je dialogové okno heslo přerušení. 
    > [!Important]
    > Ignorovat toto dialogové **nejsou** klikněte na **přihlásit se účtem microsoft** tlačítko.

5. Přejděte do [ (Nastavení)https://www.nuget.org/account/transform](https://www.nuget.org/account/transform) (Integrace a služby). To vám umožní převést účet nuget.org organizací bez propojení s účtem Microsoft.
6. Zadejte uživatelské jméno správce pro váš účet osobní nuget.org/účet, který jste vytvořili v kroku 1.
7. Postupujte podle pokynů k dokončení transformace tento účet organizace.

    ![Dialogové okno MSA odkaz](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>pro účty AAD pomocí nespravovaného tenanta vydá nuget.org přihlášení?

Pokud se zobrazí chyba typu pod během přihlášení tok s vaši e-mailovou doménu účtu (@yourdomain.com), najdete v článku kroků k obnovení vašeho účtu nuget.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Co je tuto věc nespravovaném stavu během přihlašování? A proč se to děje nyní?** 

Váš účet zdá se, že dříve zaregistrován jako osobní účet Microsoft a fungovaly správně, ale teď to vypadá jako váš účet zaregistrovaný jako tenanta služby "Nespravovaného" ve službě Azure Active Directory (identity službu, která používáme k ověření Účet Microsoft). 

To by mohlo dojít, pokud vy nebo někdo z vaší organizace (s @yourdomain.com e-mailová adresa) zaregistrovaný jedním ze služby AAD integrované nebo nebyla [Samoobslužná registrace do služby Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), například vytváří " Nespravované"tenanta pro doménu používá účet Microsoft (@yourdomain.com ve vašem případě). 

**Co mám dělat obnovit svůj účet?**

V tuto chvíli není pro nás (nuget.org) způsob ověřování účtů pomocí takové "Nespravovaného" tenanta účty ve službě Azure Active directory. Chceme lepší způsob, jak ověřovat tyto účty.

Pokud chcete k přihlášení do nuget.org se svým účtem Microsoft (@yourdomain.com), můžete (nebo správcem ve vaší společnosti) bude muset nárokovat vlastnictví AAD provedením ověření DNS k ověřování uživatelů pomocí e-mailovou adresu "@yourdomain.com". Postupujte podle kroků pro [převzetí správce domény](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) zdokumentované v Azure Active directory. Až to uděláte, běžné přihlašovací měly začít fungovat.

**Nechci se nyní udělat všem, co je další způsob, jak obnovit svůj účet?**

Je možné [vytvořit](https://www.microsoft.com/en-us/account) nový účet Microsoft (s e-mailu **není** přidružené @yourdomain.com). Postupujte podle kroků uvedených v [obnovení vašeho účtu nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) oddílu.

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Změna Moje uživatelské jméno účtu nuget.org

Nemůžete. Jak zásady jsme neumožňuje změnu ještě v úložišti uživatelských jmen. Chcete-li vytvořit nový účet s požadované uživatelské jméno je jediný způsob, jak změnit svoje uživatelské jméno. Doporučujeme vám odstranit stávajícího účtu před vytvořením nového, v opačném případě nebude možné opakovaně používat zaregistrovaným účtem Microsoft.
> [!Important]
> Odstraňuje se uživatel bude stále **rezervovat** `username`. Nebude moct znovu použít stejné uživatelské jméno a **jedná se o změnu písmen**. Jako příklad: Pokud jste vytvořili uživatele s uživatelským jménem `mycoolname` a vy chcete změnit tuto hodnotu na `MyCoolName`(změny se velká a malá písmena), nebude možné po odstranění uživatele.

Postupujte podle kroků uvedených v [odstranění účtu nuget.org](#how-to-delete-my-nugetorg-account) oddílu a [zaregistrovat nový účet](#how-to-create-a-new-nugetorg-account) s správné uživatelské jméno.

### <a name="how-to-delete-my-nugetorg-account"></a>Jak odstraním svůj účet nuget.org?

Chcete-li odstranit svůj účet, mějte prosím na paměti, že vám doporučujeme převést vlastnictví všechny balíčky, kde jste jediným vlastníkem. Další informace o [Správa vlastníků balíčku](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) o tom, jak to udělat. To vám také pomůže nám ohledně urychlení jejich zpracování vaší žádosti.

> [!Important]
> Odstraňuje se uživatel bude mít za následek následující:
>  1. Odvolat přidružené klíče rozhraní API. 
>  2. Tento účet odeberte jako vlastníka pro všechny balíčky, které podřízené.
>  3. Zrušit přidružení všechny dříve existující rezervace předpony ID, pomocí tohoto účtu.
>  4. Odeberte účet členem jakékoli organizace.
>  5. Vaše uživatelské jméno se vyhradí a nebude moci znovu jeho použití znovu bez naše oprávnění.

Postupujte podle následujících kroků a pokračujte odstranění účtu.
1. [Přihlaste se k nuget.org](https://www.nuget.org/users/account/LogOn) pomocí účtu, který chcete odstranit.
2. Klikněte na tuto adresu url: [ https://www.nuget.org/account/delete ](https://www.nuget.org/account/delete) a postupujte podle pokynů k odeslání žádosti o odstranění účtu.

Naše Zákaznická podpora bude tento požadavek zpracovat a provést odstranění účtu.
