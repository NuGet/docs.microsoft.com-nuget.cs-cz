---
title: Zpráva k vydání verze NuGet 1.0 a 1.1
description: Zpráva k vydání verze NuGet 1.1, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547018"
---
# <a name="nuget-10-and-11-release-notes"></a>Zpráva k vydání verze NuGet 1.0 a 1.1

[NuGet 1.2 poznámky](../release-notes/nuget-1.2.md)

NuGet 1.0 byla vydána 13. ledna 2011.  NuGet 1.1 byl vydán 12. února 2011.

## <a name="overview"></a>Přehled

Tento dokument obsahuje poznámky k verzi pro různé verze 1.0 NuGet seskupené podle hlavní verze preview verzi.

NuGet obsahuje následující součásti:

* *NuGet.Tools.vsix* * která se skládá ze:
  * **Přidat Dialog balíček knihovny** * dialogového okna v sadě Visual Studio umožňuje procházet a instalovat balíčky.
  * **Konzola správce balíčků** * konzoly Powershellu v sadě Visual Studio.
* *Nástroj příkazového řádku NuGet* * nástroj používá k vytvoření (a nakonec publikování) balíčky.

NuGet nástroje Visual Studio Extension (*NuGet.Tools.vsix*) vyžaduje:

* Visual Studio 2010 nebo Visual Web Developer 2010 Express.

Nástroj příkazového řádku NuGet vyžaduje:

* Verze rozhraní .NET framework 4

## <a name="installation"></a>Instalace

Chcete-li použít [nejnovější vydaná verze](http://nuget.codeplex.com/releases/view/52018):

* Nejprve odinstalujte starší sestavení. Budete muset spustit jako správce k tomu VS.
* Odeberte všechny existující informační kanály, které máte.
* Přidat nový informační kanál odkazující na [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Seznam opravených chybách v této verzi [najdete tady](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Jeden problém byl vyřešen pro verzi RTM od verze RC.

* [Problém 474: Odebrání balíčků se týká všech projektů v řešení](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Verze Release Candidate

Tady jsou změny provedené v této verzi Release Candidate od verze CTP 2. Navštivte web sledování problémů, které chcete zobrazit úplný seznam chyb.

* [Aktualizuje se balíček z konzoly neaktualizuje závislosti.](http://nuget.codeplex.com/workitem/443)
* [Přidání balíčku příjmem bin balíček není odkaz (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aktualizuje se balíček opustí poškozenými odkazy](http://nuget.codeplex.com/workitem/440)
* [Get-Package-aktualizace nezdaří, v dialogovém okně nebo "všechny agregovaného zdroje je vybraný v konzole](http://nuget.codeplex.com/workitem/439)
* [Chyby ověření balíčku](http://nuget.codeplex.com/workitem/426)
* [Upozornit uživatele, když balíček nelze nainstalovat z tohoto dialogového okna Přidat balíček](http://nuget.codeplex.com/workitem/425)
* [Get-Package-aktualizuje vyvolá výjimku při aktualizaci velkého počtu balíčků](http://nuget.codeplex.com/workitem/424)
* [Zlepšení zpracování chyb při nesprávně vytvořené souborů nuspec](http://nuget.codeplex.com/workitem/423)
* [Balíček Nuget ignoruje zadané soubory](http://nuget.codeplex.com/workitem/422)
* [Odebráním zdroje druhé poslední balíček a pak levým na "Dolů" dojde k chybě VS](http://nuget.codeplex.com/workitem/418)
* [Odebrat odkaz na sestavení při instalaci balíčků](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException při otevírání dialogové okno nastavení](http://nuget.codeplex.com/workitem/411)
* [Přístupový klíč zdroje balíčku v konzole Správce balíčků nefunguje](http://nuget.codeplex.com/workitem/410)
* [NuGet VS přístupových klíčů k dialogové okno nastavení fokusu na nesprávné pole](http://nuget.codeplex.com/workitem/409)
* [Intellisense ID balíčku nesmí dotaz příliš mnoho položek](http://nuget.codeplex.com/workitem/404)
* [Chyba přidání balíčku do projektu s tečku v názvu projektu](http://nuget.codeplex.com/workitem/403)
* [Problém s zadané soubory v souboru nuspec](http://nuget.codeplex.com/workitem/400)
* [Správné oficiální informačního kanálu by měl získat zaregistrován při použití novější sestavení](http://nuget.codeplex.com/workitem/399)
* [Značky by měla využívat mezery namísto #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata chybí některé užitečné informace](http://nuget.codeplex.com/workitem/388)
* [Do dialogového okna Přidat odkaz na sestavu urážlivý příspěvek](http://nuget.codeplex.com/workitem/386)
* [K rozbalení konce balíčky v sadě Visual Studio pomocí App_Data](http://nuget.codeplex.com/workitem/380)
* [Implementace značky](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder umožňuje prázdný balíček nemá žádné závislosti, který se má vytvořit](http://nuget.codeplex.com/workitem/373)
* [Přidat vlastníky pole pro balíček](http://nuget.codeplex.com/workitem/365)
* [Aktualizujte manifest VSIX do Řekněme, že Správce balíčků NuGet, místo nástroje VSIX](http://nuget.codeplex.com/workitem/364)
* [Příkaz Get-Package vyvolá chybu, pokud je vybrána všechny zdroje](http://nuget.codeplex.com/workitem/359)
* [Povolit řazení zdroje balíčků v dialogovém okně Možnosti](http://nuget.codeplex.com/workitem/356)
* [Update-Package neodebere starší verze](http://nuget.codeplex.com/workitem/352)
* [Rozsah verzí implementace specifikace pro závislosti](http://nuget.codeplex.com/workitem/347)
* [Visual Studio dojde k chybě při kliknutí na "Přidat nový balíček"](http://nuget.codeplex.com/workitem/346)
* [Zobrazit soubory ke stažení a hodnocení v dialogovém okně Přidat balíček](http://nuget.codeplex.com/workitem/345)
* [Změna mezi zdroje balíčků v dialogovém okně neaktualizuje aktivní zdrojová](http://nuget.codeplex.com/workitem/344)
* [Odebrat klávesovou zkratku pro okna konzoly Správce balíčků](http://nuget.codeplex.com/workitem/339)
* [Install-Package není rozpoznán jako název rutiny...](http://nuget.codeplex.com/workitem/338)
* [Instalace balíčku z místního kanálu závislosti na regulární informačních kanálů nejsou Vyřešeno](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies přeskočte závislosti, které jsou stále používán](http://nuget.codeplex.com/workitem/331)
* [Pokud Probíhá rušení navigace po stránkách, uživatel nedá se Navigovat na jinou stránku a vrátí původní požadavek na stránku](http://nuget.codeplex.com/workitem/325)
* [Vyšetřování výkonu z NuPack.Server pro poskytování informační kanály s velkého počtu balíčků.](http://nuget.codeplex.com/workitem/324)
* [Druhý čas, který mohu filtrovat pro balíček používá zdroj balíčku "New" namísto dříve vybraný zdroj.](http://nuget.codeplex.com/workitem/321)
* [Výchozí zdroj balíčku musí být vybrána, když vyberete kartu "Online" v dialogovém okně.](http://nuget.codeplex.com/workitem/320)
* [Seznam balíčků by se ve výchozím nastavení Zobrazit nainstalované balíčky](http://nuget.codeplex.com/workitem/309)
* [HintPaths odkaz na sestavení](http://nuget.codeplex.com/workitem/294)
* [Výjimka při spuštění konzoly Správce balíčků](http://nuget.codeplex.com/workitem/268)
* [Technologie intellisense konzoly stáhne celý kanál](http://nuget.codeplex.com/workitem/259)
* ["Výchozí" zdroj balíčku by měl přejmenují na "Aktivní"](http://nuget.codeplex.com/workitem/258)
* [Zdroje balíčku uživatelského rozhraní: Kliknutím na tlačítko OK by měl přidat nový zdroj, pokud název/zdrojového pole jsou prázdné](http://nuget.codeplex.com/workitem/257)
* [Dialogové okno změní velmi pomalé, pokud je velký počet nainstalovaných balíčků](http://nuget.codeplex.com/workitem/243)
* [Podpora přesměrování vazby pro sestavení se silným názvem](http://nuget.codeplex.com/workitem/238)
* [Přidání odkazu na balíček... Uživatelské rozhraní, aby zahrnout rozevírací seznam zdroje balíčku.](http://nuget.codeplex.com/workitem/226)
* [NuPack musí podporovat konfigurační transformaci agnostically daného názvu souboru config](http://nuget.codeplex.com/workitem/224)
* [Umožňuje BasePath bude přepsat v NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Chování záložní zdroj balíčku](http://nuget.codeplex.com/workitem/204)
* [Selhání v grafickém uživatelském rozhraní](http://nuget.codeplex.com/workitem/201)
* [Přidat řazení možnosti, jak přidat Dialog balíčku](http://nuget.codeplex.com/workitem/179)
* [Klávesová zkratka pro vymazání Konzola správce balíčků](http://nuget.codeplex.com/workitem/174)
* [Konzoly PowerConsole způsobí, že konzola NuPack selhání](http://nuget.codeplex.com/workitem/166)
* [Konzole a přidat Dialog balíčku by měl nastavit uživatelský agent v požadavcích](http://nuget.codeplex.com/workitem/141)
* [Nastavit číslo verze VSIX a NuPack.exe v sestavení.](http://nuget.codeplex.com/workitem/134)
* [Skrýt společné parametry prostředí PowerShell z-?](http://nuget.codeplex.com/workitem/118)
* [Add - podrobnou nápovědu pro příkazy konzoly](http://nuget.codeplex.com/workitem/110)
* [Přidat Dialog balíčku by měla umožňovat výběr aktuálním zdroji balíčků](http://nuget.codeplex.com/workitem/88)
* [Přesuňte NuPack.Core třídy do různých oborech názvů](http://nuget.codeplex.com/workitem/50)
* [Přidat nápovědu pro rutiny](http://nuget.codeplex.com/workitem/23)
* [Po dokončení stahování balíčku ověřit hash z informačního kanálu](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Tady jsou nejvýznamnější změny provedené ve verzi CTP 2:

* Přepnout balíček kanálu pro koncový bod služby OData z ATOM: Pokud provedete upgrade na verzi CTP2 balíčku nuget, je potřeba přidat následující adresy URL jako zdroj balíčku: `https://feed.nuget.org/ctp2/odata/v1/`.
* Přejmenovat příkazu Add-Package *Install-Package*.
* Aktualizuje `.nuspec` formátu. `.nuspec` Formát nyní zahrnuje *iconUrl* pole pro zadání ikony png 32 x 32, které se zobrazí v dialogovém okně Přidat balíček. Proto ji nezapomeňte nastavit, které k rozlišení vašeho balíčku. `.nuspec` Formátu obsahuje také novou *projectUrl* pole, které můžete použít tak, aby odkazoval na webovou stránku, která poskytuje další informace o balíčku.

Toto sestavení nebude fungovat se starou `.nupkg` soubory. Pokud se zobrazí odkaz s hodnotou null výjimky, které používáte své staré `.nupkg` souboru a nutné znovu sestavit s aktualizovaný [nástroj příkazového řádku NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Následuje seznam funkcí a chybám, které byly opraveny pro NuGet verze CTP 2 (neobsahuje chyby pro čištění drobné úpravy v kódu atd.).

* [Chyba dekomprimace balíčku sestavení při providers TargetFramework pro sestavení.](http://nuget.codeplex.com/workitem/10)
* [Zjistitelnost okna konzoly NuPack](http://nuget.codeplex.com/workitem/14)
* [Verze nupack.exe ILMerge.](http://nuget.codeplex.com/workitem/19)
* [Lepší zpracování chyb a výjimek](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager by měla řádně zpracovat chyby související s informačního kanálu](http://nuget.codeplex.com/workitem/28)
* [Potřebujete novou ikonu konzoly nástroje](http://nuget.codeplex.com/workitem/29)
* [V dialogovém okně řetězce pro lokalizaci](http://nuget.codeplex.com/workitem/38)
* [NuPack mezipaměti stažených souborů .nupack v paměti](http://nuget.codeplex.com/workitem/40)
* [NuPack konzoly: Změňte výchozí klávesovou zkratku pro zobrazení konzoly](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem by měly podporovat výchozí hodnoty pro běžné vlastnosti](http://nuget.codeplex.com/workitem/49)
* [Spuštění nupack.exe ve složce s pouze jeden soubor nuspec používejte tohoto souboru nuspec](http://nuget.codeplex.com/workitem/52)
* [Nabídky projektu se zobrazí i když není načtené žádné projekt/řešení](http://nuget.codeplex.com/workitem/54)
* [Build.cmd selže na vyčištění klon základu kódu](http://nuget.codeplex.com/workitem/56)
* [Funkce k dispozici aktualizace](http://nuget.codeplex.com/workitem/57)
* [Dialogové okno: Přidáte balíček pomocí dialogu odebere řádku tento příkaz v konzole](http://nuget.codeplex.com/workitem/73)
* [Přidání balíčku kliknutím na tlačítko 'Install' je často pomalé, s žádný vizuální zpětnou vazbu](http://nuget.codeplex.com/workitem/80)
* [Neexistuje žádný způsob, jak zjistit, které Moje nainstalované balíčky mají aktualizace.](http://nuget.codeplex.com/workitem/82)
* [Neexistuje žádný způsob, jak aktualizovat nainstalovaný balíček v dialogovém okně.](http://nuget.codeplex.com/workitem/83)
* [Neexistuje žádný způsob, jak odinstalovat nainstalovaného balíčku v dialogovém okně](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Přidání odkazu na balíček&hellip; &rdquo; se zobrazí v místní nabídce nainstalovaných odkazů](http://nuget.codeplex.com/workitem/85)
* [Po aktualizaci balíčku v konzole zobrazí starou a novou verzi, dokud nainstalovány](http://nuget.codeplex.com/workitem/86)
* [Aktivity v konzole, při použití dialogového okna, zmizí po použití](http://nuget.codeplex.com/workitem/87)
* [Analýza kódu v nupack.exe vyčištění příkazového řádku](http://nuget.codeplex.com/workitem/89)
* [Přidat popisný název zdroje balíčků](http://nuget.codeplex.com/workitem/98)
* [Aktualizace souboru .nuspec pro podporu včetně ikony balíčku](http://nuget.codeplex.com/workitem/103)
* [Informačního kanálu uživatelské rozhraní neumožňuje kopírování adresy URL](http://nuget.codeplex.com/workitem/105)
* [Lepší zpracování chyb remove-package.](http://nuget.codeplex.com/workitem/107)
* [Psát do okna konzoly závisí na kurzoru](http://nuget.codeplex.com/workitem/112)
* [Podívejte se awful chybové zprávy](http://nuget.codeplex.com/workitem/116)
* [Výkon odebrat balíček, který není nainstalován balíček je chybný.](http://nuget.codeplex.com/workitem/117)
* [Odebrání balíčku selže, pokud neexistují žádné zdroje balíčku](http://nuget.codeplex.com/workitem/119)
* [Remove-Package selže, pokud je k dispozici zdroj balíčku](http://nuget.codeplex.com/workitem/120)
* [Přidáte nadpis metadata balíčků a informačního kanálu.](http://nuget.codeplex.com/workitem/125)
* [Přidat parametr-zdroje zpět do Add-Package](http://nuget.codeplex.com/workitem/127)
* [Uvedení balíčku musí mít parametr – zdroj](http://nuget.codeplex.com/workitem/128)
* [Aktualizace NuPack.Server tak, aby vyžadovala NuPack uživatele chcete stáhnout balíček agenta](http://nuget.codeplex.com/workitem/142)
* [Dialogové okno přijetí licence musí seznam pro všechny závislosti, které vyžadování přijetí licence](http://nuget.codeplex.com/workitem/145)
* [Zaznamenat chybu, pokud balíček vyvolá v informačním kanálu](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe by nemělo umožňovat prázdná &lt;licenseurl&gt; – element](http://nuget.codeplex.com/workitem/152)
* [Přejmenujte List-Package Get-Package, Add-Package Install-Package a Remove-Package k odinstalaci balíčku](http://nuget.codeplex.com/workitem/155)
* [Pomocí položky nabídky přidat odkaz na balíček z navigátoru řešení dojde k chybě sady Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Popisek "zdroje balíčků k dispozici" chybí dvojtečka](http://nuget.codeplex.com/workitem/160)
* [Ujistěte se, souboru .nuspec xml element malých a velkých písmen konzistentně ve formátu camelCase notaci](http://nuget.codeplex.com/workitem/161)
* [Manifest NuPack VSIX je potřeba zapnout bit "admin"](http://nuget.codeplex.com/workitem/162)
* [Pokud spustíte seznam balíčků s žádné kanály, se zobrazí chyba nulová reference](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: Zadejte cílovou cestu](http://nuget.codeplex.com/workitem/171)
* [Otevření konzole pro správu balíčků na WinXP chyb Powershellu](http://nuget.codeplex.com/workitem/175)
* [VS selhání při pokusu o načtení seznamu balíčků](http://nuget.codeplex.com/workitem/176)
* [Povolit meta balíčky (žádné soubory, jenom závislosti)](http://nuget.codeplex.com/workitem/180)
* [Převést na modul prostředí Powershell 2.0 skript prostředí Powershell](http://nuget.codeplex.com/workitem/181)
* [PathResolver by měl zahodit cesta část when zástupné znaky, pokud je zadaný cíl](http://nuget.codeplex.com/workitem/183)
* [Žádné závislosti.](http://nuget.codeplex.com/workitem/186)
* [Chyba při instalaci Elmah](http://nuget.codeplex.com/workitem/192)
* [Konfigurační transformace nebudou správně fungovat s &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Proměnná ' $global: projectCache' nelze načíst, protože není nastavený.](http://nuget.codeplex.com/workitem/203)
* [Přidat úkol MSBuild pro vytváření balíčků NuPack](http://nuget.codeplex.com/workitem/205)
* [seznam balíčků musí podporovat vyhledávání a filtrování](http://nuget.codeplex.com/workitem/206)
* [Vždy zobrazí odkaz na licenci, pokud autora balíčku obsahuje adresu URL licence](http://nuget.codeplex.com/workitem/208)
* [Příležitostné "Přístup byl odepřen" výjimka s Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Neúspěšné testy jednotek: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Povolit pro použití náhradní lokality/výchozí sadu souborů, pokud na určitou verzi rozhraní framework nebyla nalezena.](http://nuget.codeplex.com/workitem/223)
* [Přidání odkazu na balíček... Uživatelského rozhraní nelze odebrat balíček](http://nuget.codeplex.com/workitem/225)
* [Přidat odkaz na balíček, dojde k chybě studio, když je jeden nebo více projektů není načtený](http://nuget.codeplex.com/workitem/228)
* [Konfigurační transformaci pro práci na souboru web.debug.config nezobrazí.](http://nuget.codeplex.com/workitem/229)
* [Init.ps1 se nespustí, na vlastní balíček](http://nuget.codeplex.com/workitem/237)
* [Při přidávání cest seznam kanálů, výchozí tlačítko je nastaveno na OK, takže pokud stisknutí klávesy ENTER se automaticky zavře](http://nuget.codeplex.com/workitem/240)
* [Pokus odinstalovat závislost dojde k chybě VS při pokusu o 2 časy na řádku](http://nuget.codeplex.com/workitem/241)
* [Zobrazovaná adresa URL projektu v dialogovém okně Přidat balíček](http://nuget.codeplex.com/workitem/253)
* [Výchozí dialogové okno Add-Package na nainstalované balíčky](http://nuget.codeplex.com/workitem/254)
* [Změňte položku nabídky Přidat Dialog balíčku.](http://nuget.codeplex.com/workitem/261)
* [Přejmenovat obory názvů a sestavení](http://nuget.codeplex.com/workitem/274)
* [Přejmenování projektu NuPack NuGet](http://nuget.codeplex.com/workitem/282)
* [Přidejte následující text v seznamu závislostí](http://nuget.codeplex.com/workitem/288)
* [Změní celý text přijetí licence v dialogové okno přijetí licence](http://nuget.codeplex.com/workitem/291)
* [Změní celý text v dialogové okno přijetí licence nad seznamem balíčků](http://nuget.codeplex.com/workitem/292)
* [Adresa URL odkazu fwlink nebude fungovat OData](http://nuget.codeplex.com/workitem/304)
* [Uživatelské rozhraní Správce balíčků: přes agresivní ukládání do mezipaměti počet balíčků použitý pro stránkování](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; chyba Konzola správce balíčků](http://nuget.codeplex.com/workitem/335)
* [Přidat že dialog balíčku zobrazuje licence přijetí pro již nainstalované zabalit](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Následuje seznam funkcí a chybám, které byly opraveny pro NuGet CTP 1.

* [Rozšíření balíčku by měl být přejmenován na .nupack](http://nuget.codeplex.com/workitem/1)
* [Přesuňte soubor balíčku do složky](http://nuget.codeplex.com/workitem/2)
* [Sloučit instalace &amp; příkazy přidat PS](http://nuget.codeplex.com/workitem/3)
* [Vytvoření aliasů pro rutiny sloveso-podstatné jméno](http://nuget.codeplex.com/workitem/4)
* [Získá NuPack Zaměňovat při přepnutí řešení v sadě Visual Studio](http://nuget.codeplex.com/workitem/6)
* [Jsme měli ve výchozím nastavení skrýt složku "packages" řešení](http://nuget.codeplex.com/workitem/11)
* [Přidání podpory pro nahrazování tokenů v obsahu položky.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI používejte PackageSource rozhraní API](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager označí balíčky, jak nainstalovat před instalací je](http://nuget.codeplex.com/workitem/27)
* [Odstranit výchozí projekt z řešení stále hlásí odstraněný projekt jako výchozí](http://nuget.codeplex.com/workitem/30)
* [Nový balíček selže a zobrazí se "Nelze přidat součást pro zadaný identifikátor URI protože je již v balíčku."](http://nuget.codeplex.com/workitem/32)
* [Odebrání řetězce "NuPack" Visual Studio grafického uživatelského rozhraní](http://nuget.codeplex.com/workitem/35)
* [Přidat soubor Apache záhlaví do COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Odebrat příkaz PackageSource aktualizace](http://nuget.codeplex.com/workitem/37)
* [Vyvolá výjimku, nepůjdou použít při načítání profilu Správce balíčků](http://nuget.codeplex.com/workitem/39)
* [Init.ps1 a install.ps1, uninstall.ps1 musí přijímat další stav](http://nuget.codeplex.com/workitem/41)
* [Zkombinovat do jednoho balíčku konzoly a balíčky grafického uživatelského rozhraní](http://nuget.codeplex.com/workitem/42)
* [Logiku transformace XML nebude fungovat, pokud se použije pro soubor XML, který není v kořenovém adresáři](http://nuget.codeplex.com/workitem/43)
* [Správa aktualizace konzoly NuPack dialogu nastavení zdroje balíčku](http://nuget.codeplex.com/workitem/44)
* [Uživatelské rozhraní konzoly NuPack: Přejmenování rozevíracího seznamu "Balíček informačního kanálu" k "zdroje balíčku.](http://nuget.codeplex.com/workitem/45)
* [Možnosti NuPack konzoly: Přejmenování úložiště UI pro zajištění konzistence s NuPack konzoly](http://nuget.codeplex.com/workitem/46)
* [Přidání balíčku selže proti, která byla spuštěna ze služby IIS nebo adresa URL webu](http://nuget.codeplex.com/workitem/53)
* [Zdroj Správce balíčků nefunguje s FwLink](http://nuget.codeplex.com/workitem/55)
* [Nastavit výchozí zdroj balíčku](http://nuget.codeplex.com/workitem/59)
* [Při přidávání zdroje balíčků v případech, pokud je zadán pouze jeden zdroj, se předpokládá, že je výchozí hodnota.](http://nuget.codeplex.com/workitem/60)
* [Dialogové okno uživatelského rozhraní zobrazuje falešné "poslední" balíčků](http://nuget.codeplex.com/workitem/62)
* [Možnosti: Kliknutím na Storno nezruší se změny](http://nuget.codeplex.com/workitem/63)
* [Přidání balíčku odkaz dialogové okno hledání by měla být malá a velká písmena](http://nuget.codeplex.com/workitem/65)
* [Oprava metadat společnosti v souborech AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Číslo verze souboru VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Používáte-? Zobrazí nápovědu dvakrát](http://nuget.codeplex.com/workitem/72)
* [Spouštění instalace/odinstalace balíčků pro balíčky na úrovni projektu](http://nuget.codeplex.com/workitem/74)
* [Server nemůže vytvořit kanál, když jeden nupack neprojde ověřením](http://nuget.codeplex.com/workitem/90)
* [Třeba nahradit NuPack ikony](http://nuget.codeplex.com/workitem/94)
* [Proxy server http protokolu NTLM do informačního kanálu balíčku neověřuje.](http://nuget.codeplex.com/workitem/96)
* [Dialogové okno nelze spustit vždy na střed v okně VS](http://nuget.codeplex.com/workitem/100)
* [Počet polí v podrobnostech balíčky nejsou připravují v dialogovém okně](http://nuget.codeplex.com/workitem/102)
* [Dialogové okno uživatelského rozhraní nezobrazí jména autorů](http://nuget.codeplex.com/workitem/108)
* [Proč – verze pro Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Odebrat poslední kartu v Uživatelském rozhraní dialogového okna](http://nuget.codeplex.com/workitem/115)
* [Selhání VS při vpravo klikněte na složku řešení po otevření dialogového okna uživatelského rozhraní, aspoň jeden.](http://nuget.codeplex.com/workitem/126)
* [Změna místní parametr - balíčku seznamu – nainstalována](http://nuget.codeplex.com/workitem/129)
* [Přejmenovat packages.xml NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Konzola vynutí kurzor na konec řádku](http://nuget.codeplex.com/workitem/135)
* [Remove-Package intellisense bylo přerušeno](http://nuget.codeplex.com/workitem/136)
* [Přidat příznak RequireLicenseAcceptance do souboru .nuspec a informačního kanálu](http://nuget.codeplex.com/workitem/137)
* [Přidat LicenseUrl do formátu souboru .nuspec a balíčků informačního kanálu](http://nuget.codeplex.com/workitem/138)
* [Kliknutím na nainstalovat pro balíček, který vyžaduje přijetí by se zobrazit dialogové okno přijetí](http://nuget.codeplex.com/workitem/139)
* [Přidat Text zřeknutí se práv do dialogového okna Přidat balíček](http://nuget.codeplex.com/workitem/140)
* [Přidejte, že ustanovení o právním omezení při balíček konzoly je první čas spuštění](http://nuget.codeplex.com/workitem/143)
* [Po instalaci balíčku v konzole zobrazit právní omezení](http://nuget.codeplex.com/workitem/144)
* [Přejmenovat rozšíření .nupack .nupkg](http://nuget.codeplex.com/workitem/146)