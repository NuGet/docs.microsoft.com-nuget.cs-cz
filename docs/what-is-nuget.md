---
title: Co je NuGet a co dělá?
description: Komplexní úvod do toho, co NuGet je a dělá
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: c326cf184ff20fb798a5770f0a4cf9bf42bed3f5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230691"
---
# <a name="an-introduction-to-nuget"></a>Úvod do NuGet

Základním nástrojem pro všechny moderní vývojové platformy je mechanismus, jehož prostřednictvím vývojáři mohou vytvářet, sdílet a využívat užitečný kód. Často takový kód je dodáván do "balíčky", které obsahují kompilovaný kód (jako Knihovny DLL) spolu s dalším obsahem potřebným v projektech, které spotřebovávají tyto balíčky.

Pro rozhraní .NET (včetně .NET Core) je mechanismus podporovaný společností Microsoft pro sdílení kódu **NuGet**, který definuje, jak jsou balíčky pro rozhraní .NET vytvářeny, hostovány a spotřebovány a [poskytuje nástroje](install-nuget-client-tools.md) pro každou z těchto rolí.

Jednoduše řečeno, balíček NuGet je jeden `.nupkg` soubor ZIP s příponou, která obsahuje zkompilovaný kód (DLL), další soubory související s tímto kódem a popisný manifest, který obsahuje informace, jako je číslo verze balíčku. Vývojáři s kódem pro sdílení vytvářet balíčky a publikovat je na veřejném nebo soukromém hostiteli. Příjemci balíčků získat tyto balíčky z vhodných hostitelů, přidat je do svých projektů a potom volat funkce balíčku v jejich kódu projektu. NuGet sám pak zpracovává všechny podrobnosti mezilehlé.

Vzhledem k tomu, že NuGet podporuje soukromé hostitele vedle veřejného nuget.org hostitele, můžete použít balíčky NuGet ke sdílení kódu, který je výhradní pro organizaci nebo pracovní skupinu. Můžete také použít Balíčky NuGet jako pohodlný způsob, jak faktor vlastní kód pro použití v nic, ale vlastní projekty. Stručně řečeno, Balíček NuGet je sdílet jednotku kódu, ale nevyžaduje ani neznamenají žádné konkrétní prostředky sdílení.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Tok balíčků mezi tvůrci, hostiteli a spotřebiteli

Ve své roli jako veřejný hostitel, NuGet sám udržuje centrální úložiště více než 100 000 jedinečných balíčků na [nuget.org](https://www.nuget.org). Tyto balíčky jsou zaměstnány miliony vývojářů .NET/.NET Core každý den. NuGet také umožňuje hostovat balíčky soukromě v cloudu (například na Azure DevOps), v privátní síti nebo dokonce pouze v místním systému souborů. Tímto způsobem jsou tyto balíčky k dispozici pouze pro vývojáře, kteří mají přístup k hostiteli, což vám dává možnost zpřístupnit balíčky určité skupině spotřebitelů. Možnosti jsou [vysvětleny na Hostování vlastní NuGet kanály](hosting-packages/overview.md). Prostřednictvím možností konfigurace můžete také přesně určit, ke kterým hostitelům může daný počítač přistupovat, a tím zajistit, aby balíčky byly získány z konkrétních zdrojů, nikoli z veřejného úložiště, jako je nuget.org.

Bez ohledu na jeho povahu, hostitel slouží jako bod spojení mezi *tvůrci* balíčků a *balíček spotřebitelů*. Tvůrci vytvářet užitečné balíčky NuGet a publikovat je na hostitele. Spotřebitelé pak vyhledávají užitečné a kompatibilní balíčky na přístupných hostitelích, stahují a zařazují tyto balíčky do svých projektů. Po instalaci v projektu jsou rozhraní API balíčků k dispozici pro zbytek kódu projektu.

![Vztah mezi tvůrci balíčků, hostiteli balíčků a příjemci balíčků](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Kompatibilita cílení balíčků

"Kompatibilní" balíček znamená, že obsahuje sestavení vytvořená pro alespoň jeden cílový rámec .NET framework, který je kompatibilní s cílovým rámcem náročného projektu. Vývojáři mohou vytvářet balíčky, které jsou specifické pro jednu architekturu, jako s ovládacími prvky UPW, nebo mohou podporovat širší rozsah cílů. Chcete-li maximalizovat kompatibilitu balíčku, vývojáři cíl [.NET Standard](/dotnet/standard/net-standard), které všechny .NET a .NET Core projekty mohou využívat. Jedná se o nejúčinnější prostředek pro tvůrce i spotřebitele, protože jeden balíček (obvykle obsahující jedno sestavení) funguje pro všechny náročné projekty.

Vývojáři balíčků, kteří vyžadují rozhraní API mimo standard .NET, na druhé straně vytvořte samostatná sestavení pro různé cílové architektury, které chtějí podporovat, a zahrnout všechna tato sestavení do stejného balíčku (což se nazývá "multi-targeting"). Když příjemce nainstaluje takový balíček, NuGet extrahuje pouze ty sestavení, které jsou potřebné pro projekt. Tím se minimalizuje nároky na balíček v konečné aplikaci nebo sestavení chodu tohoto projektu. Balíček s více cíleními je samozřejmě pro jeho tvůrce obtížnější udržet.

> [!Note]
> Cílení .NET Standard nahrazuje předchozí přístup pomocí různých cílů knihovny přenosných tříd (PCL). Tato dokumentace se proto zaměřuje na vytváření balíčků pro rozhraní .NET Standard.

## <a name="nuget-tools"></a>Nástroje NuGet

Kromě hostování podpory, NuGet také poskytuje celou řadu nástrojů používaných tvůrci i spotřebiteli. Informace o tom, jak získat konkrétní nástroje, najdete v [tématu Instalace klientských nástrojů NuGet.](install-nuget-client-tools.md)

| Nástroj | Platformy | Použitelné scénáře | Popis |
| --- | --- | --- | --- |
| [Rozhraní příkazového řádku dotnet](consume-packages/install-use-packages-dotnet-cli.md) | Všechny | Tvorba, spotřeba | Nástroj rozhraní CLI pro knihovny .NET Core a .NET Standard a pro projekty ve stylu sady SDK, které cílí na rozhraní .NET Framework (viz [atribut SDK).](/dotnet/core/tools/csproj#additions) Poskytuje určité funkce rozhraní NGet CLI přímo v rámci řetězce nástrojů .NET Core. Stejně `nuget.exe` jako u rozhraní se kontinua, rozhraní se kontinuu dotnet CLI nepracuje s projekty sady Visual Studio. |
| [Rozhraní příkazového řádku nuget.exe](consume-packages/install-use-packages-nuget-cli.md) | Všechny | Tvorba, spotřeba | Nástroj rozhraní CLI pro knihovny rozhraní .NET Framework a projekty, které nejsou ve stylu sady SDK a které cílí na knihovny .NET Standard. Poskytuje všechny funkce NuGet, s některými příkazy, které se vztahují konkrétně na tvůrce balíčků, některé platí pouze pro spotřebitele a jiné platí pro oba. Například tvůrci balíčků `nuget pack` používají příkaz k vytvoření balíčku z různých sestavení `nuget install` a souvisejících souborů, spotřebitelé balíčků `nuget config` používají k zahrnutí balíčků do složky projektu a všichni používají k nastavení konfiguračních proměnných NuGet. Jako nástroj bez ohledu na platformu NuGet CLI nepracuje s projekty sady Visual Studio. |
| [Konzola Správce balíčků](consume-packages/install-use-packages-powershell.md) | Visual Studio ve Windows | Využití | Poskytuje [příkazy prostředí PowerShell](reference/Powershell-Reference.md) pro instalaci a správu balíčků v projektech sady Visual Studio. |
| [Uživatelské rozhraní Správce balíčků](consume-packages/install-use-packages-visual-studio.md) | Visual Studio ve Windows | Využití | Poskytuje snadno použitelné unové pole pro instalaci a správu balíčků v projektech sady Visual Studio. |
| [Správa nugetu ui](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Využití | Poskytněte snadno použitelné ui pro instalaci a správu balíčků v projektech Visual Studia for Mac. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Tvorba, spotřeba | Poskytuje možnost vytvářet balíčky a obnovovat balíčky používané v projektu přímo prostřednictvím řetězce nástrojů MSBuild. |

Jak můžete vidět, nástroje NuGet, se kterými pracujete, do značné míry závisí na tom, jestli vytváříte, konzumujete nebo publikujete balíčky, a na platformě, na které pracujete. Tvůrce balíčků jsou obvykle také spotřebitelé, protože sestavení na vrcholu funkce, která existuje v jiných balíčcích NuGet. A tyto balíčky, samozřejmě, může zase záviset na dalších.

Další informace získáte od článků [pro vytvoření balíčku](create-packages/Overview-and-Workflow.md) a [pracovního postupu spotřebou balíčků.](consume-packages/Overview-and-Workflow.md)

## <a name="managing-dependencies"></a>Správa závislostí

Schopnost snadno stavět na práci ostatních je jednou z nejvýkonnějších funkcí systému správy balíčků. V souladu s tím, hodně z toho, co NuGet dělá je správa stromu závislostí nebo "graf" jménem projektu. Jednoduše řečeno, stačí se zabývat těmi balíčky, které přímo používáte v projektu. Pokud některý z těchto balíčků sami využívat jiné balíčky (což může zase využívat další), NuGet se postará o všechny tyto závislosti nižší úrovně.

Následující obrázek znázorňuje projekt, který závisí na pěti balíčcích, které zase závisí na řadě dalších.

![Příklad nugetového grafu závislostí pro projekt .NET](media/dependency-graph.png)

Všimněte si, že některé balíčky se zobrazí vícekrát v grafu závislostí. Například existují tři různí příjemci balíčku B a každý spotřebitel může také zadat jinou verzi pro tento balíček (není zobrazeno). To je běžný jev, zejména pro široce používané balíčky. NuGet naštěstí provádí všechny tvrdé práce přesně určit, která verze balíčku B splňuje všechny spotřebitele. NuGet pak dělá totéž pro všechny ostatní balíčky, bez ohledu na to, jak hluboko závislost grafu.

Další podrobnosti o tom, jak NuGet provádí tuto službu, naleznete [v tématu Překlad závislostí](concepts/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Sledování odkazů a obnovení balíčků

Vzhledem k tomu, že projekty lze snadno pohybovat mezi vývojářské počítače, úložiště správy zdrojového kódu, sestavení serverů a tak dále, je velmi nepraktické zachovat binární sestavení balíčků NuGet přímo vázána na projekt. Tím by se každá kopie projektu zbytečně nafoukla (a tím i plýtvání prostorem v úložištích správy zdrojového kódu). To by také velmi obtížné aktualizovat binární soubory balíčku na novější verze jako aktualizace by musely být použity ve všech kopiích projektu.

NuGet místo toho udržuje jednoduchý referenční seznam balíčků, na kterých závisí projekt, včetně závislostí na nejvyšší i nižší úrovni. To znamená, že při každé instalaci balíčku z některého hostitele do projektu, NuGet zaznamenává identifikátor balíčku a číslo verze v seznamu odkazů. (Odinstalování balíčku, samozřejmě, odstraní ze seznamu.) NuGet pak poskytuje prostředky k obnovení všech odkazovaných balíčků na vyžádání, jak je popsáno na [package restore](consume-packages/package-restore.md).

![Seznam odkazů NuGet je vytvořen při instalaci balíčku a lze jej použít k obnovení balíčků jinde](media/nuget-restore.png)

Pouze seznam odkazů NuGet pak můžete&mdash;přeinstalovat, který *je, obnovit*&mdash;všechny tyto balíčky z veřejných nebo soukromých hostitelů v pozdější době. Při posunutí projektu ke správě zdrojového kódu nebo jeho sdílení jiným způsobem zahrnete pouze seznam odkazů a vyloučíte všechny binární soubory balíčků (viz [Balíčky a správa zdrojového kódu](consume-packages/packages-and-source-control.md).)

Počítač, který obdrží projekt, jako je například sestavení serveru získání kopie projektu jako součást systému automatického nasazení, jednoduše požádá NuGet obnovit závislosti, kdykoli jsou potřeba. Sestavení systémů, jako je Azure DevOps poskytují "NuGet obnovení" kroky pro tento přesný účel. Podobně když vývojáři získat kopii projektu (jako při klonování úložiště), `nuget restore` mohou vyvolat příkaz `dotnet restore` jako (NuGet CLI), (dotnet CLI) nebo `Install-Package` (Konzola správce balíčků) získat všechny potřebné balíčky. Visual Studio, pro jeho část automaticky obnoví balíčky při vytváření projektu (za předpokladu, že automatické obnovení je povoleno, jak je popsáno na [obnovení balíčku).](consume-packages/package-restore.md)

Je zřejmé, že primární role NuGet, pokud se jedná o vývojáře, udržuje tento seznam odkazů jménem vašeho projektu a poskytuje prostředky k efektivnímu obnovení (a aktualizaci) těchto odkazovaných balíčků. Tento seznam je udržován v jednom ze dvou *formátů správy balíčků*, jak se nazývají:

- [PackageReference](consume-packages/package-references-in-project-files.md) (nebo "odkazy na balíčky v souborech projektu") | *(NuGet 4,0+)* Udržuje seznam závislostí nejvyšší úrovně projektu přímo v souboru projektu, takže není potřeba žádný samostatný soubor. Přidružený soubor `obj/project.assets.json`, je dynamicky generován pro správu grafu celkových závislostí balíčků, které projekt používá spolu se všemi závislostmi nižší úrovně. PackageReference je vždy používán projekty .NET Core.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0+)* Soubor XML, který udržuje plochý seznam všech závislostí v projektu, včetně závislostí jiných nainstalovaných balíčků. Nainstalované nebo obnovené balíčky `packages` jsou uloženy ve složce.

Formát správy balíčků se používá v daném projektu závisí na typu projektu a dostupné verze NuGet (a/nebo Visual Studio). Chcete-li zkontrolovat, jaký formát `packages.config` se používá, jednoduše se podívejte do kořenového adresáře projektu po instalaci prvního balíčku. Pokud tento soubor nemáte, vyhledejte v souboru \<projektu\> přímo element PackageReference.

Pokud máte na výběr, doporučujeme použít PackageReference. `packages.config`je udržována pro starší účely a již není v aktivním vývoji.

> [!Tip]
> Různé `nuget.exe` příkazy příkazu `nuget install`příkazu příkazu příkazu příkazu , jako je například , nepřidávají balíček automaticky do seznamu odkazů. Seznam je aktualizován při instalaci balíčku se Správcem balíčků sady Visual `dotnet.exe` Studio (UI nebo Console) a s cli.

## <a name="what-else-does-nuget-do"></a>Co dalšího nuget dělá?

Zatím jste se naučili následující charakteristiky NuGet:

- NuGet poskytuje centrální nuget.org úložiště s podporou pro soukromý hosting.
- NuGet poskytuje nástroje, které vývojáři potřebují pro vytváření, publikování a využívání balíčků.
- A co je nejdůležitější, NuGet udržuje referenční seznam balíčků používaných v projektu a schopnost obnovit a aktualizovat tyto balíčky z tohoto seznamu.

Chcete-li tyto procesy pracovat efektivně, NuGet provede některé optimalizace na pozadí. N. Get zejména spravuje mezipaměť balíčků a složku globálních balíčků pro instalaci a přeinstalaci zástupců. Mezipaměť zabraňuje stahování balíčku, který již byl v počítači nainstalován. Složka globální balíčky umožňuje více projektů sdílet stejný nainstalovaný balíček, čímž se sníží celkové nároky NuGet v počítači. Složka mezipaměti a globální balíčky jsou také velmi užitečné, když často obnovujete větší počet balíčků, jako na serveru sestavení. Další podrobnosti o těchto mechanismech naleznete [v tématu Správa globálních balíčků a složek mezipaměti](consume-packages/managing-the-global-packages-and-cache-folders.md).

V rámci jednotlivého projektu NuGet spravuje celkový graf závislostí, který opět zahrnuje řešení více odkazů na různé verze stejného balíčku. Je zcela běžné, že projekt má závislost na jednom nebo více balíčcích, které samy o sobě mají stejné závislosti. Některé z nejužitečnějších balíčků nástrojů na nuget.org jsou využívány mnoha dalšími balíčky. V grafu závislostí pak můžete snadno mít deset různých odkazů na různé verze stejného balíčku. Chcete-li se vyhnout uvedení více verzí tohoto balíčku do samotné aplikace, NuGet seřadí, které jednu verzi lze použít všechny spotřebitele. (Další informace naleznete v [tématu Řešení závislostí](concepts/dependency-resolution.md).)

Kromě toho NuGet udržuje všechny specifikace týkající se struktury balíčků (včetně [lokalizačních](create-packages/creating-localized-packages.md) a [ladicích symbolů)](create-packages/symbol-packages-snupkg.md)a způsobu, jakým jsou [odkazovány](consume-packages/package-references-in-project-files.md) (včetně [rozsahů verzí](concepts/package-versioning.md#version-ranges) a [předběžných verzí](create-packages/prerelease-packages.md).) NuGet také poskytuje různá rozhraní API pro práci s jeho služby programově a poskytuje podporu pro vývojáře, kteří píší rozšíření sady Visual Studio a šablony projektů.

Udělejte si chvilku procházet obsah pro tuto dokumentaci a uvidíte všechny tyto funkce zastoupeny tam, spolu s poznámkami k verzi se datuje k začátkům NuGet.

## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/What-is-NuGet-1-of-5/player]

Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="comments-contributions-and-issues"></a>Komentáře, příspěvky a problémy

Nakonec velmi vítáme komentáře a příspěvky&mdash;do této dokumentace, stačí vybrat příkazy **Zpětná vazba** a **upravit** v horní části libovolné stránky nebo navštívit [seznam problémů dokumentů](https://github.com/NuGet/docs.microsoft.com-nuget/) a [dokumentů](https://github.com/NuGet/docs.microsoft.com-nuget/issues) na GitHubu.

Vítáme také příspěvky do nuGet sám prostřednictvím různých [úložišť GitHub](https://github.com/NuGet/Home); NuGet problémy lze [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues)nalézt na .

Užijte si svůj NuGet zážitek!
