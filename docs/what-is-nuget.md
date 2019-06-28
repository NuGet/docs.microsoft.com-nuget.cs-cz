---
title: Co je NuGet a co to dělá?
description: Ucelený Úvod do jaké NuGet je a provede
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: 087bb043ba4b388b9de6d94cd838915a2e7247f4
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426135"
---
# <a name="an-introduction-to-nuget"></a>Úvod do NuGet

Je to důležitý nástroj pro libovolnou platformu moderní vývojové mechanismus, pomocí kterého můžete vytvořit, sdílet a využívat užitečné kód vývojáře. Takový kód je často seskupeny do "packages", které obsahují zkompilovaného kódu (jako knihovny DLL) společně s další obsah, je potřeba v projektech, které využívají tyto balíčky.

Pro platformu .NET (včetně .NET Core), je mechanismus podporovaný společností Microsoft ke sdílení kódu **NuGet**, která definuje, jak jsou vytvoření balíčků pro .NET, prostředí a spotřebované, a [poskytuje nástroje,](install-nuget-client-tools.md) pro každou z Tyto role.

Jednoduše řečeno, umístěte NuGet je balíček jednoho souboru ZIP s `.nupkg` rozšíření, které obsahuje zkompilovaný kód knihovny (DLL), další soubory související s tímto kódem a popisný manifestu, který obsahuje informace, jako číslo verze balíčku. Vývojářům kód sdílet vytvořit balíčky a publikujte do veřejných nebo privátních hostitele. Spotřebitele balíčku získat tyto balíčky z vhodné hostitele, je přidat do svých projektů a poté zavolejte funkci balíčku v jejich projektu kódu. NuGet samotné pak zpracovává všechny zprostředkující podrobnosti.

Protože NuGet podporuje privátní hostitele spolu s nuget.org veřejné hostitele, můžete sdílet kód, který je určen výhradně pro organizace nebo pracovní skupině balíčky NuGet. Balíčky NuGet můžete použít také jako pohodlný způsob, jak vlastní kód pro použití v nic ale svoje vlastní projekty. Stručně řečeno, balíček NuGet je jednotka ke sdílení kódu, ale ne vyžadují ani neznamená žádné konkrétní způsob sdílení.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Tok balíčky mezi autory, hostitele a příjemců

V jeho role jako veřejný hostitel NuGet sama udržuje centrálním úložišti víc než 100 000 jedinečné balíčky v [nuget.org](https://www.nuget.org). Tyto balíčky jsou náhradník miliony vývojářů.NET/.NET Core každý den. NuGet také umožňuje hostování balíčků soukromě v cloudu (například na Azure DevOps), v privátní síti, nebo dokonce i na právě vašeho místního systému souborů. Díky tomu tyto balíčky jsou k dispozici pouze vývojáři, kteří mají přístup k hostiteli získáte tak schopnost zpřístupnit balíčky do konkrétní skupiny příjemců. Možnosti jsou vysvětlené v [hostování vlastní kanály NuGet](hosting-packages/overview.md). Pomocí možnosti konfigurace můžete také řídit přesně hostitele je přístupný daného počítače, a zajistí tak, že balíčky jsou získávány z konkrétního zdroje spíše než veřejné úložiště, jako je nuget.org.

Bez ohledu jejich povaze hostitele slouží jako bod připojení mezi balíček *creators* a balíček *příjemci*. Tvůrce sestavení užitečné balíčky NuGet a publikujte je na hostiteli. Příjemci vyhledejte balíčky užitečné a kompatibilní na hostitelích přístupné, stahování a včetně těchto balíčků ve svých projektech. Po instalaci v projektu, rozhraní API balíčky jsou k dispozici pro zbývající část kódu projektu.

![Vztah mezi Tvůrce balíčku, balíčku hostitele a spotřebitele balíčku](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Cílení na kompatibilitu balíčku

Balík "kompatibilní" znamená, že obsahuje sestavení vytvořené pro rozhraní .NET framework minimálně jeden cíl, který je kompatibilní s cílové rozhraní projektu náročné. Vývojáři můžou vytvořit balíčky, které jsou specifické pro jedno rozhraní, stejně jako u ovládacích prvků UPW, nebo zajistit podporu pro používání nástroje většímu počtu cílů. Pro zajištění maximální kompatibility daného balíčku, cíl vývojáři [.NET Standard](/dotnet/standard/net-standard), které můžete využívat projekty všech .NET a .NET Core. To je nejúčinnější způsob pro tvůrců a příjemců, protože jeden balíček (obvykle obsahuje jedno sestavení) se dá použít pro všechny projekty náročné.

Balíček vývojáři, kteří vyžadují rozhraní API mimo .NET Standard, na druhé straně vytvořit samostatné sestavení pro jiné cílové architektury, které mají podporu a zahrnují všechny z těchto sestavení ve stejném balíčku (která se nazývá "cílení na více platforem"). Při instalaci těchto balíčků příjemce extrahuje NuGet pouze sestavení, které jsou potřeba v projektu. Tím se minimalizují nároky balíčku v konečné aplikace a/nebo sestavení vytvořené v daném projektu. Cílení na více platforem balíček je samozřejmě i pro její Autor udržovat obtížnější.

> [!Note]
> Cílení na .NET Standard nahrazuje předchozí přístup používat různé cíle (PCL) knihovny přenosných tříd. Tato dokumentace se proto zaměřuje na vytváření balíčků pro .NET Standard.

## <a name="nuget-tools"></a>Nástroje NuGet

Kromě hostování podpory NuGet také poskytuje celou řadu nástrojů, které používají tvůrců a příjemců. Zobrazit [instalace balíčků NuGet klientské nástroje](install-nuget-client-tools.md) pro získání konkrétních nástrojů.

| Nástroj | Platformy | Použít scénáře | Popis |
| --- | --- | --- | --- |
| [dotnet CLI](consume-packages/install-use-packages-dotnet-cli.md) | Všechny | Vytvoření, spotřeby | Nástroje rozhraní příkazového řádku pro knihovny .NET Core a .NET Standard a sady SDK – vizuální styl projekty, které cílí na rozhraní .NET Framework (viz [SDK atribut](/dotnet/core/tools/csproj#additions)). Poskytuje určité rozhraní příkazového řádku NuGet funkce přímo v rámci řetězce nástrojů .NET Core. Stejně jako u rozhraní příkazového řádku NuGet rozhraní příkazového řádku dotnet nekomunikuje s projekty aplikace Visual Studio. |
| [nuget.exe CLI](consume-packages/install-use-packages-nuget-cli.md) | Všechny | Vytvoření, spotřeby | Nástroj příkazového řádku pro knihovny rozhraní .NET Framework a sady SDK styl projekty, které cílit na knihovny .NET Standard. Nabízí všechny funkce NuGet, kdy některé příkazy použití speciálně pro tvůrce balíčku, použití pouze pro uživatele, a ostatní použitím obou. Například použití Tvůrce balíčku `nuget pack` příkaz pro vytvoření balíčku z různých sestavení a související soubory, balíček příjemci použití `nuget install` zahrnout balíčky do složky projektu a všichni používá `nuget config` nastavit konfiguraci NuGet proměnné. Jako nástroj pro více platforem rozhraní příkazového řádku NuGet nekomunikuje s projekty aplikace Visual Studio. |
| [Konzola Správce balíčků](tools/package-manager-console.md) | Visual Studio na Windows | Využití | Poskytuje [příkazy prostředí PowerShell](tools/Powershell-Reference.md) pro instalaci a správu balíčků v projektech Visual Studio. |
| [Uživatelské rozhraní Správce balíčků](tools/package-manager-ui.md) | Visual Studio na Windows | Využití | Poskytuje snadným ovládáním uživatelského rozhraní pro instalaci a správu balíčků v projektech Visual Studio. |
| [Spravovat NuGet uživatelského rozhraní](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Využití | Poskytují-použití uživatelského rozhraní pro instalaci a správu balíčků v sadě Visual Studio pro Mac projekty. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Vytvoření, spotřeby | Umožňuje vytvořit balíčky a obnovení balíčků se používá v projektu přímo prostřednictvím řetězec nástroje MSBuild. |

Jak je vidět, nástroje NuGet, které při práci s velmi lišit v závislosti na tom, jestli už vytváříte, využívání nebo publikování balíčků a platformy, na kterém pracujete. Tvůrce balíčku jsou obvykle také spotřebitelů, protože jsou postaveny funkce, která existuje v dalších balíčcích NuGet. A tyto balíčky, samozřejmě, může pak záviset na stále jiných.

Další informace, začněte s [pracovní postup vytvoření balíčku](create-packages/Overview-and-Workflow.md) a [zabalit pracovní postup využití](consume-packages/Overview-and-Workflow.md) článků.

## <a name="managing-dependencies"></a>Správa závislostí

Možnost snadno vytvářet na práci ostatních je jednou z nejúčinnějších funkcí systém správy balíčků. Většinu toho, co dělá NuGet je odpovídajícím způsobem, správou tento strom závislostí nebo "graf" jménem projektu. Jednoduše ale nutné dodat, budete potřebovat pouze se týkají sami s balíčky, které používáte přímo v projektu. Pokud žádný z těchto balíčků sami využívání dalších balíčků (které můžou zase využívat stále ostatní), postará o těchto nižší úrovně závislostí NuGet.

Následující obrázek ukazuje projekt, který závisí na pět balíčky, které pak závisí na celé řadě dalších.

![Ukázka grafu závislostí NuGet pro projekt .NET](media/dependency-graph.png)

Všimněte si, že některé balíčky se zobrazí v grafu závislostí více než jednou. Například existují tři různé spotřebitele balíčku B a každý příjemce může také určit jinou verzi pro tento balíček (nezobrazení). To je běžné výskyt, zejména pro nejběžněji používanými balíčky. NuGet naštěstí vykonává všechnu práci obtížné určit přesně kterou verzi balíčku B splňuje všichni příjemci. NuGet pak provede stejné pro všechny ostatní balíčky, bez ohledu na to, jak hluboko grafu závislostí.

Další podrobnosti o jak NuGet provádí této služby najdete v tématu [řešení závislostí](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Sledovacích odkazů a obnovují se balíčky

Protože projekty můžete snadno přesouvat mezi vývojových prostředích, úložišť správy zdrojového kódu, buildovací servery a atd., je vysoce nepraktické, aby binární sestavení přímo vázaný do projektu balíčky NuGet. Mohlo by každou kopii zbytečně opakovaném projektu (a tím odpad místo úložiště správy zdrojového kódu). Ji by také být velmi obtížné aktualizovat binární soubory balíčku na novější verze, protože aktualizace bude muset uplatnit na veškeré kopie tohoto projektu.

NuGet udržuje místo jednoduchých odkazů seznam balíčky, na které projekt závisí, včetně závislosti nejvyšší úrovně a nižší úrovně. To znamená, že pokaždé, když se instalace balíčku z některých hostitele do projektu NuGet zaznamenává identifikátor balíčku a číslo verze v seznamu referencí. (Odinstalovává se balíček, samozřejmě, odebere se ze seznamu.) NuGet pak umožňuje obnovit všechny odkazované balíčky na vyžádání, jak je popsáno na [obnovení balíčku](consume-packages/package-restore.md).

![Seznam odkazů NuGet na instalace balíčku se vytvoří a slouží k obnovení balíčků jinde](media/nuget-restore.png)

S pouze seznam odkazů můžete opětovnou NuGet&mdash;tedy *obnovení*&mdash;všech těchto balíčků z veřejné nebo privátní hostitelů kdykoli později. Při potvrzování projekt do správy zdrojového kódu nebo sdílení jiným způsobem, pouze odkaz na seznamu pro zahrnutí a vyloučení žádné binární soubory balíčku (viz [balíčky a Správa zdrojového kódu](consume-packages/packages-and-source-control.md).)

Počítač, který přijímá projektu, jako je získání kopie projektu jako součást automatizované nasazení systému, server sestavení jednoduše požádá pokaždé, když je budete potřebovat obnovit závislosti balíčků NuGet. Vytvořte systémy, jako je Azure DevOps popisují "Obnovení NuGet" pro tento účel přesné. Podobně, když vývojáři získejte kopii souboru projektu (stejně jako při klonování úložiště), se může vyvolat příkaz podobný `nuget restore` (NuGet rozhraní příkazového řádku), `dotnet restore` (rozhraní příkazového řádku dotnet), nebo `Install-Package` (konzola Správce balíčků) získat všechny potřebné balíčky. Při sestavování projektu sady Visual Studio, jeho části, automaticky obnoví balíčky (za předpokladu, že je povoleno automatické obnovení, jak je popsáno na [obnovení balíčku](consume-packages/package-restore.md)).

Je zřejmé pak Nugetu primární roli. Pokud máte obavy vývojáři udržuje tento odkaz seznam jménem vašeho projektu a poskytuje způsob, jak efektivně obnovení (a aktualizovat) odkazované balíčky. Tento seznam je zachován v jedné ze dvou *balíček správy formáty*, jako jsou volány:

- [PackageReference](consume-packages/package-references-in-project-files.md) (nebo "balíček odkazy v souborech projektu") | *(NuGet 4.0 +)* udržuje seznam nejvyšší úrovně závislosti projektu přímo v rámci souboru projektu, takže je potřeba žádný samostatný soubor. Přidružený soubor `obj/project.assets.json`, generuje dynamicky spravovat celkový graf závislosti balíčků, které projekt používá spolu se všemi závislostmi nižší úrovně. PackageReference vždy používá projekty .NET Core.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 +)*  Soubor ve formátu XML, který udržuje seznam bez stromové struktury všechny závislosti v projektu, včetně závislostí jiných nainstalované balíčky. Balíčky nainstalované nebo obnovený jsou uložené v `packages` složky.

Které formát správy balíčků se použijí v každého projektu závisí na typu projektu a k dispozici verze NuGet (a/nebo Visual Studio). Chcete-li zjistit, jaký formát se používá, jednoduše vyhledejte `packages.config` v kořenové složce projektu po instalaci první balíčku. Pokud tento soubor nemáte, vyhledejte v souboru projektu přímo \<PackageReference\> elementu.

Pokud máte možnost volby, doporučujeme pomocí PackageReference. `packages.config` je zachován z důvodu starší verze účely a už se aktivně vyvíjí.

> [!Tip]
> Různé `nuget.exe` příkazy rozhraní příkazového řádku, jako je třeba `nuget install`, balíček automaticky nepřidávejte do seznam odkazů. V seznamu je aktualizována při instalaci balíčku s Visual Studio Správce balíčků (uživatelského rozhraní nebo konzola) a s `dotnet.exe` rozhraní příkazového řádku.

## <a name="what-else-does-nuget-do"></a>Co dělá NuGet?

Zatím jste se naučili následující vlastnosti balíčku nuget:

- NuGet poskytuje centrální nuget.org úložiště s podporou pro privátní hostování.
- NuGet poskytuje že nástroje, které vývojáři potřebují pro vytváření, publikování a využívání balíčků.
- Co je nejdůležitější NuGet udržuje seznam odkazů v projektu a možnost použít k obnovení a aktualizovat tyto balíčky z tohoto seznamu balíčků.

Chcete-li tyto procesy pracovat efektivně, nemá NuGet optimalizovali pozadí. Zejména NuGet spravuje mezipaměť balíčků a globálních balíčků složku pro místní instalace a přeinstalace. Mezipaměť se vyhnete stahování balíčku, který je už nainstalovaný na počítači. Složka globálních balíčků umožňuje více projektů sdílet stejnou nainstalovaný balíček, a tím snižuje celkový objem NuGet v počítači. Mezipaměť a globální složku balíčků jsou také velmi užitečné, pokud budete často obnovení větší počet balíčků, jak na serveru sestavení. Další podrobnosti o těchto mechanismů, naleznete v tématu [Správa globálních balíčků a složek mezipaměti](consume-packages/managing-the-global-packages-and-cache-folders.md).

V rámci jednotlivých projektů spravuje NuGet celkový graf závislostí, která znovu zahrnuje řešení více odkazů na různé verze stejného balíčku. Je celkem běžné, že projekt je závislá na jeden nebo více balíčků, že sami mají stejné závislosti. Některé nejužitečnější nástroj balíčků na nuget.org se použijí podle mnoha jiných balíčků. V grafu celý závislostí, může snadno máte deset různé odkazy na různé verze stejného balíčku. Chcete-li zabránit přináší více verzí tohoto balíčku do vlastní aplikace, NuGet seřadí si jedné verze mohou využívat všichni příjemci se ve. (Další informace najdete v tématu [řešení závislostí](consume-packages/dependency-resolution.md).)

Kromě toho, NuGet uchovává všechny specifikace související se strukturou balíčky (včetně [lokalizace](create-packages/creating-localized-packages.md) a [symboly ladění](create-packages/symbol-packages.md)) a jak se na ně odkazuje (včetně [ rozsahů verzí](reference/package-versioning.md#version-ranges-and-wildcards) a [předběžných verzí](create-packages/prerelease-packages.md).) NuGet také nabízí různá rozhraní API pro práci se službami prostřednictvím kódu programu a poskytuje podporu pro vývojáře, kteří vytvářejí šablony projektů a rozšíření sady Visual Studio.

Za chvíli procházet obsah pro tuto dokumentaci a uvidíte všechny tyto funkce reprezentována, spolu s přejímá vlastnost Nugetu beginnings zpráva k vydání verze.

## <a name="comments-contributions-and-issues"></a>Komentáře, příspěvky a problémů

Nakonec moc Vítáme komentáře a příspěvky v této dokumentaci&mdash;stačí vybrat **zpětnou vazbu** a **upravit** příkazy horní části libovolné stránky nebo navštivte [dokumentace úložiště](https://github.com/NuGet/docs.microsoft.com-nuget/) a [seznam problémů dokumentace](https://github.com/NuGet/docs.microsoft.com-nuget/issues) na Githubu.

Také Vítáme všechny příspěvky na NuGet, samotný prostřednictvím jeho [různých úložištích GitHub](https://github.com/NuGet/Home); Problémy s NuGet najdete na [ https://github.com/NuGet/home/issues ](https://github.com/NuGet/home/issues).

Užijte si prostředí NuGet!
