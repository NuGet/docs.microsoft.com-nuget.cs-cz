---
title: Osvědčené postupy pro zabezpečený dodavatelský řetězec softwaru
description: Osvědčené postupy pro zabezpečení vašeho dodavatelskýho řetězce softwaru pomocí NuGet & GitHubu.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: e0f235d99e41e23a4551fbf7577f6c42e3381f5b
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859223"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Osvědčené postupy pro zabezpečený dodavatelský řetězec softwaru

Open Source je všude. Je v mnoha proprietárních základech kódu a komunitních projektech. V případě organizací a jednotlivců není otázka dnes bez ohledu na to, jestli nepoužíváte open source kód, ale jaký open source kód používáte a kolik máte.

Pokud si nejste vědomi toho, co se nachází ve vašem řetězci pro poskytování softwaru, může být nadřízená zranitelnost v jedné z vašich závislostí závažná a vaše zákazníci je zranitelná s potenciálním ohrožením. V tomto dokumentu budeme podrobně hlubší informace o termínech "dodavatelský řetězec softwaru", proč je to důležité, a jak můžete přispět k zabezpečení dodavatelského řetězce s doporučenými postupy.

![Stav Octoverse 2020-Open Source](media/opensource-percent.png)

## <a name="dependencies"></a>Závislosti 

Termín "dodavatelský řetězec softwaru" se používá k odkazování na všechno, co se týká vašeho softwaru a odkud pochází. Jedná se o závislosti a vlastnosti závislostí, na kterých závisí váš dodavatelský řetězec softwaru. Závislost je to, co váš software potřebuje spustit. Může to být kód, binární soubory nebo jiné komponenty a místo, kde pocházejí z, jako je úložiště nebo správce balíčků.

Obsahuje informace o tom, kdo napsal kód, kdy byl, jak byl přezkoumán z důvodu problémů se zabezpečením, známých chyb zabezpečení, podporovaných verzí, informací o licencích a jenom těch, které se v jakémkoli bodě tohoto procesu dotkne.

Váš dodavatelský řetězec zahrnuje i další části zásobníku mimo jednu aplikaci, jako jsou například vaše skripty sestavení a balíčku nebo software, který spouští infrastrukturu, na které vaše aplikace spoléhá.

## <a name="vulnerabilities"></a>Ohrožení zabezpečení

V současné době jsou závislosti softwaru Pervasive. Pro vaše projekty je poměrně běžné používat stovky Open Source závislostí pro funkce, které jste nemuseli psát sami. To může znamenat, že většina vaší aplikace se skládá z kódu, který jste nevytvořili. 

![Stav rozhraní Octoverse 2020 – závislosti](media/dependencies.png)

Možné chyby zabezpečení v závislostech na Open Source třetích stran nebo otevřených zdrojích se považují za nepřesný kód, který se dá přesně řídit jako kód, který píšete, což může v zásobovacím řetězci způsobit potenciální bezpečnostní rizika.

Pokud jedna z těchto závislostí má ohrožení zabezpečení, je pravděpodobné, že máte také ohrožení zabezpečení. To může být Scary, protože jedna z vašich závislostí se může změnit, aniž byste to ještě znali. I v případě, že v dnešní době existuje ohrožení zabezpečení, ale není zneužitelné, může být možné ho využít i v budoucnu. 

Schopnost využít práci tisíců Open Source vývojářů a tvůrců knihoven znamená, že tisíce cizís mohou efektivně přispět přímo k produkčnímu kódu. Váš produkt je prostřednictvím vašeho dodavatelského řetězce ovlivněn neopravenými chybami zabezpečení, innocentí chyb nebo dokonce škodlivými útoky na závislosti.

## <a name="supply-chain-compromises"></a>Ohrožení zabezpečení dodavatelských řetězců

Tradiční definice dodavatelského řetězce pochází z výroby; je to řetězec procesů potřebných k provedení a poskytnutí nějakého. Zahrnuje plánování, dodávání materiálu, výroby a maloobchodního prodeje. Dodavatelský řetězec je podobný, s výjimkou materiálu, ale je to kód. Namísto výroby se jedná o vývoj. Místo prozkoumá rudy od země je kód od dodavatelů, komerčního nebo open source a obecně platí, že open source kód pochází z úložišť. Přidání kódu z úložiště znamená, že váš produkt má na tomto kódu závislost.

Jedním z příkladů útoku na dodavatelský řetězec softwaru nastane, když se škodlivý kód záměrně přidaný do závislosti, a to pomocí dodavatelského řetězce této závislosti k distribuci kódu na jeho oběti. Útoky dodavatelských řetězců jsou reálné. Existuje mnoho metod útoku na dodavatelský řetězec, od přímého vkládání škodlivého kódu jako nového přispěvatele, pro převzetí účtu přispěvatele bez dalších všímáte nebo dokonce porušení podpisového klíče pro distribuci softwaru, který není oficiálně součástí závislosti.

Útok softwaru na dodavatelského řetězce je v systému a sám o sobě výjimečně koncovým cílem, ale je začátek příležitosti útočníka k vložení malwaru nebo poskytnutí zadní vrátka k budoucímu přístupu.

![Stav životního cyklu Octoverse 2020-zranitelnost](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Neopravný software

Používání Open Source dnes je významné a neočekává se, že se krátce zpomaluje. Vzhledem k tom, že nebudeme používat open source software, hrozba pro poskytnutí zabezpečení řetězce je neopravený software. S vědomím, jak můžete vyřešit riziko, že závislost projektu má ohrožení zabezpečení?

- **Znalost toho, co je ve vašem prostředí.** To vyžaduje zjištění závislostí a všech přenosných závislostí, aby bylo možné pochopit rizika těchto závislostí, jako jsou chyby zabezpečení nebo licenční omezení.
- **Spravujte své závislosti.** Pokud je zjištěna nová ohrožení zabezpečení, je třeba zjistit, zda jste ovlivnili, a pokud ano, aktualizovat na nejnovější verzi a opravu zabezpečení k dispozici. To je obzvláště důležité pro kontrolu změn, které zavádějí nové závislosti nebo pravidelně auditují starší závislosti.
- **Monitorujte svůj dodavatelský řetězec.** To je auditováním ovládacích prvků, které jste nastavili pro správu závislostí. To vám pomůže vymáhat více omezující podmínky pro splnění vašich závislostí.

![Stav Octoverse 2020 – Advisory](media/advisories.png)

Budeme se zabývat různými nástroji a technikami, které nabízí NuGet a GitHub. můžete je využít k tomu, abyste mohli řešit potenciální rizika v rámci projektu. 

## <a name="knowing-what-is-in-your-environment"></a>Znalost toho, co je ve vašem prostředí

### <a name="nuget-dependency-graph"></a>Graf závislosti NuGet

**📦 Uživatel balíčku**

Závislosti NuGet můžete zobrazit v projektu přímo v příslušném souboru projektu.

Obvykle se nachází na jednom ze dvou míst:

-   [`packages.config`](../reference/packages-config.md) – Umístěný v kořenovém adresáři projektu.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Nachází se v souboru projektu. 

V závislosti na tom, jakou metodu používáte ke správě závislosti NuGet, můžete také použít sadu Visual Studio k zobrazení závislostí přímo v [Průzkumník řešení](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) nebo [Správce balíčků NuGet](../consume-packages/install-use-packages-visual-studio.md).

Pro prostředí rozhraní příkazového řádku můžete použít [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) příkaz k vypsání závislosti projektu nebo řešení. 

Další informace o správě závislostí NuGet [najdete v následující dokumentaci](../consume-packages/overview-and-workflow.md).

### <a name="github-dependency-graph"></a>Graf závislosti GitHubu 

**📦 Uživatel balíčku | 📦🖊 Autor balíčku**

Pomocí grafu závislostí na GitHubu můžete zobrazit balíčky, na kterých je váš projekt závislý, a úložiště, která na něm závisejí. To vám může pomáhat při zobrazení všech ohrožení zabezpečení zjištěných v závislosti.

Další informace o závislostech úložiště GitHub [najdete v následující dokumentaci](https://github.co/dependency-graph).

### <a name="dependency-versions"></a>Verze závislostí

**📦 Uživatel balíčku | 📦🖊 Autor balíčku**

Aby se zajistil zabezpečený dodavatelský řetězec závislostí, budete mít jistotu, že všechny závislosti & nástroje se pravidelně aktualizují na nejnovější stabilní verzi, protože budou často zahrnovat nejnovější funkce a opravy zabezpečení známých chyb zabezpečení. Vaše závislosti můžou zahrnovat kód, na který jste měli na zpracování používané binární soubory, používat nástroje a další komponenty. To může zahrnovat:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK & runtime](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Balíčky NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Správa závislostí

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet zastaralé a ohrožené závislosti

**📦 Uživatel balíčku | 📦🖊 Autor balíčku**

Můžete použít rozhraní příkazového [řádku dotnet](/dotnet/core/tools/dotnet-list-package) k vypsání známých neznámých nebo ohrožených závislostí, které jste mohli mít v rámci projektu nebo řešení. Můžete použít příkaz `dotnet list package --deprecated` nebo `dotnet list package --vulnerable` k poskytnutí seznamu známých zastaralých a neznámých chyb.

### <a name="github-vulnerable-dependencies"></a>Ohrožené závislosti GitHubu

**📦 Uživatel balíčku | 📦🖊 Autor balíčku**

Pokud je váš projekt hostovaný na GitHubu, můžete využít [zabezpečení GitHubu](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) k vyhledání chyb zabezpečení a chyb v projektu a Dependabot je opravit otevřením žádosti o přijetí změn v základu kódu. 

Před tím, než se tyto ohrožené závislosti zachytí, je jedním z cílů přesunu ["Shift Left"](https://en.wikipedia.org/wiki/Shift-left_testing) . Můžou mít informace o vašich závislostech, jako jsou jejich licence, přenosné závislosti a stáří závislostí, a to jenom vy.

Další informace o výstrahách Dependabot & aktualizacích zabezpečení [najdete v následující dokumentaci](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).

### <a name="nuget-feeds"></a>Kanály NuGet

**📦 Uživatel balíčku**

Pokud používáte více veřejných & privátních zdrojů NuGet, balíček se dá stáhnout ze všech informačních kanálů. Aby bylo zajištěno, že vaše sestavení je předvídatelné a zabezpečené před známými útoky, jako jsou například [záměna závislostí](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), zajistěte, aby konkrétní kanály, ze kterých vaše balíčky přicházejí, byly osvědčenými postupy. Můžete použít jeden nebo soukromý informační kanál s funkcemi pro zajištění ochrany před podproudy.

Další informace o zabezpečení kanálů balíčků najdete v tématu [3 způsoby, jak zmírnit riziko při použití kanálů soukromého balíčku](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>Zásady důvěryhodnosti klientů

**📦 Uživatel balíčku**

Existují zásady, na které můžete vyjádřit výslovný souhlas s balíčky, které používáte k podepsání. To vám umožňuje důvěřovat autorovi balíčku, pokud je podepsaný autorem, nebo důvěřovat balíčku, pokud je vlastněn konkrétním uživatelem nebo účtem, který je v úložišti podepsaném NuGet.org.

Pokud chcete nakonfigurovat zásady důvěryhodnosti klientů, [Přečtěte si následující dokumentaci](../consume-packages/installing-signed-packages.md).

### <a name="lock-files"></a>Zamknout soubory

**📦 Uživatel balíčku**

Uzamknout soubory uložte hodnotu hash obsahu balíčku. Pokud se hodnota hash obsahu balíčku, který chcete nainstalovat, shoduje se souborem zámku, zajistíte tak, aby se balíčky opakovaly.

Pokud chcete povolit soubory zámku, [Přečtěte si následující dokumentaci](../consume-packages/package-references-in-project-files.md#locking-dependencies).

## <a name="monitor-your-supply-chain"></a>Monitorování dodavatelského řetězce

### <a name="github-secret-scanning"></a>Skenování tajných kódů GitHubu

**📦🖊 Autor balíčku**

GitHub hledá klíče rozhraní API NuGet v úložištích, aby zabránil podvodnému používání tajných kódů, které byly omylem potvrzeny. 

Další informace o kontrole tajných klíčů najdete v tématu [Kontrola tajného](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)kódu.

### <a name="author-package-signing"></a>Vytvořit podpis balíčku

**📦🖊 Autor balíčku**

[Podepisování autora](../reference/signed-packages-reference.md) umožňuje autorovi balíčku razítko své identity na balíčku a příjemce, aby ověřil, že jste dostali. To vás chrání proti falšování obsahu a slouží jako jediný zdroj pravdy na začátku balíčku a pravosti balíčku. V kombinaci se zásadami důvěryhodnosti klientů můžete ověřit, že balíček pochází od určitého autora.

Chcete-li vytvořit podpis balíčku, přečtěte si téma [Sign a Package](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Ověřování Two-Factor (2FA)

**📦🖊 Autor balíčku**

Povolení dvojúrovňové ověřování (2FA) může přidat další úroveň zabezpečení při [přihlašování k účtu GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) nebo k [úložišti veřejného balíčku NuGet.org](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa). Doporučujeme, abyste pro ochranu svého účtu povolili dvojúrovňové ověřování.

### <a name="package-id-prefix-reservation"></a>Rezervace předpony ID balíčku 

**📦🖊 Autor balíčku**

Pokud chcete chránit identitu vašich balíčků, můžete si vyhradit předponu ID balíčku s vaším příslušným oborem názvů, abyste přiřadili odpovídajícího vlastníka, pokud identifikátor ID balíčku správně spadá do [zadaných kritérií](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria). 

Další informace o rezervaci předpon IDENTIFIKÁTORů najdete v tématu [rezervace identifikátoru ID balíčku](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Vyřazení a odbalení chybných balíčků

**📦🖊 Autor balíčku**

Chcete-li chránit ekosystém balíčků rozhraní .NET v případě, že víte o ohrožení zabezpečení v balíčku, který jste vytvořili, je vhodné tento balíček vyřadit a zrušit jeho seznam, aby byl skrytý pro uživatele, kteří hledají balíčky. Pokud pracujete s balíčkem, který je zastaralý a není v seznamu, neměli byste tento balíček používat.

Informace o tom, jak zařadit a odpisovat balíček, najdete v následující dokumentaci týkající se [zastaralých](../nuget-org/deprecate-packages.md) a [odpisovatcích balíčků](../nuget-org/policies/deleting-packages.md#unlisting-a-package).

## <a name="summary"></a>Souhrn

Váš dodavatelský řetězec je cokoli, co se dostane do kódu nebo na něj má vliv. I když ohrožení bezpečnosti dodavatelských řetězců je reálné a rostoucí v oblíbenosti, jsou stále vzácná; Nejdůležitější věcí, které můžete udělat, je chránit váš dodavatelský řetězec tím **, že si znáte své závislosti, spravujete závislosti** a **sledujete dodavatelský řetězec.**

Seznámili jste se s různými metodami, které nabízí NuGet a [GitHub](/learn/modules/maintain-secure-repository-github/) , které máte v současnosti k dispozici k efektivnějšímu zobrazení, správě a monitorování vašeho dodavatelského řetězce.

Další informace o zabezpečení softwaru na světě najdete v tématu [stav sestavy zabezpečení Octoverse 2020](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
