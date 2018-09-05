---
title: Vyhledání a výběr balíčků NuGet
description: Přehled o tom, jak najít a vybrat nejlepší balíčky NuGet pro projekt, včetně podrobností o syntaxi vyhledávání NuGet.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 81672abf0362e053da2b71c8bd39bd7f96ddf73b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549412"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Vyhledávání a hodnocení balíčky NuGet pro projekt

Při spouštění jakéhokoli projektu .NET nebo pokaždé, když se identifikovat funkční potřebu svou aplikaci nebo službu, můžete si ušetřit spoustu času a potíže s pomocí existující balíčky NuGet, které splňují tuto potřebu. Tyto balíčky můžou pocházet z veřejné kolekce [nuget.org](http://www.nuget.org/packages/), nebo privátní zdroje, která je k dispozici ve vaší organizaci nebo jiná třetí strana.

## <a name="finding-packages"></a>Vyhledávání balíčků

Navštivte nuget.org nebo otevřete uživatelské rozhraní Správce balíčků ve Visual Studiu, uvidíte seznam balíčků, seřazené podle celkový počet souborů ke stažení. Okamžitě zobrazí balíčky nejvíce nejběžněji používanými v milionech projekty .NET. Existuje šance. pak, alespoň některé balíčky uvedené v prvních několika stránek budou užitečné ve vašich projektech.

![Výchozí zobrazení nuget.org/packages zobrazující nejoblíbenějších balíčků](media/Finding-01-Popularity.png)

Všimněte si, že **zahrnout předběžné verze** možnost v horním pravém rohu stránky. Pokud je vybráno, zobrazí nuget.org všechny verze balíčků, včetně beta a jiné raných verzích. Chcete-li zobrazit pouze stabilní verze vydání, zrušte zaškrtnutí políčka.

Pro konkrétní potřeby hledání podle klíčových slov (v rámci správce sady Visual Studio balíček nebo na portálu, jako je nuget.org) je nejběžnější způsob zjišťování vhodný balíček. Například hledání "json" zobrazí seznam všech balíčků NuGet, které jsou označené pomocí tohoto klíčového slova a proto některé relace do formátu JSON.

![Výsledky hledání "json" na nuget.org](media/Finding-02-SearchResults.png)

Můžete také prohledat pomocí ID balíčku, pokud ji znáte. Zobrazit [hledání syntaxe](#search-syntax) níže.

V tuto chvíli jsou seřazeny výsledky hledání pouze podle relevance, takže obecně muset projít alespoň prvních několik stránek výsledky pro balíčky, které vyhovují vašim potřebám nebo Upřesnit na konkrétnější podmínky hledání.

### <a name="does-the-package-support-my-projects-target-framework"></a>Podporuje balíček Můj projekt cílovou architekturu?

NuGet nainstaluje balíček do projektu pouze v případě, že tento balíček podporované architektury patří cílové rozhraní projektu. Pokud balíček není kompatibilní, NuGet vyvolá chybu.

Některé balíčky seznamu jejich podporované architektury přímo v galerii nuget.org, ale vzhledem k tomu, že tyto údaje se nevyžaduje, řada balíčků nezahrnují tohoto seznamu. V současné době neexistuje žádný způsob, jak hledat nuget.org pro balíčky, které podporují konkrétní cílového rozhraní framework (funkce je v úvahu, naleznete v tématu [NuGet problém 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Naštěstí můžete určit jinými způsoby. dvě podporované architektury:

1. Pokus o instalaci balíčku do projektu s použitím [ `Install-Package` ](../tools/ps-ref-install-package.md) příkazu v konzole Správce balíčků NuGet. Pokud balíček není kompatibilní, tento příkaz zobrazí podporované architektury balíčku.

1. Stáhněte si balíček z její stránky na nuget.org pomocí **ruční stažení** odkaz pod **informace**. Změňte příponu z `.nupkg` k `.zip`a otevřete soubor a zkoumat obsah jeho `lib` složky. Zobrazit podsložky pro každou z podporovaných rozhraních, kde je každá podsložka s názvem s moniker cílového rozhraní (TFM; viz [cílových rozhraní](../reference/target-frameworks.md)). Pokud se zobrazí žádné podsložky `lib` a pouze jednoho souboru knihovny DLL, bude nutné pokusíte nainstalovat balíček ve vašem projektu a zjišťovat kompatibilitu.

## <a name="pre-release-packages"></a>Balíčky v předběžné verzi

Mnoho autory balíčku provést ve verzi preview a beta verze k dispozici jako nadále mohli vylepšit a hledat zpětnou vazbu na jejich nejnovější revize.

Ve výchozím nastavení zobrazuje nuget.org balíčky v předběžné verzi ve výsledcích hledání. Chcete-li hledat pouze stabilní verze, zrušte **zahrnout předběžné verze** možnost v horním pravém rohu stránky

![Zahrnout předběžnou verzi zaškrtávací políčko na nuget.org](media/Finding-06-include-prerelease.png)

V sadě Visual Studio a při použití nástroje rozhraní příkazového řádku dotnet a NuGet nezahrnuje NuGet předběžných verzí ve výchozím nastavení. Chcete-li toto chování změnit, proveďte následující kroky:

- **Uživatelské rozhraní Správce balíčků v sadě Visual Studio**: V **spravovat balíčky NuGet** uživatelského rozhraní, nastavte **zahrnout předběžné verze** pole. Nastavení nebo zrušením zaškrtnutí tohoto políčka aktualizuje uživatelské rozhraní Správce balíčků a seznam dostupných verzí, kterou můžete nainstalovat.

    ![Políčko zahrnout předběžné verze v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Konzola správce balíčků**: použijte `-IncludePrerelease` přepněte se `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, a `Update-Package` příkazy. Odkazovat [referenční informace prostředí PowerShell](../tools/powershell-reference.md).

- **rozhraní příkazového řádku nuget.exe**: použití `-prerelease` přepněte se `install`, `update`, `delete`, a `mirror` příkazy. Odkazovat [odkaz na rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md)

- **DotNet.exe rozhraní příkazového řádku**: zadat přesné předběžné verze pomocí `-v` argument. Odkazovat [se příkaz dotnet add odkaz na balíček](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Nativní balíčky jazyka C++

NuGet podporuje můžete nativní C++ balíčky, které můžete použít v projektech C++ v sadě Visual Studio. Díky tomu **spravovat balíčky NuGet** zavádí příkaz místní nabídky pro projekty, `native` cílové rozhraní framework a zajišťuje integraci nástroje MSBuild.

Najít nativní balíčky na [nuget.org](https://www.nuget.org/packages), hledání, které používá `tag:native`. Tyto balíčky obvykle poskytují `.targets` a `.props` soubory, které NuGet importuje automaticky při přidání balíčku do projektu.

## <a name="evaluating-packages"></a>Vyhodnocení balíčky

Nejlepší způsob, jak vyhodnotit použitelnost balíčku je si ho stáhnout a vyzkoušet v kódu (všech balíčků na nuget.org jsou pravidelně vyhledány viry, tím, jak). Po všech všech vysoce oblíbených balíčků začínal s pouze několika vývojářům, kteří používají ho a může být jedna z inovátoři!

Ve stejnou dobu pomocí balíčku NuGet znamená, že se tak závislosti na něj, proto ověřte, že je robustní a spolehlivé. Je časově náročná instalace a testování přímo balíček, také další mnohem o kvalitu balíčků podle informací uvedených na stránce balíčku:

- *Soubory ke stažení statistiky*: na stránce balíčků na nuget.org, **statistiky** část uvádí celkový počet souborů ke stažení, soubory ke stažení nejnovější verze a soubory ke stažení průměr za den. Vyšší čísla označují, že mnoho dalších vývojářů udělali závislost na balíčku, což znamená, že se ukázal.

    ![Statistika na stránce balíček pro stahování](media/Finding-03-Downloads.png)

- *Historie verzí*: na stránce balíček pro, podívejte se do části **informace** pro datum poslední aktualizace a zkontrolujte **historie verzí**. Dobře udržované balíček obsahuje nejnovější aktualizace a historie bohaté verzí. Opomíjený balíčky mají několik aktualizací a často se neaktualizovaly za nějakou dobu.

    ![Historie verzí na stránce balíčku](media/Finding-04-VersionHistory.png)

- *Poslední nainstaluje*: na stránce balíček pro v rámci **statistiky**vyberte **zobrazit úplnou statistiky**. Na stránce Statistika úplné ukazuje, že se že balíček nainstaluje za posledních šest týdnů podle čísla verze. Balíček, který ostatní vývojáři aktivně používají je obvykle vhodnější než ten, který není.

- *Podpora*: na stránce balíček pro v rámci **informace o**vyberte **web projektu** (Pokud je k dispozici) zobrazíte, jaká podpora možnosti Autor poskytuje. Projekt se vyhrazený je obecně vhodnější.

- *Historie pro vývojáře*: na stránce balíček pro v rámci **vlastníky**, vyberte vlastníka, pokud chcete zobrazit další balíčky, které jste publikovali. Ty, které mají víc balíčků pravděpodobněji budete dále podporovat v budoucnu své práce.

- *Otevřít zdroj příspěvky*: Mnoho balíčků jsou zachována ve úložišť open source, což umožní vývojářům v závislosti na jejich přímo přispívat opravy chyb a vylepšení funkcí. Příspěvek historie libovolný daný balíček je také jasně ukazuje na tom, kolik vývojáři aktivně podílejí.

- *Dotazovat vlastníci*: pro nové vývojáře určitě může být stejně zaměřuje na vytváření skvělých balíčků můžete použít, a je dobré dáte jim možnost vám něco nového ekosystému NuGet. S myslete na to, kontaktujte přímo do balíčku vývojáře prostřednictvím **kontakt vlastníky** v části **informace** na stránce výpis. Je pravděpodobné, že potěší spolupracovat s vámi na sloužit vašim potřebám!

- *Vyhrazené předpony adres ID balíčku*: jste použili pro mnoho vlastníků balíčku a byla udělena [předpona ID balíčku vyhrazené](../reference/id-prefix-reservation.md). Když se zobrazí vizuální značky zaškrtnutí vedle ID balíčku na [nuget.org](https://www.nuget.org/), nebo v sadě Visual Studio, to znamená, že splňuje vlastníka balíčku naše [kritéria](../reference/id-prefix-reservation.md#id-prefix-reservation-criteria) ID předpony rezervace. To znamená, že se vymazat o identifikaci sami sebe i jejich balíček vlastníka balíčku.

> [!Note]
> Vždycky mějte balíčku licenčních podmínek, které můžete zobrazit tak, že vyberete **informace o licenci** na stránce balíčků na nuget.org. Pokud balíček nejsou zadány licenční podmínky, obraťte se přímo pomocí vlastníka balíčku **obraťte se na vlastníky** odkaz na stránce balíček. Společnost Microsoft není licence duševního vlastnictví, od poskytovatelů třetích stran balíček a neodpovídá za informace, které jsou poskytovány třetími stranami.

## <a name="search-syntax"></a>Syntaxe vyhledávání

Balíček NuGet – hledání funguje na nuget.org, z příkazového řádku NuGet a z tohoto rozšíření Správce balíčků NuGet v sadě Visual Studio. Obecně platí hledání se použije pro klíčová slova, jakož i popis balíčku.

- **Klíčová slova**: Vyhledá odpovídající balíčky, které obsahují některé zadaná klíčová slova. Příklad: `modern UI`. Hledání pro balíčky, které obsahují všechna zadaná klíčová slova, použijte "+" mezi podmínky, jako například `modern+UI`.
- **Fráze**: zadání termínů v uvozovkách hledá přesné shod nerozlišujících velikost písmen s těmito podmínkami. Příklad: `"modern UI" package`
- **Filtrování**: můžete použít hledaný výraz na specifickou vlastnost pomocí syntaxe `<property>:<term>` kde `<property>` (velká a malá písmena) může být `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, a `owner`. Podmínky mohou být obsaženy v uvozovkách podle potřeby a více vlastností můžete vyhledat ve stejnou dobu. Také, hledá `id` vlastnosti jsou shody podřetězců, zatímco `packageid` používá přesnou shodu. Příklady:

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
