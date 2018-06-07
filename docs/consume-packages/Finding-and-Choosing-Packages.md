---
title: Vyhledání a výběr balíčků NuGet
description: Přehled o tom, jak najít a vybrat nejlepší balíčky NuGet pro projekt, včetně podrobností o syntaxe vyhledávání NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: f1bb145229b0db0e8fdb7fdb31a59aa50bd1d57b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817899"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Hledání a vyhodnocení balíčky NuGet pro projekt

Při spouštění všech rozhraní .NET projektu, nebo vždy, když identifikovat funkční potřebu aplikace nebo služby, můžete si ušetřit spoustu času a řešení problémů pomocí existující balíčky NuGet, které kterém musí splnit. Tyto balíčky mohou pocházet z veřejné kolekce [nuget.org](http://www.nuget.org/packages/), nebo privátní zdroj, který poskytuje vaší organizace nebo jiným třetí strany.

## <a name="finding-packages"></a>Hledání balíčků

Když navštíví nuget.org nebo otevřete uživatelské rozhraní Správce balíčků v sadě Visual Studio, zobrazí se seznam balíčků, které jsou seřazené podle celkový počet souborů ke stažení. To okamžitě ukazuje balíčky nejvíce široce používaný mezi miliony projekty rozhraní .NET. Je velmi pravděpodobné, pak, který alespoň některé balíčky uvedené na stránkách první několik budou užitečné v projektech.

![Výchozí zobrazení nuget.org/packages zobrazující nejoblíbenější balíčky](media/Finding-01-Popularity.png)

Upozornění **zahrnout předběžné verze** možnost v horní pravé části stránky. Při výběru nuget.org ukazuje všechny verze balíčků včetně beta a dalších raných verzích. Chcete-li zobrazit pouze stabilní vydaných, zrušte zaškrtnutí políčka.

Pro konkrétní potřeby vyhledávání podle značky (v rámci správce balíčku sady Visual Studio nebo na portálu jako nuget.org) je nejběžnější způsob zjišťování vhodný balíček. Například vyhledávání na "json" uvádí všechny balíčky NuGet, které jsou označené této – klíčové slovo a proto mají některé relace do formátu JSON.

![Výsledky hledání, json, v nuget.org](media/Finding-02-SearchResults.png)

Můžete také prohledat pomocí ID balíčku, pokud ho znáte. V tématu [hledání syntaxe](#search-syntax) níže.

V tomto okamžiku vyhledávání výsledky jsou seřazené jenom podle závažnosti, proto je obecně projděte alespoň první několik stránkách s výsledky pro balíčky, která vyhovuje vašim potřebám, nebo upřesnit termíny být konkrétnější.

### <a name="does-the-package-support-my-projects-target-framework"></a>Podporuje balíček cílový framework projektu Moje?

Pouze v případě, že tento balíček podporované architektury patří cílový framework projektu na NuGet nainstaluje balíček do projektu. Pokud balíček není kompatibilní, vydá NuGet k chybě.

Některé balíčky seznamu jejich podporované architektury přímo v galerii nuget.org, ale protože taková data se nevyžaduje, mnoho balíčky nezahrnují tohoto seznamu. V současné době neexistuje žádný způsob, jak hledat nuget.org pro balíčky, které podporují konkrétní cílové rozhraní (Tato funkce je v úvahu, najdete v části [NuGet problém 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Naštěstí můžete zjistit podporované architektury dvě jinými způsoby:

1. Pokus o instalaci balíčku do projektu pomocí [ `Install-Package` ](../tools/ps-ref-install-package.md) příkazu v konzole Správce balíčků NuGet. Pokud balíček není kompatibilní, tento příkaz zobrazí podporované architektury balíčku.

1. Stáhněte si balíček z jeho stránky na nuget.org pomocí **ruční stažení** v části **informace**. Změňte příponu z `.nupkg` k `.zip`a otevřete soubor a zkontrolujte obsah jeho `lib` složky. Vidíme podsložky pro každou z podporovaných rozhraní, kde je každý podsložku s názvem se Přezdívka cílový framework (TFM; najdete v části [cílové rozhraní](../reference/target-frameworks.md)). Pokud se zobrazí žádné podsložky `lib` a pouze jeden soubor DLL a potom jste musí pokusíte nainstalovat balíček ve vašem projektu a zjistit jeho kompatibility.

## <a name="pre-release-packages"></a>Předběžné verze balíčků

Beta verze i dál vylepšení a hledat zpětnou vazbu na jejich nejnovější revize k dispozici mnoho autoři balíček zpřístupněte preview.

Ve výchozím nastavení zobrazuje nuget.org předběžné verze balíčků ve výsledcích hledání. Chcete-li vyhledávat pouze stabilní verze, zrušte **zahrnout předběžné verze** možnost v horní pravé části stránky

![Zahrnout předběžné verze zaškrtávací políčko je na nuget.org](media/Finding-06-include-prerelease.png)

V sadě Visual Studio a při použití rozhraní příkazového řádku nástroje NuGet a dotnet nezahrnuje NuGet předprodejní verze ve výchozím nastavení. Chcete-li toto chování změnit, proveďte následující kroky:

- **Správce balíčků uživatelského rozhraní v sadě Visual Studio**: V **spravovat balíčky NuGet** uživatelského rozhraní, nastavte **zahrnout předběžné verze** pole. Nastavení nebo zrušíte zaškrtnutí tohoto políčka aktualizuje uživatelské rozhraní Správce balíčků a seznam dostupných verzí, které můžete instalovat.

    ![Políčko zahrnout předběžné verze v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Konzola správce balíčků**: použití `-IncludePrerelease` přepínač s `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, a `Update-Package` příkazy. Odkazovat [referenční informace prostředí PowerShell](../tools/powershell-reference.md).

- **nuget.exe rozhraní příkazového řádku**: použití `-prerelease` přepínač s `install`, `update`, `delete`, a `mirror` příkazy. Odkazovat [odkaz NuGet rozhraní příkazového řádku](../tools/nuget-exe-cli-reference.md)

- **DotNet.exe rozhraní příkazového řádku**: Zadejte přesnou předběžnou verzi pomocí `-v` argument. Odkazovat [dotnet přidat odkaz na balíček](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Nativní balíčky C++

NuGet podporuje nativní C++ balíčky můžete použitého v projektech C++ v sadě Visual Studio. Díky tomu **spravovat balíčky NuGet** zavádí příkaz kontextové nabídky pro projekty, `native` cílový framework a aby poskytuje integraci nástroje MSBuild.

Najít nativní balíčky na [nuget.org](https://www.nuget.org/packages), vyhledávání pomocí `tag:native`. Tyto balíčky obvykle poskytují `.targets` a `.props` soubory, které NuGet importuje automaticky při přidání balíčku do projektu.

## <a name="evaluating-packages"></a>Vyhodnocení balíčky

Stáhněte a vyzkoušejte ji v kódu (všechny balíčky v nuget.org pravidelně hledat viry, tím) je nejlepší způsob, jak vyhodnotit užitečnost balíčku. Po všech každého balíčku pro vysoce oblíbených získali začít s jenom pár vývojářům používat, a může být jedním z inovátoři!

Ve stejnou dobu pomocí balíčku NuGet, znamená, že trvá závislost, takže chcete Ujistěte se, zda je robustní a spolehlivé. Vzhledem k instalaci a přímo testování balíček je časově náročná, můžete si také přečíst mnoho o kvality balíček podle informací uvedených na stránce výpis balíčku:

- *Soubory ke stažení statistiky*: na stránce balíček na nuget.org, **statistiky** část zobrazuje celkový počet souborů ke stažení, soubory ke stažení nejnovější verze, a stáhne průměr za den. Vyšší číslo vyjadřuje, že mnoho jinými vývojáři trvá závislost na balíčku, což znamená, že ho ukázal.

    ![Statistika na stránce balíček pro výpis stahování](media/Finding-03-Downloads.png)

- *Historie verzí*: na stránce balíček, podívejte se do části **informace** k datu nejnovější aktualizace a prozkoumat **historie verzí**. Dobře zachována balíček obsahuje nejnovější aktualizace a historie bohaté verzí. Opomenutí balíčky několik aktualizace a nebyly často aktualizovány za chvíli.

    ![Historie verzí na stránce balíček pro výpis](media/Finding-04-VersionHistory.png)

- *Poslední nainstaluje*: na stránce balíček pod **statistiky**, vyberte **zobrazit úplnou statistiky**. Stránka úplné statistiky ukazuje, že balíček nainstaluje za posledních šest týdny číslem verze. Balíček, který používáte aktivně jinými vývojáři je obvykle vhodnější než ten, který není.

- *Podpora*: na stránce balíček v části **informace o**, vyberte **web projektu** (Pokud je k dispozici) chcete zobrazit, jaké podporu možnosti Autor poskytuje. Obecně je lépe podporována projektu s lokalitou vyhrazené.

- *Historie vývojáře*: na stránce balíček pod **vlastníky**, vyberte vlastníka zobrazíte další balíčky, které budou jste publikovali. Ty s více balíčků budou s větší pravděpodobností, chcete-li pokračovat, podporuje práci v budoucnu.

- *Otevřete zdroj příspěvky*: mnoho balíčky jsou zachována ve open-source úložiště, aby bylo možné pro vývojáře v závislosti na jejich přímo přispívat oprav chyb a vylepšení funkcí. Příspěvek historii libovolný daný balíček je také kolik vývojáři aktivně podílejí vhodný indikátor.

- *Dotazovat vlastníci*: nové vývojáře určitě může být stejně potvrdit k vytváření kvalitních balíčky budete muset používat a je vhodné jim dát šanci, aby něco nové ekosystému NuGet. Myslete na to, oslovení přímo pro vývojáře balíček prostřednictvím **obraťte se na vlastníky** možnost pod **informace o** na stránce výpis. Pravděpodobné, bude se radostí spolupracovat s vámi na slouží vašim potřebám!

- *Rezervované předpony ID balíčku*: jste použili pro mnoho vlastníky balíček a byla udělena [předpona ID vyhrazené balíček](../reference/id-prefix-reservation.md). Až se zobrazí visual zaškrtnutí vedle ID balíčku na [nuget.org](https://www.nuget.org/), nebo v sadě Visual Studio, to znamená, že vlastníka balíčku splnil naše [kritéria](../reference/id-prefix-reservation.md#id-prefix-reservation-criteria) pro ID předpony rezervace. To znamená, že vlastníka balíčku se vymazat o identifikaci sami a jejich balíčku.

> [!Note]
> Vždycky mějte na paměti balíček licenčních podmínek, které se zobrazí tak, že vyberete **licenční informace** na stránce výpis balíčku v nuget.org. Pokud balíček neurčuje licenční podmínky, obraťte se na vlastníka balíčku přímo pomocí **obraťte se na vlastníky** odkaz na stránce balíček. Společnost Microsoft není licence duševního vlastnictví vám ze zprostředkovatelů balíček třetích stran a není zodpovědná za informace třetích stran.

## <a name="search-syntax"></a>Syntaxe vyhledávání

Hledání balíčků NuGet funguje stejně v nuget.org, z příkazového řádku NuGet a v rámci rozšíření Správce balíčků NuGet v sadě Visual Studio. Obecně platí hledání se použije pro klíčová slova, jakož i popis balíčku.

- **Klíčová slova**: vyhledávání hledá relevantní balíčky, které obsahují všechny zadané klíčová slova. Příklad: `modern UI`. K vyhledání pro balíčky, které obsahují všechny zadané klíčová slova, použijte "+" mezi podmínky, jako například `modern+UI`.
- **Fráze**: zadání termínů v uvozovkách hledá přesné velká a malá písmena shody pro tyto podmínky. Příklad: `"modern UI" package`
- **Filtrování**: můžete použít hledaný termín k určité vlastnosti pomocí syntaxe `<property>:<term>` kde `<property>` (velká a malá písmena) může být `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, a `owner`. Podmínek může být obsažený v uvozovkách, v případě potřeby a více vlastností můžete vyhledat ve stejnou dobu. Navíc hledá `id` vlastnost jsou odpovídá dílčí řetězec, zatímco `packageid` používá přesnou shodu. Příklady:

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
