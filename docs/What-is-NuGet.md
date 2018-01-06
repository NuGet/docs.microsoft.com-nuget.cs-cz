---
title: "Co je NuGet a co se dělá? | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "Komplexní úvod do jaké NuGet je a nemá"
keywords: "Správce balíčků NuGet, využívání, vytvoření balíčku, balíčku, který je hostitelem"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bc6a9e154df287fee6a7e00cc1349dfa2100643
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="an-introduction-to-nuget"></a>Úvod do NuGet

Základní nástroj pro libovolnou platformu pro vývoj moderních je mechanismus, pomocí kterého mohou vývojáři vytvářet, sdílet a využívat užitečné kódu. Takový kód je často seskupeny do "packages" obsahující zkompilovaný kód (jako knihovny DLL) společně s další obsah, je potřeba v projektů, které využívají tyto balíčky.

Pro platformu .NET, tento mechanismus pro sdílení kódu je **NuGet**, který definuje jak balíčky pro rozhraní .NET vytvářené hostované a využívat a poskytuje nástroje pro každou z těchto rolí. 

Uveďte, jednoduše NuGet je balíček jednoho souboru ZIP s `.nupkg` rozšíření, která obsahuje zkompilovaný kód (DLL), ostatní soubory související s tímto kódem a popisný manifestu, který obsahuje informace, jako číslo verze balíčku. Knihovna vývojáři vytvářet soubory balíčku a publikovat je na hostiteli. Balíček příjemci příjem těchto balíčků, přidejte je do jejich projektů a pak volání funkce této knihovny v jejich kód projektu. NuGet samotné pak zpracovává všechny zprostředkující podrobnosti.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Tok balíčky mezi tvůrcích, hostitele a spotřebitelé

V jeho role jako hostitel NuGet sama udržuje centrálním úložišti víc než 60 000 balíčků jedinečný, veřejně dostupné v [nuget.org](https://www.nuget.org). Tyto balíčky jsou zaměstnaní miliony vývojářů .NET každý den. NuGet můžete také k hostování balíčků soukromě v cloudu, v privátní síti nebo dokonce i v právě do místního systému souborů. Díky tomu jsou k dispozici pouze vývojáři v rámci konkrétní skupiny organizace nebo zákazníkovi tyto balíčky. Možnosti jsou vysvětlené na [hostování vlastními kanály NuGet](Hosting-Packages/Overview.md).

Ať jeho povahy, hostitel slouží jako bod připojení mezi balíček *creators* a balíček *příjemci*. Tvůrci sestavení užitečné balíčků NuGet a publikovat je na hostiteli. Příjemci knihovny vyhledejte užitečné a kompatibilní balíčky v přístupné hostitelích, stahování a zahrnutí tyto balíčky do jejich projektů. Po instalaci v projektu, rozhraní API se balíčky jsou k dispozici s ostatními kód projektu.

![Vztah mezi creators balíčku, balíčku hostitelů a spotřebitelé balíčku](media/nuget-roles.png)

"Kompatibilní" balíček v tomto případě znamená, že obsahuje sestavení vytvořené pro rozhraní .NET framework minimálně jeden cíl, který je kompatibilní s cílový framework projektu na využívání. Chcete-li balíček široce kompatibilní, autorovi zkompiluje samostatné sestavení pro různé cílové architektury a obsahuje všechny z nich ve stejném balíčku. Při instalaci tohoto balíčku příjemce NuGet extrahuje pouze sestavení, které jsou vyžadovány projektu. Tím se minimalizují nároky balíčku v konečné aplikace nebo sestavení vyprodukované daného projektu.

## <a name="nuget-tools"></a>Nástroje pro NuGet

Kromě hostování podpory, NuGet také poskytuje celou řadu nástrojů používané creators a spotřebitelé:

| Nástroj | Platformy | Použít scénáře | Popis |
| --- | --- | --- | --- |
| [nuget.exe rozhraní příkazového řádku](Tools/nuget-exe-CLI-Reference.md) | Všechny | Vytváření, spotřeba | Nabízí všechny funkce NuGet, se některé příkazy platného pro balíček tvůrcích, použití pouze k příjemce, a ostatní použití na obojí. Například balíček creators použití `nuget pack` příkazu vytvořit balíček z různých sestavení a související soubory, balíček příjemci použití `nuget install` mezi ně patřit balíčky v projektu a everyone používá `nuget config` nastavit konfiguraci NuGet proměnné.  |
| [Uživatelské rozhraní Správce balíčků](Tools/Package-Manager-UI.md) | Visual Studio v systému Windows | Spotřeba | Poskytuje snadno použitelné uživatelské rozhraní pro instalaci a správě balíčků v projektech pro rozhraní .NET. | 
| [Spravovat NuGet uživatelského rozhraní](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Spotřeba | Zadejte snadno použitelné uživatelské rozhraní pro instalaci a správě balíčků v projektech pro rozhraní .NET. |
| [Konzola Správce balíčků](Tools/Package-Manager-Console.md) | Visual Studio v systému Windows | Spotřeba | Poskytuje [příkazy prostředí PowerShell](Tools/Powershell-Reference.md) k instalaci a správě balíčků v projektech pro rozhraní .NET. | 
| [DotNet rozhraní příkazového řádku](Tools/dotnet-Commands.md) | Všechny | Vytváření, spotřeba | Poskytuje rozhraní příkazového řádku určité NuGet možnosti přímo v rámci nástrojů .NET Core. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Vytváření, spotřeba | Umožňuje vytvořit balíčky a balíčky v projektu přímo prostřednictvím nástrojů MSBuild použité obnovení. |

Jak vidíte, se kterými pracujete s NuGet nástroje závisí výrazně na jestli jste vytváření (a publikování) balíčky nebo využívání a platformu pracujete. Podrobnější informace najdete v [pracovní postup vytvoření balíčku](Create-Packages/Overview-and-Workflow.md) a [pracovního postupu spotřeba balíček](Consume-Packages/Overview-and-Workflow.md) témata, společně s další témata v těchto částech. 

Tvůrci balíčku jsou obvykle také příjemci, při vytváření nad funkce, která existuje v dalších balíčcích NuGet. A tyto balíčky samozřejmě může zase závisí na ještě jiné.

## <a name="managing-dependencies"></a>Správa závislostí

Umožňuje snadno vytvářet na práci jiných je jednou z věcí, které umožňuje tak výkonný systém správy balíčků. Podle toho hodně jaké NuGet spravuje tento strom závislosti nebo "grafu" jménem projektu. Jednoduše řečeno, budete potřebovat vztahuje pouze na sami s balíčky, které přímo používáte v projektu. Pokud žádný z těchto balíčků sami využívat jiné balíčky (které můžou využívat balíčky), má na starosti NuGet všechny tyto závislosti nižší úrovně.

Následující obrázek znázorňuje projekt, který závisí na pět balíčků, které pak závisí na několika jiných.  

![Příklad NuGet závislost grafu pro rozhraní .NET projektu](media/dependency-graph.png)

Všimněte si, že některé balíčky zobrazí v grafu závislostí vícekrát. Například existují tři různé zákazníci balíčku B a každý příjemce může také zadejte jinou verzi pro tento balíček (není vidět). Protože to je běžné v situaci, NuGet naštěstí nepodporuje odstranění náročné práce k určení přesně kterou verzi balíčku B splňuje všechny jeho příjemci. NuGet pak dělá to stejné pro všechny ostatní balíčky, bez ohledu na to, jak hluboko bude graf závislostí.

Další informace o tom, jak NuGet provede této služby najdete v tématu [řešení závislostí](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Sledování odkazů a obnovení balíčků

Protože projekty můžou snadno přesunout mezi počítači vývojáře, zdrojová ovládací prvek úložiště, servery sestavení a atd., je vysoce nepraktické zachovat binární sestavení z balíčků NuGet přímo spojen s projektem. Nejen by to mít každý zkopírujte zbytečně opakovaném projektu (a tím odpady místa v zdrojová ovládací prvek úložiště), jeho by způsobují, že velmi obtížné binární soubory balíčku aktualizace na novější verze, jako by to mít v rámci všechny kopie projekt. 

Místo toho NuGet jednoduše udržuje odkaz na seznam balíčků, na kterých závisí (včetně závislostí nejvyšší úrovně a nižší úrovně) na projekt a poskytuje způsob, jak obnovit všechny odkazované balíčky na vyžádání, jak je popsáno na [balíčku Obnovit](Consume-Packages/Package-Restore.md). To znamená vždy, když nainstalovat balíček z některé hostitele do projektu, NuGet zaznamenává identifikátor balíčku a číslo verze v tomto seznamu odkaz. (Odinstalaci balíčku, samozřejmě odstraní ji ze seznamu.) 

![Je vytvořen na instalace balíčku NuGet referenční seznam a slouží k obnovení balíčků jinde](media/nuget-restore.png)

S pouze seznam odkazů, můžete znovu NuGet&mdash;tedy obnovit&mdash;všech těchto balíčků z veřejné nebo soukromé hostitelů kdykoli později. (Z tohoto důvodu nuget.org neumožňuje trvalé odstranění publikovaných balíčků, i když může být skryté; najdete v části [odstraněním balíčků](Policies/deleting-packages.md).) Při potvrzování projektu do správy zdrojového kódu nebo sdílení jiným způsobem, musí obsahovat pouze seznam odkazů a nemusí zahrnovat všechny binární soubory balíčku (viz [balíčky a Správa zdrojového kódu](Consume-Packages/Packages-and-Source-Control.md).)

Počítač, který obdrží projektu, například server sestavení získat kopii projektu v rámci systému automatického nasazení, jednoduše požádá NuGet vždy, když už jste zapotřebí obnovit závislosti. Sestavte systémy jako Visual Studio Team Services popisují "NuGet restore" pro tento účel přesný. Podobně když vývojáři získejte kopii souboru projektu (stejně jako při klonování úložiště) pak otevřete projekt v sadě Visual Studio a spustit sestavení, Visual Studio automaticky obnoví potřebné balíčky NuGet. Vývojáři, můžete zjistit také NuGet pro obnovování balíčků v současně pomocí `nuget restore` rozhraní příkazového řádku příkaz nebo `Install-Package` rutiny v konzole Správce balíčků.

Je zřejmé pak NuGet primární roli, kde jsou příslušné vývojáři udržuje tento odkaz seznam jménem projektu a poskytuje možnosti pro efektivní obnovení (a aktualizovat) tyto odkazované balíčky.

Jak přesně tomu má vyvinuly přes různé verze NuGet, což vede k několik *balíček správy formáty*, jak se nazývají se:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0 +)* soubor ve formátu XML, který udržuje plochý seznam všechny závislosti v projektu, včetně závislostí jiné nainstalované balíčky. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0 +)* A JSON soubor, který udržuje seznam závislosti projektu s celkové balíček grafu v přidružený soubor, `project.lock.json`. Tato struktura zajišťuje lepší výkon přes `packages.config` jak je popsáno na [řešení závislostí](Consume-Packages/Dependency-Resolution.md), včetně přenositelné obnovení, ale samotný obecně nahradila PackageReference níže.
- [Balíček odkazy v souborech projektu](Consume-Packages/Package-References-in-Project-Files.md) (také označované jako "PackageReference") | *(NuGet 4.0 +)* udržuje seznam nejvyšší úrovně závislosti projektu přímo v souboru projektu, aby bylo možné žádný samostatný soubor. Přidružený soubor, `project.assets.json`, se dynamicky vygeneruje jako `project.lock.json` ke správě celkové graf závislostí.

Formát balíčku správy zaměstnání v jakékoli dané projektu závisí na typu projektu a dostupná verze NuGet a sady Visual Studio. Pokud chcete zkontrolovat, jaký formát se používá, jednoduše vyhledejte `packages.config` nebo `project.json` v kořenu projektu po instalaci vašeho prvního balíčku. Pokud nevidíte buď soubor, vyhledejte v souboru projektu přímo pro &lt;PackageReference&gt;element.

V aplikaci Visual Studio 2017, například většina projektu typy použití `packages.config` s výjimkou projekty UWP C# a .NET Core, které používají PackageReference. 

## <a name="what-else-does-nuget-do"></a>Co dalšího NuGet dělá?

Chcete-li shrnout, co jsme jste zahrnutých dosavadní, NuGet poskytuje centrální nuget.org úložiště (v jeho hostování role) a podporuje privátní hostování. NuGet poskytuje že vývojářům nástroje pro vytváření, publikování a využívání balíčky potřebovat. A co je nejdůležitější NuGet udržuje odkaz na seznam balíčků v projektu a možnost umožňuje obnovit a aktualizovat tyto balíčky z tohoto seznamu.

Chcete-li tyto procesy efektivní práci, nemá NuGet některé servisní optimalizace. Zejména NuGet spravuje obou celý počítač a ukládá do mezipaměti specifické pro projekt balíček na místní instalace a přeinstalace. Pokud se týká mezipaměti platná pro celý počítač, všechny balíček, který si stáhnout a nainstalovat v projektu je uložený v mezipaměti, tak, aby instalace stejného balíčku v jiném projektu nemá stáhnout znovu. To je jasně velmi užitečné při se často obnovení větší počet balíčků, protože na serveru sestavení. Další podrobnosti pro tento mechanismus a jak s ním pracovat najdete v tématu [Správa mezipaměti NuGet](Consume-Packages/Managing-the-Nuget-Cache.md).

V rámci jednotlivých projektů nemá NuGet velké množství pracovních ke správě celkové závislost grafu. (Při použití `project.json` nebo &lt;PackageReference&gt;, NuGet zajišťuje, že informace v souboru sekundární název `project.lock.json` a `project.assets.json`, v uvedeném pořadí.) Zahrnuje to znovu, řešení více odkazů pro různé verze stejného balíčku.

To znamená je celkem běžné, že projektu trvá závislost na jeden nebo více balíčků, aby sami mají stejné závislosti. Například některé balíčky nejužitečnější nástroj na nuget.org zaměstnává mnoho dalších balíčků. V celé závislost grafu, 10, můžete snadno může mít deset jiné odkazy na různé verze stejného balíčku. Ale nechcete tím, že několik verzí tohoto balíčku do vlastní, aplikace, seřadí NuGet, na které jedné verzi, která každý uživatel může použít. (Viz [řešení závislostí](Consume-Packages/Dependency-Resolution.md) Další informace v tomto tématu.)

Kromě toho, NuGet udržuje všechny specifikace související na tom, jak jsou strukturovaná balíčky (včetně [lokalizace](Create-Packages/Creating-Localized-Packages.md) a [symboly ladění](Create-Packages/Symbol-Packages.md)) a jak se odkazuje (včetně [ verze rozsahy](reference/package-versioning.md#version-ranges-and-wildcards) a [předprodejní verze](create-packages/Prerelease-Packages.md).) NuGet také poskytuje rozhraní API pro poskytovatele přihlašovacích údajů (pro přístup k hostitelům privátní) a pro vývojáře, kteří vytvářejí rozšíření Visual Studia a šablony projektu.

Za chvíli procházet obsah pro tuto dokumentaci, a uvidíte všechny tyto funkce reprezentované existuje, společně s poznámky k verzi z roku NuGet beginnings.

## <a name="comments-contributions-and-issues"></a>Komentáře, příspěvky a problémy

Nakonec velmi mnohem Vítáme komentáře a příspěvky k této dokumentace&mdash;právě vyberte **komentáře** a **upravit** příkazy na všech stránky, nebo navštívit [úložiště dokumentace ](https://github.com/NuGet/docs.microsoft.com-nuget/) a [dokumentace problém seznamu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) na Githubu.

Vítáme příspěvky k NuGet samotné prostřednictvím jeho [různých úložišť GitHub](https://github.com/NuGet/Home); Problémy s NuGet najdete na [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Užijte si ji prostředí NuGet!
