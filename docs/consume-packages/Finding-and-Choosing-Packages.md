---
title: Hledání a výběr nugetových balíčků
description: Přehled, jak najít a vybrat nejlepší balíčky NuGet pro projekt, včetně podrobností o syntaxi hledání NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 9f427005251bc2bf7a8a79285e39b4bd49062dbf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428854"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Hledání a vyhodnocování balíčků NuGet pro váš projekt

Při spuštění libovolného projektu .NET nebo kdykoli zjistíte funkční potřebu vaší aplikace nebo služby, můžete ušetřit spoustu času a problémů pomocí existujících balíčků NuGet, které splňují tuto potřebu. Tyto balíčky mohou pocházet z veřejné kolekce na [nuget.org](https://www.nuget.org/packages/)nebo ze soukromého zdroje poskytovaného vaší organizací nebo jinou třetí stranou.

## <a name="finding-packages"></a>Hledání balíčků

Když navštívíte nuget.org nebo otevřete ui Správce balíčků v sadě Visual Studio, zobrazí se seznam balíčků seřazených podle celkového počtu stažení. To okamžitě zobrazí nejpoužívanější balíčky napříč miliony projektů .NET. Je tedy velká šance, že alespoň některé balíčky uvedené na prvních několika stránkách budou užitečné ve vašich projektech.

![Výchozí zobrazení nuget.org/packages zobrazující nejoblíbenější balíčky](media/Finding-01-Popularity.png)

Všimněte si **možnosti Zahrnout předběžnou verzi** v pravém horním pravém horním části stránky. Pokud je tato možnost vybrána, nuget.org zobrazí všechny verze balíčků včetně beta verzí a dalších dřívějších verzí. Chcete-li zobrazit pouze stabilní propuštěn, zrušte zaškrtnutí možnosti.

Pro konkrétní potřeby hledání podle značek (ve Správci balíčků sady Visual Studio nebo na portálu, jako je nuget.org) je nejběžnější způsob, jak zjistit vhodný balíček. Například hledání na "json" uvádí všechny balíčky NuGet, které jsou označeny tímto klíčovým slovem a proto mají nějaký vztah k formátu dat JSON.

![Výsledky hledání pro 'json' na nuget.org](media/Finding-02-SearchResults.png)

Můžete také vyhledávat pomocí ID balíčku, pokud ho znáte. Viz [Syntaxe hledání](#search-syntax) níže.

V současné době jsou výsledky hledání seřazeny pouze podle relevance, takže obecně chcete procházet alespoň několik prvních stránek výsledků pro balíčky, které vyhovují vašim potřebám, nebo upřesnit hledané termíny tak, aby byly konkrétnější.

### <a name="does-the-package-support-my-projects-target-framework"></a>Podporuje balíček cílový rámec mého projektu?

NuGet nainstaluje balíček do projektu pouze v případě, že tento balíček podporované architektury zahrnují cílové rozhraní projektu. Pokud balíček není kompatibilní, NuGet problémy chyby.

Některé balíčky uvádějí své podporované architektury přímo v galerii nuget.org, ale protože tato data nejsou vyžadována, mnoho balíčků tento seznam neobsahuje. V současné době neexistuje žádný způsob, jak vyhledávat nuget.org balíčky, které podporují konkrétní cílový rámec (funkce je zvažována, viz [NuGet Issue 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Naštěstí můžete určit podporované architektury pomocí dvou dalších prostředků:

1. Pokuste se nainstalovat balíček [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) do projektu pomocí příkazu v konzole Správce balíčků NuGet. Pokud balíček je nekompatibilní, tento příkaz zobrazí podporované architektury balíčku.

1. Stáhněte si balíček ze své stránky na nuget.org pomocí **manuálu ke stažení** odkaz v části **Info**. Změňte příponu z `.nupkg` do `.zip`a otevřete `lib` soubor a zkontrolujte obsah jeho složky. Zde vidíte podsložky pro každý z podporovaných rámců, kde každá podsložka je pojmenována s zástupným názvem cílové ho rozhraní (TFM; viz [cílové architektury).](../reference/target-frameworks.md) Pokud pod ním nejsou `lib` žádné podsložky a pouze jedna dll, musíte se pokusit nainstalovat balíček v projektu, abyste zjistili jeho kompatibilitu.

## <a name="pre-release-packages"></a>Předběžné verze balíčků

Mnoho autorů balíčků zpřístupní náhled a beta verze, protože pokračují v vylepšování a hledání zpětné vazby na své nejnovější revize.

Ve výchozím nastavení nuget.org zobrazuje předběžné balíčky ve výsledcích hledání. Chcete-li vyhledat pouze stabilní verze, zrušte zaškrtnutí možnosti **Zahrnout předběžnou verzi** v pravém horním masu stránky.

![Zahrnout zaškrtávací políčko předběžné verze na nuget.org](media/Finding-06-include-prerelease.png)

V sadě Visual Studio a při použití nástrojů NuGet a dotnet CLI NuGet neobsahuje předběžné verze ve výchozím nastavení. Chcete-li toto chování změnit, proveďte následující kroky:

- **UI Správce balíčků v sadě Visual Studio**: V **uprávě Spravovat balíčky NuGet** nastavte pole **Zahrnout předběžnou verzi.** Nastavení nebo zrušení zaškrtnutí tohoto pole aktualizuje ui Správce balíčků a seznam dostupných verzí, které můžete nainstalovat.

    ![Zaškrtávací políčko Zahrnout předběžnou verzi v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Konzola Správce**balíčků `-IncludePrerelease` : `Find-Package`Použijte `Get-Package` `Install-Package`přepínač `Sync-Package`s `Update-Package` příkazy , , , a příkazy. Odkazovat na [odkaz prostředí PowerShell](../reference/powershell-reference.md).

- **nuget.exe CLI**: `-prerelease` Použijte `install`přepínač `update` `delete`s `mirror` příkazy , , a. Odkazovat na [odkaz NuGet CLI](../reference/nuget-exe-cli-reference.md)

- **dotnet.exe CLI**: Zadejte přesnou `-v` předběžnou verzi pomocí argumentu. Viz [dotnet přidat odkaz na balíček](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Nativní balíčky C++

NuGet podporuje nativní balíčky Jazyka C++, které lze použít v projektech jazyka C++ v sadě Visual Studio. To umožňuje **spravovat nugetbalíčky** kontextové nabídky příkaz `native` pro projekty, zavádí cílové rozhraní a poskytuje integraci MSBuild.

Chcete-li najít [nuget.org](https://www.nuget.org/packages)nativní `tag:native`balíčky na nuget.org , vyhledejte pomocí . Tyto balíčky `.targets` obvykle `.props` poskytují a soubory, které NuGet importuje automaticky při přidání balíčku do projektu.

## <a name="evaluating-packages"></a>Vyhodnocení balíčků

Nejlepší způsob, jak vyhodnotit užitečnost balíčku, je stáhnout jej a vyzkoušet si jej ve vašem kódu (všechny balíčky na nuget.org jsou mimochodem běžně kontrolovány na přítomnost virů). Koneckonců, každý velmi populární balíček začal jen s několika vývojáři, kteří jej používají, a můžete být jedním z prvních osvojitelů!

Současně pomocí balíčku NuGet znamená převzetí závislosti na něm, takže chcete ujistěte se, že je robustní a spolehlivé. Vzhledem k tomu, že instalace a přímé testování balíčku je časově náročné, můžete se také dozvědět mnoho o kvalitě balíčku pomocí informací na stránce s výpisem balíčku:

- *Statistiky ke stažení*: na stránce balíčku na nuget.org zobrazuje sekce **Statistika** celkový počet stažení, stažení nejnovější verze a průměrné stahování za den. Větší čísla označují, že mnoho dalších vývojářů přijalo závislost na balíčku, což znamená, že se osvědčil.

    ![Stažení statistik na stránce s výpisem balíčku](media/Finding-03-Downloads.png)

- *Využití GitHubu:* na stránce balíčku je v části **Využití GitHubu** uveden seznam veřejných úložišť GitHub, které jsou závislé na tomto balíčku a které mají na GitHubu vysoký počet hvězdiček. Počet hvězd, které úložiště GitHub udávají, obecně naznačuje, jak populární je toto úložiště s uživateli GitHubu (více hvězd obvykle znamená více populární). Další informace o systému hodnocení hvězd a úložišť GitHubu najdete na stránce Začínáme na [GitHubu.](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars)

    ![Využití GitHubu](media/GitHub-Usage.png)

    > [!Note]
    > Sekce využití GitHubu balíčku se generuje automaticky, pravidelně, bez lidské kontroly jednotlivých úložišť a výhradně pro informační účely, aby se vám ukázaly úložiště GitHub, které závisí na balíčku a které jsou oblíbené u uživatelů GitHubu.

- *Historie verzí*: Na stránce balíčku vyhledejte datum poslední aktualizace v části **Informace** a zkontrolujte **historii verzí**. Dobře udržovaný balíček obsahuje nejnovější aktualizace a bohatou historii verzí. Zanedbané balíčky mají několik aktualizací a často nebyly aktualizovány v určité době.

    ![Historie verzí na stránce s výpisem balíčku](media/Finding-04-VersionHistory.png)

- *Poslední instalace*: na stránce balíčku v části **Statistika**vyberte **Zobrazit úplné statistiky**. Na stránce úplné statistiky se zobrazí balíček nainstaluje za posledních šest týdnů podle čísla verze. Balíček, který ostatní vývojáři aktivně používají, je obvykle lepší volbou než ten, který není.

- *Podpora*: Na stránce balíčku v části **Informace**vyberte **Web projektu** (pokud je k dispozici), abyste zjistili, jaké možnosti podpory autor nabízí. Projekt s vyhrazeným webem je obecně lépe podporován.

- *Historie vývojářů*: Na stránce balíčku v části **Vlastníci**vyberte vlastníka, abyste zjistili, jaké další balíčky publikovali. Ti, kteří mají více balíčků, budou v budoucnu nadále podporovat svou práci.

- *Open source příspěvky*: mnoho balíčků je udržováno v open-source repozitářích, což umožňuje vývojářům v závislosti na nich přímo přispívat opravami chyb a vylepšeními funkcí. Historie příspěvků daného balíčku je také dobrým ukazatelem toho, kolik vývojářů je aktivně zapojeno.

- *Rozhovor s vlastníky*: noví vývojáři mohou být jistě stejně odhodláni vyrábět skvělé balíčky, které můžete použít, a je dobré jim dát šanci přinést něco nového do ekosystému NuGet. S ohledem na tuto skutečnost oslovte přímo vývojáře balíčků prostřednictvím **možnosti Vlastníci kontaktů** v části **Informace** na stránce výpisu. Je pravděpodobné, že budou rádi, že s vámi budou spolupracovat, aby sloužili vašim potřebám!

- *Předpony ID rezervovaného balíčku*: Mnoho vlastníků balíčků požádalo o [předponu ID rezervovaného balíku](../nuget-org/id-prefix-reservation.md)a bylo jí uděleno. Když se zobrazí vizuální zaškrtnutí vedle ID balíčku na [nuget.org](https://www.nuget.org/)nebo v sadě Visual Studio, znamená to, že vlastník balíčku splnil naše [kritéria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) pro rezervaci předpony ID. To znamená, že vlastník balíčku je jasné, na identifikaci sebe a jejich balíček.

> [!Note]
> Vždy mějte na paměti licenční podmínky balíčku, které můžete vidět výběrem **licenčních informací** na stránce s výpisem balíčku na nuget.org. Pokud balíček nespecifikuje licenční podmínky, obraťte se přímo na vlastníky balíčku pomocí odkazu **Vlastníci kontaktů** na stránce balíčku. Společnost Microsoft vám nelicencuje žádné duševní vlastnictví od poskytovatelů balíčků třetích stran a není odpovědná za informace poskytnuté třetími stranami.

## <a name="license-url-deprecation"></a>Vyřazení adresy URL licence
Jako jsme přechod z [licenseUrl](../reference/nuspec.md#licenseurl) na [licenci](../reference/nuspec.md#license), některé NuGet klienty a NuGet kanály ještě nemusí mít možnost povrchové licenční informace v některých případech. Chcete-li zachovat zpětnou kompatibilitu, odkazuje adresa URL licence na tento dokument, který hovoří o tom, jak v takových případech načíst informace o licenci.

Pokud vás kliknutím na licenční adresu URL balíčku přenesete na tuto stránku, znamená to, že balíček obsahuje licenční soubor a
* Jste připojeni k informačnímu kanálu, který ještě neví, jak interpretovat a vyložit nové informace o licenci klientovi **nebo**
* Používáte klienta, který ještě neví, jak interpretovat a číst nové informace o licenci, které jsou potenciálně poskytovány zdrojem **NEBO**
* Kombinace obojího

Zde je, jak si můžete přečíst informace obsažené v licenčním souboru uvnitř balíčku:
1. Stáhněte balíček NuGet a rozbalte jeho obsah do složky.
1. Otevřete `.nuspec` soubor, který by byl v kořenovém adresáři této složky.
1. Mělo by mít `<license type="file">license\license.txt</license>`značku jako . To znamená, že `license.txt` licenční soubor je pojmenován `license` a je uvnitř složky s názvem, která by také byla v kořenovém adresáři této složky.
1. Přejděte `license` do složky `license.txt` a otevřete soubor.

Pro MSBuild ekvivalentní nastavení licence `.nuspec`v , podívejte se na [Balení licenční výraz nebo licenční soubor](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).

## <a name="search-syntax"></a>Syntaxe hledání

NuGet balíček hledání funguje stejně na nuget.org, z NuGet CLI a v rámci rozšíření NuGet Package Manager v sadě Visual Studio. Obecně platí, že vyhledávání se použije na klíčová slova, stejně jako popisy balíčků.

- **Filtrování**: Hledaný výraz můžete použít na určitou `<property>:<term>` `<property>` vlastnost pomocí syntaxe, `id`kde `packageid` `version`(bez rozlišování velkých a malých písmen) může být , , `title` `tags`, `author`, `description` `summary`, , a `owner`. Můžete vyhledat více vlastností současně. Vyhledávání na `id` vlastnost jsou podřetězce shody, vzhledem k tomu, `packageid` a `owner` používá přesné, malá a velká písmena shody. Příklady:

```
PackageId:jquery             # Match the package ID in an exact, case-insensitive manner

owner:microsoft              # Match the owner in an exact, case-insensitive manner

id:NuGet.Core                # Match any part of the ID property
Id:"Nuget.Core"
ID:jQuery
id:jquery id:ui              # Search for multiple terms in the ID
id:jquery tags:validation    # Search multiple properties

invalid:jquery ui            # Unsupported properties are ignored, so this
                             # is the same as searching on ui
```
