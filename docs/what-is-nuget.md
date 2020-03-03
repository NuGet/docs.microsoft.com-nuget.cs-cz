---
title: Co je NuGet a co dělá?
description: Komplexní Úvod do toho, co je NuGet a dělá
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: c326cf184ff20fb798a5770f0a4cf9bf42bed3f5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230691"
---
# <a name="an-introduction-to-nuget"></a>Úvod do NuGetu

Důležitým nástrojem pro moderní vývojovou platformu je mechanismus, pomocí kterého můžou vývojáři vytvářet, sdílet a využívat užitečný kód. Tento kód je často obsažen do balíčku "Packages", které obsahují zkompilovaný kód (jako knihovny DLL), spolu s dalším obsahem potřebným v projektech, které využívají tyto balíčky.

Pro .NET (včetně .NET Core) je mechanismus podporovaný společností Microsoft pro sdílení kódu **NuGet**, který definuje, jak se vytvářejí, hostují a spotřebovávají balíčky pro .NET, a [poskytuje nástroje](install-nuget-client-tools.md) pro každou z těchto rolí.

Jednoduše řečeno, balíček NuGet je jeden soubor ZIP s rozšířením `.nupkg`, které obsahuje zkompilovaný kód (DLL), další soubory související s tímto kódem a popisným manifestem, který obsahuje informace, jako je číslo verze balíčku. Vývojáři s kódem ke sdílení vytváření balíčků a jejich publikování na veřejném nebo privátním hostiteli. Příjemci balíčku získají tyto balíčky od vhodných hostitelů, přidají je do svých projektů a pak volají funkce balíčku ve svém kódu projektu. Samotný NuGet potom zpracuje všechny mezilehlé podrobnosti.

Vzhledem k tomu, že NuGet podporuje privátní hostitele spolu s veřejným hostitelem nuget.org, můžete použít balíčky NuGet ke sdílení kódu, který je exkluzivní pro organizaci nebo pracovní skupinu. Balíčky NuGet můžete také použít jako pohodlný způsob, jak sami použít vlastní kód pro použití v žádném, ale ve svých vlastních projektech. V krátkém případě je balíčkem NuGet jednotka, která je sdílená, ale nevyžaduje ani neimplikuje jakýkoliv konkrétní způsob sdílení.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Tok balíčků mezi tvůrci, hostiteli a příjemci

Ve své roli jako veřejný hostitel aplikace NuGet udržuje centrální úložiště více než 100 000 jedinečných balíčků na [NuGet.org](https://www.nuget.org). Tyto balíčky jsou zaměstnaní miliony vývojářů .NET/.NET Core každý den. NuGet taky umožňuje hostovat balíčky soukromě v cloudu (například na Azure DevOps), v privátní síti nebo dokonce jenom v místním systému souborů. Díky tomu jsou tyto balíčky k dispozici pouze vývojářům, kteří mají přístup k hostiteli, což vám umožní zpřístupnit balíčky pro konkrétní skupinu uživatelů. Tyto možnosti jsou vysvětleny na [hostování vlastních kanálů NuGet](hosting-packages/overview.md). Prostřednictvím možností konfigurace můžete také řídit přesně to, k jakým hostitelům je možné získat pøístup z určitého počítače, a zajistit tak, aby se balíčky získaly z konkrétních zdrojů, a ne jako veřejné úložiště, jako je nuget.org.

Bez ohledu na jeho charakter hostitel slouží jako bod propojení mezi *tvůrci* *balíčků a uživateli balíčku.* Tvůrci sestavují užitečné balíčky NuGet a publikují je na hostitele. Příjemci pak hledají užitečné a kompatibilní balíčky na dostupných hostitelích, stahují a zahrnují tyto balíčky v jejich projektech. Po instalaci v projektu jsou balíčky rozhraní API k dispozici pro zbytek kódu projektu.

![Vztah mezi tvůrci balíčků, hostiteli balíčků a příjemci balíčku](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Kompatibilita cílení balíčku

"Kompatibilní" balíček znamená, že obsahuje sestavení vytvořená pro alespoň jeden cílový rozhraní .NET Framework kompatibilní s cílovým rozhraním .NET Framework projektu. Vývojáři mohou vytvářet balíčky, které jsou specifické pro jedno rozhraní, stejně jako u ovládacích prvků UWP nebo mohou podporovat širší rozsah cílů. Pro maximalizaci kompatibility balíčku cílí vývojářům [.NET Standard](/dotnet/standard/net-standard), které mohou využívat všechny projekty .NET a .NET Core. Toto je nejúčinnější způsob pro tvůrce i spotřebitele, jako jeden balíček (obvykle obsahující jedno sestavení) funguje pro všechny náročné projekty.

Vývojáři balíčku, kteří potřebují rozhraní API mimo .NET Standard, vytvoří na druhé straně samostatné sestavení pro různé cílové architektury, které chtějí podporovat, a zahrnují všechna tato sestavení ve stejném balíčku (což se označuje jako "cílení na více verzí"). Když příjemce takový balíček nainstaluje, NuGet extrahuje pouze ta sestavení, která jsou potřebná pro projekt. Tím se minimalizují nároky balíčku do konečné aplikace nebo sestavení vytvořená tímto projektem. Balíček s vícenásobným cílením je samozřejmě obtížnější pro jeho správu.

> [!Note]
> Cílení na .NET Standard nahrazují předchozí přístup pomocí různých cílů přenosných knihoven tříd (PCL). Tato dokumentace se proto zaměřuje na vytváření balíčků pro .NET Standard.

## <a name="nuget-tools"></a>Nástroje NuGet

Kromě podpory hostování nabízí také NuGet celou řadu nástrojů používaných tvůrci i spotřebiteli. Informace o tom, jak získat konkrétní nástroje, najdete v tématu [Instalace nástrojů klienta NuGet](install-nuget-client-tools.md) .

| Nástroj | Platformy | Příslušné scénáře | Popis |
| --- | --- | --- | --- |
| [dotnet CLI](consume-packages/install-use-packages-dotnet-cli.md) | Všechny | Vytváření, spotřeba | Nástroj rozhraní příkazového řádku pro knihovny .NET Core a .NET Standard a pro projekty ve stylu sady SDK, které cílí na .NET Framework (viz [atribut sady SDK](/dotnet/core/tools/csproj#additions)). Poskytuje určité funkce rozhraní příkazového řádku NuGet přímo v řetězu nástrojů .NET Core. Stejně jako u `nuget.exe` CLI, rozhraní příkazového řádku dotnet nekomunikuje s projekty sady Visual Studio. |
| [nuget.exe CLI](consume-packages/install-use-packages-nuget-cli.md) | Všechny | Vytváření, spotřeba | Nástroj rozhraní příkazového řádku pro knihovny .NET Framework a projekty, které nejsou ve stylu sady SDK, které cílí na .NET Standard knihovny. Poskytuje všechny funkce NuGet a některé příkazy, které se konkrétně použijí pro tvůrce balíčků, některé se použijí jenom pro příjemce a jiné, jak se používají. Tvůrci balíčků můžou například pomocí příkazu `nuget pack` vytvořit balíček z různých sestavení a souvisejících souborů. příjemci balíčku používají `nuget install` k zahrnutí balíčků do složky projektu a všichni používají `nuget config` k nastavení konfiguračních proměnných NuGet. Jako nástroj Platform-nezávislá, rozhraní příkazového řádku NuGet nekomunikuje s projekty sady Visual Studio. |
| [Konzola Správce balíčků](consume-packages/install-use-packages-powershell.md) | Visual Studio ve Windows | Využití | Poskytuje [Příkazy prostředí PowerShell](reference/Powershell-Reference.md) pro instalaci a správu balíčků v projektech sady Visual Studio. |
| [Uživatelské rozhraní Správce balíčků](consume-packages/install-use-packages-visual-studio.md) | Visual Studio ve Windows | Využití | Poskytuje snadno použitelné uživatelské rozhraní pro instalaci a správu balíčků v projektech sady Visual Studio. |
| [Spravovat uživatelské rozhraní NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio pro Mac | Využití | Poskytněte snadno použitelné uživatelské rozhraní pro instalaci a správu balíčků v Visual Studio pro Macch projektech. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Vytváření, spotřeba | Poskytuje možnost vytvářet balíčky a balíčky pro obnovení používané v projektu přímo prostřednictvím řetězce nástroje MSBuild. |

Jak vidíte, nástroje NuGet, se kterými pracujete, závisí na tom, jestli vytváříte, spotřebováváte nebo publikujete balíčky a platformu, na které pracujete. Tvůrci balíčků jsou obvykle také příjemci, protože se vytvářejí nad funkcemi, které existují v jiných balíčcích NuGet. A tyto balíčky samozřejmě můžou záviset na ostatních.

Další informace najdete v článcích pracovní postup [Vytvoření balíčku](create-packages/Overview-and-Workflow.md) a [pracovní postup spotřeby balíčku](consume-packages/Overview-and-Workflow.md) .

## <a name="managing-dependencies"></a>Správa závislostí

Možnost snadného sestavování na práci s ostatními je jedním z nejvýkonnějších funkcí systém správy balíčků. Proto mnoho z toho, co NuGet, spravuje strom závislostí nebo "Graph" jménem projektu. Jednoduše řečeno, potřebujete se s balíčky, které přímo používáte v projektu, týkat pouze sebe. Pokud některý z těchto balíčků využívá jiné balíčky (které můžou zase využívat jiné), NuGet se stará o všechny závislosti nižší úrovně.

Následující obrázek ukazuje projekt, který závisí na pěti balíčcích, což zase závisí na několika dalších.

![Příklad grafu závislosti NuGet pro projekt .NET](media/dependency-graph.png)

Všimněte si, že některé balíčky se v grafu závislostí zobrazují několikrát. Například existují tři různé uživatele balíčku B a každý příjemce může také určit jinou verzi pro daný balíček (nezobrazuje se). Jedná se o běžný výskyt, hlavně pro široce používané balíčky. NuGet Naštěstí má veškerou práci přesně určit, která verze balíčku B splňuje všechny uživatele. NuGet pak bude stejný pro všechny ostatní balíčky bez ohledu na to, jak hluboko mají graf závislosti.

Další podrobnosti o tom, jak NuGet provádí tuto službu, najdete v tématu věnovaném [řešení závislosti](concepts/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Sledování odkazů a obnovování balíčků

Vzhledem k tomu, že se projekty mohou snadno přesouvat mezi vývojářskými počítači, úložišti správy zdrojového kódu, servery sestavení a tak dále, je vysoce praktické uchovávat binární sestavení balíčků NuGet přímo vázaných na projekt. To by vedlo k tomu, že každá kopie projektu zbytečně bloated (a tím se zaznamenalo volné místo v úložištích správy zdrojového kódu). V důsledku toho by bylo obtížné aktualizovat binární soubory balíčku na novější verze, protože by se aktualizace musely použít ve všech kopiích projektu.

NuGet místo toho udržuje jednoduchý seznam odkazů balíčků, na kterých závisí projekt, včetně závislostí na nejvyšší úrovni i na nižší úrovni. To znamená, že při každém instalaci balíčku z nějakého hostitele do projektu zaznamená NuGet identifikátor balíčku a číslo verze v seznamu odkazů. (Odinstalace balíčku je samozřejmě odebrána ze seznamu.) NuGet pak poskytuje způsob obnovení všech odkazovaných balíčků na vyžádání, jak je popsáno v tématu [obnovení balíčků](consume-packages/package-restore.md).

![Seznam odkazů NuGet se vytvoří při instalaci balíčku a dá se použít k obnovení balíčků jinde.](media/nuget-restore.png)

Balíčky NuGet pak můžou znovu přeinstalovat jenom v seznamu odkazů,&mdash;to znamená *obnovit*&mdash;všechny tyto balíčky z veřejných i privátních hostitelů. Když potvrdíte projekt do správy zdrojového kódu nebo ho nasdílíte jiným způsobem, zahrnete pouze seznam odkazů a vyloučíte všechny binární soubory balíčku (viz [balíčky a Správa zdrojového kódu](consume-packages/packages-and-source-control.md)).

Počítač, který obdrží projekt, jako je například server sestavení, získá kopii projektu jako součást systému automatizovaného nasazení, jednoduše požádá NuGet, aby obnovil závislosti, kdykoli je budete potřebovat. Systémy sestavení, jako je Azure DevOps, poskytují pro tento přesný účel kroky obnovení NuGet. Obdobně, když vývojáři získají kopii projektu (jako při klonování úložiště), mohou vyvolat příkaz jako `nuget restore` (CLI CLI), `dotnet restore` (dotnet CLI), nebo `Install-Package` (konzola správce balíčků) a získat všechny potřebné balíčky. Sada Visual Studio pro svou součást automaticky obnoví balíčky při sestavování projektu (za předpokladu, že automatické obnovení je povoleno, jak je popsáno v tématu [obnovení balíčku](consume-packages/package-restore.md)).

Jasně a pak primární role NuGet, kde se vývojáři týkají, udržují tento seznam odkazů jménem projektu a poskytují způsob, jak efektivně obnovit (a aktualizovat) tyto balíčky, na které se odkazuje. Tento seznam je udržován v jednom ze dvou *formátů správy balíčků*, jak se nazývají:

- [PackageReference](consume-packages/package-references-in-project-files.md) (nebo "odkazy na balíčky v souborech projektu") | *(NuGet 4.0 +)* Udržuje seznam závislostí nejvyšší úrovně projektu přímo v rámci souboru projektu, takže není potřeba žádný samostatný soubor. Přidružený soubor `obj/project.assets.json`, je dynamicky generován pro správu celkového grafu závislostí balíčků, které projekt používá společně se všemi závislostmi na nižší úrovni. PackageReference se vždy používají v projektech .NET Core.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 +)* soubor XML, který udržuje plochý seznam všech závislostí v projektu, včetně závislostí dalších instalovaných balíčků. Nainstalované nebo obnovené balíčky se ukládají do složky `packages`.

Který formát správy balíčků je zaměstnán v libovolném daném projektu, závisí na typu projektu a dostupné verzi NuGetu (a/nebo Visual studia). Pokud chcete zkontrolovat, který formát se používá, stačí po instalaci prvního balíčku najít `packages.config` v kořenovém adresáři projektu. Pokud tento soubor nemáte, hledejte v souboru projektu přímo pro \<PackageReference\> elementu.

Pokud máte možnost výběru, doporučujeme použít PackageReference. `packages.config` se udržuje pro starší účely a už není v aktivním vývoji.

> [!Tip]
> Různé `nuget.exe` příkazy rozhraní příkazového řádku, jako je `nuget install`, nepřidá balíček do seznamu odkazů automaticky. Seznam se aktualizuje při instalaci balíčku pomocí Správce balíčků sady Visual Studio (uživatelského rozhraní nebo konzoly) a pomocí `dotnet.exe` CLI.

## <a name="what-else-does-nuget-do"></a>Co další NuGet dělá?

Zatím jste se seznámili s následujícími charakteristikami NuGet:

- NuGet poskytuje centrální úložiště nuget.org s podporou pro soukromé hostování.
- NuGet poskytuje vývojářům nástroje potřebu vytvářet, publikovat a využívat balíčky.
- V důsledku toho NuGet udržuje odkazový seznam balíčků použitých v projektu a možnost obnovit a aktualizovat tyto balíčky z tohoto seznamu.

Aby tyto procesy byly efektivně fungovat, NuGet provede některé optimalizace na pozadí. Zejména NuGet spravuje mezipaměť balíčků a globální složku balíčků pro instalaci a přeinstalaci zástupce. Mezipaměť zabraňuje stažení balíčku, který již byl na počítači nainstalován. Složka globální balíčky umožňuje více projektům sdílet stejný nainstalovaný balíček, čímž se sníží celková nároky na počítač NuGet. Složka mezipaměti a globální balíčky jsou také velmi užitečné, pokud často obnovujete větší počet balíčků, jako na serveru sestavení. Další informace o těchto mechanismech najdete v tématu [Správa globálních balíčků a složek mezipaměti](consume-packages/managing-the-global-packages-and-cache-folders.md).

V rámci jednotlivého projektu NuGet spravuje celkový graf závislostí, který znovu zahrnuje překlad více odkazů na různé verze stejného balíčku. Je poměrně běžné, že projekt přebírá závislost na jednom nebo více balíčcích, které mají stejné závislosti. Některé z nejužitečnějších balíčků nástrojů na nuget.org jsou zaměstnané mnoha dalšími balíčky. V celém grafu závislostí můžete snadno mít deset různých odkazů na různé verze stejného balíčku. Aby se zabránilo zavedení více verzí tohoto balíčku do samotné aplikace, NuGet vyřadí jednotlivé verze, které mohou používat všichni uživatelé. (Další informace najdete v tématu věnovaném [řešení závislostí](concepts/dependency-resolution.md).)

Kromě toho NuGet udržuje všechny specifikace týkající se strukturování balíčků (včetně [lokalizačních](create-packages/creating-localized-packages.md) a [ladicích symbolů](create-packages/symbol-packages-snupkg.md)) a způsobu jejich [odkazování](consume-packages/package-references-in-project-files.md) (včetně [rozsahů verzí](concepts/package-versioning.md#version-ranges) a [předběžných verzí](create-packages/prerelease-packages.md)). NuGet také poskytuje různá rozhraní API pro práci s jejími službami programově a poskytuje podporu pro vývojáře, kteří napisují rozšíření sady Visual Studio a šablony projektů.

Chvíli počkejte, než projdete obsah této dokumentace, a zobrazí se všechny tyto funkce, společně s poznámkami k verzi dating zpět na začátek NuGetu.

## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/What-is-NuGet-1-of-5/player]

Další videa k NuGetu najdete na webu [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="comments-contributions-and-issues"></a>Komentáře, příspěvky a problémy

A konečně hodně úvodní komentáře a příspěvky k této dokumentaci&mdash;stačí vybrat příkazy pro **zpětnou vazbu** a **Úpravy** v horní části libovolné stránky nebo přejít na seznam [úložišť docs](https://github.com/NuGet/docs.microsoft.com-nuget/) a [dokumentace k dokumentaci](https://github.com/NuGet/docs.microsoft.com-nuget/issues) na GitHubu.

Také jsme provedli příspěvky do NuGet samotné prostřednictvím [různých úložišť GitHubu](https://github.com/NuGet/Home). Problémy NuGet najdete na [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Využijte své zkušenosti s NuGet!
