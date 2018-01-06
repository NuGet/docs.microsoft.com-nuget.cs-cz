---
title: "Poznámky k verzi NuGet 1.0 a 1.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0e7688f7-09d2-4477-9fdf-0e27f572a4de
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.1 NuGet."
keywords: "NuGet 1.1 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 593848b3e5e063816fbbec8b4d11e6fc789d05cd
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-10-and-11-release-notes"></a>Poznámky k verzi NuGet 1.0 a 1.1

[NuGet 1.2 poznámky](../release-notes/nuget-1.2.md)

NuGet 1.0 byla vydána 13. ledna 2011.  NuGet 1.1 byla vydána 12. února 2011.

## <a name="overview"></a>Přehled

Tento dokument obsahuje poznámky k verzi pro různé verze 1.0 NuGet seskupené podle verze hlavní preview.

NuGet obsahuje následující součásti:

* *NuGet.Tools.vsix* * která zahrnuje:
  * **Balíček knihovny dialogové okno Přidání** * dialogové okno v sadě Visual Studio, které se používá k procházení a instalaci balíčků.
  * **Konzola správce balíčků** * založené na prostředí Powershell konzoly v sadě Visual Studio.
* *Nástroj pro příkazový řádek NuGet* * nástroj použít k vytvoření (a nakonec publikování) balíčky.

Rozšíření Visual Studio NuGet nástroje (*NuGet.Tools.vsix*) vyžaduje:

* Visual Studio 2010 a Visual Web Developer 2010 Express.

Nástroje příkazového řádku NuGet vyžaduje:

* Verze rozhraní .NET framework 4

## <a name="installation"></a>Instalace

Chcete-li použít [nejnovější verze](http://nuget.codeplex.com/releases/view/52018):

* Nejprve odinstalujte starší buildu. Budete muset spustit jako správce k tomu VS.
* Odeberte všechny existující kanály, které máte.
* Přidat nový kanál odkazující na [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Seznam chyby v této verzi [naleznete zde](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>RTM NuGet 1.0

Jeden problém byl opraven pro verzi RTM od RC.

* [Problém 474: Odebrání balíčků ovlivňuje všechny projekt v řešení](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Verze Release Candidate

Níže jsou změny provedené v této verzi Release Candidate od verze CTP 2. Přejděte ke sledovacímu modulu problém chcete zobrazit úplný seznam chyb.

* [Aktualizace balíčku z konzoly neaktualizuje závislosti.](http://nuget.codeplex.com/workitem/443)
* [Přidání balíčku příjmem bin balíček není odkaz (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aktualizace balíčku opustí poškozenými odkazy](http://nuget.codeplex.com/workitem/440)
* [Get-Package-aktualizace nezdaří, v dialogovém okně, nebo když 'všechny agregovaného zdroje. je vybraný v konzole](http://nuget.codeplex.com/workitem/439)
* [Dochází k chybám ověření balíčku](http://nuget.codeplex.com/workitem/426)
* [Upozornit uživatele, když balíček nelze nainstalovat z tohoto dialogového okna Přidat balíček](http://nuget.codeplex.com/workitem/425)
* [Get-Package-aktualizace generuje při aktualizaci více balíčků](http://nuget.codeplex.com/workitem/424)
* [Zlepšení zpracování chyb, pokud jsou správně vytvořeny souborů nuspec.](http://nuget.codeplex.com/workitem/423)
* [Nuget pack ignoruje zadané soubory](http://nuget.codeplex.com/workitem/422)
* [Odebrání zdroj balíčku sekundu poslední a pak kliknutím na "Dolů" dojde k chybě VS](http://nuget.codeplex.com/workitem/418)
* [Odebrat odkaz na sestavení při instalaci balíčků](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException při otevření dialogu nastavení](http://nuget.codeplex.com/workitem/411)
* [Přístupový klíč pro zdroj balíčku v konzole Správce balíčků nefunguje](http://nuget.codeplex.com/workitem/410)
* [NuGet VS nastavení dialogové okno přístupové klíče fokus se nesprávný pole](http://nuget.codeplex.com/workitem/409)
* [Intellisense ID balíčku by neměla dotaz příliš mnoho položek](http://nuget.codeplex.com/workitem/404)
* [Chyba přidání balíčku do projektu s tečku v názvu projektu](http://nuget.codeplex.com/workitem/403)
* [Problém s zadané soubory v nuspec](http://nuget.codeplex.com/workitem/400)
* [Správné oficiální kanálu by měl získat zaregistrován při použití novější sestavení](http://nuget.codeplex.com/workitem/399)
* [Značky musí prostory místo #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata chybí některé užitečné informace](http://nuget.codeplex.com/workitem/388)
* [Přidat odkaz na dialogové okno](http://nuget.codeplex.com/workitem/386)
* [Pomocí App_Data dekomprimovat zalomení balíčky v sadě Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Implementace značky](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder umožňuje prázdný balíček nemá žádné závislosti, který se má vytvořit](http://nuget.codeplex.com/workitem/373)
* [Přidat pole vlastníků pro balíček](http://nuget.codeplex.com/workitem/365)
* [Aktualizovat manifest VSIX. Tím vyjádříte Správce balíčků NuGet místo nástroje VSIX](http://nuget.codeplex.com/workitem/364)
* [Příkaz Get-Package vyvolá chybu, pokud je vybrána všechny zdroje](http://nuget.codeplex.com/workitem/359)
* [Povolit řazení zdroji balíčků v dialogovém okně Možnosti](http://nuget.codeplex.com/workitem/356)
* [Balíček aktualizace neodebere starší verze](http://nuget.codeplex.com/workitem/352)
* [Specifikace rozsahu verze implementace pro závislosti](http://nuget.codeplex.com/workitem/347)
* [Visual Studio dojde k chybě při kliknutím na tlačítko "Přidat nový balíček"](http://nuget.codeplex.com/workitem/346)
* [Zobrazit soubory ke stažení a hodnocení v dialogovém okně Přidat balíček](http://nuget.codeplex.com/workitem/345)
* [Změna mezi zdroji balíčku v dialogovém okně neaktualizuje aktivní zdrojová](http://nuget.codeplex.com/workitem/344)
* [Odeberte vazbu na klíč pro okno konzoly Správce balíčků](http://nuget.codeplex.com/workitem/339)
* [Instalace balíčku není rozpoznán jako název rutiny...](http://nuget.codeplex.com/workitem/338)
* [Instalace balíčku z místní kanálu závislosti na regulární kanály nejsou přeložit.](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies přeskočte závislosti, které se používají](http://nuget.codeplex.com/workitem/331)
* [Pokud zrušení navigaci na stránce, uživatele, nejde přejít na jinou stránku při vrátí původní požadavek na stránku](http://nuget.codeplex.com/workitem/325)
* [Prozkoumejte výkonu NuPack.Server pro obsluhovat informačních kanálů s velkého počtu balíčků.](http://nuget.codeplex.com/workitem/324)
* [Druhý době filtrovat pro balíček používá zdroji balíčku "New" místo dříve vybraný zdroj.](http://nuget.codeplex.com/workitem/321)
* [Při výběru na kartě "Online" v dialogovém okně, měla by být vybrána výchozí zdroj balíčku.](http://nuget.codeplex.com/workitem/320)
* [Seznam balíčků by měl zobrazit balíčků nainstalovaných ve výchozím nastavení](http://nuget.codeplex.com/workitem/309)
* [HintPaths odkaz na sestavení](http://nuget.codeplex.com/workitem/294)
* [Výjimka při spuštění konzoly Správce balíčků](http://nuget.codeplex.com/workitem/268)
* [Intellisense konzoly stahuje celého kanálu](http://nuget.codeplex.com/workitem/259)
* [Zdroj balíčku "Výchozí" by měl být přejmenován na "Aktivní"](http://nuget.codeplex.com/workitem/258)
* [Balíček zdroje uživatelského rozhraní: stisknutím OK musí přidat nový zdroj, pokud jsou neprázdný název nebo zdroj pole](http://nuget.codeplex.com/workitem/257)
* [Dialogové okno změní super pomalé, pokud je velký počet nainstalované balíčky](http://nuget.codeplex.com/workitem/243)
* [Podpora přesměrování vazby sestavení se silným názvem](http://nuget.codeplex.com/workitem/238)
* [Přidáte odkaz na balíček... Uživatelského rozhraní pro zahrnutí rozevírací dolů zdroje balíčku](http://nuget.codeplex.com/workitem/226)
* [NuPack musí podporovat konfigurační transformaci agnostically z názvu souboru config](http://nuget.codeplex.com/workitem/224)
* [Umožňuje BasePath k být přepsána v NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Chování záložní zdroje balíčku](http://nuget.codeplex.com/workitem/204)
* [Havárií na grafickém uživatelském rozhraní](http://nuget.codeplex.com/workitem/201)
* [Přidat řazení možnosti Přidat balíček dialogového okna](http://nuget.codeplex.com/workitem/179)
* [Klávesová zkratka zrušte Konzola správce balíčků](http://nuget.codeplex.com/workitem/174)
* [Konzoly PowerConsole způsobí, že konzola NuPack selhání](http://nuget.codeplex.com/workitem/166)
* [Konzole a přidat Dialog balíček měli nastavit uživatelský agent v žádosti](http://nuget.codeplex.com/workitem/141)
* [Nastavit počet verze VSIX a NuPack.exe v buildu.](http://nuget.codeplex.com/workitem/134)
* [Skrýt společné parametry prostředí PowerShell od-?](http://nuget.codeplex.com/workitem/118)
* [Přidat – podrobnou nápovědu pro příkazy konzoly](http://nuget.codeplex.com/workitem/110)
* [Přidat dialogové okno balíček by měl povolit výběr aktuálním zdroji balíčků](http://nuget.codeplex.com/workitem/88)
* [Třídy NuPack.Core přesunout do jiné oborů názvů](http://nuget.codeplex.com/workitem/50)
* [Přidat nápovědy k rutinám](http://nuget.codeplex.com/workitem/23)
* [Po dokončení stahování balíčku ověřit hodnotu hash z kanálu](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Tady jsou nejdůležitější změny provedené v CTP 2:

* Přepnout balíček informační kanál z ATOM koncový bod služby OData: Pokud upgradujete na verzi CTP2 NuGet, je nutné přidat následující adresy URL jako zdroj balíčků: [http://go.microsoft.com/fwlink/?LinkID=204820](http://go.microsoft.com/fwlink/?LinkID=204820).
* Přejmenovat příkaz Add-Package k *Install-Package*.
* Aktualizovat `.nuspec` formátu. `.nuspec` Formátu nyní zahrnuje *iconUrl* pole pro zadání ikonou png 32 x 32, který se zobrazí v dialogovém okně Přidat balíček. Proto nezapomeňte nastavit, které k rozlišení vašeho balíčku. `.nuspec` Formátu obsahuje také nové *adrese projectUrl* pole, které můžete použít tak, aby odkazoval na webové stránce, která poskytuje další informace o vašeho balíčku.

Toto sestavení nebude fungovat se starý `.nupkg` soubory. Pokud získáte odkazu s hodnotou null výjimky, které používáte své staré `.nupkg` souborů a nutné znovu sestavit s aktualizovaný [nástroj pro příkazový řádek NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Následuje seznam funkcí a chyby, které jsme vyřešili pro NuGet CTP 2 (nezahrnuje chyby pro uvolnění menší kódu atd.).

* [Chyba dekomprimace balíček sestavení při zadání TargetFramework pro sestavení.](http://nuget.codeplex.com/workitem/10)
* [Vytvoření okna konzoly NuPack zjistitelná](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe verze](http://nuget.codeplex.com/workitem/19)
* [Lepší chyby nebo zpracování výjimek](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager by měl pohodlné zpracování chyby související s informačního kanálu](http://nuget.codeplex.com/workitem/28)
* [Třeba novou ikonu pro konzolu nástroje](http://nuget.codeplex.com/workitem/29)
* [V dialogovém okně řetězce pro lokalizaci](http://nuget.codeplex.com/workitem/38)
* [NuPack mezipamětí stažené soubory .nupack v paměti](http://nuget.codeplex.com/workitem/40)
* [Konzola NuPack: Změňte výchozí zástupce pro zobrazení konzoly](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem by měly podporovat výchozí hodnoty pro běžné vlastnosti](http://nuget.codeplex.com/workitem/49)
* [Spuštění nupack.exe ve složce obsahující pouze jeden soubor nuspec by měl používat tento soubor nuspec](http://nuget.codeplex.com/workitem/52)
* [Nabídky projektu se zobrazí i když je načten žádný projekt nebo řešení](http://nuget.codeplex.com/workitem/54)
* [Build.cmd selže čistou klonu základu kódu](http://nuget.codeplex.com/workitem/56)
* [Aktualizace k dispozici funkce](http://nuget.codeplex.com/workitem/57)
* [Dialogové okno: Přidání balíčku pomocí dialogu odebere řádku v konzole](http://nuget.codeplex.com/workitem/73)
* [Přidání balíčku kliknutím na tlačítko 'nainstalovat, je často pomalé, s žádné vizuální zpětnou vazbu](http://nuget.codeplex.com/workitem/80)
* [Neexistuje žádný způsob, jak zjistit, které ze Moje nainstalované balíčky mají aktualizace.](http://nuget.codeplex.com/workitem/82)
* [Neexistuje žádný způsob, jak aktualizovat nainstalovaným balíčkem v dialogovém okně.](http://nuget.codeplex.com/workitem/83)
* [Neexistuje žádný způsob, jak odinstalovat nainstalovaným balíčkem v dialogovém okně](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Přidat odkaz na balíček&hellip; &rdquo; se zobrazí v místní nabídce nainstalované odkazy](http://nuget.codeplex.com/workitem/85)
* [Po aktualizaci balíčku v konzole, se zobrazí na novou verzi i předchozí verzi aplikace jako nainstalované](http://nuget.codeplex.com/workitem/86)
* [Aktivity v konzole, při použití tohoto dialogového okna zmizí po použití](http://nuget.codeplex.com/workitem/87)
* [Analýza v nupack.exe čištění příkazového řádku](http://nuget.codeplex.com/workitem/89)
* [Přidat popisný název pro zdroje balíčků](http://nuget.codeplex.com/workitem/98)
* [Aktualizovat příponou .nuspec pro podporu včetně ikony balíčku](http://nuget.codeplex.com/workitem/103)
* [Informačního kanálu uživatelského rozhraní neumožňuje kopírování adresu URL](http://nuget.codeplex.com/workitem/105)
* [Zpracování chyb lepší odebrat balíček.](http://nuget.codeplex.com/workitem/107)
* [Zadáním v okně konzoly závisí na kurzoru](http://nuget.codeplex.com/workitem/112)
* [Podívejte se awful chybové zprávy](http://nuget.codeplex.com/workitem/116)
* [Výkon odebrat balíčku pro balíček, který není nainstalován je chybný.](http://nuget.codeplex.com/workitem/117)
* [Odebrání balíčku selže, pokud neexistují žádné zdroje balíčku](http://nuget.codeplex.com/workitem/119)
* [Odebrání balíčku selže, pokud zdroj balíčku nedostupný](http://nuget.codeplex.com/workitem/120)
* [Přidejte název metadata balíčků a informačního kanálu.](http://nuget.codeplex.com/workitem/125)
* [Přidat zdroje parametru - zpět přidat balíček](http://nuget.codeplex.com/workitem/127)
* [Seznam balíček musí mít parametr - zdroje](http://nuget.codeplex.com/workitem/128)
* [Aktualizace NuPack.Server tak, aby vyžadovala NuPack uživatele k Stáhnout balíček agenta](http://nuget.codeplex.com/workitem/142)
* [Dialogové okno přijetí licenční musí seznam licence pro všechny závislosti, které vyžadují přijetí](http://nuget.codeplex.com/workitem/145)
* [Přihlásit k chybě, pokud balíček vyvolá v informačním kanálu](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe neměli povolit prázdnou &lt;licenseurl&gt; – element](http://nuget.codeplex.com/workitem/152)
* [Přejmenování seznamu balíček do Get balíčku, přidejte – balíček a Install-Package a Remove-Package k odinstalaci balíčku](http://nuget.codeplex.com/workitem/155)
* [Pomocí položky nabídky přidat odkaz na balíček z navigátoru řešení sady Visual Studio dojde k chybě](http://nuget.codeplex.com/workitem/158)
* [Popisek "zdroje balíčků dostupné" chybí dvojtečka](http://nuget.codeplex.com/workitem/160)
* [Ujistěte se, příponou .nuspec xml element velká a malá písmena konzistentně formátu camelCase použita](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX manifest je potřeba zapnout bit "admin"](http://nuget.codeplex.com/workitem/162)
* [Pokud spustíte seznamu balíček s žádné kanály, se zobrazí chyba ref hodnotu null.](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: Zadejte cílovou cestu](http://nuget.codeplex.com/workitem/171)
* [Otevření konzoly pro správu balíček na WinXP chyby prostředí PowerShell](http://nuget.codeplex.com/workitem/175)
* [VS dojde k chybě při pokusu načíst seznam balíčků](http://nuget.codeplex.com/workitem/176)
* [Povolit meta balíčky (žádné soubory, jenom závislosti)](http://nuget.codeplex.com/workitem/180)
* [Převést skript prostředí Powershell do modulu prostředí Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver by měl zahodit cesta část předcházející zástupné znaky, když je zadaný cíl](http://nuget.codeplex.com/workitem/183)
* [Žádné závislosti](http://nuget.codeplex.com/workitem/186)
* [Chyba při instalaci Elmah](http://nuget.codeplex.com/workitem/192)
* [Konfigurace transformací nefungují správně s &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Proměnná ' $globální: projectCache' nelze načíst, protože není nastaveno.](http://nuget.codeplex.com/workitem/203)
* [Přidat úlohy nástroje MSBuild pro vytváření balíčků NuPack](http://nuget.codeplex.com/workitem/205)
* [Seznam balíčku musí podporovat hledání nebo filtrování](http://nuget.codeplex.com/workitem/206)
* [Pokud autora balíčku poskytuje adresu URL licence být vždy zobrazen odkaz na licencí](http://nuget.codeplex.com/workitem/208)
* [Příležitostně "Přístup byl odepřen" výjimka odebrat balíček](http://nuget.codeplex.com/workitem/213)
* [Testování částí nedaří: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Povolit pro záložní přihlašování nebo výchozí sadu souborů, pokud framework verze specifická nebyl nalezen.](http://nuget.codeplex.com/workitem/223)
* [Přidáte odkaz na balíček... Uživatelské rozhraní nelze odebrat balíček](http://nuget.codeplex.com/workitem/225)
* [Přidat odkaz na balíček dojde k chybě studio, pokud jeden nebo více projektu je odpojen](http://nuget.codeplex.com/workitem/228)
* [Konfigurační transformaci pracovat na soubor web.debug.config nezobrazí.](http://nuget.codeplex.com/workitem/229)
* [Init.ps1 se nespustí, na vlastní balíček](http://nuget.codeplex.com/workitem/237)
* [Při přidávání cesty do seznam kanálů, výchozí tlačítko je nastavené na OK, takže pokud stisknutí klávesy ENTER automaticky ukončí](http://nuget.codeplex.com/workitem/240)
* [Pokus o odinstalaci závislost dojde k chybě VS Pokud pokus o 2 časy v řádku](http://nuget.codeplex.com/workitem/241)
* [Zobrazovaná adresa URL projektu v dialogovém okně Přidat balíček](http://nuget.codeplex.com/workitem/253)
* [Výchozí zobrazení dialogového okna Přidat balíček nainstalované balíčky](http://nuget.codeplex.com/workitem/254)
* [Změňte položku nabídky Přidat Dialog balíčku.](http://nuget.codeplex.com/workitem/261)
* [Přejmenujte obory názvů a sestavení](http://nuget.codeplex.com/workitem/274)
* [Přejmenujte projektu NuPack NuGet](http://nuget.codeplex.com/workitem/282)
* [Přidejte následující text v seznamu závislostí](http://nuget.codeplex.com/workitem/288)
* [Změňte text přijetí licence v dialogovém okně přijetí licence](http://nuget.codeplex.com/workitem/291)
* [Změňte text v dialogovém okně licence přijetí výše seznam balíčků](http://nuget.codeplex.com/workitem/292)
* [Adresa URL fwlink nebude fungovat OData](http://nuget.codeplex.com/workitem/304)
* [Uživatelské rozhraní Správce balíčků: přes agresivní ukládání do mezipaměti balíček počet používaný pro stránkování](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; chybě Konzola správce balíčků](http://nuget.codeplex.com/workitem/335)
* [Přidat že dialog balíčku zobrazuje licence přijetí pro již nainstalované zabalené](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Následuje seznam funkcí a chyby, které jsme vyřešili pro NuGet CTP 1.

* [Balíček rozšíření by měl být přejmenován na .nupack](http://nuget.codeplex.com/workitem/1)
* [Přesuňte soubor balíčku do složky](http://nuget.codeplex.com/workitem/2)
* [Sloučení instalace &amp; příkazy přidat PS](http://nuget.codeplex.com/workitem/3)
* [Vytvořit aliasy pro rutiny sloveso-podstatné jméno](http://nuget.codeplex.com/workitem/4)
* [Získá NuPack nerozumíte při přechodu řešení v sadě VS](http://nuget.codeplex.com/workitem/6)
* [Ve výchozím nastavení jsme měli skrýt složky 'packages' řešení](http://nuget.codeplex.com/workitem/11)
* [Přidáte podporu pro token nahrazení obsahu položky.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI by měl použít rozhraní API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager označí balíčky jako nainstalována před jejich instalací](http://nuget.codeplex.com/workitem/27)
* [Odstraňování výchozí projekt z řešení stále zobrazuje odstraněný projekt jako výchozí](http://nuget.codeplex.com/workitem/30)
* [Nový balíček selže s "Nelze přidat část pro zadaný identifikátor URI protože je již v balíčku."](http://nuget.codeplex.com/workitem/32)
* [Odebrání řetězce "NuPack" Visual Studio grafického uživatelského rozhraní](http://nuget.codeplex.com/workitem/35)
* [Přidání souboru Apache hlavičky k COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Odeberte příkaz Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Vyvolá výjimku, nelze jej použít při načítání profilu Správce balíčků](http://nuget.codeplex.com/workitem/39)
* [Init.ps1 a install.ps1, uninstall.ps1 musí přijímat další stav](http://nuget.codeplex.com/workitem/41)
* [Zkombinovat do jednoho balíčku konzoly a balíčky grafického uživatelského rozhraní](http://nuget.codeplex.com/workitem/42)
* [Logika transformace XML nebude fungovat, pokud kód XML, který není v kořenovém adresáři](http://nuget.codeplex.com/workitem/43)
* [Spravovat dialogu nastavení zdroje balíčku není aktualizace konzoly NuPack](http://nuget.codeplex.com/workitem/44)
* [Uživatelské rozhraní konzoly NuPack: Přejmenujte 'Balíček kanálu' rozevíracího seznamu "zdroji balíčku.](http://nuget.codeplex.com/workitem/45)
* [NuPack konzoly možnosti: Přejmenovat 'úložiště uživatelského rozhraní, aby byla konzistentní s konzolou NuPack](http://nuget.codeplex.com/workitem/46)
* [Přidání balíčku selže na web, který byl otevřen ze služby IIS nebo z adresy URL](http://nuget.codeplex.com/workitem/53)
* [Zdroj Správce balíčků nefunguje s FwLink](http://nuget.codeplex.com/workitem/55)
* [Nastavit výchozí zdroj balíčku](http://nuget.codeplex.com/workitem/59)
* [Při přidávání zdroje balíčků ve volbě, když je zadat jenom jeden zdroj, předpokládá, že je výchozí hodnota.](http://nuget.codeplex.com/workitem/60)
* [Dialogové okno uživatelského rozhraní zobrazuje falešných "posledního" balíčky](http://nuget.codeplex.com/workitem/62)
* [Možnosti: Kliknutím na tlačítko Storno nezrušíte změny](http://nuget.codeplex.com/workitem/63)
* [Přidejte že balíček odkaz dialogové okno hledání by měl být malá a velká písmena](http://nuget.codeplex.com/workitem/65)
* [Opravte společnosti metadata v AssemblyInfo.cs soubory](http://nuget.codeplex.com/workitem/67)
* [Číslo verze pro VSIX](http://nuget.codeplex.com/workitem/71)
* [Odebrat balíček: Pomocí-? Zobrazí nápovědu dvakrát](http://nuget.codeplex.com/workitem/72)
* [Spuštění instalace nebo odinstalace balíčků pro projekt úrovně balíčky](http://nuget.codeplex.com/workitem/74)
* [Server nelze vytvořit kanál při ověřování se nezdaří, jeden nupack](http://nuget.codeplex.com/workitem/90)
* [Je třeba vyměnit NuPack ikony](http://nuget.codeplex.com/workitem/94)
* [Server proxy protokolu http NTLM neověřuje balíčku informačního kanálu.](http://nuget.codeplex.com/workitem/96)
* [Dialogové okno nelze spustit vždy zarovnaný na střed v okně VS](http://nuget.codeplex.com/workitem/100)
* [Počet polí v podrobnostech balíčky se nezobrazí v dialogovém okně](http://nuget.codeplex.com/workitem/102)
* [Dialogové okno uživatelského rozhraní nezobrazí jmen autorů](http://nuget.codeplex.com/workitem/108)
* [Proč – verze pro odebrání balíčku](http://nuget.codeplex.com/workitem/113)
* [Odebrat poslední kartu v dialogovém okně uživatelského rozhraní](http://nuget.codeplex.com/workitem/115)
* [VS havárií při správné, klikněte na složku řešení po otevření dialogu uživatelského rozhraní, alespoň jeden.](http://nuget.codeplex.com/workitem/126)
* [Změna místní parametr - seznamu balíčku na - nainstalován](http://nuget.codeplex.com/workitem/129)
* [Přejmenujte packages.xml NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Konzole vynutí kurzor na konec řádku](http://nuget.codeplex.com/workitem/135)
* [Je poškozený balíček odebrat intellisense](http://nuget.codeplex.com/workitem/136)
* [Přidejte příznak RequireLicenseAcceptance příponou .nuspec a informačního kanálu](http://nuget.codeplex.com/workitem/137)
* [Přidat LicenseUrl příponou .nuspec formátu a balíček kanálu](http://nuget.codeplex.com/workitem/138)
* [Kliknutím na instalaci pro balíček, který vyžaduje přijetí by měl zobrazit dialogové okno přijetí](http://nuget.codeplex.com/workitem/139)
* [Přidat Text zřeknutí se práv do dialogu přidat balíček](http://nuget.codeplex.com/workitem/140)
* [Přidat že právní omezení při balíček konzole je spustit při prvním](http://nuget.codeplex.com/workitem/143)
* [Po instalaci balíčku v konzole zobrazit právní omezení](http://nuget.codeplex.com/workitem/144)
* [Přejmenujte rozšíření .nupack .nupkg](http://nuget.codeplex.com/workitem/146)