---
title: NuGet.org často kladené otázky
description: Běžné otázky a odpovědi pro práci s galerií NuGet
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 24e35f4b2c047d5f337a1779e63846b11b0c1011
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380581"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org často kladené otázky

## <a name="license-terms"></a>Licenční podmínky

**Jaké jsou výchozí licenční smlouvy, pokud balíček neposkytuje konkrétní informace o licenci?**

Každý balíček se řídí podmínkami, které jsou součástí balíčku. Příslušné podmínky byste si měli projít před přístupem, stažením nebo získáním balíčků. V NuGet.org použijte odkaz **informace o licenci** na stránce balíček.

Pokud balíček neurčí licenční podmínky, obraťte se na vlastníka balíčku přímo pomocí odkazu **vlastníci kontaktu** na stránce balíček NuGet.org. Společnost Microsoft nelicencuje žádné duševní vlastnictví od poskytovatelů balíčků třetích stran a nezodpovídá za informace poskytované třetími stranami.

## <a name="managing-packages-on-nugetorg"></a>Správa balíčků na NuGet.org

**Můžu po nahrání metadat balíčku upravit?**

NuGet doporučuje, aby byly všechny balíčky podepsané. Principem návrhu podepisování balíčku je, že obsah podepsaného balíčku musí být neměnný, což zahrnuje nuspec. Když upravíte metadata balíčku, dojde ke změnám v nuspec, při které se neověřují stávající podpisy. Doporučujeme změnit existující pracovní postupy tak, aby po vytvoření balíčku nevyžadovaly úpravu metadat balíčku.

Všimněte si, že závislosti uvedené pro váš balíček jsou vygenerovány automaticky z samotného balíčku a nelze je upravovat.

Kromě toho je nahrávání balíčků do [int.nugettest.org](https://int.nugettest.org) skvělým způsobem, jak otestovat a ověřit váš balíček, aniž by bylo možné zpřístupnit balíček ve veřejné galerii. Koncový bod rozhraní API: https://apiint.nugettest.org/v3/index.json

**Můžu odstranit balíček publikovaný do NuGet.org?**

Obecně platí, že odstranění balíčku publikovaného na NuGet.org nepodporujeme. Přečtěte si další informace o našich [zásadách odstraňování balíčků](policies/deleting-packages.md).

**Je možné rezervovat názvy pro balíčky, které budou publikovány v budoucnu?**

Ano. ID pro balíčky na [NuGet.org](https://www.nuget.org/) můžete vyhradit tak, že si pro svůj účet vyžádáte předponu ID balíčku. Pokud chcete požádat o předponu ID balíčku, postupujte podle pokynů v [dokumentaci](id-prefix-reservation.md).

**Návody vlastnictví deklarací pro balíčky?**

Viz [Správa vlastníků balíčků na NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Návody se zabývat vlastníkem balíčku, který porušuje licenci na software?**

Doporučujeme, aby komunita NuGet spolupracovala s řešením všech sporů, které mohou nastat mezi vlastníky balíčku a vlastníky jiného softwaru. Před vyžádáním NuGet.org správců do intercede jsme tento [proces řešení sporů](policies/dispute-resolution.md) provedli.

**Doporučuje se nahrát testovací balíčky do NuGet.org?**

Pro účely testování můžete použít [int.nugettest.org](https://int.nugettest.org)nebo alternativní veřejné servery NuGet, jako je [Myget.org](https://myget.org) nebo [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Všimněte si, že balíčky nahrané do int.nugettest.org nemusí být zachovány.

**Jaká je maximální velikost balíčků, které můžu nahrát na NuGet.org?**

NuGet.org umožňuje balíčkům až 250MB, ale doporučujeme udržovat balíčky pod 1 MB, pokud je to možné, a použít závislosti k propojení balíčků dohromady. Jako pravidlo pro palec balíčky obsahují jenom jedno sestavení, aby se předešlo kolizím.

NuGet ke stažení balíčků používá protokol HTTP, takže větší balíčky mají vyšší pravděpodobnost neúspěšných instalací, než jsou menší.

Je možné sdílet závislosti mezi několika balíčky, takže celková velikost stahovaných souborů pro uživatele vašich balíčků NuGet je menší.

Závislosti jsou většinou statické a nikdy se nemění. Při opravě chyby v kódu nemusí být nutné aktualizovat závislosti. Pokud provedete závislosti sady prostředků, budete pokaždé, když budete znovu dodávat větší balíčky. Díky rozdělení balíčků NuGet do souvisejících závislostí jsou upgrady mnohem podrobněji pro uživatele vašeho balíčku.

## <a name="nugetorg-not-accessible"></a>NuGet.org není přístupná.

**Proč nemůžu stahovat balíčky z nebo nahrávat balíčky do NuGet.org?**

Nejdřív se ujistěte, že používáte nejnovější verze NuGetu. Pokud se tato verze stále nedaří, obraťte se na [podporu](https://www.nuget.org/policies/Contact) a poskytněte další informace pro řešení potíží s připojením, včetně:

- Verze sady NuGet, kterou používáte
- Zdroje balíčků, které používáte
- Protokol obnovení s podrobnou mírou podrobností
- Trasování MTR nebo Fiddler (viz níže)
- Vaše geografická oblast
- Bez ohledu na to, jestli je váš počítač za proxy nebo bránou firewall?
- Je váš počítač umístěný v datovém centru poskytovatelů cloudu (Azure, AWS atd.)? Pokud ano, zadejte prosím název poskytovatele a oblast.

*Pro zachycení MTR:*

- Stáhněte si [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download).
- Jako název hostitele zadejte `api.nuget.org` a klikněte na **Spustit**.
- Počkejte, dokud se sloupec **odeslán** > = 100.

    ![Zachycení MTR](media/mtr.png)

- Zkopírovat text do schránky.

*Pro zachycení Fiddler:*

- Nainstalujte nejnovější verzi [Fiddler](http://www.telerik.com/download/fiddler).
- Spusťte Fiddler a zakažte zachycení provozu pomocí nabídky **soubor > zachytit provoz** .
- Odeberte všechny relace (vyberte všechny položky v seznamu a stiskněte klávesu **Delete** ).
- Nakonfigurujte Fiddler pro zachycení provozu HTTPS tím, že zkontrolujete **dešifrování přenosů** https na kartě **https** v nabídce **Nástroje > Fiddler možnosti...** .
- Zavřete Visual Studio.
- Povolte nabídku **soubor > zachytit provoz** .
- Spusťte aplikaci Visual Studio nebo NuGet. exe. exe a proveďte akce, které nefungují. Přenosy vygenerované těmito akcemi by se měly zobrazit v Fiddler.
- Po spuštění akcí použijte **soubor > uložit > všechny relace** pro uložení zachycených relací.

Poznámka: může být potřeba nastavit proměnnou prostředí `HTTP_PROXY` na `http://127.0.0.1:8888` pro směrování provozu NuGet přes Fiddler.

Pokud se to nepovede, zkuste [tipy zmíněné v tomto příspěvku StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Správa účtů NuGet.org

### <a name="how-to-recover-nugetorg-password-login"></a>Jak obnovit přihlášení k NuGet.org hesla?

Všimněte si, že [přihlášení k heslu NuGet.org bylo ukončeno](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) a jediným způsobem, jak se přihlásit k NuGet.org, je účet osobní účet Microsoft (MSA) nebo Azure Active Directory (AAD). Pokud ale nemůžete získat přístup k přidruženým účtům MSA/AAD, možná budete muset pro obnovu účtu NuGet.org použít přihlášení k heslu. V takovém případě postupujte podle následujících kroků.
- **Požadavek:** Budete potřebovat přístup k e-mailu, který je přidružený k účtu, pro který potřebujete heslo obnovit.
- Přejít na [stránku zapomenuté heslo](https://www.nuget.org/account/ForgotPassword)
- Zadejte **e-mailovou** adresu, která je přidružená k účtu NuGet.org, který chcete obnovit.
- Klikněte na tlačítko **Odeslat** .
- Dostanete e-mail na zadaný účet e-mailové adresy s odkazem na resetování hesla. Klikněte na tento odkaz a nastavte nové heslo. Pokud nemůžete najít e-mail, vraťte se do složky Nevyžádaná pošta.
- Po dokončení se teď můžete přihlásit pomocí uživatelského jména a hesla na NuGet.
- Pokud se chcete přihlásit pomocí uživatelského jména a hesla, použijte odkaz **přihlašovat pomocí účtu NuGet.org** na [přihlašovací stránce NuGet.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Který účet Microsoft je propojený s účtem NuGet.org?

Pokud jste zapomněli, která účet Microsoft je přidružená k vašemu účtu NuGet.org, použijte následující postup, abyste získali pomoc.
1. Přejít na [přihlašovací stránku NuGet.org](https://www.nuget.org/users/account/LogOn) a kliknout na **potřebujete pomoc s přihlášením?** odkaz.
1. Zobrazí se automaticky otevírané okno s žádostí o pomoc. Postupujte podle kroků v tomto dialogovém okně, abyste se seznámili s přidruženými účet Microsoftmi pro svůj účet NuGet.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Jak změnit účet Microsoft používám pro přihlášení NuGet.org?
Pokud chcete změnit účet Microsoft pro uživatele NuGet.org, postupujte podle následujících kroků. Umožňuje vyslovit účet Microsoft s e-mailem `account1@outlook.com` je přidružen k vašemu účtu NuGet.org s uživatelským jménem `MyNuGetAccount`. Chcete změnit přihlašovací údaje k jinému účet Microsoft e-mailem `account2@outlook.com`
1. Po kliknutí na **Přihlásit se účtem Microsoft**se prosím přihlaste pomocí **aktuálně přidruženého účet Microsoft** , například `account1@outlook.com` na [přihlašovací stránce](https://www.nuget.org/users/account/LogOn) .
1. Po přihlášení přejdete na stránku [Nastavení účtu](https://www.nuget.org/account) .
1. Rozbalte část pro **přihlašovací účet**. Klikněte na tlačítko **změnit účet** .
1. Teď budete přesměrováni na přihlašovací stránku Microsoftu. Přihlaste se prosím pomocí účtu, pro který chcete změnit přidružení, tj. `account2@outlook.com`. **Poznámka**: možná budete muset kliknout na **Odhlásit se a přihlásit se pomocí jiného účtu** během přihlašování, abyste se mohli přihlásit s jiným účet Microsoft.
1. Pokud se zobrazí chyba níže, přečtěte si téma [účet Microsoft je propojeno s jiným účtem NuGet.org](#microsoft-account-is-linked-with-another-nugetorg-account) , kde najdete další podrobnosti.
    >_Nepovedlo se aktualizovat účet Microsoft pomocí ' Account2 <account2@outlook.com> '. K tomu může dojít, pokud je už propojený s jiným účtem NuGet. Pokud chcete získat další informace, obraťte se na podporu._

1. Po úspěšném přihlášení k druhému účtu budete přesměrováni zpátky na stránku nastavení účtu NuGet.org a teď byste měli vidět novou účet Microsoft přidruženou jako přihlašovací účet. Až se vám bude přihlašovat k NuGet.org, měli byste tento účet použít.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Účet Microsoft je propojen s jiným účtem NuGet.org.

Pokud jste se pokusili změnit přihlašovací údaje Microsoftu a viděli chybu níže:
> _Nepovedlo se aktualizovat účet Microsoft pomocí ' Account2 <account2@outlook.com> '. K tomu může dojít, pokud je už propojený s jiným účtem NuGet. Pokud chcete získat další informace, obraťte se na podporu._

Řekněme, že jste se pokoušeli změnit účet Microsoft přihlašovací jméno z `account1@outlook.com` pro uživatele NuGet.org s uživatelským jménem `MyNuGetAccount1` na jiný účet Microsoft s e-mailovou `account2@outlook.com`. A zobrazí se chyba výše.

**Co výše chyba znamená?**

Znamená to, že existuje jiný účet NuGet.org, který je spojený s účet Microsoft, na kterou se pokoušíte změnit. v předchozím příkladu účet Microsoft s e-mailem `<account2@outlook.com>` je přidružen k jinému účtu NuGet.org s, řekněme, username @no__ t-1.

Přidružené přihlašovací údaje nemůžete změnit na účet Microsoft, která je propojená s jiným účtem NuGet.org.

**Zapomněl jsem jiný účet NuGet.org, jak zjistím, který účet NuGet.org je?**

Přihlaste se k druhé účet Microsoft na [přihlašovací stránce](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "přihlašovací stránka"). Tím se přihlásíte k účtu NuGet.org, který je aktuálně přidružený k druhému účet Microsoft. Pak můžete zobrazit nahrané balíčky a provádět správu účtů na tomto účtu.

**Nezáleží na tomto druhém účtu NuGet.org, chci změnit přihlašovací jméno pro první účet NuGet.org s druhým účet Microsoft. Co mám dělat?**

Pokud si nepřejete, abyste se s druhým účtem NuGet.orgi jisti a stále chcete znovu použít přidružený účet Microsoft s e-mailovou `account2@outlook.com`. 

Přidružení mezi účtem účet Microsoft a NuGet.org můžete uvolnit tak, že odstraníte účet NuGet.org.
1. Použijte postup [odstranění uživatele](#how-to-delete-my-nugetorg-account) pro druhý účet NuGet.org `MyNuGetAccount2`. 
1. Po odstranění tohoto účtu můžete opakovat postup pro [změnu účet Microsoft přihlášení](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Počkejte, I když se tento druhý účet používá. Nechci přijít o tento účet, ale u prvního účtu se změní moje přihlašovací jména svého přidruženého účtu.**

Budete muset vytvořit nebo použít třetí účet Microsoft s e-mailovou `account3@outlook.com`. 
1. Nejdřív byste se měli přihlásit s druhým účet Microsoft `account2@outlook.com` v NuGet.org. Podle výše uvedených kroků změňte přidružená přihlášení a přidružte třetí účet Microsoft k tomuto účtu NuGet.org.
1. Až to bude hotové, vaše druhá účet Microsoft s e-mailovou `account2@outlook.com` je zdarma přidružit k vašemu prvnímu účtu NuGet.org, `MyNuGetAccount1`. Pomocí výše uvedených kroků změňte přihlašovací údaje Microsoftu na druhý účet Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Přihlášení pomocí účet Microsoft zobrazuje můj e-mail propojený s jiným účet Microsoft

Pokud jste se pokusili přihlásit pomocí účet Microsoft, například pomocí e-mailu `account1@outlook.com` a zobrazí se chyba podobná této:
> _Účet s e-mailem account1@outlook.com je propojený s jiným účtem Microsoft._
>
> _Pokud chcete aktualizovat propojený účet Microsoft můžete to provést ze stránky nastavení účtu._

**Co výše chyba znamená?**

Při vytvoření účtu v NuGet.org je k tomuto účtu přidružena e-mailová adresa pro komunikaci. To je obvykle stejné jako e-mailová adresa, která se používá pro přidruženou účet Microsoft. Můžete ale zvolit, že chcete zadat jinou e-mailovou adresu pro komunikaci. To znamená, že můžete mít různé účet Microsoft, například `account2@outlook.com`, který je propojený s účtem NuGet.org s e-mailovou adresou pro komunikaci jako `account1@outlook.com`.

Takže výše uvedená chyba znamená, že už existuje účet NuGet.org s e-mailovou adresou pro komunikaci `account1@outlook.com`, ale je přidružený k jinému účet Microsoft s e-mailem **, který** není `account1@outlook.com`.

**Návody zjistit, které účet Microsoft je propojeno s tímto účtem NuGet.org?**

K zjištění, které účet Microsoft jsou propojeny s účtem NuGet.org s e-mailovou adresou `account1@outlook.com`, byste měli použít postup pro [pomoc s přihlašováním](#which-microsoft-account-is-linked-to-my-nugetorg-account) .

**Chci tento účet přepsat pomocí mých účet Microsoft**

Postupujte podle kroků v části [nelze použít přihlášení Microsoft, jak obnovit svůj NuGet.org účet](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) a přidružit k vašemu účet Microsoft existujícímu účtu NuGet.org.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Nemůžete použít přihlašovací údaje Microsoftu, jak obnovím svůj účet NuGet.org?

Pokud jste se pokusili použít [pomoc při přihlašování](#which-microsoft-account-is-linked-to-my-nugetorg-account) a nemáte přístup k účet Microsoft, která je přidružená k vašemu účtu NuGet.org, postupujte podle následujících kroků, abyste provedli propojení nového účet Microsoft s účtem NuGet.org.
1. **Požadavek**: budete potřebovat přístup k účet Microsoft, která není přidružena k žádnému existujícímu účtu NuGet.org. Pokud žádný nemáte, můžete si ho [vytvořit](https://signup.live.com) .
2. Pokud jste zapomněli své uživatelské jméno a heslo pro svůj účet NuGet.org, postupujte podle [pokynů pro obnovení přihlašovacích údajů k heslu](#how-to-recover-nugetorg-password-login).
3. [Přihlaste se k NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) pomocí přihlášení uživatelského jména a hesla.
4. Po přihlášení se zobrazí dialogové okno se zobrazí, jak je uvedeno níže. Toto je dialogové okno pro odpokračování hesla.
5. **Poznámka**: ponechejte prosím pokyn pro přihlášení se zadaným účet Microsoft. Svůj účet NuGet.org teď můžete propojit s ostatními přihlašovacími údaji Microsoftu.
6. Klikněte na tlačítko **Přihlásit se účtem Microsoft** a přihlaste se k účet Microsoft, ke kterému máte přístup, jak je uvedeno v kroku 1.
7. Váš účet bude teď propojený s novým účet Microsoft, který můžete použít k přihlášení do NuGet.org.

    ![Dialog MSA propojení](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Jak transformovat svůj účet NuGet.org na organizaci?

Pokud chcete účet transformovat na organizaci a tento účet už je přidružený k účet Microsoft přihlašování, postupujte prosím podle kroků uvedených v dokumentaci pro [organizace v rámci nástroje NuGet org](organizations-on-nuget-org.md).

Pokud ale účet NuGet.org není přidružený/propojený s účet Microsoft, můžete pomocí následujících kroků tento účet transformovat na organizaci.
1. **Požadavek**: Nejdřív musíte mít vytvořený jednotlivý účet na NuGet.org, který se použije jako správce účtu org. Pokud ho ještě nemáte, [vytvořte prosím nový účet NuGet.org](individual-accounts.md) .
2. Pokud pro něj nepoužíváte přihlášení k heslu, postupujte podle [pokynů pro obnovení hesla](#how-to-recover-nugetorg-password-login) k vašemu účtu NuGet.org. Pokud to uděláte, přeskočte tento krok.
3. [Přihlaste se k NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) pomocí přihlášení uživatelského jména a hesla.
4. Po přihlášení se zobrazí dialogové okno se zobrazí, jak je uvedeno níže. Toto je dialogové okno pro odpokračování hesla. 
    > [!Important]
    > Toto dialogové okno ignorujte **tak, že** nekliknete na tlačítko **Přihlásit se přes Microsoft** .

5. Přejít na [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). To vám umožní převést účet NuGet.org na org bez propojení účet Microsoft.
6. Zadejte uživatelské jméno správce pro svůj účet osobní NuGet.org nebo účet, který jste vytvořili v kroku 1.
7. Dokončete transformaci tohoto účtu na organizaci podle pokynů.

    ![Dialog MSA propojení](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>NuGet.org se problémy s přihlášením pro účty AAD s nespravovaným tenantem?

Pokud se během procesu přihlašování v doméně e-mailového účtu (@yourdomain.com) zobrazí chyba, podívejte se na následující postup a obnovte si účet NuGet.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Co je tento nespravovaný stav věc během přihlášení? A proč k této situaci dochází nyní?** 

Zdá se, že váš účet se dřív zaregistroval jako osobní účet Microsoft a pracoval správně, ale zdá se, že váš účet byl zaregistrován jako "nespravovaný" tenant v Azure Active Directory (služba identity, kterou používáme k ověřování Účty Microsoft). 

K tomuto problému může dojít, pokud jste vy nebo někdo z vaší organizace (s e-mailovou adresou @yourdomain.com) zaregistrovali jednu z integrovaných služeb AAD nebo [pro Azure Active Directory použili samoobslužnou registraci](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), která pro službu vytvořila takového nespravovaného tenanta. v případě použití účet Microsoft domény (@yourdomain.com). 

**Co můžu udělat k obnovení svého účtu?**

V současné době neexistuje způsob, jak US (NuGet.org) ověřovat účty s takovými nespravovanými klientskými účty v Azure Active Directory. Těšíme se na lepší způsob, jak tyto účty ověřit.

Pokud se chcete přihlásit k NuGet.org pomocí účet Microsoft (@yourdomain.com), budete vy (nebo správce vaší společnosti) muset vyžádat vlastnictví AAD tím, že provedete ověření DNS pro ověřování uživatelů pomocí e-mailové adresy @yourdomain.com. Postupujte prosím podle kroků pro [převzetí správce domén](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) zdokumentované službou Azure Active Directory. Až to uděláte, vaše normální přihlášení by mělo začít pracovat.

**Nechci všechno udělat, jaký je druhý způsob, jak obnovit svůj účet?**

Můžete [vytvořit](https://www.microsoft.com/en-us/account) nový účet Microsoft (s e-mailem, který **není** přidružený k @yourdomain.com). Postupujte podle kroků uvedených v části [obnovení účtu NuGet.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) .

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Návody změnit uživatelské jméno účtu NuGet.org?

Nemůžete. V rámci zásad neumožňujeme ještě měnit uživatelská jména. Jediným způsobem, jak změnit uživatelské jméno, je vytvořit nový účet s požadovaným uživatelským jménem. Před vytvořením nového účtu doporučujeme odstranit stávající účet, jinak nebudete moci znovu použít své registrované účet Microsoft.
> [!Important]
> Odstraněním uživatele se pořád **rezervuje** `username`. Stejné uživatelské jméno nebude možné znovu znovu použít a **to zahrnuje změnu malých a velkých písmen**. Příklad: Pokud jste vytvořili uživatele s uživatelským jménem `mycoolname` a chcete ho změnit na `MyCoolName` (změny velikosti písmen), po odstranění uživatele nebude možné.

Postupujte podle kroků uvedených v části [odstranění účtu NuGet.org](#how-to-delete-my-nugetorg-account) a [Zaregistrujte nový účet](individual-accounts.md) se správným uživatelským jménem.

### <a name="how-to-delete-my-nugetorg-account"></a>Jak odstranit svůj účet NuGet.org?

Pokud chcete odstranit svůj účet, doporučujeme, abyste přenesli vlastnictví všech balíčků, ve kterých jste jediným vlastníkem. Další informace o tom, jak to udělat, najdete v článku o [správě vlastníků balíčků](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) . Pomůže vám to také při urychlení vaší žádosti.

Pokud chcete účet transformovat na organizaci, postupujte podle kroků uvedených v části [transformace účtu NuGet.org na organizaci](#how-to-transform-my-nugetorg-account-to-an-organization).

> [!Important]
> Odstranění uživatele bude mít za následek následující:
>  1. Vaše uživatelské jméno bude rezervované a nikdo ho nebude moct znovu použít k vytvoření jednotlivého účtu nebo účtu organizace.
>  1. Odvolat přidružené klíče (y) rozhraní API. 
>  1. Odeberte účet jako vlastníka všech podřízených balíčků.
>  1. Zrušte přidružení všech dříve stávajících IDENTIFIKÁTORů předpon předpony k tomuto účtu.
>  1. Odeberte účet jako člena všech organizací.

Pokud chcete pokračovat v odstraňování účtů, postupujte podle následujících kroků.
1. [Přihlaste se k NuGet.org](https://www.nuget.org/users/account/LogOn) pomocí účtu, který chcete odstranit.
2. Klikněte na tuto adresu URL: [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) a podle pokynů odešlete žádost o odstranění účtu.

Naše zákaznická podpora zpracuje tuto žádost a provede odstranění účtu.
