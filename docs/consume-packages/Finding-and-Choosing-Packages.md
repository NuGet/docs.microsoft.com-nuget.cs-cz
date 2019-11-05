---
title: Hledání a výběr balíčků NuGet
description: Přehled toho, jak najít a zvolit nejlepší balíčky NuGet pro projekt, včetně podrobností o syntaxi hledání NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 9947a490e4373bb0b8b7fb0814828ff2a60615a8
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611076"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Hledání a vyhodnocení balíčků NuGet pro váš projekt

Při spouštění jakéhokoli projektu .NET nebo při každém určení funkčního potřeb vaší aplikace nebo služby můžete ušetřit spoustu času a potíží pomocí existujících balíčků NuGet, které tyto požadavky splňují. Tyto balíčky můžou pocházet z veřejné kolekce na [NuGet.org](https://www.nuget.org/packages/)nebo z privátního zdroje poskytovaného vaší organizací nebo jinou třetí stranou.

## <a name="finding-packages"></a>Hledání balíčků

Když navštívíte nuget.org nebo otevřete uživatelské rozhraní Správce balíčků v aplikaci Visual Studio, zobrazí se seznam balíčků seřazených podle celkového počtu stažení. Tím okamžitě ukážete nejpoužívanější balíčky v milionech projektů .NET. Je velmi pravděpodobné, že v projektech budou užitečné alespoň některé balíčky uvedené na prvních několika stránkách.

![Výchozí zobrazení nuget.org/packages znázorňující nejoblíbenější balíčky](media/Finding-01-Popularity.png)

Všimněte si, že v pravém horním rohu stránky je možnost **Zahrnout předprodejní verze** . Když se tato možnost vybere, zobrazí nuget.org všechny verze balíčků včetně beta verze a dalších počátečních verzí. Chcete-li zobrazit pouze stabilní uvolněné možnosti, zrušte zaškrtnutí políčka.

Pro konkrétní potřeby je vyhledávání pomocí značek (ve Správci balíčků sady Visual Studio nebo na portálu jako nuget.org) nejběžnějším prostředkem pro zjištění vhodného balíčku. Například hledání "JSON" vypíše všechny balíčky NuGet označené tímto klíčovým slovem a má tedy nějaký vztah ke formátu dat JSON.

![Výsledky hledání pro JSON na nuget.org](media/Finding-02-SearchResults.png)

Pokud víte, můžete také vyhledat ID balíčku pomocí ID. Viz [syntaxe vyhledávání](#search-syntax) níže.

V současné době jsou výsledky hledání seřazené pouze podle relevance, takže obecně chcete projít alespoň prvních několika stránek výsledků pro balíčky, které vyhovují vašim potřebám, nebo Upřesnit hledané výrazy, aby byly konkrétnější.

### <a name="does-the-package-support-my-projects-target-framework"></a>Podporuje balíček cílový rámec projektu?

NuGet nainstaluje balíček do projektu pouze v případě, že podporované architektury tohoto balíčku zahrnují cílové rozhraní projektu. Pokud balíček není kompatibilní, NuGet vyvolá chybu.

Některé balíčky obsahují jejich podporovaná rozhraní přímo v galerii nuget.org, ale vzhledem k tomu, že taková data se nevyžadují, mnoho balíčků tento seznam neobsahuje. V současné době neexistuje žádný způsob, jak hledat v nuget.org balíčky, které podporují konkrétní cílové rozhraní (Tato funkce je popsána v tématu [problém nuget 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Naštěstí můžete určit podporované architektury prostřednictvím dvou dalších prostředků:

1. Pokuste se nainstalovat balíček do projektu pomocí příkazu [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) v konzole správce balíčků NuGet. Pokud je balíček nekompatibilní, tento příkaz zobrazí podporované architektury balíčku.

1. Stáhněte balíček ze své stránky na nuget.org pomocí odkazu pro **Ruční stažení** v části **informace**. Změňte rozšíření z `.nupkg` na `.zip`a otevřete soubor pro prohlédnutí obsahu jeho složky `lib`. Pro každou z podporovaných rozhraní se zobrazí podsložky, kde je každá podsložka pojmenována s monikerem cílového rozhraní (TFM; viz [cílové architektury](../reference/target-frameworks.md)). Pokud nevidíte žádné podsložky pod `lib` a jenom jedinou knihovnou DLL, pak se musíte pokusit nainstalovat balíček do svého projektu, abyste zjistili jeho kompatibilitu.

## <a name="pre-release-packages"></a>Předběžné verze balíčků

Spousta tvůrců balíčků zpřístupňuje verze Preview a beta, protože jsou dál v vylepšování a hledají zpětnou vazbu k jejich nejnovější revizi.

Ve výchozím nastavení nuget.org zobrazuje předběžné verze balíčků ve výsledcích hledání. Chcete-li hledat pouze stabilní verze, zrušte zaškrtnutí políčka **zahrnout předběžné verze** v pravém horním rohu stránky.

![Zahrnout zaškrtávací políčko pro předběžné vydání na nuget.org](media/Finding-06-include-prerelease.png)

V aplikaci Visual Studio a při použití nástrojů NuGet a dotnet CLI nástroj NuGet ve výchozím nastavení neobsahuje předběžné verze. Chcete-li toto chování změnit, proveďte následující kroky:

- **Uživatelské rozhraní Správce balíčků v sadě Visual Studio**: v uživatelském rozhraní pro **správu balíčků NuGet** nastavte pole **zahrnout předběžné verze** . Nastavením nebo zrušením zaškrtnutí tohoto políčka aktualizujete uživatelské rozhraní Správce balíčků a seznam dostupných verzí, které můžete nainstalovat.

    ![Zaškrtávací políčko zahrnout předběžné verze v aplikaci Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Konzola správce balíčků**: použijte přepínač `-IncludePrerelease` s příkazy `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`a `Update-Package`. Podívejte se na [referenční informace k prostředí PowerShell](../reference/powershell-reference.md).

- **NuGet. exe CLI**: použijte přepínač `-prerelease` s příkazy `install`, `update`, `delete`a `mirror`. Přečtěte si [referenční informace k NUGET CLI](../reference/nuget-exe-cli-reference.md)

- **dotnet. exe CLI**: Určete přesnou předběžnou verzi verze pomocí argumentu `-v`. Přečtěte si [odkaz na přidání balíčku dotnet](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Nativní C++ balíčky

NuGet podporuje nativní C++ balíčky, které lze použít v C++ projektech v aplikaci Visual Studio. To umožňuje, aby příkaz **Spravovat balíčky NuGet** v nabídce pro projekty, zavádí `native` cílovou architekturu a poskytoval integraci nástroje MSBuild.

Pokud chcete najít nativní balíčky na [NuGet.org](https://www.nuget.org/packages), hledejte pomocí `tag:native`. Takové balíčky obvykle poskytují `.targets` a `.props` soubory, které NuGet importuje automaticky při přidání balíčku do projektu.

## <a name="evaluating-packages"></a>Vyhodnocení balíčků

Nejlepším způsobem, jak vyhodnotit užitečnost balíčku, je stáhnout si ho a vyzkoušet si ho ve svém kódu (všechny balíčky na nuget.org jsou pravidelně prohledávány tak, aby se viry kontrolovaly). Každý vysoce oblíbený balíček je po všech verzích spuštěný s několika vývojáři, kteří ho používají, a možná jste jedním z prvních výrobců.

Zároveň použití balíčku NuGet znamená, že se v něm nachází závislost, takže je potřeba zajistit, aby byla robustní a spolehlivá. Vzhledem k tomu, že instalace a přímá testování balíčku je časově náročné, můžete také zjistit spoustu kvality balíčku pomocí informací na stránce se seznamem balíčku:

- *Statistika ke stažení*: na stránce balíček na NuGet.org se v části **Statistika** zobrazuje celkový počet stažení, stažení nejnovější verze a průměrné stahování za den. Větší čísla označují, že mnoho dalších vývojářů zavedlo závislost na balíčku, což znamená, že se prověřil.

    ![Stáhnout statistiku na stránce se seznamem balíčku](media/Finding-03-Downloads.png)

- *Použití GitHubu*: na stránce balíček obsahuje oddíl **použití GitHubu** hlavní úložiště GitHub, která závisí na tomto balíčku. Balíček, na kterém je mnoho oblíbených úložišť GitHubu, závisí obvykle na lepším výběru.

    ![Použití GitHubu](media/GitHub-Usage.png)

- *Historie verzí*: na stránce balíček vyhledejte v části **informace** datum poslední aktualizace a zkontrolujte **historii verzí**. Dobře uchovávaný balíček má nedávné aktualizace a bohatou historii verzí. Opomíjené balíčky mají několik aktualizací a v některých časových intervalech se často neaktualizovaly.

    ![Historie verzí na stránce se seznamem balíčku](media/Finding-04-VersionHistory.png)

- *Poslední instalace*: na stránce balíček v části **Statistika**vyberte **Zobrazit úplné statistiky**. Na stránce úplných statistik se zobrazuje balíček, který se nainstaluje za posledních šest týdnů podle čísla verze. Balíček, který používají jiní vývojáři, je obvykle lepší volbou než ten, který není.

- *Podpora*: na stránce balíček v části **informace**vyberte možnost **Web projektu** (Pokud je k dispozici) a zjistěte, jaké možnosti podpory Autor poskytuje. Projekt s vyhrazenou lokalitou je obecně lepší podporovat.

- *Historie pro vývojáře*: na stránce balíček v části **vlastníci**vyberte vlastníka a podívejte se, jaké další balíčky se publikovaly. U zařízení s více balíčky je pravděpodobnější, že budou v budoucnu nadále podporovat svou práci.

- *Příspěvky na Open Source*: mnoho balíčků se uchovává v úložištích open source, což umožňuje vývojářům v závislosti na tom, jak přímo přispívá k opravám chyb a vylepšení funkcí. Historie příspěvků každého daného balíčku je také dobrým ukazatelem toho, kolik vývojářů je aktivně zapojeno.

- *Rozhovor s vlastníky*: noví vývojáři můžou být ve stejném pořádku, aby využívali Skvělé balíčky, abyste je mohli použít, a je dobré jim dát možnost přispívat do ekosystému NuGet něco nového. Na základě toho se můžete obrátit přímo na vývojáře balíčku prostřednictvím možnosti **vlastníci kontaktů** v části **informace** na stránce výpis. Je pravděpodobné, že budete spokojeni s tím, abyste mohli spolupracovat na svých potřebách.

- *Rezervované předpony ID balíčku*: mnoho vlastníků balíčků bylo aplikováno pro a byla udělena [vyhrazená předpona ID balíčku](../nuget-org/id-prefix-reservation.md). Když uvidíte vizuální značku vedle ID balíčku v [NuGet.org](https://www.nuget.org/)nebo v aplikaci Visual Studio, to znamená, že vlastník balíčku splnil [kritéria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) pro rezervaci předpony ID. To znamená, že vlastník balíčku je jasný k identifikaci a jejich balíčku.

> [!Note]
> Vždy si zavědomete licenčních podmínek balíčku, které můžete zobrazit výběrem **informace o licenci** na stránce se seznamem balíčku na NuGet.org. Pokud balíček neurčí licenční smlouvu, obraťte se na vlastníka balíčku přímo pomocí odkazu **vlastníci kontaktu** na stránce balíček. Společnost Microsoft nelicencuje žádné duševní vlastnictví od poskytovatelů balíčků třetích stran a nezodpovídá za informace poskytované třetími stranami.

## <a name="license-url-deprecation"></a>Zastaralá adresa URL licence
Protože jsme přešli z [licenseUrl](../reference/nuspec.md#licenseurl) na [licenci](../reference/nuspec.md#license), někteří klienti NuGet a kanály NuGet nemusí mít v některých případech možnost surfovat informace o licencích. Aby se zachovala zpětná kompatibilita, adresa URL licence odkazuje na tento dokument, který mluví o tom, jak v takových případech získat informace o licenci.

Pokud po kliknutí na adresu URL licence balíčku přejdete na tuto stránku, znamená to, že balíček obsahuje soubor s licencí a
* Jste připojeni k informačnímu kanálu, který ještě nevíte, jak interpretovat a obcházet nové informace o licenci pro klienta **nebo**
* Používáte klienta, který ještě nevíte, jak interpretovat a číst nové informace o licencích, které jsou potenciálně poskytované informačním kanálem **nebo**
* Kombinace obou

Tady je postup, jak si přečíst informace obsažené v souboru s licencí v balíčku:
1. Stáhněte si balíček NuGet a rozbalíte jeho obsah do složky.
1. Otevřete `.nuspec` soubor, který by byl v kořenu této složky.
1. Měla by obsahovat značku jako `<license type="file">license\license.txt</license>`. To znamená, že soubor s licencí má název `license.txt` a je uvnitř složky s názvem `license`, která by byla také v kořenu této složky.
1. Přejděte do složky `license` a otevřete soubor `license.txt`.

V případě, že nástroj MSBuild odpovídá nastavení licence v `.nuspec`, podívejte se na [balení licenčního výrazu nebo souboru s licencí](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).

## <a name="search-syntax"></a>Syntaxe hledání

Vyhledávání balíčků NuGet funguje stejně v nuget.org, z rozhraní NuGet CLI a v rámci rozšíření Správce balíčků NuGet v sadě Visual Studio. Obecně platí, že vyhledávání je použito pro klíčová slova a popisy balíčků.

- **Klíčová slova**: hledání vyhledá relevantní balíčky, které obsahují některá z poskytnutých klíčových slov. Příklad: `modern UI`. Chcete-li vyhledat balíčky obsahující všechna zadaná klíčová slova, použijte mezi těmito podmínkami znak "+", například `modern+UI`.
- **Fráze**: Zadání podmínek v rámci uvozovek vyhledá přesné shody velkých a malých písmen s těmito podmínkami. Příklad: `"modern UI" package`
- **Filtrování**: můžete použít hledaný termín pro konkrétní vlastnost pomocí syntaxe `<property>:<term>`, kde `<property>` (bez rozlišení velkých a malých písmen) může být `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`a `owner`. V případě potřeby mohou být výrazy obsaženy v uvozovkách a můžete vyhledávat více vlastností současně. Také vyhledávání na vlastnosti `id` jsou shody podřetězců, zatímco `packageid` používá přesnou shodu. Příklady:

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
