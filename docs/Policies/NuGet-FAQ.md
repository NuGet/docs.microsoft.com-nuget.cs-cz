---
title: "NuGet – nejčastější dotazy | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Běžné otázky a odpovědi na příkazovém řádku a v sadě Visual Studio pomocí nástroje NuGet a práce s galerii NuGet."
keywords: "Verze balíčku NuGet otázek a odpovědí, otázky a odpovědi, běžné problémy, verze NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3782fe5dcf8df002d99446aa7548a6eacc62211c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="nuget-frequently-asked-questions"></a>Nejčastější dotazy NuGet

**Co je potřeba spustit NuGet?**

Všechny informace ohledně uživatelského rozhraní a nástroje příkazového řádku je k dispozici v [instalace Průvodce](../install-nuget-client-tools.md).

**Podporuje NuGet Mono?**

Nástroj příkazového řádku `nuget.exe`, sestavení a běží pod Mono 3.2 + a balíčky lze vytvořit mono.

I když `nuget.exe` funguje plně v systému Windows, existují známé problémy na Linuxu a OS X. najdete [Mono problémy](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na Githubu.

A [grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.

**Jak mohu zjistit, co balíček obsahuje a zda je stabilní a užitečné pro Moje aplikace?**

Primární zdroj informací o balíčku je stránka výpis na nuget.org (nebo jiného privátního kanálu). Každý balíček stránky na nuget.org obsahuje popis balíčku, jeho historie verzí a Statistika využití. **Informace** části na stránce balíček také obsahuje odkaz na projektu webové stránky, kde je obvykle najít mnoho příklady a další dokumentaci, která vás se způsobu použití balíčku.

Další informace najdete v tématu [vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet v sadě Visual Studio

**Jak se podporuje NuGet v různých produktů Visual Studio?**

- Visual Studio v systému Windows podporuje [uživatelského rozhraní Správce balíčků](../tools/package-manager-ui.md) a [Konzola správce balíčků](../tools/package-manager-console.md).
- Visual Studio pro Mac obsahuje integrované funkce NuGet, jak je popsáno na [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (všechny platformy) nemá žádné přímé integrace NuGet. Použití [NuGet CLI](../tools/nuget-exe-cli-reference.md) nebo [dotnet rozhraní příkazového řádku](../tools/dotnet-commands.md).
- Visual Studio Team Services poskytuje [krok sestavení pro obnovování balíčků NuGet](/vsts/build-release/tasks/package/nuget). Můžete také [privátní balíček NuGet hostitele kanály na Team Services](https://www.visualstudio.com/docs/package/nuget/publish).

**Jak zkontrolovat přesnou verzi systému NuGet nástroje, které jsou nainstalovány?**

V sadě Visual Studio, použijte **pomoci > o sadě Microsoft Visual Studio** příkazů a podívejte se na verzi zobrazí vedle možnosti **Správce balíčků NuGet**.

Alternativně spusťte konzolu nástroje Správce balíčků (**nástroje > Správce balíčků NuGet > Konzola správce balíčků**) a zadejte `$host` zobrazíte informace o systému NuGet, včetně verze.

**Jaké programovací jazyky jsou podporované systémem NuGet?**

NuGet obecně se dá použít pro jazyky rozhraní .NET a je navržená tak, aby knihovny .NET do projektu. Vzhledem k tomu, že podporuje také MSBuild a Visual Studio automatizace v některé typy projektů, podporuje také další projekty a jazyky do různých stupňů.

Nejnovější verzi NuGet podporuje C#, Visual Basic, F #, WiX a C++.

**Jaké šablony projektů jsou podporované systémem NuGet?**

NuGet má plnou podporu pro celou řadu šablon projektu, například Windows, webové, Cloud, SharePoint, Wix a tak dále.

**Jak aktualizovat balíčky, které jsou součástí šablony sady Visual Studio**

Přejděte na **aktualizace** v uživatelském rozhraní Správce balíčků a vyberte **Aktualizovat vše**, nebo použijte [ `Update-Package` příkaz](../tools/ps-ref-update-package.md) z konzoly Správce balíčků.

Aktualizovat šablonu sám sebe, musíte ručně aktualizovat úložiště šablon. V tématu [Xavier Decoster blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na toto téma. Všimněte si, že to se provádí na vlastní nebezpečí, protože ruční aktualizace může dojít k poškození šablony Pokud nejnovější verzi všechny závislosti nejsou vzájemně kompatibilní.

**Můžete použít balíček NuGet mimo Visual Studio?**

Ano, NuGet pracuje přímo z příkazového řádku. Najdete v článku [instalace Průvodce](../install-nuget-client-tools.md) a [referenční dokumentace rozhraní příkazového řádku](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>NuGet příkazového řádku

**Jak lze získat nejnovější verzi nástroje příkazového řádku NuGet?**

Najdete v článku [instalace Průvodce](../install-nuget-client-tools.md).

**Co je licence k nuget.exe?**

Jsou povoleny nuget.exe v rámci podmínek licencí MIT znovu distribuovat. Jste zodpovědní za aktualizace a údržba všechny kopie nuget.exe, které chcete znovu distribuovat.

**Je možné rozšířit nástroje příkazového řádku NuGet?**

Ano, je možné přidat vlastní příkazy `nuget.exe`, jak je popsáno v [post Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konzola správce balíčků NuGet (Visual Studio v systému Windows)

**Jak získat přístup k objektu DTE v konzole Správce balíčků**

Objekt nejvyšší úrovně v sadě Visual Studio automatizace objektový model se nazývá objekt prostředí DTE (Development Tools Environment). To konzole poskytuje prostřednictvím proměnné s názvem `$DTE`. Další informace najdete v tématu [Přehled automatizace modelu](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci k rozšiřitelnosti Visual Studio.

**Pokusu převést proměnnou $DTE typu DTE2, ale zobrazí chybová zpráva: nelze převést hodnotu "EnvDTE.DTEClass" typ "EnvDTE.DTEClass" typ "EnvDTE80.DTE2". Co je?**

Jde o známý problém s jak prostředí PowerShell komunikuje s objektem COM. Zkuste následující postup:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` Přidat hostitele NuGet PowerShell pomocné funkce.

## <a name="creating-and-publishing-packages"></a>Vytváření a publikování balíčků

**Jak seznamu Moje balíčku v informačním kanálu?**

V tématu [vytváření a publikování balíčku](../quickstart/create-and-publish-a-package.md).

**Mám několik verzí mé knihovny, které jiné cílové verze rozhraní .NET Framework. Jak lze vytvořit jeden balíček, který to podporuje?**

V tématu [podpora více verzí rozhraní .NET Framework a profily](../create-packages/supporting-multiple-target-frameworks.md).

**Jak mám nastavit vlastní úložiště nebo informační kanál?**

Najdete v článku [hostování balíčků přehled](../hosting-packages/overview.md).

**Jak můžete nahrát balíčky pro moje NuGet kanálu hromadně?**

V tématu [hromadné publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Práce s balíčky

**Jaký je rozdíl mezi balíčkem úrovni projektu a řešení úrovni balíčku?**

Balíček úrovni řešení (NuGet 3.x+) se nainstaluje pouze jednou v řešení a pak je k dispozici pro všechny projekty v řešení. Balíček úrovni projektu je nainstalována v každém projektu, který používá je. Balíček úrovni řešení může také nainstalovat nové příkazy, které lze volat z konzoly Správce balíčků.

**Je možné nainstalovat balíčky NuGet bez připojení k Internetu?**

Ano, najdete v příspěvku blogu Scott Hanselman [postup při nuget.org je dolů (nebo jste do roviny) získat přístup k NuGet](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Jak instalovat balíčky v jiném umístění z výchozí složku balíčků?**

Nastavte [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) nastavení v `Nuget.Config` pomocí `nuget config -set repositoryPath=<path>`.

**Jak vyhnout, přidání složky balíčků NuGet do do správy zdrojového kódu?**

Nastavte [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) v `Nuget.Config` k `true`. Tento klíč funguje v řešení úroveň a proto musí být přidán do `$(Solutiondir)\.nuget\Nuget.Config` souboru. Povolení obnovení balíčku ze sady Visual Studio automaticky vytvoří tento soubor.

**Jak lze vypnout obnovení balíčků?**

V tématu [povolení a zákaz obnovení balíčků](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Proč se zobrazila "Nelze přeložit došlo k chybě závislosti" při instalaci balíčku, místní vzdálené závislosti?**

Je nutné vybrat **všechny** zdroje při instalaci místní balíčku do projektu. To agreguje informační kanály místo použití pouze jeden. Tato chyba se zobrazí důvodem je, že uživatelé místní úložiště se často chtít vyhnout omylem instalaci vzdálených balíčků z důvodu podnikové zásady.

**Je nutné více projektů ve stejné složce, jak můžete použít samostatné packages.config soubory pro každý projekt?**

Ve většině projekty bydlišti samostatné projekty v samostatné složky, to není problém jako NuGet identifikuje `packages.config` soubory do každého projektu. U balíčku NuGet 3.3 + a více projektů ve stejné složce, můžete vložit název projektu do `packages.config` názvy souborů pomocí vzoru `packages.{project-name}.config`, a NuGet použije tento soubor.

To není problém při použití PackageReference, protože každý soubor projektu obsahuje vlastní seznam závislosti.

**Nuget.org se nezobrazí v seznamu úložišť, jak lze získat ho zpátky?**

- Přidat `https://api.nuget.org/v3/index.json` si na seznam zdrojů, nebo
- Odstranit `%appdata%\.nuget\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a umožní NuGet znovu vytvořit.

**Jaké jsou výchozí licenční podmínky Pokud balíček neposkytuje konkrétní informace o licencích?**

Každý balíček se řídí podmínkami, které jsou součástí balíčku. Přečtěte si podmínky použít před přístup, stahování nebo získávání všechny balíčky. Na nuget.org, použijte **licenční informace** odkaz na stránce balíček.

Pokud balíček neurčuje licenční podmínky, obraťte se na vlastníka balíčku přímo pomocí **obraťte se na vlastníky** odkaz na stránce balíček nuget.org. Společnost Microsoft není licence duševního vlastnictví vám ze zprostředkovatelů balíček třetích stran a není zodpovědná za informace třetích stran.

## <a name="managing-packages-on-nugetorg"></a>Spravovat balíčky v nuget.org

**Můžete upravit metadata balíčků, až se nahrají? Proč požadujete úpravy soubor nuspec a odesílání nový balíček pro provádění změn do balíčku metadata?**

NuGet vyžaduje všechny balíčky k podepsání. Princip návrhu podepisování balíčku je, že podepsaný balíček obsahu musí být neměnné, což zahrnuje soubor nuspec. Úpravy metadata balíčků výsledkem změny pro soubor nuspec, zneplatnění existující podpisy. Doporučujeme, abyste úprava existující pracovní postupy a nevyžadují úpravy metadata balíčků po vytvoření balíčku.

Všimněte si, že pro svůj balíček uvedené závislosti jsou automaticky generovány z balíčku sám sebe a nelze jej upravit.

Kromě toho odesílání balíčků [staging.nuget.org](http://staging.nuget.org) je skvělým způsobem, jak testování a ověření vašeho balíčku bez zpřístupnění balíček ve veřejné galerii.

**Je možné rezervovat názvy pro balíčky, které budou publikovány v budoucnosti?**

Ano. ID můžete vyhradit pro balíčky na [nuget.org](https://www.nuget.org/) tím, že požádá předponu ID balíčku pro váš účet. Chcete-li požádat o předponu ID balíčku, postupujte podle pokynů [dokumentaci](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Jak nárokovat vlastnictví pro balíčky?**

V tématu [Správa vlastníků balíčku na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Řešení s vlastníka balíčku, který je bychom při tom porušili Moje softwarových licencí**

Doporučujeme komunitou NuGet spolupracovat na řešení sporů, které může způsobit mezi balíček vlastníků a vlastníci na ostatní software. Budeme mít vytvořené [proces řešení sporu](../policies/dispute-resolution.md) dříve, než s dotazem, správcům nuget.org intercede.

**Se doporučuje nahrát Moje testovací balíčky do nuget.org?**

Pro účely testování můžete použít [staging.nuget.org](http://staging.nuget.org), nebo jako alternativní veřejné servery NuGet [myget.org](https://myget.org) nebo [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Všimněte si, že balíčky nahrán do staging.nuget.org nelze zachovat. V tématu [dát sbohem všem preview](http://blog.nuget.org/20130419/goodbye-preview.html).

**Jaká je maximální velikost balíčků, které I můžete uložit do nuget.org?**

nuget.org umožňuje balíčky až 250MB, ale nemůžeme doporučujeme zachovat balíčky v části 1MB, pokud je to možné a použití závislosti propojení balíčky současně. Balíčky jako existuje pravidlo, obsahovat pouze jeden sestavení, aby se zabránilo kolizí.

NuGet stáhnout balíčky, takže větší balíčky mít vyšší pravděpodobnost selhání nainstaluje než menším pomocí protokolu HTTP.

Je možné sdílet závislosti mezi více balíčků, zmenšit velikost stažených pro příjemci vašich balíčků NuGet.

Závislosti jsou většinou statické a nikdy změnit. Při opravě chyby v kódu, nemusí být závislosti nutné aktualizovat. Pokud jste sady závislosti, skončili reshipping pokaždé, když větší balíčky. Rozdělením balíčků NuGet do související závislosti, upgrade je mnohem podrobnějšího pro spotřebitele vašeho balíčku.

## <a name="nugetorg-not-accessible"></a>není k dispozici nuget.org

**Proč nelze stáhnout balíčky nebo balíčky odešlete do nuget.org?**

První Ujistěte se, že používáte nejnovější verze NuGet. Pokud tuto verzi dále nedaří, [obraťte se na podporu](https://www.nuget.org/policies/Contact) a poskytnout další připojení, řešení potíží s informace, včetně:

- Verze NuGet používáte
- Zdroje balíčku, kterou používáte
- Obnovení protokolu s podrobné podrobností
- MTR nebo Fiddler trasování (viz níže)
- Zeměpisná oblast
- Verze vašeho operačního systému
- Konfigurace počítače (procesor, sítě, pevný disk)
- Jestli je váš počítač za proxy nebo brány firewall
- Verze rozhraní .NET, které jsou nainstalovány na počítači
- Verze nástrojů pro různé platformy jako je rozhraní příkazového řádku .NET nebo dnů, který používáte

*Chcete-li zaznamenat MTR:*

- Stáhněte si WinMTR z [http://winmtr.net/download/](http://winmtr.net/)
- Zadejte `api.nuget.org` jako název hostitele a klikněte na tlačítko **spustit**.
- Počkejte **odeslané** sloupec je sloupec > = 100.

    ![Zaznamenání MTR](media/mtr.png)

- Zkopírujte text do schránky.

*Chcete-li zaznamenat Fiddler:*

- Nainstalujte nejnovější verzi [Fiddler](http://www.telerik.com/download/fiddler).
- Spusťte aplikaci Fiddler a zakázat pomocí zaznamenávání provoz **soubor > zachycování provozu** nabídky.
- Odeberte všechny relace (vyberte všechny položky v seznamu, stiskněte **odstranit** klíč).
- Nakonfigurujte aplikaci Fiddler k zachycení provoz HTTPS kontrolou **provoz HTTPS dešifrovat** v **HTTPS** kartě **nástroje > Možnosti Fiddler...**  nabídky.
- Zavřete Visual Studio.
- Povolit **soubor > zachycování provozu** nabídky.
- Spusťte Visual Studio nebo nuget.exe .exe a provádět akce, které nefungují. Přenosy dat vytvářené pomocí tyto akce by měl zobrazí v aplikaci Fiddler.
- Jakmile akce, které jste spustili, použijte **soubor > Uložit > všechny relace** k uložení zaznamenané relací.

Poznámka: může být nezbytné k nastavení `HTTP_PROXY` proměnnou prostředí `http://127.0.0.1:8888` pro směrování provozu NuGet prostřednictvím aplikaci Fiddler.

Pokud se nezdaří, zkuste [tipy uvedených v tomto blogu StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**Jaké jsou koncové body rozhraní API pro nuget.org?**

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Všimněte si, že rozhraní API verze 2 je zastaralá a nefunguje s NuGet 4 +.)
