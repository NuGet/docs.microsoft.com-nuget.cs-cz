---
title: Co je NuGet a co se dělá? | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/10/2018
ms.topic: overview
ms.prod: nuget
ms.technology: ''
description: Komplexní úvod do jaké NuGet je a nemá
keywords: Správce balíčků NuGet, spotřebu, vytvoření balíčku, který je hostitelem balíčku, rozhraní .NET balíčky, .NET Core balíčky
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0d2094177f919d27b9a8320e60c8d1d75ec18fb6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="an-introduction-to-nuget"></a>Úvod do NuGet

Základní nástroj pro libovolnou platformu pro vývoj moderních je mechanismus, pomocí kterého mohou vývojáři vytvářet, sdílet a využívat užitečné kódu. Takový kód je často seskupeny do "packages", které obsahují zkompilovaný kód (jako knihovny DLL) společně s další obsah, je potřeba v projektů, které využívají tyto balíčky.

Pro platformu .NET (včetně .NET Core), je podporováno Microsoft mechanismus pro sdílení kódu **NuGet**, který definuje jak balíčky pro rozhraní .NET vytvářené hostované a využívat a poskytuje nástroje pro každou z těchto rolí.

Uveďte, jednoduše NuGet je balíček jednoho souboru ZIP s `.nupkg` rozšíření, která obsahuje zkompilovaný kód (DLL), ostatní soubory související s tímto kódem a popisný manifestu, který obsahuje informace, jako číslo verze balíčku. Sdílení vývojáři kódem vytváření balíčků a publikovat je do veřejných nebo privátních hostitele. Balíček příjemci získat tyto balíčky z vhodné hostitele, přidejte je do jejich projektů a pak volání funkce balíčku v jejich kód projektu. NuGet samotné pak zpracovává všechny zprostředkující podrobnosti.

Protože NuGet podporuje privátní hostitele spolu s hostiteli veřejné nuget.org, můžete sdílet kód, který je určena výhradně pro organizaci nebo pracovní skupině balíčky NuGet. Balíčky NuGet můžete použít také jako pohodlný způsob zohlednit vlastní kód pro použití v nic ale vašich vlastních projektů. Stručně řečeno, balíček NuGet je ke sdílení jednotka kódu, ale není vyžadovat ani implikují žádné konkrétní znamená sdílení.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Tok balíčky mezi tvůrcích, hostitele a spotřebitelé

V jeho role jako veřejný hostitel udržuje NuGet samotné centrálním úložištěm více než 100 000 jedinečné balíčky v [nuget.org](https://www.nuget.org). Tyto balíčky jsou zaměstnaní miliony vývojářů.NET/.NET základní každý den. NuGet můžete taky hostitele balíčků soukromě v cloudu (například na Visual Studio Team Services), v privátní síti, nebo dokonce i v právě do místního systému souborů. Díky tomu jsou tyto balíčky k dispozici pouze vývojáři, kteří mají přístup k hostiteli, což vám umožní zpřístupnit balíčky na konkrétní skupinu spotřebitelů. Možnosti jsou vysvětlené na [hostování vlastními kanály NuGet](hosting-packages/overview.md). Pomocí možnosti konfigurace můžete taky řídit, přesně které hostitele je přístupný pomocí libovolného daného počítače a zajistí tak, že balíčky jsou získány z konkrétní zdroje namísto veřejného úložiště jako nuget.org.

Ať jeho povahy, hostitel slouží jako bod připojení mezi balíček *creators* a balíček *příjemci*. Tvůrci sestavení užitečné balíčků NuGet a publikovat je na hostiteli. Příjemci knihovny vyhledejte užitečné a kompatibilní balíčky v přístupné hostitelích, stahování a zahrnutí tyto balíčky do jejich projektů. Po instalaci v projektu, rozhraní API se balíčky jsou k dispozici s ostatními kód projektu.

![Vztah mezi creators balíčku, balíčku hostitelů a spotřebitelé balíčku](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Balíček zaměřený na kompatibility

"Kompatibilní" balíček znamená, že obsahuje sestavení vytvořené pro rozhraní .NET framework minimálně jeden cíl, který je kompatibilní s cílový framework projektu na využívání. Vývojáři mohou vytvořit balíčky, které jsou specifické pro jeden prostředí, stejně jako u UWP ovládací prvky, nebo mohou podporovat většímu počtu cílů. Maximalizovat kompatibilitu balíček, vývojáři cíl [.NET Standard](/dotnet/standard/net-standard), které může využívat všechny .NET a .NET Core projekty. Toto je nejúčinnější způsob pro creators i příjemci, jako jednoho balíčku (obvykle obsahující jednoho sestavení) se dá použít na všechny projekty náročná.

Balíček vývojáře, kteří potřebují rozhraní API mimo standardní .NET na druhé straně vytvořit samostatné sestavení pro různé cílové rozhraní, které chtějí podporovat a zahrnout všechny tyto sestavení stejného balíčku (což se označuje jako "cílení na více"). Při instalaci příjemce takový balíček NuGet extrahuje pouze sestavení, které jsou vyžadovány projektu. Tím se minimalizují nároky balíčku v konečné aplikace nebo sestavení vyprodukované daného projektu. Cílení na více balíček je kurzu pro jeho autorovi udržovat obtížnější.

> [!Note]
> Cílení na rozhraní .NET standardní nahrazuje předchozí postup použití různých tříd portable knihovny (PCL) cíle. Tato dokumentace se proto zaměřuje na vytvoření balíčků pro .NET Standard.

## <a name="nuget-tools"></a>Nástroje pro NuGet

Kromě hostování podpory, NuGet taky poskytuje celou řadu nástrojů používané creators a příjemce. V tématu [NuGet instalaci klienta nástroje](install-nuget-client-tools.md) pro získání konkrétních nástrojů.

| Nástroj | Platformy | Použít scénáře | Popis |
| --- | --- | --- | --- |
| [nuget.exe CLI](tools/nuget-exe-cli-reference.md) | Všechny | Vytváření, spotřeba | Nabízí všechny funkce NuGet, se některé příkazy platného pro balíček tvůrcích, použití pouze k příjemce, a ostatní použití na obojí. Například balíček creators použití `nuget pack` příkazu vytvořit balíček z různých sestavení a související soubory, balíček příjemci použití `nuget install` mají být zahrnuty balíčků ve složce projektu a everyone používá `nuget config` nastavit konfiguraci NuGet proměnné. Jako nástroj bez ohledu na platformu rozhraní příkazového řádku NuGet nekomunikuje s projektů sady Visual Studio. |
| [dotnet CLI](tools/dotnet-Commands.md) | Všechny | Vytváření, spotřeba | Poskytuje rozhraní příkazového řádku určité NuGet možnosti přímo v řetězu nástroj .NET Core. Stejně jako u rozhraní příkazového řádku NuGet dotnet rozhraní příkazového řádku nekomunikuje s projektů sady Visual Studio. |
| [Konzola Správce balíčků](tools/package-manager-console.md) | Visual Studio v systému Windows | Spotřeba | Poskytuje [příkazy prostředí PowerShell](tools/Powershell-Reference.md) k instalaci a správě balíčků v projektech Visual Studio. |
| [Uživatelské rozhraní Správce balíčků](tools/package-manager-ui.md) | Visual Studio v systému Windows | Spotřeba | Poskytuje snadno použitelné uživatelské rozhraní pro instalaci a správě balíčků v projektech Visual Studio. |
| [Spravovat NuGet uživatelského rozhraní](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Spotřeba | Zadejte snadno použitelné uživatelské rozhraní pro instalaci a správě balíčků v sadě Visual Studio pro Mac projekty. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Vytváření, spotřeba | Umožňuje vytvořit balíčky a balíčky v projektu přímo přes řetězu nástroje MSBuild použité obnovení. |

Jak vidíte, nástroje NuGet, které pracujete s velmi lišit v závislosti na tom, zda vytváříte, využívání nebo publikování balíčků a platformy, na kterém pracujete. Tvůrci balíčku jsou obvykle také příjemci, při vytváření nad funkce, která existuje v dalších balíčcích NuGet. A tyto balíčky samozřejmě může zase závisí na ještě jiné.

Další informace, začínat [pracovní postup vytvoření balíčku](create-packages/Overview-and-Workflow.md) a [balíček spotřeba pracovního postupu](consume-packages/Overview-and-Workflow.md) články.

## <a name="managing-dependencies"></a>Správa závislostí

Umožňuje snadno vytvářet na práci jiných je jedním z nejúčinnějších funkce systém správy balíčků. Podle toho hodně jaké NuGet spravuje tento strom závislosti nebo "grafu" jménem projektu. Jednoduše řečeno, budete potřebovat vztahuje pouze na sami s balíčky, které přímo používáte v projektu. Pokud žádný z těchto balíčků sami využívat jiné balíčky (které, pak spotřebovat stále ostatní), má na starosti NuGet všechny tyto závislosti nižší úrovně.

Následující obrázek znázorňuje projekt, který závisí na pět balíčků, které pak závisí na několika jiných.

![Příklad NuGet závislost grafu pro rozhraní .NET projektu](media/dependency-graph.png)

Všimněte si, že některé balíčky zobrazí v grafu závislostí vícekrát. Například existují tři různé zákazníci balíčku B a každý příjemce může také zadejte jinou verzi pro tento balíček (není vidět). To je běžné v situaci, zejména pro nejběžněji používané balíčky. NuGet naštěstí vykonává všechnu práci pevný k určení přesně kterou verzi balíčku B splňuje všichni příjemci. NuGet pak dělá to stejné pro všechny ostatní balíčky, bez ohledu na to, jak hluboko graf závislostí.

Další informace o tom, jak NuGet provede této služby najdete v tématu [řešení závislostí](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Sledování odkazů a obnovení balíčků

Protože projekty můžou snadno přesunout mezi počítači vývojáře, zdrojová ovládací prvek úložiště, servery sestavení a atd., je vysoce nepraktické zachovat binární sestavení balíčky NuGet přímo spojen s projektem. To by každý kopii zbytečně opakovaném projektu (a tím odpady místa v zdrojová ovládací prvek úložiště). Ho by způsobují, že velmi obtížné aktualizovat binární soubory balíčku na novější verze, které aktualizace se vztahovat na celou všechny kopie projektu.

NuGet místo uchovává jednoduchý odkaz seznam balíčků, na kterých závisí na projekt včetně závislosti nejvyšší úrovně a nižší úrovně. To znamená vždy, když nainstalovat balíček z některé hostitele do projektu, NuGet zaznamenává identifikátor balíčku a číslo verze v seznamu odkaz. (Odinstalaci balíčku, samozřejmě odstraní ji ze seznamu.) NuGet pak poskytuje prostředky ke obnovit všechny odkazované balíčky na vyžádání, jak je popsáno na [obnovení balíčků](consume-packages/package-restore.md).

![Je vytvořen na instalace balíčku NuGet referenční seznam a slouží k obnovení balíčků jinde](media/nuget-restore.png)

S pouze seznam odkazů, můžete znovu NuGet&mdash;tedy *obnovení*&mdash;všech těchto balíčků z veřejné nebo soukromé hostitelů kdykoli později. Při potvrzování projektu do správy zdrojového kódu nebo sdílení jiným způsobem, můžete zahrnout pouze seznam odkazů a vyloučit všechny binární soubory balíčku (viz [balíčky a Správa zdrojového kódu](consume-packages/packages-and-source-control.md).)

Počítač, který obdrží projektu, například server sestavení získat kopii projektu v rámci systému automatického nasazení, jednoduše požádá NuGet vždy, když už jste zapotřebí obnovit závislosti. Sestavte systémy jako Visual Studio Team Services popisují "NuGet restore" pro tento účel přesný. Podobně když vývojáři získejte kopii souboru projektu (stejně jako při klonování úložiště), se může vyvolat příkaz jako `nuget restore` (NuGet rozhraní příkazového řádku), `dotnet restore` (dotnet rozhraní příkazového řádku), nebo `Install-Package` (konzolu Správce balíčků) a získat všechny potřebné balíčky. Při sestavování projektu Visual Studio pro jeho část automaticky obnoví balíčky (za předpokladu, že je povoleno automatické obnovení, jak je popsáno na [obnovení balíčků](consume-packages/package-restore.md)).

Je zřejmé pak NuGet primární roli, kde jsou příslušné vývojáři udržuje tento odkaz seznam jménem projektu a poskytuje možnosti pro efektivní obnovení (a aktualizovat) tyto odkazované balíčky. Tento seznam se udržuje v jednom ze dvou *balíček správy formáty*, jak se nazývají se:

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 +)* soubor ve formátu XML, který udržuje plochý seznam všechny závislosti v projektu, včetně závislostí jiné nainstalované balíčky. Instalace nebo obnovený balíčky jsou uložené v `packages` složky.

- [PackageReference](consume-packages/package-references-in-project-files.md) (nebo "balíček odkazy v souborech projektu") | *(NuGet 4.0 +)* udržuje seznam nejvyšší úrovně závislosti projektu přímo v souboru projektu, aby bylo možné žádný samostatný soubor. Přidružený soubor, `obj/project.assets.json`, se dynamicky vygeneruje ke správě celkové graf závislosti balíčků, které projektu používá spolu s všechny závislosti nižší úrovně. PackageReference vždy používá projekty .NET Core.

Formát balíčku správy zaměstnání v jakékoli dané projektu závisí na typu projektu a dostupná verze NuGet (nebo v sadě Visual Studio). Pokud chcete zkontrolovat, jaký formát se používá, jednoduše vyhledejte `packages.config` v kořenu projektu po instalaci vašeho prvního balíčku. Pokud nemáte tento soubor, vyhledejte v souboru projektu přímo pro \<PackageReference\> element.

Pokud máte možnost volby, doporučujeme používat PackageReference. `packages.config` bude zachována pro účely starší verze a již není ve službě active vývoji.

> [!Tip]
> Různé `nuget.exe` příkazy rozhraní příkazového řádku, jako je třeba `nuget install`, balíček automaticky nepřidávejte do seznamu odkaz. V seznamu je aktualizována při instalaci balíčku a s Visual Studio Správce balíčků (uživatelského rozhraní nebo konzola) s `dotnet.exe` rozhraní příkazového řádku.

## <a name="what-else-does-nuget-do"></a>Co dalšího NuGet dělá?

Když, pokud jste se naučili následující vlastnosti balíčku nuget:

- NuGet poskytuje centrální nuget.org úložiště s podporou pro privátní hostování.
- NuGet poskytuje že vývojářům nástroje pro vytváření, publikování a využívání balíčky potřebovat.
- Co je nejdůležitější – NuGet udržuje odkaz na seznam balíčků v projektu a možnost umožňuje obnovit a aktualizovat tyto balíčky z tohoto seznamu.

Chcete-li tyto procesy efektivní práci, nemá NuGet některé servisní optimalizace. Zejména NuGet spravuje balíček mezipaměti a globální balíčky složku pro místní instalace a přeinstalace. Mezipaměti zabraňuje, stahování balíčku, který je už nainstalovaný na počítači. Složku globální balíčky umožňuje více projektů sdílet stejné nainstalovaným balíčkem, což snižuje celkové nároky NuGet v počítači. Do mezipaměti a globální balíčky složky jsou také velmi užitečné, pokud se často obnovení větší počet balíčků, jako na sestavení serveru. Další informace o těchto mechanismů v [správy globální balíčky a složky mezipaměti](consume-packages/managing-the-global-packages-and-cache-folders.md).

V rámci jednotlivých projektů spravuje NuGet celkové graf závislostí, která znovu obsahuje několik odkazů na různé verze stejného balíčku řešení. Je celkem běžné, že projektu trvá závislost na jeden nebo více balíčků, aby sami mají stejné závislosti. Některé balíčky nejužitečnější nástroj na nuget.org zaměstnává mnoho dalších balíčků. V tomto grafu celý závislostí pak můžete snadno mít deset jiné odkazy na různé verze stejného balíčku. Abyste se vyhnuli, přináší několik verzí tohoto balíčku do vlastní aplikace, NuGet seřadí se které jedna verze mohou využívat všichni příjemci. (Další informace najdete v tématu [řešení závislostí](consume-packages/dependency-resolution.md).)

Kromě toho, NuGet udržuje všechny specifikace související na tom, jak jsou strukturovaná balíčky (včetně [lokalizace](create-packages/creating-localized-packages.md) a [symboly ladění](create-packages/symbol-packages.md)) a jak se odkazuje (včetně [ verze rozsahy](reference/package-versioning.md#version-ranges-and-wildcards) a [předprodejní verze](create-packages/prerelease-packages.md).) NuGet také poskytuje různé rozhraní API pro práci s jeho služby prostřednictvím kódu programu a poskytuje podporu pro vývojáře, kteří vytvářejí rozšíření sady Visual Studio a projekt šablony.

Za chvíli procházet obsah pro tuto dokumentaci, a zobrazí všechny tyto funkce reprezentované existuje, společně s poznámky k verzi z roku NuGet beginnings.

## <a name="comments-contributions-and-issues"></a>Komentáře, příspěvky a problémy

Nakonec velmi mnohem Vítáme komentáře a příspěvky k této dokumentace&mdash;právě vyberte **zpětné vazby** a **upravit** příkazy horní všechny stránky, nebo navštívit [dokumentace úložiště](https://github.com/NuGet/docs.microsoft.com-nuget/) a [dokumentace problém seznamu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) na Githubu.

Vítáme příspěvky k NuGet samotné prostřednictvím jeho [různých úložišť GitHub](https://github.com/NuGet/Home); Problémy s NuGet najdete na [ https://github.com/NuGet/home/issues ](https://github.com/NuGet/home/issues).

Užijte si ji prostředí NuGet!
