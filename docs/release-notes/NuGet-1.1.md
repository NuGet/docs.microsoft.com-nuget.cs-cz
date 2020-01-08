---
title: Poznámky k verzi NuGet 1,0 a 1,1
description: Poznámky k verzi pro NuGet 1,1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4f90888eae4d039c99d6f6879a06107ec5a31a82
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384694"
---
# <a name="nuget-10-and-11-release-notes"></a>Poznámky k verzi NuGet 1,0 a 1,1

[Zpráva k vydání verze NuGet 1,2](../release-notes/nuget-1.2.md)

NuGet 1,0 byl vydán 13. ledna 2011.  NuGet 1,1 byl vydaný 12. února 2011.

## <a name="overview"></a>Přehled

Tento dokument obsahuje poznámky k verzi pro různé verze NuGet 1,0 seskupené podle hlavní verze Preview.

NuGet zahrnuje tyto komponenty:

* *NuGet. Tools. vsix* *, který se skládá z:
  * Dialogové okno **Přidat balíček knihovny** * v sadě Visual Studio se používá k procházení a instalaci balíčků.
  * **Konzola správce balíčků** * konzola založená na PowerShellu v sadě Visual Studio.
* *Nástroj příkazového řádku NuGet* * nástroj, který se používá k vytváření (a nakonec publikování) balíčků.

Rozšíření nástroje NuGet pro Visual Studio (*NuGet. Tools. vsix*) vyžaduje:

* Visual Studio 2010 nebo Visual Web Developer 2010 Express.

Nástroj příkazového řádku NuGet vyžaduje:

* .NET Framework verze 4

## <a name="installation"></a>Instalace služby

Chcete-li použít tuto [nejnovější verzi](http://nuget.codeplex.com/releases/view/52018):

* Nejdřív odinstalujte starší Build. K tomu je potřeba spustit VS jako správce.
* Odeberte všechny existující kanály, které máte.
* Přidejte nový informační kanál, který odkazuje na <https://go.microsoft.com/fwlink/?LinkId=206669>.

## <a name="nuget-11"></a>NuGet 1.1

Seznam problémů opravených v této verzi najdete [tady](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0) .

## <a name="nuget-10-rtm"></a>NuGet 1,0 RTM

Jeden problém byl vyřešen pro RTM od verze RC.

* [Problém 474: odebírání balíčků má vliv na všechny projekty v řešení](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Verze Release Candidate

Níže jsou uvedené změny v této verzi kandidáta od verze CTP 2. Pokud chcete zobrazit úplný seznam chyb, přejděte na sledování problémů.

* [Aktualizace balíčku z konzoly neaktualizuje závislosti.](http://nuget.codeplex.com/workitem/443)
* [Přidání balíčku vyskladnění neodkazování na balíček (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aktualizace balíčku opustí poškozené odkazy](http://nuget.codeplex.com/workitem/440)
* [Příkaz Get-Package-Updates se v dialogovém okně nepovede nebo když je v konzole vybraný Agregovaný zdroj ALL.](http://nuget.codeplex.com/workitem/439)
* [Načítají se chyby ověření balíčku.](http://nuget.codeplex.com/workitem/426)
* [Upozornit uživatele, když se balíček nedá nainstalovat z dialogu přidat balíček](http://nuget.codeplex.com/workitem/425)
* [Get-Package-Updates vyvolá se při aktualizaci velkého počtu balíčků.](http://nuget.codeplex.com/workitem/424)
* [Zlepšení zpracování chyb při nesprávném vytváření souborů nuspec](http://nuget.codeplex.com/workitem/423)
* [Sada NuGet Pack ignoruje zadané soubory.](http://nuget.codeplex.com/workitem/422)
* [Odebrání druhého zdroje balíčků a následným kliknutím na tlačítko "přesunout dolů" VS](http://nuget.codeplex.com/workitem/418)
* [Odebrat odkaz na sestavení při instalaci balíčků](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException při otevírání dialogového okna nastavení](http://nuget.codeplex.com/workitem/411)
* [Přístupový klíč pro zdroj balíčku v konzole správce balíčků nefunguje](http://nuget.codeplex.com/workitem/410)
* [Přístup k dialogovému oknu Nastavení NuGetu VS](http://nuget.codeplex.com/workitem/409)
* [ID balíčku IntelliSense by neměl dotazovat na příliš mnoho položek](http://nuget.codeplex.com/workitem/404)
* [Chyba při přidávání balíčku do projektu se znakem tečky v názvu projektu](http://nuget.codeplex.com/workitem/403)
* [Problém se zadanými soubory v nuspec](http://nuget.codeplex.com/workitem/400)
* [Při použití novějšího buildu by měl být zaregistrován správný oficiální kanál.](http://nuget.codeplex.com/workitem/399)
* [Značky by měly používat mezery místo #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata neobsahuje některé užitečné informace.](http://nuget.codeplex.com/workitem/388)
* [Přidat odkaz na zneužití sestav do dialogového okna](http://nuget.codeplex.com/workitem/386)
* [Použití App_Data k deextrahování konců balíčků v aplikaci Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementace značek](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder umožňuje prázdný balíček bez závislostí, které se mají vytvořit.](http://nuget.codeplex.com/workitem/373)
* [Přidat pole vlastníků pro balíček](http://nuget.codeplex.com/workitem/365)
* [Aktualizace manifestu VSIX pro vyslovení správce balíčků NuGet místo nástrojů VSIX](http://nuget.codeplex.com/workitem/364)
* [Příkaz Get-Package vyvolá chybu, když je vybraný všechen zdroj.](http://nuget.codeplex.com/workitem/359)
* [Povolení řazení zdrojů balíčků v dialogovém okně Možnosti](http://nuget.codeplex.com/workitem/356)
* [Update – balíček neodebere starší verzi.](http://nuget.codeplex.com/workitem/352)
* [Implementovat specifikaci rozsahu verzí pro závislosti](http://nuget.codeplex.com/workitem/347)
* [Po kliknutí na Přidat nový balíček dojde k chybě sady Visual Studio.](http://nuget.codeplex.com/workitem/346)
* [Zobrazení souborů ke stažení a hodnocení v dialogovém okně Přidat balíček](http://nuget.codeplex.com/workitem/345)
* [Změna mezi zdroji balíčku v dialogu neaktualizuje aktivní zdroj.](http://nuget.codeplex.com/workitem/344)
* [Odebrat vazbu klíče pro okno konzoly Správce balíčků](http://nuget.codeplex.com/workitem/339)
* [Install-Package není rozpoznán jako název rutiny...](http://nuget.codeplex.com/workitem/338)
* [Instalace balíčku z místního kanálu se nevyřešily závislosti na běžných kanálech.](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies by měly přeskočit závislosti, které se pořád používají.](http://nuget.codeplex.com/workitem/331)
* [Při rušení navigace na stránce nemůže uživatel přejít na jinou stránku, zatímco se vrátí původní požadavek na stránku.](http://nuget.codeplex.com/workitem/325)
* [Prozkoumejte výkon serveru NuPack. Server pro poskytování informačních kanálů s velkým počtem balíčků.](http://nuget.codeplex.com/workitem/324)
* [Při druhém vyfiltrování balíčku používá nový zdroj balíčku namísto dříve vybraného zdroje.](http://nuget.codeplex.com/workitem/321)
* [Při výběru karty online v dialogovém okně by měl být vybrán výchozí zdroj balíčku.](http://nuget.codeplex.com/workitem/320)
* [Seznam-balíček by měl ve výchozím nastavení zobrazovat nainstalované balíčky.](http://nuget.codeplex.com/workitem/309)
* [HintPaths odkazu na sestavení](http://nuget.codeplex.com/workitem/294)
* [Výjimka při otevírání konzoly Správce balíčků](http://nuget.codeplex.com/workitem/268)
* [Konzola IntelliSense stáhne celý informační kanál](http://nuget.codeplex.com/workitem/259)
* [Zdroj balíčku default by měl být přejmenovaný na aktivní.](http://nuget.codeplex.com/workitem/258)
* [Uživatelské rozhraní zdrojů balíčku: stisknutím OK by se měl přidat nový zdroj, pokud jsou název nebo zdrojová pole neprázdná.](http://nuget.codeplex.com/workitem/257)
* [Dialog bude velmi pomalý, pokud je počet nainstalovaných balíčků velký](http://nuget.codeplex.com/workitem/243)
* [Podpora přesměrování vazby pro silná pojmenovaná sestavení](http://nuget.codeplex.com/workitem/238)
* [Přidat odkaz na balíček... Uživatelské rozhraní pro zahrnutí rozevíracího seznamu pro zdroj balíčku](http://nuget.codeplex.com/workitem/226)
* [NuPack musí podporovat konfigurační transformaci agnostically názvu konfiguračního souboru.](http://nuget.codeplex.com/workitem/224)
* [Umožňuje přepsat BasePath v NuPack. exe.](http://nuget.codeplex.com/workitem/222)
* [Chování záložního zdroje balíčku](http://nuget.codeplex.com/workitem/204)
* [Selhání v grafickém uživatelském rozhraní](http://nuget.codeplex.com/workitem/201)
* [Přidání možností řazení do dialogového okna Přidat balíček](http://nuget.codeplex.com/workitem/179)
* [Klávesová zkratka pro vymazání konzoly Správce balíčků](http://nuget.codeplex.com/workitem/174)
* [Konzoly powerconsole způsobí selhání konzole NuPack](http://nuget.codeplex.com/workitem/166)
* [Dialog konzole a přidat balíček by měl nastavit agenta uživatele v žádosti.](http://nuget.codeplex.com/workitem/141)
* [Nastavte číslo verze VSIX a NuPack. exe v sestavení.](http://nuget.codeplex.com/workitem/134)
* [Skrýt běžné parametry PowerShellu z-?](http://nuget.codeplex.com/workitem/118)
* [Přidat podrobné nápovědu pro příkazy konzoly](http://nuget.codeplex.com/workitem/110)
* [Dialog Přidat balíček by měl umožňovat výběr aktuálního zdroje balíčku.](http://nuget.codeplex.com/workitem/88)
* [Přesunout třídy NuPack. Core do různých oborů názvů](http://nuget.codeplex.com/workitem/50)
* [Přidat pomocníka k rutinám](http://nuget.codeplex.com/workitem/23)
* [Po stažení balíčku ověřit hash z kanálu](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Níže jsou uvedené nejvýznamnější změny provedené ve CTP 2:

* Přepnuli jste kanál balíčku z ATOM na koncový bod služby OData: Pokud upgradujete na verzi CTP2 NuGet, nezapomeňte přidat následující adresu URL jako zdroj balíčku: `https://feed.nuget.org/ctp2/odata/v1/`.
* Byl přejmenován příkaz Add-Package pro *instalaci balíčku*.
* Aktualizace formátu `.nuspec`. Formát `.nuspec` nyní zahrnuje pole *iconUrl* pro zadání ikony png 32x32, která se zobrazí v dialogovém okně Přidat balíček. Nezapomeňte proto nastavit, aby rozlišil váš balíček. `.nuspec` formát obsahuje také nové pole *projectUrl* , které můžete použít k ukázání na webovou stránku, která poskytuje další informace o balíčku.

Toto sestavení nebude fungovat se starými `.nupkg` soubory. Pokud získáte výjimky s odkazem s hodnotou null, použijete starý soubor `.nupkg` a budete ho muset znovu sestavit pomocí aktualizovaného [nástroje příkazového řádku NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Následuje seznam funkcí a chyb, které byly opraveny pro NuGet CTP 2 (nezahrnuje chyby pro drobné čištění kódu atd.).

* [Při dekomprimaci sestavení balíčku při specifiyingi TargetFramework pro sestavení došlo k chybě.](http://nuget.codeplex.com/workitem/10)
* [Nastavit okno konzoly NuPack o více zjistitelnosti](http://nuget.codeplex.com/workitem/14)
* [ILMerge vydání nupack. exe](http://nuget.codeplex.com/workitem/19)
* [Lepší zpracování chyb a výjimek](http://nuget.codeplex.com/workitem/24)
* [[Nupack. Core]: PackageManager by měl řádně zpracovat chyby související s informačním kanálem.](http://nuget.codeplex.com/workitem/28)
* [Pro konzolu nástroje je potřeba nová ikona.](http://nuget.codeplex.com/workitem/29)
* [Lokalizovat řetězce v dialogovém okně](http://nuget.codeplex.com/workitem/38)
* [NuPack cache stáhly soubory. NuPack v paměti](http://nuget.codeplex.com/workitem/40)
* [Konzola NuPack: Změna výchozího zástupce pro zobrazení konzoly](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem by měl podporovat výchozí hodnoty pro společné vlastnosti.](http://nuget.codeplex.com/workitem/49)
* [Spuštění nupack. exe ve složce s pouze jedním souborem nuspec by mělo používat tento nuspec](http://nuget.codeplex.com/workitem/52)
* [Nabídka projektu se zobrazí i v případě, že není načten žádný projekt nebo řešení.](http://nuget.codeplex.com/workitem/54)
* [operace Build. cmd se nezdařila při čistém klonu základu kódu.](http://nuget.codeplex.com/workitem/56)
* [Funkce dostupné pro aktualizace](http://nuget.codeplex.com/workitem/57)
* [Dialog: Přidání balíčku pomocí dialogového okna odebere výzvu v konzole.](http://nuget.codeplex.com/workitem/73)
* [Přidání balíčku kliknutím na instalovat je často pomalé, bez vizuální zpětné vazby.](http://nuget.codeplex.com/workitem/80)
* [Neexistuje žádný způsob, jak zjistit, který z mých nainstalovaných balíčků obsahuje aktualizace.](http://nuget.codeplex.com/workitem/82)
* [Neexistuje žádný způsob, jak aktualizovat nainstalovaný balíček v dialogovém okně.](http://nuget.codeplex.com/workitem/83)
* [Neexistuje žádný způsob, jak odinstalovat nainstalovaný balíček v dialogovém okně.](http://nuget.codeplex.com/workitem/84)
* [v kontextové nabídce nainstalovaných odkazů se zobrazí &ldquo;přidat odkaz na balíček&hellip;&rdquo;](http://nuget.codeplex.com/workitem/85)
* [Po aktualizaci balíčku z konzoly se zobrazí stará verze i nová verze, jak je nainstalovaná.](http://nuget.codeplex.com/workitem/86)
* [Aktivita v konzole při použití dialogového okna po použití zmizí](http://nuget.codeplex.com/workitem/87)
* [Vyčištění příkazového řádku pro vyčištění v nupack. exe](http://nuget.codeplex.com/workitem/89)
* [Přidat do zdrojů balíčku popisný název](http://nuget.codeplex.com/workitem/98)
* [Update. nuspec pro podporu zahrnutí ikon balíčku](http://nuget.codeplex.com/workitem/103)
* [Uživatelské rozhraní informačního kanálu nepovoluje kopírování adresy URL.](http://nuget.codeplex.com/workitem/105)
* [Lepší zpracování chyb při odebrání balíčku.](http://nuget.codeplex.com/workitem/107)
* [Psaní v okně konzoly závisí na fokusu kurzoru.](http://nuget.codeplex.com/workitem/112)
* [Chybové zprávy vypadají awful](http://nuget.codeplex.com/workitem/116)
* [Výkon odebrání balíčku pro balíček, který není nainstalován, je chybný.](http://nuget.codeplex.com/workitem/117)
* [Odebrání balíčku se nepovede, když neexistují žádné zdroje balíčků.](http://nuget.codeplex.com/workitem/119)
* [Remove-Package se nezdařil, pokud je zdroj balíčku nedostupný.](http://nuget.codeplex.com/workitem/120)
* [Přidejte název k metadatům balíčku a informačnímu kanálu.](http://nuget.codeplex.com/workitem/125)
* [Přidejte parametr-source zpátky do Add-Package.](http://nuget.codeplex.com/workitem/127)
* [List-Package by měl mít parametr-source.](http://nuget.codeplex.com/workitem/128)
* [Aktualizujte NuPack. Server, aby se vyžadovalo stažení balíčku NuPack uživatelský agent.](http://nuget.codeplex.com/workitem/142)
* [Dialog pro přijetí licence musí vypsat licence pro všechny závislosti, které vyžadují přijetí.](http://nuget.codeplex.com/workitem/145)
* [Při vyvolání balíčku v informačním kanálu zaprotokolovat chybu](http://nuget.codeplex.com/workitem/150)
* [NuPack. exe by neměl umožňovat prázdné &lt;licenseurl elementu&gt;](http://nuget.codeplex.com/workitem/152)
* [Přejmenovat list-Package na Get-Package, Add-Package pro Install-Package a Remove-Package k odinstalaci balíčku](http://nuget.codeplex.com/workitem/155)
* [Použití položky nabídky Přidat odkaz na balíček z Navigátoru řešení zhroucení sady Visual Studio](http://nuget.codeplex.com/workitem/158)
* [U jmenovky dostupné zdroje balíčků chybí dvojtečka.](http://nuget.codeplex.com/workitem/160)
* [Make. nuspec – velká písmena elementu XML konzistentně ve stylu CamelCase použita](http://nuget.codeplex.com/workitem/161)
* [Manifest VSIX NuPack musí zapnout bit admin.](http://nuget.codeplex.com/workitem/162)
* [Pokud spustíte list-Package bez kanálů, dostanete chybu s odkazem s hodnotou null.](http://nuget.codeplex.com/workitem/164)
* [NuGet. exe: zadání cílové cesty](http://nuget.codeplex.com/workitem/171)
* [Chyby PowerShellu při otevírání konzoly Správa balíčků v WinXP](http://nuget.codeplex.com/workitem/175)
* [Selhání VS při pokusu o načtení seznamu balíčků](http://nuget.codeplex.com/workitem/176)
* [povoluje meta balíčky (žádné soubory, pouze závislosti).](http://nuget.codeplex.com/workitem/180)
* [Převod skriptu PowerShellu na modul PowerShellu 2,0](http://nuget.codeplex.com/workitem/181)
* [PathResolver by měl zahodit část cesty předcházející zástupným znakům, když je zadaný cíl.](http://nuget.codeplex.com/workitem/183)
* [Žádné závislosti](http://nuget.codeplex.com/workitem/186)
* [Chyba při instalaci knihovny elmah](http://nuget.codeplex.com/workitem/192)
* [Transformace konfigurace nefungují správně s &lt;configSections&gt;](http://nuget.codeplex.com/workitem/194)
* [Proměnnou $global:p rojectCache nelze načíst, protože nebyla nastavena.](http://nuget.codeplex.com/workitem/203)
* [Přidat úlohu MSBuild pro vytváření balíčků NuPack](http://nuget.codeplex.com/workitem/205)
* [seznam-balíček musí podporovat vyhledávání a filtrování.](http://nuget.codeplex.com/workitem/206)
* [Pokud autor balíčku poskytuje adresu URL licence, vždy se zobrazí odkaz na licenci.](http://nuget.codeplex.com/workitem/208)
* [Příležitostného přístupu "Odepřít" s výjimkou Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Selhání testů jednotek: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Umožňuje použít záložní/výchozí sadu souborů, pokud nejde najít verzi rozhraní určitou skupinu Framework.](http://nuget.codeplex.com/workitem/223)
* [Přidat odkaz na balíček... Uživatelské rozhraní nemůže odebrat balíček.](http://nuget.codeplex.com/workitem/225)
* [Přidat selhání odkazu na balíček Studio, když se jeden nebo víc projektů uvolní](http://nuget.codeplex.com/workitem/228)
* [V souboru Web. Debug. config se zdá, že transformace konfigurace nefunguje](http://nuget.codeplex.com/workitem/229)
* [init. ps1 se nevyvolává na vlastním balíčku.](http://nuget.codeplex.com/workitem/237)
* [Při přidávání cest k feedlist je výchozí tlačítko nastavené na OK, takže když stisknete klávesu ENTER automaticky se zavře](http://nuget.codeplex.com/workitem/240)
* [Pokus o odinstalaci závislosti se nezdařil, VS. Pokud se v řádku pokusí 2 časy.](http://nuget.codeplex.com/workitem/241)
* [Zobrazit adresu URL projektu v dialogu přidat balíček](http://nuget.codeplex.com/workitem/253)
* [Výchozí dialogové okno Přidat balíček pro nainstalované balíčky](http://nuget.codeplex.com/workitem/254)
* [Změna položky nabídky dialogového okna Přidat balíček](http://nuget.codeplex.com/workitem/261)
* [Přejmenování oborů názvů a sestavení](http://nuget.codeplex.com/workitem/274)
* [Přejmenování projektu NuPack na NuGet](http://nuget.codeplex.com/workitem/282)
* [Do seznamu závislostí přidejte následující text.](http://nuget.codeplex.com/workitem/288)
* [Změna textu přijetí licence v dialogu pro přijetí licence](http://nuget.codeplex.com/workitem/291)
* [Změňte text v dialogu pro přijetí licence nad seznamem balíčků.](http://nuget.codeplex.com/workitem/292)
* [OData nefunguje s adresou URL fwlink.](http://nuget.codeplex.com/workitem/304)
* [Uživatelské rozhraní Správce balíčků: u více než agresivního ukládání do mezipaměti se počet balíčků pro stránkování použil.](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet-&gt; chyba konzoly Správce balíčků](http://nuget.codeplex.com/workitem/335)
* [Dialog Přidat balíček zobrazuje přijetí licence pro již nainstalované balíčky.](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Následuje seznam funkcí a chyb, které byly opraveny pro NuGet CTP 1.

* [Rozšíření balíčku by mělo být přejmenováno na. nupack](http://nuget.codeplex.com/workitem/1)
* [Přesunout soubor balíčku do složky](http://nuget.codeplex.com/workitem/2)
* [Sloučit instalaci &amp; přidat příkazy PS](http://nuget.codeplex.com/workitem/3)
* [Vytváření aliasů pro rutiny příkazového/podstatného jména](http://nuget.codeplex.com/workitem/4)
* [NuPack se při přepnutí řešení v VS.](http://nuget.codeplex.com/workitem/6)
* [Ve výchozím nastavení by se měla skrýt složka řešení Packages.](http://nuget.codeplex.com/workitem/11)
* [Přidání podpory pro nahrazení tokenu v položkách obsahu](http://nuget.codeplex.com/workitem/12)
* [NuPack. UI by mělo používat rozhraní PackageSource API.](http://nuget.codeplex.com/workitem/26)
* [[Nupack. Core]: PackageManager označí balíčky jako nainstalované před jejich instalací.](http://nuget.codeplex.com/workitem/27)
* [Při odstranění výchozího projektu z řešení se stále zobrazuje odstraněný projekt jako výchozí.](http://nuget.codeplex.com/workitem/30)
* [Příkaz New-Package se nezdařil s názvem "nelze přidat součást pro určený identifikátor URI, protože již je v balíčku."](http://nuget.codeplex.com/workitem/32)
* [Odebrání řetězců "NuPack" z grafického uživatelského rozhraní sady Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Přidat hlavičku Apache do souboru COPYRIGHT. txt](http://nuget.codeplex.com/workitem/36)
* [Příkaz Remove Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Správce balíčků se nedá použít, když načítání profilu vyvolá výjimku.](http://nuget.codeplex.com/workitem/39)
* [init. ps1, Install. ps1 a Uninstall. ps1 musí přijmout další stav.](http://nuget.codeplex.com/workitem/41)
* [Kombinování balíčků konzoly a grafického uživatelského rozhraní do jednoho balíčku](http://nuget.codeplex.com/workitem/42)
* [Logika transformace XML nefunguje, pokud se použije na XML, které není v kořenovém adresáři.](http://nuget.codeplex.com/workitem/43)
* [Dialog spravovat nastavení zdrojů balíčků aktualizace konzoly NuPack](http://nuget.codeplex.com/workitem/44)
* [Uživatelské rozhraní konzoly NuPack: Přejmenujte rozevírací seznam Package feed na zdroj balíčku.](http://nuget.codeplex.com/workitem/45)
* [Možnosti konzoly NuPack: přejmenovat uživatelské rozhraní úložiště tak, aby bylo konzistentní s konzolou NuPack](http://nuget.codeplex.com/workitem/46)
* [Příkaz Add-Package se nezdařil proti webovému serveru, který byl otevřen ze služby IIS nebo adresy URL.](http://nuget.codeplex.com/workitem/53)
* [Zdroj Správce balíčků nefunguje s FwLink](http://nuget.codeplex.com/workitem/55)
* [Nastavit výchozí zdroj balíčku](http://nuget.codeplex.com/workitem/59)
* [Při přidávání zdrojů balíčků do možnosti, pokud je zadaný jenom jeden zdroj, Předpokládejme, že je výchozí hodnota.](http://nuget.codeplex.com/workitem/60)
* [Uživatelské rozhraní dialogového okna zobrazuje falešné balíčky "poslední".](http://nuget.codeplex.com/workitem/62)
* [Možnosti: kliknutím na tlačítko Storno nedojde ke zrušení změn](http://nuget.codeplex.com/workitem/63)
* [Při hledání dialogového okna Přidat odkaz na balíček by se mělo rozlišovat velká a malá písmena](http://nuget.codeplex.com/workitem/65)
* [Oprava metadat společnosti v souborech AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Číslo verze VSIX](http://nuget.codeplex.com/workitem/71)
* [Odebrat-balíček: using-? zobrazuje dvojitou podruhé.](http://nuget.codeplex.com/workitem/72)
* [Spustit instalační/odinstalační balíčky pro balíčky na úrovni projektu](http://nuget.codeplex.com/workitem/74)
* [Server nemůže vytvořit informační kanál, když se jeden nupack nepodaří ověřit.](http://nuget.codeplex.com/workitem/90)
* [Je potřeba nahradit ikony NuPack](http://nuget.codeplex.com/workitem/94)
* [Proxy server http protokolu NTLM se neověřuje na informační kanál balíčku.](http://nuget.codeplex.com/workitem/96)
* [Dialog se v okně VS vždy nespustí uprostřed](http://nuget.codeplex.com/workitem/100)
* [Mnohé z polí v podrobnostech balíčků se v dialogovém okně neplní.](http://nuget.codeplex.com/workitem/102)
* [Uživatelské rozhraní dialogu nezobrazuje jména autorů.](http://nuget.codeplex.com/workitem/108)
* [Proč – verze pro příkaz Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Odebrat kartu nedávné v uživatelském rozhraní dialogu](http://nuget.codeplex.com/workitem/115)
* [Chyba VS při kliknutí pravým tlačítkem na složku řešení po otevření dialogového okna uživatelského rozhraní dialogového okna alespoň jednoho.](http://nuget.codeplex.com/workitem/126)
* [Změnit parametr-Local v seznamu-Package na-Installed](http://nuget.codeplex.com/workitem/129)
* [Přejmenujte Packages. XML na NuPack. config.](http://nuget.codeplex.com/workitem/132)
* [Konzola vynutí kurzor na konec řádku.](http://nuget.codeplex.com/workitem/135)
* [Odstranění balíčku IntelliSense je přerušené.](http://nuget.codeplex.com/workitem/136)
* [Přidání příznaku RequireLicenseAcceptance do. nuspec a informačního kanálu](http://nuget.codeplex.com/workitem/137)
* [Přidat LicenseUrl do formátu. nuspec a informační kanál balíčku](http://nuget.codeplex.com/workitem/138)
* [Kliknutím na instalovat pro balíček, který vyžaduje přijetí, by se mělo zobrazit dialogové okno přijetí.](http://nuget.codeplex.com/workitem/139)
* [Přidat do dialogového okna Přidat balíček text právního omezení](http://nuget.codeplex.com/workitem/140)
* [Při prvním spuštění konzoly balíčku přidat právní omezení](http://nuget.codeplex.com/workitem/143)
* [Zobrazit právní omezení po instalaci balíčku v konzole nástroje](http://nuget.codeplex.com/workitem/144)
* [Přejmenujte příponu. nupack na. nupkg](http://nuget.codeplex.com/workitem/146)