---
title: NuGet – nejčastější dotazy
description: Běžné otázky a odpovědi na příkazovém řádku a v sadě Visual Studio pomocí nástroje NuGet a práci v galerii NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: 8c63abc9971623e0732ae8d973fafcd04c5d9f48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548801"
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
- Visual Studio Team Services poskytuje [kroku sestavení pro obnovování balíčků NuGet](/vsts/build-release/tasks/package/nuget). Můžete také [privátní balíček NuGet hostitele informační kanály ve službě Team Services](https://www.visualstudio.com/docs/package/nuget/publish).

**Jak můžu ověřit přesnou verzi, které jsou nainstalované nástroje NuGet?**

V sadě Visual Studio, použijte **Nápověda > o Microsoft Visual Studio** příkazů a podívejte se na verzi vedle položky **Správce balíčků NuGet**.

Alternativně spusťte konzolu Správce balíčků (**nástroje > Správce balíčků NuGet > Konzola správce balíčků**) a zadejte `$host` zobrazíte informace o systému NuGet, včetně verze.

**Jaké programovací jazyky podporují NuGet?**

NuGet obecně se dá použít pro jazyky .NET a je určený pro přenesení do projektu knihovny .NET. Vzhledem k tomu, že v některých typech projektů podporuje také automatizaci MSBuild a sadě Visual Studio, podporuje také dalších projektů a jazyky na různých úrovních.

Nejnovější verzi balíčku nuget podporuje C#, Visual Basic, F #, WiX a C++.

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

**Můžu zkusit přetypovat $DTE proměnnou typu DTE2, ale se zobrazí chyba: nelze převést hodnotu "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" typ "EnvDTE80.DTE2". Co je?**

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

## <a name="managing-packages-on-nugetorg"></a>Správa balíčků na nuget.org

**Můžete upravit po je nahraná metadata balíčků?**

NuGet doporučuje podepsat všechny balíčky. Princip návrhu podpisu balíčku je, že je podepsaný balíček obsahu neměnný, což zahrnuje soubor nuspec. Úpravy metadat balíčku výsledkem změny do souboru nuspec, proto už není platná existující podpisy. Doporučujeme, abyste úpravy stávajících pracovních postupů, aby nebyl vyžadován upravovat metadata balíčku po vytvoření balíčku.

Všimněte si, že závislostí uvedených pro váš balíček se generují automaticky z balíčku samotného a nelze jej upravit.

Kromě toho nahrání balíčků [staging.nuget.org](http://staging.nuget.org) je skvělý způsob, jak otestovat a ověřit váš balíček přitom balíček k dispozici ve veřejné galerii.

**Je možné rezervovat názvy balíčků, které se publikují v budoucnosti?**

Ano. ID můžete vyhradit pro balíčky na [nuget.org](https://www.nuget.org/) vyžádáním předponu ID balíčku pro váš účet. Aby bylo možné požádat o předponu ID balíčku, postupujte podle pokynů [dokumentaci](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Jak uplatním nárok na vlastnictví pro balíčky?**

Zobrazit [vlastníky Správa balíčků na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Jak zacházet s vlastníka balíčku, který porušuje licence na software**

Doporučujeme komunity NuGet spolupráce řešení všech sporů, které mohou vzniknout mezi vlastníky balíčku a vlastníci dalšího softwaru. Jsme vytvořený [spor proces překladu](../policies/dispute-resolution.md) dodržovat před položením správcům nuget.org intercede.

**Je doporučeno uložit Moje testovací balíčky nuget.org?**

Pro účely testování můžete použít [staging.nuget.org](http://staging.nuget.org), nebo jako alternativní veřejné servery NuGet [webu myget.org](https://myget.org) nebo [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Všimněte si, že nemusí být zachována balíčky nahráli do staging.nuget.org. Zobrazit [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).

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
- Verze vašeho operačního systému
- Konfigurace počítače (procesor, síť, pevný disk)
- Určuje, zda váš počítač není za proxy nebo brány firewall
- Verze rozhraní .NET, které jsou nainstalované na počítači
- Verze nástrojů pro různé platformy jako .NET CLI nebo dnů, které používáte

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

**Jaké jsou koncové body rozhraní API pro nuget.org?**

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Všimněte si, že rozhraní API verze 2 je zastaralý a nefunguje s NuGet 4 +.)
