---
title: Osvědčené postupy pro zabezpečený dodavatelský řetězec softwaru
description: Osvědčené postupy pro zabezpečení dodavatelského řetězce softwaru pomocí NuGet & GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726974"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Osvědčené postupy pro zabezpečený dodavatelský řetězec softwaru

Open Source je všude. Je v mnoha proprietárních kódových bázech a komunitní projektech. Pro organizace a jednotlivce není dnes otázkou, jestli používáte nebo ne, ale jaký open source kód používáte a kolik toho používáte.

Pokud nevíte, co je ve vašem dodavatelském řetězci softwaru, může být ohrožení zabezpečení v jedné z vašich závislostí závažné, což vás a vaše zákazníky může ohrozit potenciální ohrožení zabezpečení. V tomto dokumentu se ponoříme hlouběji do toho, co pojem "dodavatelský řetězec softwaru" znamená, proč na tom záleží a jak můžete pomocí osvědčených postupů zabezpečit dodavatelský řetězec projektu.

![The State of the Octoverse 2020 – Open Source](media/opensource-percent.png)

## <a name="dependencies"></a>Závislosti 

Termín dodavatelský řetězec softwaru se používá k odkazování na všechno, co se týká vašeho softwaru a odkud pochází. Jsou to závislosti a vlastnosti závislostí, na které závisí váš dodavatelský řetězec softwaru. Závislost je to, co váš software potřebuje ke spuštění. Může to být kód, binární soubory nebo jiné komponenty a odkud pocházejí, například úložiště nebo správce balíčků.

Zahrnuje to to, kdo kód napsal, kdy byl přidán, jak byl z hlediska problémů se zabezpečením přezkoumán, známá ohrožení zabezpečení, podporované verze, licenční informace a cokoli, co se ho v každém okamžiku procesu dotýká.

Váš dodavatelský řetězec zahrnuje i další části zásobníku nad rámec jedné aplikace, jako jsou například skripty sestavení a balení nebo software, na který běží infrastruktura, na kterou vaše aplikace spoléhá.

## <a name="vulnerabilities"></a>Ohrožení zabezpečení

V současné době se závislosti softwaru pervazivní. Je celkem běžné, že vaše projekty používají stovky open source závislostí pro funkce, které jste si dělali sami. To může znamenat, že většina vaší aplikace se skládá z kódu, který jste nevytváříte. 

![Stav octoverse 2020 – závislosti](media/dependencies.png)

Možné chyby zabezpečení v závislostech třetích stran nebo open source jsou pravděpodobně závislosti, které nemůžete řídit tak těsně jako kód, který napíšete, což může ve vašem dodavatelském řetězci vytvořit potenciální rizika zabezpečení.

Pokud u jedné z těchto závislostí existuje ohrožení zabezpečení, pravděpodobně máte i ohrožení zabezpečení. To může být šmešš, protože se jedna z vašich závislostí může změnit, aniž byste o tom věděli. I v případě, že v dnešní době existuje ohrožení zabezpečení, ale není zneužitelné, může být v budoucnu zneužitelné. 

Když budete moct využít práci tisíců vývojářů a autorů knihoven open source, znamená to, že tisíce michátek mohou efektivně přispívat přímo do produkčního kódu. Váš produkt prostřednictvím softwarového dodavatelského řetězce je ovlivněný neochyceným ohrožením zabezpečení, chybným útokem nebo dokonce škodlivými útoky proti závislostem.

## <a name="supply-chain-compromises"></a>Kompromisy v dodavatelském řetězci

Tradiční definice dodavatelského řetězce pochází z výroby. Je to řetězec procesů, které jsou potřeba k tomu, aby něco bylo možné vytvořit a poskytnout. Zahrnuje plánování, dodávky materiálů, výroba a maloobchod. Softwarový dodavatelský řetězec je podobný, ale místo materiálů se jedná o kód. Místo výroby se jedná o vývoj. Kód pochází od dodavatelů, komerčních nebo open source a obecně jde o open source kód z úložišť. Přidání kódu z úložiště znamená, že váš produkt je na tomto kódu závislé.

Jedním z příkladů útoku na dodavatelský řetězec softwaru je záměrné přidání škodlivého kódu do závislosti, kdy se pomocí dodavatelského řetězce této závislosti distribuuje kód jeho hrozbě. Útoky v dodavatelském řetězci jsou skutečné. Existuje mnoho metod útoku na dodavatelský řetězec, od přímého vložení škodlivého kódu jako nového přispěvatele, převzetí účtu přispěvatele bez toho, aby si toho ostatní všimli, nebo dokonce ohrožení podepisování klíče pro distribuci softwaru, který oficiálně není součástí závislosti.

Útok v dodavatelském řetězci softwaru je sám o sobě zřídka konečným cílem, spíše je to začátek příležitosti pro útočníka, aby vložil malware nebo poskytl zadní vrátka pro budoucí přístup.

![Stav životního cyklu ohrožení zabezpečení z října 2020](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Nepatchovaný software

Použití tohoto open source je významné a neočekává se, že se v nejbližší době zpomalí. Vzhledem k tomu, že nepřestaneme používat open source software, představuje ohrožení zabezpečení dodavatelského řetězce neopatrovaný software. Když víte, jak můžete řešit riziko ohrožení zabezpečení závislosti vašeho projektu?

- **Znalost toho, co je ve vašem prostředí** To vyžaduje zjištění závislostí a všech tranzitivních závislostí, abyste porozuměli rizikům těchto závislostí, jako jsou ohrožení zabezpečení nebo licenční omezení.
- **Spravujte své závislosti.** Při zjištění nové chyby zabezpečení musíte určit, jestli se vás to týká, a pokud ano, aktualizovat na nejnovější verzi a dostupnou opravu zabezpečení. To je zvlášť důležité ke kontrolování změn, které zavádějí nové závislosti nebo pravidelně auditují starší závislosti.
- **Monitorujte svůj dodavatelský řetězec.** To je auditování ovládacích prvků, které máte k dispozici pro správu závislostí. To vám pomůže vynucovat přísnější podmínky, které budou splněny pro vaše závislosti.

![The State of the Octoverse 2020 – Advisories](media/advisories.png)

Budeme se zabývat různými nástroji a technikami, které NuGet a GitHub, které můžete v současné době použít k řešení potenciálních rizik v rámci projektu. 

## <a name="knowing-what-is-in-your-environment"></a>Znalost toho, co je ve vašem prostředí

### <a name="nuget-dependency-graph"></a>NuGet závislostí

**📦 Příjemce balíčku**

Závislosti projektu NuGet zobrazit přímo v příslušném souboru projektu.

Obvykle se nachází na jednom ze dvou míst:

-   [`packages.config`](../reference/packages-config.md) – Nachází se v kořenovém adresáři projektu.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Nachází se v souboru projektu. 

V závislosti na tom, jakou metodu použijete ke správě závislostí NuGet, můžete také použít Visual Studio k zobrazení závislostí přímo v nástroji [Průzkumník řešení](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) [nebo NuGet Správce balíčků](../consume-packages/install-use-packages-visual-studio.md).

V prostředích rozhraní příkazového řádku můžete pomocí příkazu zobrazit seznam závislostí projektu [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) nebo řešení. 

Další informace o správě závislostí NuGet najdete [v následující dokumentaci.](../consume-packages/overview-and-workflow.md)

### <a name="github-dependency-graph"></a>Graf závislosti GitHubu 

**📦 Package Consumer | 📦🖊 Autor balíčku**

Pomocí grafu GitHub závislostí můžete zobrazit balíčky, na které váš projekt závisí, a úložiště, která na ní závisejí. To vám může pomoct zjistit všechna ohrožení zabezpečení zjištěná v jeho závislostech.

Další informace o závislostech GitHub úložišti najdete [v následující dokumentaci.](https://github.co/dependency-graph)

### <a name="dependency-versions"></a>Verze závislostí

**📦 Package Consumer | 📦🖊 Autor balíčku**

Abyste zajistili zabezpečený dodavatelský řetězec závislostí, budete chtít zajistit, aby se všechny vaše nástroje závislostí & pravidelně aktualizovaly na nejnovější stabilní verzi, protože často zahrnují nejnovější funkce a opravy zabezpečení známých ohrožení zabezpečení. Mezi závislosti může zahrnovat kód, na který závisíte, binární soubory, které využíváte, nástroje, které používáte, a další komponenty. To může zahrnovat:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK & Runtime](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Balíčky NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Správa závislostí

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet zastaralé a ohrožené závislosti

**📦 Package Consumer | 📦🖊 Autor balíčku**

Pomocí rozhraní příkazového řádku [dotnet můžete](/dotnet/core/tools/dotnet-list-package) zobrazit seznam známých zastaralých nebo ohrožených závislostí, které můžete mít ve svém projektu nebo řešení. Pomocí příkazu nebo můžete poskytnout seznam známých vynětů nebo `dotnet list package --deprecated` `dotnet list package --vulnerable` ohrožení zabezpečení.

### <a name="github-vulnerable-dependencies"></a>GitHub závislosti s ohroženým zabezpečením

**📦 Package Consumer | 📦🖊 Autor balíčku**

Pokud je váš projekt hostovaný v GitHub, můžete využít zabezpečení GitHub k vyhledání chyb zabezpečení v projektu [a](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) Dependabot je opraví otevřením žádosti o stažení pro váš kód. 

Zachycení ohrožených závislostí před jejich použitím je jedním z cílů přesunu ["Shift](https://en.wikipedia.org/wiki/Shift-left_testing) doleva". Právě to vám pomůže mít informace o vašich závislostech, jako je jejich licence, tranzitivní závislosti a stáří závislostí.

Další informace o výstrahách Dependabotu & aktualizacích zabezpečení najdete [v následující dokumentaci.](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)

### <a name="nuget-feeds"></a>NuGet informační kanály

**📦 Příjemce balíčku**

Pokud používáte více veřejných & privátních NuGet zdrojových informačních kanálů, můžete balíček stáhnout z libovolného informačního kanálu. Pokud chcete zajistit předvídatelnost a zabezpečení sestavení [](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)před známými útoky, jako jsou nejasnosti závislostí, je znalost konkrétních informačních kanálů, ze které vaše balíčky přicházejí, osvědčeným postupem. Pro ochranu můžete použít jeden nebo privátní informační kanál s funkcemi upstreamingu.

Další informace o zabezpečení informačních kanálů balíčků najdete v tématu 3 Způsoby zmírnění rizika při [použití privátních informačních kanálů balíčků.](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)

### <a name="client-trust-policies"></a>Zásady důvěryhodnosti klientů

**📦 Příjemce balíčku**

Existují zásady, ke kterým můžete vyjádřit výslovný souhlas a které vyžadují, aby byly balíčky, které používáte, podepsané. To umožňuje důvěřovat autorovi balíčku, pokud je podepsaný autorem, nebo důvěřovat balíčku, pokud je vlastněn konkrétním uživatelem nebo účtem, který je úložištěm podepsaný NuGet.org.

Informace o konfiguraci zásad důvěryhodnosti klientů [najdete v následující dokumentaci.](../consume-packages/installing-signed-packages.md)

### <a name="lock-files"></a>Uzamčení souborů

**📦 Příjemce balíčku**

Uzamknout soubory ukládají hodnotu hash obsahu balíčku. Pokud se hodnota hash obsahu balíčku, který chcete nainstalovat, shoduje se souborem zámku, zajistí opakovatelnost balíčku.

Informace o povolení zamykací [souborů najdete v následující dokumentaci.](../consume-packages/package-references-in-project-files.md#locking-dependencies)

## <a name="monitor-your-supply-chain"></a>Monitorování dodavatelského řetězce

### <a name="github-secret-scanning"></a>Skenování tajných kódů GitHubu

**📦🖊 Autor balíčku**

GitHub vyhledává v úložištích klíče NuGet API, aby se zabránilo podvodnému použití náhodně potvrzených tajných kódů. 

Další informace o kontrole tajných kódů najdete v tématu [Informace o kontrole tajných kódů.](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)

### <a name="author-package-signing"></a>Podepisování balíčků pro vytváření

**📦🖊 Autor balíčku**

[Podepisování](../reference/signed-packages-reference.md) autorů umožňuje autorovi balíčku vytvořit razítko své identity u balíčku a aby příjemce ověřil, že balíček pochází od vás. To vás chrání před manipulací s obsahem a slouží jako jediný zdroj pravdivých informací o původu balíčku a pravosti balíčku. V kombinaci se zásadami důvěryhodnosti klienta můžete ověřit, že balíček pochází od konkrétního autora.

Pokud chcete balíček podepisovat, podívejte se [na podepisovat balíček.](../create-packages/sign-a-package.md)

### <a name="two-factor-authentication-2fa"></a>Two-Factor ověřování (2FA)

**📦🖊 Autor balíčku**

Povolení dvojfaktorového ověřování (2FA) může při přihlašování k účtu [GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) nebo veřejnému úložišti balíčků NuGet.org přidat další [vrstvu zabezpečení.](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa) K ochraně účtu doporučujeme povolit dvojfaktorové ověřování.

### <a name="package-id-prefix-reservation"></a>Rezervace předpony ID balíčku 

**📦🖊 Autor balíčku**

Pokud chcete chránit identitu balíčků, můžete rezervovat předponu ID balíčku k příslušnému oboru názvů a přidružit odpovídajícího vlastníka, pokud předpona ID balíčku správně spadá pod [zadaná kritéria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria). 

Další informace o rezervaci předpon ID najdete v tématu [Rezervace předpon ID balíčku.](../nuget-org/id-prefix-reservation.md)

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Vynění ohroženého balíčku ze seznamu a jeho vynětování ze seznamu

**📦🖊 Autor balíčku**

Pokud chcete chránit ekosystém balíčků .NET, pokud jste si vědomi ohrožení zabezpečení v balíčku, který jste napsali, vyhověte a zrušte jeho seznam, aby byl skrytý před uživateli, kteří hledají balíčky. Pokud balíček, který je zastaralý a neuvedený, byste se měli tomuto balíčku vyhnout.

Informace o vynětu nebo zrušení seznamu balíčku najdete [](../nuget-org/deprecate-packages.md) v následující dokumentaci k vynětu nebo zrušení seznamu [balíčků](../nuget-org/policies/deleting-packages.md#unlisting-a-package).

## <a name="summary"></a>Souhrn

Váš dodavatelský řetězec softwaru je cokoli, co se týká vašeho kódu nebo ho ovlivňuje. I když jsou kompromisy v dodavatelském řetězci skutečné a stále roste jejich oblíbenost, jsou stále vzácné. Nejdůležitější věc, kterou můžete udělat, je chránit dodavatelský řetězec **tím,** že budete vědět o závislostech, spravovat závislosti a **monitorovat dodavatelský řetězec.**

Dozvěděli jste se o různých metodách, které NuGet a [GitHub](/learn/modules/maintain-secure-repository-github/) které jsou vám dnes k dispozici, abyste si ho prohlížet, správou a monitorováním dodavatelského řetězce efektivněji prohlížet, spravovat a monitorovat.

Další informace o zabezpečení softwaru na světě najdete v tématu [The State of the Octoverse 2020 Security Report](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
