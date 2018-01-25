---
title: "Co je NuGet a co se dělá? | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/10/2018
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
description: "Komplexní úvod do jaké NuGet je a nemá"
keywords: "Správce balíčků NuGet, využívání, vytvoření balíčku, balíčku, který je hostitelem"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e670fa6174f8dc9954ef9eebc06f61e84112117d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="an-introduction-to-nuget"></a>Úvod do NuGet

Základní nástroj pro libovolnou platformu pro vývoj moderních je mechanismus, pomocí kterého mohou vývojáři vytvářet, sdílet a využívat užitečné kódu. Takový kód je často seskupeny do "packages", které obsahují zkompilovaný kód (jako knihovny DLL) společně s další obsah, je potřeba v projektů, které využívají tyto balíčky.

Pro platformu .NET, je podporováno Microsoft mechanismus pro sdílení kódu **NuGet**, který definuje jak balíčky pro rozhraní .NET vytvářené hostované a využívat a poskytuje nástroje pro každou z těchto rolí.

Uveďte, jednoduše NuGet je balíček jednoho souboru ZIP s `.nupkg` rozšíření, která obsahuje zkompilovaný kód (DLL), ostatní soubory související s tímto kódem a popisný manifestu, který obsahuje informace, jako číslo verze balíčku. Sdílení vývojáři kódem vytváření balíčků a publikovat je do veřejných nebo privátních hostitele. Balíček příjemci získat tyto balíčky z vhodné hostitele, přidejte je do jejich projektů a pak volání funkce balíčku v jejich kód projektu. NuGet samotné pak zpracovává všechny zprostředkující podrobnosti.

Protože NuGet podporuje privátní hostitele spolu s hostiteli veřejné nuget.org, můžete sdílet kód, který je určena výhradně pro organizaci nebo pracovní skupině balíčky NuGet. Balíčky NuGet můžete použít také jako pohodlný způsob zohlednit vlastní kód pro použití v nic ale vašich vlastních projektů. Stručně řečeno, balíček NuGet je ke sdílení jednotka kódu, ale není vyžadovat ani implikují žádné konkrétní znamená sdílení.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Tok balíčky mezi tvůrcích, hostitele a spotřebitelé

V jeho role jako veřejný hostitel udržuje NuGet samotné centrálním úložištěm více než 100 000 jedinečné balíčky v [nuget.org](https://www.nuget.org). Tyto balíčky jsou zaměstnaní miliony vývojářů .NET každý den. NuGet můžete taky hostitele balíčků soukromě v cloudu (například na Visual Studio Team Services), v privátní síti, nebo dokonce i v právě do místního systému souborů. Díky tomu jsou tyto balíčky k dispozici pouze vývojáři, kteří mají přístup k hostiteli, což vám umožní zpřístupnit balíčky na konkrétní skupinu spotřebitelů. Možnosti jsou vysvětlené na [hostování vlastními kanály NuGet](Hosting-Packages/Overview.md). Pomocí možnosti konfigurace můžete taky řídit, přesně které hostitele je přístupný pomocí libovolného daného počítače a zajistí tak, že balíčky jsou získány z konkrétní zdroje namísto veřejného úložiště jako nuget.org.

Ať jeho povahy, hostitel slouží jako bod připojení mezi balíček *creators* a balíček *příjemci*. Tvůrci sestavení užitečné balíčků NuGet a publikovat je na hostiteli. Příjemci knihovny vyhledejte užitečné a kompatibilní balíčky v přístupné hostitelích, stahování a zahrnutí tyto balíčky do jejich projektů. Po instalaci v projektu, rozhraní API se balíčky jsou k dispozici s ostatními kód projektu.

![Vztah mezi creators balíčku, balíčku hostitelů a spotřebitelé balíčku](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Balíček zaměřený na kompatibility

"Kompatibilní" balíček znamená, že obsahuje sestavení vytvořené pro rozhraní .NET framework minimálně jeden cíl, který je kompatibilní s cílový framework projektu na využívání. Vývojáři mohou vytvořit balíčky, které jsou specifické pro jeden prostředí, stejně jako u UWP ovládací prvky, nebo mohou podporovat většímu počtu cílů. Maximalizovat kompatibilitu balíček, vývojáři cíl [.NET Standard](/dotnet/standard/net-standard), které může využívat všechny projekty rozhraní .NET. Toto je nejúčinnější způsob pro creators i příjemci, jako jednoho balíčku (obvykle obsahující jednoho sestavení) se dá použít na všechny projekty náročná.

Balíček vývojáře, kteří potřebují rozhraní API mimo standardní .NET na druhé straně vytvořit samostatné sestavení pro různé cílové rozhraní, které chtějí podporovat a zahrnout všechny tyto sestavení stejného balíčku (což se označuje jako "cílení na více"). Při instalaci příjemce takový balíček NuGet extrahuje pouze sestavení, které jsou vyžadovány projektu. Tím se minimalizují nároky balíčku v konečné aplikace nebo sestavení vyprodukované daného projektu. Cílení na více balíček Pokud kurzu pro jeho autorovi udržovat obtížnější.

> [!Note]
> Cílení na rozhraní .NET standardní nahrazuje předchozí postup použití různých "knihovny přenosných tříd" (PCL) cíle. Tato dokumentace se proto zaměřuje na vytvoření balíčků pro .NET Standard.

## <a name="nuget-tools"></a>Nástroje pro NuGet

Kromě hostování podpory, NuGet také poskytuje celou řadu nástrojů používané creators a spotřebitelé:

| Nástroj | Platformy | Použít scénáře | Popis |
| --- | --- | --- | --- |
| [nuget.exe CLI](Tools/nuget-exe-CLI-Reference.md) | Všechny | Vytváření, spotřeba | Nabízí všechny funkce NuGet, se některé příkazy platného pro balíček tvůrcích, použití pouze k příjemce, a ostatní použití na obojí. Například balíček creators použití `nuget pack` příkazu vytvořit balíček z různých sestavení a související soubory, balíček příjemci použití `nuget install` mají být zahrnuty balíčků ve složce projektu a everyone používá `nuget config` nastavit konfiguraci NuGet proměnné. Jako nástroj bez ohledu na platformu rozhraní příkazového řádku NuGet nekomunikuje s projektů sady Visual Studio. |
| [dotnet CLI](Tools/dotnet-Commands.md) | Všechny | Vytváření, spotřeba | Poskytuje rozhraní příkazového řádku určité NuGet možnosti přímo v řetězu nástroj .NET Core. Stejně jako u rozhraní příkazového řádku NuGet dotnet rozhraní příkazového řádku nekomunikuje s projektů sady Visual Studio. |
| [Konzola Správce balíčků](Tools/Package-Manager-Console.md) | Visual Studio v systému Windows | Spotřeba | Poskytuje [příkazy prostředí PowerShell](Tools/Powershell-Reference.md) k instalaci a správě balíčků v projektech Visual Studio. |
| [Uživatelské rozhraní Správce balíčků](Tools/Package-Manager-UI.md) | Visual Studio v systému Windows | Spotřeba | Poskytuje snadno použitelné uživatelské rozhraní pro instalaci a správě balíčků v projektech Visual Studio. |
| [Spravovat NuGet uživatelského rozhraní](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Spotřeba | Zadejte snadno použitelné uživatelské rozhraní pro instalaci a správě balíčků v sadě Visual Studio pro Mac projekty. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Vytváření, spotřeba | Umožňuje vytvořit balíčky a balíčky v projektu přímo přes řetězu nástroje MSBuild použité obnovení. |

Jak vidíte, nástroje NuGet, které pracujete s velmi lišit v závislosti na tom, zda vytváříte, využívání nebo publikování balíčků a platformy, na kterém pracujete. Tvůrci balíčku jsou obvykle také příjemci, při vytváření nad funkce, která existuje v dalších balíčcích NuGet. A tyto balíčky samozřejmě může zase závisí na ještě jiné.

Další informace, začínat [pracovní postup vytvoření balíčku](Create-Packages/Overview-and-Workflow.md) a [balíček spotřeba pracovního postupu](Consume-Packages/Overview-and-Workflow.md) články.

## <a name="managing-dependencies"></a>Správa závislostí

Umožňuje snadno vytvářet na práci jiných je jedním z nejúčinnějších funkce systém správy balíčků. Podle toho hodně jaké NuGet spravuje tento strom závislosti nebo "grafu" jménem projektu. Jednoduše řečeno, budete potřebovat vztahuje pouze na sami s balíčky, které přímo používáte v projektu. Pokud žádný z těchto balíčků sami využívat jiné balíčky (které, pak spotřebovat stále ostatní), má na starosti NuGet všechny tyto závislosti nižší úrovně.

Následující obrázek znázorňuje projekt, který závisí na pět balíčků, které pak závisí na několika jiných.

![Příklad NuGet závislost grafu pro rozhraní .NET projektu](media/dependency-graph.png)

Všimněte si, že některé balíčky zobrazí v grafu závislostí vícekrát. Například existují tři různé zákazníci balíčku B a každý příjemce může také zadejte jinou verzi pro tento balíček (není vidět). To je běžné v situaci, zejména pro nejběžněji používané balíčky. NuGet naštěstí vykonává všechnu práci pevný k určení přesně kterou verzi balíčku B splňuje všichni příjemci. NuGet pak dělá to stejné pro všechny ostatní balíčky, bez ohledu na to, jak hluboko graf závislostí.

Další informace o tom, jak NuGet provede této služby najdete v tématu [řešení závislostí](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Sledování odkazů a obnovení balíčků

Protože projekty můžou snadno přesunout mezi počítači vývojáře, zdrojová ovládací prvek úložiště, servery sestavení a atd., je vysoce nepraktické zachovat binární sestavení z balíčků NuGet přímo spojen s projektem. To by to vytvořit každou kopii zbytečně opakovaném projektu (a tím odpady místa v zdrojová ovládací prvek úložiště). Ho by způsobují, že velmi obtížné aktualizovat binární soubory balíčku na novější verze, které aktualizace se vztahovat na celou všechny kopie projektu.

NuGet místo uchovává jednoduchý odkaz seznam balíčků, na kterých závisí na projekt včetně závislosti nejvyšší úrovně a nižší úrovně. To znamená vždy, když nainstalovat balíček z některé hostitele do projektu, NuGet zaznamenává identifikátor balíčku a číslo verze v seznamu odkaz. (Odinstalaci balíčku, samozřejmě odstraní ji ze seznamu.) NuGet pak poskytuje prostředky ke obnovit všechny odkazované balíčky na vyžádání, jak je popsáno na [obnovení balíčků](Consume-Packages/Package-Restore.md).

![Je vytvořen na instalace balíčku NuGet referenční seznam a slouží k obnovení balíčků jinde](media/nuget-restore.png)

S pouze seznam odkazů, můžete znovu NuGet&mdash;tedy *obnovení*&mdash;všech těchto balíčků z veřejné nebo soukromé hostitelů kdykoli později. Při potvrzování projektu do správy zdrojového kódu nebo sdílení jiným způsobem, můžete zahrnout pouze seznam odkazů a vyloučit všechny binární soubory balíčku (viz [balíčky a Správa zdrojového kódu](Consume-Packages/Packages-and-Source-Control.md).)

Počítač, který obdrží projektu, například server sestavení získat kopii projektu v rámci systému automatického nasazení, jednoduše požádá NuGet vždy, když už jste zapotřebí obnovit závislosti. Sestavte systémy jako Visual Studio Team Services popisují "NuGet restore" pro tento účel přesný. Podobně když vývojáři získejte kopii souboru projektu (stejně jako při klonování úložiště), se může vyvolat příkaz jako `nuget restore` (NuGet rozhraní příkazového řádku), `dotnet restore` (dotnet rozhraní příkazového řádku), nebo `Install-Package` (konzolu Správce balíčků) a získat všechny nezbytné balíčků. Visual Studio pro jeho část automaticky obnoví balíčky při vytváření projektu.

Je zřejmé pak NuGet primární roli, kde jsou příslušné vývojáři udržuje tento odkaz seznam jménem projektu a poskytuje možnosti pro efektivní obnovení (a aktualizovat) tyto odkazované balíčky. Tento seznam se udržuje v jednom ze dvou *balíček správy formáty*, jak se nazývají se:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0 +)* soubor ve formátu XML, který udržuje plochý seznam všechny závislosti v projektu, včetně závislostí jiné nainstalované balíčky.
- [PackageReference](Consume-Packages/Package-References-in-Project-Files.md) (nebo "balíček odkazy v souborech projektu") | *(NuGet 4.0 +)* udržuje seznam nejvyšší úrovně závislosti projektu přímo v souboru projektu, aby bylo možné žádný samostatný soubor. Přidružený soubor, `project.assets.json`, se dynamicky vygeneruje ke správě celkové graf závislostí.

Formát balíčku správy zaměstnání v jakékoli dané projektu závisí na typu projektu a dostupná verze NuGet (nebo v sadě Visual Studio). Pokud chcete zkontrolovat, jaký formát se používá, jednoduše vyhledejte `packages.config` v kořenu projektu po instalaci vašeho prvního balíčku. Pokud není tento soubor hledat v souboru projektu přímo pro &lt;PackageReference&gt;element.

## <a name="what-else-does-nuget-do"></a>Co dalšího NuGet dělá?

Když, pokud jste se naučili následující vlastnosti balíčku nuget:
- NuGet poskytuje centrální nuget.org úložiště s podporou pro privátní hostování.
- NuGet poskytuje že vývojářům nástroje pro vytváření, publikování a využívání balíčky potřebovat.
- Co je nejdůležitější – NuGet udržuje odkaz na seznam balíčků v projektu a možnost umožňuje obnovit a aktualizovat tyto balíčky z tohoto seznamu.

Chcete-li tyto procesy efektivní práci, nemá NuGet některé servisní optimalizace. Zejména NuGet spravuje obou celý počítač a ukládá do mezipaměti specifické pro projekt balíček na místní instalace a přeinstalace. Pokud jde o mezipaměť platná pro celý počítač, všechny balíček, který si stáhnout a nainstalovat v projektu je uložený v mezipaměti, tak, aby instalace stejného balíčku v jiném projektu není zpoplatněná jiné stahování. To je jasně velmi užitečné při se často obnovení větší počet balíčků, protože na serveru sestavení. Další podrobnosti pro tento mechanismus a jak s ním pracovat najdete v tématu [Správa mezipaměti NuGet](Consume-Packages/Managing-the-Nuget-Cache.md).

V rámci jednotlivých projektů spravuje NuGet celkové graf závislostí, která znovu obsahuje několik odkazů na různé verze stejného balíčku řešení. Je celkem běžné, že projektu trvá závislost na jeden nebo více balíčků, aby sami mají stejné závislosti. Některé balíčky nejužitečnější nástroj na nuget.org zaměstnává mnoho dalších balíčků. V tomto grafu celý závislostí pak můžete snadno mít deset jiné odkazy na různé verze stejného balíčku. Abyste se vyhnuli, přináší několik verzí tohoto balíčku do vlastní aplikace, NuGet seřadí se které jedna verze mohou využívat všichni příjemci. (Další informace najdete v tématu [řešení závislostí](Consume-Packages/Dependency-Resolution.md).)

Kromě toho, NuGet udržuje všechny specifikace související na tom, jak jsou strukturovaná balíčky (včetně [lokalizace](Create-Packages/Creating-Localized-Packages.md) a [symboly ladění](Create-Packages/Symbol-Packages.md)) a jak se odkazuje (včetně [ verze rozsahy](reference/package-versioning.md#version-ranges-and-wildcards) a [předprodejní verze](create-packages/Prerelease-Packages.md).) NuGet také poskytuje různé rozhraní API pro práci s jeho služby prostřednictvím kódu programu a poskytuje podporu pro vývojáře, kteří vytvářejí rozšíření sady Visual Studio a projekt šablony.

Za chvíli procházet obsah pro tuto dokumentaci, a uvidíte všechny tyto funkce reprezentované existuje, společně s poznámky k verzi z roku NuGet beginnings.

## <a name="comments-contributions-and-issues"></a>Komentáře, příspěvky a problémy

Nakonec velmi mnohem Vítáme komentáře a příspěvky k této dokumentace&mdash;právě vyberte **zpětné vazby** a **upravit** příkazy horní všechny stránky, nebo navštívit [dokumentace úložiště](https://github.com/NuGet/docs.microsoft.com-nuget/) a [dokumentace problém seznamu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) na Githubu.

Vítáme příspěvky k NuGet samotné prostřednictvím jeho [různých úložišť GitHub](https://github.com/NuGet/Home); Problémy s NuGet najdete na [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Užijte si ji prostředí NuGet!
