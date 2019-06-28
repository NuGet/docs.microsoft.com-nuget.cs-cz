---
title: Nejčastější dotazy NuGet.org
description: Běžné otázky a odpovědi pro práci v galerii NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c2fc11c0f5dd5d98c40c8b97f9d5a72c4a334b79
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427602"
---
# <a name="nugetorg-frequently-asked-questions"></a>Nejčastější dotazy NuGet.org

## <a name="license-terms"></a>Licenční podmínky

**Co jsou výchozí licenční podmínky Pokud balíček neobsahuje konkrétní informace o licencích?**

Každý balíček se řídí podmínkami, které jsou součástí balíčku. Přečtěte si před přístupem k, stahování nebo získání všechny balíčky, které příslušné podmínky. Na nuget.org, použijte **informace o licenci** odkaz na stránce balíček.

Pokud balíček neurčuje licenční podmínky, obraťte se přímo pomocí vlastníka balíčku **obraťte se na vlastníky** odkazu na stránce balíček pro nuget.org. Společnost Microsoft není licence duševního vlastnictví, od poskytovatelů třetích stran balíček a neodpovídá za informace, které jsou poskytovány třetími stranami.

## <a name="managing-packages-on-nugetorg"></a>Správa balíčků na NuGet.org

**Můžete upravit po je nahraná metadata balíčků?**

NuGet doporučuje podepsat všechny balíčky. Princip návrhu podpisu balíčku je, že je podepsaný balíček obsahu neměnný, což zahrnuje soubor nuspec. Úpravy metadat balíčku výsledkem změny do souboru nuspec, proto už není platná existující podpisy. Doporučujeme, abyste úpravy stávajících pracovních postupů, aby nebyl vyžadován upravovat metadata balíčku po vytvoření balíčku.

Všimněte si, že závislostí uvedených pro váš balíček se generují automaticky z balíčku samotného a nelze jej upravit.

Kromě toho nahrání balíčků [int.nugettest.org](https://int.nugettest.org) je skvělý způsob, jak otestovat a ověřit váš balíček přitom balíček k dispozici ve veřejné galerii. Koncový bod rozhraní API: https://apiint.nugettest.org/v3/index.json

**Můžete odstranit balíček publikovány na NuGet.org?**

Odstranění balíčku publikují do NuGet.org obecně nepodporujeme. Další informace o našich [zásady týkající se odstraněním balíčků](policies/deleting-packages.md).

**Je možné rezervovat názvy balíčků, které se publikují v budoucnosti?**

Ano. ID můžete vyhradit pro balíčky na [nuget.org](https://www.nuget.org/) vyžádáním předponu ID balíčku pro váš účet. Aby bylo možné požádat o předponu ID balíčku, postupujte podle pokynů [dokumentaci](id-prefix-reservation.md).

**Jak uplatním nárok na vlastnictví pro balíčky?**

Zobrazit [vlastníky Správa balíčků na nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Jak zacházet s vlastníka balíčku, který porušuje licence na software**

Doporučujeme komunity NuGet spolupráce řešení všech sporů, které mohou vzniknout mezi vlastníky balíčku a vlastníci dalšího softwaru. Jsme vytvořený [spor proces překladu](policies/dispute-resolution.md) dodržovat před položením správcům nuget.org intercede.

**Je doporučeno uložit Moje testovací balíčky nuget.org?**

Pro účely testování můžete použít [int.nugettest.org](https://int.nugettest.org), nebo jako alternativní veřejné servery NuGet [webu myget.org](https://myget.org) nebo [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Všimněte si, že nemusí být zachována balíčky nahráli do int.nugettest.org.

**Jaká je maximální velikost balíčky, které můžu nahrát do nuget.org?**

nuget.org umožňuje balíčky až 250MB, ale My doporučujeme udržování balíčky v části 1MB. Pokud je to možné a používání závislosti, které balíčky se propojují. Balíčky jako říci, obsahovat pouze jedno sestavení pro zabránění kolizím.

Stáhnout balíčky, takže větší balíčky mají vyšší pravděpodobnost selhání instalace, než menších NuGet pomocí protokolu HTTP.

Je možné sdílet závislosti mezi více balíčků zmenšit celková stahovaná velikost spotřebitelé vaše balíčky NuGet.

Závislosti jsou většinou statická a nikdy změnit. Pokud opravujete chybu v kódu, závislosti nemusí aktualizovat. Pokud seskupíte závislosti, skončíte reshipping pokaždé, když větší balíčky. Rozdělením balíčky NuGet na související závislosti jsou mnohem podrobnějšího pro spotřebitele balíčku upgradu.

## <a name="nugetorg-not-accessible"></a>není k dispozici nuget.org

**Proč nejde stáhnout balíčky z nebo nahrání balíčků na nuget.org?**

Nejprve ujistěte se, že používáte nejnovější verze nugetu. Pokud tuto verzi ani potom nedaří, [obraťte se na podporu](https://www.nuget.org/policies/Contact) a poskytují další připojení, řešení potíží s informací, včetně:

- Verze balíčku nuget, které používáte
- Zdroje balíčků, které používáte
- Obnovení protokolu s podrobnou úroveň podrobností
- MTR nebo trasování Fiddler (viz níže)
- Zeměpisné oblasti
- Určuje, zda váš počítač není za proxy nebo brány firewall?
- Je váš počítač umístěný v datovém centru poskytovatelů cloudu (Azure, AWS atd.)? Pokud ano, zadejte prosím název poskytovatele a oblast.

*K zachycení MTR:*

- Stáhněte si WinMTR z [http://winmtr.net/download/](http://winmtr.net/)
- Zadejte `api.nuget.org` jako název hostitele a klikněte na **Start**.
- Počkejte, dokud **odeslané** je sloupec > = 100.

    ![Zachytávání MTR](media/mtr.png)

- Zkopírování textu do schránky.

*K zachycení Fiddleru:*

- Nainstalujte nejnovější verzi [Fiddler](http://www.telerik.com/download/fiddler).
- Spusťte aplikaci Fiddler a zakázat zachytávání provozu pomocí **soubor > Capture Traffic** nabídky.
- Odebrat všechny relace (vybrat všechny položky v seznamu, stiskněte **odstranit** klíč).
- Konfigurace aplikace Fiddler k zachycení přenosy HTTPS tak, že zkontrolujete **přenosy HTTPS dešifrovat** v **HTTPS** karty **nástroje > Možnosti Fiddleru...**  nabídky.
- Zavřete Visual Studio.
- Povolit **soubor > Capture Traffic** nabídky.
- Spusťte Visual Studio nebo nuget.exe .exe a provádět akce, které nefungují. Přenosy generované tyto akce by měla objevoval ve Fiddleru.
- Po spuštění akce, které mají používat **soubor > Uložit > všechny relace** k uložení zaznamenané relace.

Poznámka: to může být nutné nastavit `HTTP_PROXY` proměnnou prostředí, aby `http://127.0.0.1:8888` za směrování přenosů NuGet pomocí Fiddleru.

Pokud se to nepodaří, zkuste [tipy uvedených v tomto příspěvku na StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Správa účtů nuget.org

### <a name="how-to-recover-nugetorg-password-login"></a>Jak obnovit heslo přihlášení nuget.org?

Pamatujte, že [nebyly vyřazeny nuget.org heslu](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) a jediný způsob, jak se přihlásit do nuget.org se pomocí osobního účtu Microsoft (MSA) nebo účet Azure Active Directory (AAD). Ale v případě, že nelze získat přístup k vaší přidružené účty MSA nebo AAD můžete potřebovat pro použití přihlášení k heslo pro obnovení účtu nuget.org. V takovém případě postupujte podle následujících kroků.
- **Požadavek:** Musíte mít přístup k e-mailu, který je přidružen k účtu, pro kterou je potřeba obnovit heslo.
- Přejděte [stránka zapomenuté heslo](https://www.nuget.org/account/ForgotPassword)
- Zadejte **e-mailu** adresu, která je přidružená k účtu nuget.org, které chcete obnovit.
- Klikněte na tlačítko **odeslat** tlačítko.
- Zobrazí se e-mailu pro účet zadané e-mailové adresy se odkaz na resetování hesla. Klikněte na tento odkaz a nastavte nové heslo. Pokud nemůžete najít e-mailu Zkontrolujte složku s "nevyžádanou poštou".
- Až budete hotovi, můžete teď přihlásit se pomocí uživatelského jména a hesla na webu NuGet.
- Chcete-li se přihlásit pomocí uživatelského jména a hesla, použijte **přihlaste pomocí účtu Nuget.org** odkaz na [nuget.org přihlašovací stránku](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Který účet Microsoft je propojený s účtem Moje nuget.org?

Pokud jste zapomněli účtu Microsoft, který je přidružen k vašemu účtu nuget.org, postupujte podle kroků níže a vyžádejte si pomoc.
1. Přejděte na [nuget.org přihlašovací stránku](https://www.nuget.org/users/account/LogOn) a klikněte na **potřebujete pomoc s přihlášením?** odkaz.
1. To se seznámíte místním dialogovém žádostí o pomoc. Postupujte podle kroků v tomto dialogovém pochopit přidružené účty Microsoft pro váš účet nuget.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Jak změnit účet Microsoft, které používám pro přihlášení nuget.org?
Pokud chcete změnit účet Microsoft pro uživatele nuget.org, použijte následující postup. Umožňuje Dejme tomu, že váš účet Microsoft s e-mailem `account1@outlook.com` souvisí s vaším účtem nuget.org s uživatelským jménem `MyNuGetAccount`. Chcete změnit přihlášení do jiného účtu Microsoft s e-mailem `account2@outlook.com`
1. Přihlaste se prosím pomocí **aktuálně přiřazen účet Microsoft** tedy `account1@outlook.com` na [přihlašovací stránku](https://www.nuget.org/users/account/LogOn) po kliknutí na tlačítko **přihlásit se účtem Microsoft**.
1. Po přihlášení, přejděte k vaší [nastavení účtu](https://www.nuget.org/account) stránky.
1. Rozbalte v části **přihlašovací účet**. Klikněte na **změnit účet** tlačítko.
1. Nyní budou přesměrováni na přihlašovací stránku Microsoftu. Přihlaste se prosím pomocí účtu, který chcete změnit přidružení tedy `account2@outlook.com`. **Poznámka:** : možná budete muset kliknout na **přihlásit na více instancí a přihlaste se pomocí jiného účtu** během tok pro přihlašování k nebudou moct přihlásit s jiným účtem Microsoft.
1. Pokud se zobrazí chyba podobná níže uvedenému příkladu naleznete v tématu [účet Microsoft je propojený s jiným účtem nuget.org](#microsoft-account-is-linked-with-another-nugetorg-account) další podrobnosti.
    >_Nepovedlo se aktualizovat účet Microsoft s "obchodní vztah 2 <account2@outlook.com>". K tomu může dojít, pokud je už propojený s jiným účtem NuGet. Další informace, obraťte se na podporu._

1. Až se úspěšně se pomocí svého druhého účtu, budete přesměrováni zpět na stránku nastavení účtu nuget.org a měli byste vidět nový účet Microsoft spojený jako přihlašovací účet. Do budoucna můžete používejte tento účet při přihlašování do nuget.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Účet Microsoft je propojený s jiným účtem nuget.org.

Pokud se při změně vaše přihlašovací údaje Microsoft viděli následující chyba:
> _Nepovedlo se aktualizovat účet Microsoft s "obchodní vztah 2 <account2@outlook.com>". K tomu může dojít, pokud je už propojený s jiným účtem NuGet. Další informace, obraťte se na podporu._

Dejme tomu, že jste se pokoušeli změnit Microsoft vám umožňuje účtu přihlášení z `account1@outlook.com` nuget.org uživatele s uživatelským jménem `MyNuGetAccount1` do jiného účtu Microsoft s e-mailem `account2@outlook.com`. A zobrazí výše uvedenou chybu.

**Co znamená výše uvedenou chybu?**

Znamená to, že je jiný účet nuget.org, který je přidružen k účtu Microsoft, že se pokoušíte změnit tak, tedy v nad příklad účet Microsoft s e-mailu `<account2@outlook.com>` je spojen s jiným účtem nuget.org se například uživatelské jméno `MyNuGetAccount2`.

Nelze změnit přidružený přihlášení pomocí účtu Microsoft, který je propojený s účtem různé nuget.org.

**Nemohu si vzpomenout, že jsem měl jiný účet nuget.org, jak zjistím účtu nuget.org, který se jedná?**

Přihlaste se pomocí druhého účtu Microsoft na [přihlašovací stránku](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "přihlašovací stránku"). To se můžete přihlásit na nuget.org účet, který je teď přidružená druhého účtu Microsoft. Pak můžete zobrazit nahrané balíčků a provádět správu účtu na tento účet.

**Můžu nezáleží na tento druhý účet nuget.org, chci změnit přihlašovací údaje pro první účet nuget.org pomocí druhého účtu Microsoft. Co mám dělat?**

Pokud budete chtít není záleží druhého účtu nuget.org a stále chcete znovu použít přidružený účet Microsoft s e-mailem `account2@outlook.com`. 

Přidružení účtu Microsoft a nuget.org účtu můžete uvolnit tak, že odstraníte účet nuget.org.
1. Uvedený postup [odstranit uživatele](#how-to-delete-my-nugetorg-account) druhého účtu nuget.org `MyNuGetAccount2`. 
1. Jakmile tento účet je odstraněn, můžete opakovat postup [změnit přihlášení k účtu Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Počkejte, nezajímá tento druhý účet příliš. Můžu nechcete přijít o tento účet ale změnit Moje přihlašovací jména k souvisejícím účtům pro první účet.**

Budete muset vytvořit/použít jiného účtu Microsoft, například s e-mailem `account3@outlook.com`. 
1. Nejdřív byste se měli přihlásit se pomocí svého druhého účtu Microsoft, `account2@outlook.com` na nuget.org. Postupujte podle výše uvedené kroky a změnit přidružené přihlašovací údaje a přidružit třetí účet Microsoft s tímto účtem nuget.org.
1. Až to bude hotové, druhý účtu Microsoft s e-mailem `account2@outlook.com` je zdarma chcete přidružit k účtu první nuget.org `MyNuGetAccount1`. Postupujte podle stejných kroků výše, chcete-li změnit přihlašovací údaje microsoft druhého účtu Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Přihlášení pomocí účtu Microsoft ukáže se, že synchronizuji si e-maily z je propojená s jiným účtem Microsoft

Pokud jste se pokusili přihlaste pomocí svého účtu Microsoft, například s e-mailem `account1@outlook.com` a zobrazit chyba podobná níže uvedenému příkladu:
> _Účet s e-mailu "account1@outlook.com" je propojený s jiným účtem microsoft._
>
> _Pokud chcete aktualizovat propojeným účtem Microsoft, že můžete tak učinit na stránce nastavení účtu._

**Co znamená výše uvedenou chybu?**

Při vytvoření účtu na nuget.org je přidružený k tomuto účtu komunikace e-mailovou adresu. To je obvykle stejné jako e-mailovou adresu, která slouží k souvisejícímu účtu Microsoft. Ale můžete se rozhodnout zadejte jinou e-mailovou adresu pro komunikaci. Proto technicky vzato můžete mít různé Microsoft account, Řekněme, že se `account2@outlook.com` , který je propojený s účtem nuget.org s komunikace e-mailovou adresu jako `account1@outlook.com`.

Takže výše uvedená chyba znamená, že už existuje účet nuget.org komunikace e-mailovou adresou `account1@outlook.com` je spojen s jiným účtem Microsoft s e-mailem, ale **, který není** `account1@outlook.com`.

**Jak zjistím, které společnost Microsoft k tomuto účtu nuget.org je propojený účet?**

Měli byste použít [přihlášení potřebujete pomoc](#which-microsoft-account-is-linked-to-my-nugetorg-account) toku můžete zjistit, který účet Microsoft je propojený s účtem nuget.org s e-mailovou adresu `account1@outlook.com`.

**Chcete přepsat tento účet pomocí účtu Microsoft**

Postupujte podle kroků v [nelze pro použití přihlášení k Microsoftu, jak obnovit svůj účet nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) části postupu přidružte svůj účet Microsoft s existujícím účtem nuget.org.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Nelze pro použití přihlášení k Microsoftu, jak obnovit svůj účet nuget.org?

Pokud jste se pokusili pomocí [přihlášení pomoc](#which-microsoft-account-is-linked-to-my-nugetorg-account) a nemáte přístup k účtu Microsoft, který je spojen s vaším účtem nuget.org, postupujte podle následujících kroků, abyste propojit nový účet Microsoft se svým účtem nuget.org.
1. **Požadavek**: Budete potřebovat přístup k účtu Microsoft, který není spojen s některé existující účty nuget.org. Pokud nemáte, můžete si [vytvořit](https://signup.live.com) jeden.
2. Pokud jste zapomněli svoje uživatelské jméno a heslo pro váš účet nuget.org, postupujte [postupů k obnovení vašeho hesla přihlášení](#how-to-recover-nugetorg-password-login).
3. [Přihlaste se k nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) pomocí přihlášení uživatelského jména a hesla.
4. Po přihlášení, zobrazí se dialogové okno automaticky otevírané okno zobrazit až podobná níže uvedenému příkladu. Toto je dialogové okno heslo přerušení.
5. **POZNÁMKA:** : Ignorujte podle pokynů k přihlášení pomocí zadaného účtu Microsoft. Teď můžete propojit účet nuget.org pro další přihlášení společnosti Microsoft.
6. Klikněte na tlačítko **přihlásit se účtem Microsoft** a přihlaste se pomocí účtu Microsoft, že máte přístup do, jak je uvedeno v kroku 1.
7. Váš účet bude nyní propojen nový účet Microsoft, který můžete použít k přihlášení do nuget.org do budoucna.

    ![Dialogové okno MSA odkaz](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Jak transformovat nuget.org účet organizace?

Pokud chcete transformovat váš účet organizace, a tento účet je již přidružen přihlašovací údaje účtu Microsoft, postupujte podle kroků uvedených v dokumentaci k [organizace v organizaci nuget](organizations-on-nuget-org.md).

Pokud však nuget.org účtu není přidružené nebo propojených s účtem Microsoft, můžete podle následujících pokynů pro transformaci tento účet organizace.
1. **Požadavek**: Musíte mít samostatný účet prvním vytvoření na nuget.org se použije jako správce účtu organizace. Pokud nemáte, [vytvořit nový účet nuget.org](individual-accounts.md)
2. Postupujte podle [postupů k obnovení vašeho hesla přihlášení](#how-to-recover-nugetorg-password-login) pro váš účet nuget.org, pokud nemáte přihlašovací heslo pro něj, pokud, tento krok přeskočit.
3. [Přihlaste se k nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) pomocí přihlášení uživatelského jména a hesla.
4. Po přihlášení, zobrazí se dialogové okno automaticky otevírané okno zobrazit až podobná níže uvedenému příkladu. Toto je dialogové okno heslo přerušení. 
    > [!Important]
    > Ignorovat toto dialogové **nejsou** klikněte na **přihlásit se účtem microsoft** tlačítko.

5. Přejděte do [ (Nastavení)https://www.nuget.org/account/transform](https://www.nuget.org/account/transform) (Integrace a služby). To vám umožní převést účet nuget.org organizací bez propojení s účtem Microsoft.
6. Zadejte uživatelské jméno správce pro váš účet osobní nuget.org/účet, který jste vytvořili v kroku 1.
7. Postupujte podle pokynů k dokončení transformace tento účet organizace.

    ![Dialogové okno MSA odkaz](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>pro účty AAD pomocí nespravovaného tenanta vydá nuget.org přihlášení?

Pokud se zobrazí chyba typu pod během přihlášení tok s vaši e-mailovou doménu účtu (@yourdomain.com), najdete v článku kroků k obnovení vašeho účtu nuget.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Co je tuto věc nespravovaném stavu během přihlašování? A proč se to děje nyní?** 

Váš účet zdá se, že dříve zaregistrován jako osobní účet Microsoft a fungovaly správně, ale teď to vypadá jako váš účet zaregistrovaný jako tenanta služby "Nespravovaného" ve službě Azure Active Directory (identity službu, která používáme k ověření Účet Microsoft). 

To by mohlo dojít, pokud vy nebo někdo z vaší organizace (s @yourdomain.com e-mailová adresa) zaregistrovaný jedním ze služby AAD integrované nebo nebyla [Samoobslužná registrace do služby Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), například vytváří " Nespravované"tenanta pro doménu používá účet Microsoft (@yourdomain.com ve vašem případě). 

**Co mám dělat obnovit svůj účet?**

V tuto chvíli není pro nás (nuget.org) způsob ověřování účtů pomocí takové "Nespravovaného" tenanta účty ve službě Azure Active directory. Chceme lepší způsob, jak ověřovat tyto účty.

Pokud chcete k přihlášení do nuget.org se svým účtem Microsoft (@yourdomain.com), můžete (nebo správcem ve vaší společnosti) bude muset nárokovat vlastnictví AAD provedením ověření DNS k ověřování uživatelů pomocí e-mailovou adresu "@yourdomain.com". Postupujte podle kroků pro [převzetí správce domény](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) zdokumentované v Azure Active directory. Až to uděláte, běžné přihlašovací měly začít fungovat.

**Nechci se nyní udělat všem, co je další způsob, jak obnovit svůj účet?**

Je možné [vytvořit](https://www.microsoft.com/en-us/account) nový účet Microsoft (s e-mailu **není** přidružené @yourdomain.com). Postupujte podle kroků uvedených v [obnovení vašeho účtu nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) oddílu.

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Změna Moje uživatelské jméno účtu nuget.org

Nemůžete. Jak zásady jsme neumožňuje změnu ještě v úložišti uživatelských jmen. Chcete-li vytvořit nový účet s požadované uživatelské jméno je jediný způsob, jak změnit svoje uživatelské jméno. Doporučujeme vám odstranit stávajícího účtu před vytvořením nového, v opačném případě nebude možné opakovaně používat zaregistrovaným účtem Microsoft.
> [!Important]
> Odstraňuje se uživatel bude stále **rezervovat** `username`. Nebude moct znovu použít stejné uživatelské jméno a **jedná se o změnu písmen**. Jako příklad: Pokud jste vytvořili uživatele s uživatelským jménem `mycoolname` a vy chcete změnit tuto hodnotu na `MyCoolName`(změny se velká a malá písmena), nebude možné po odstranění uživatele.

Postupujte podle kroků uvedených v [odstranění účtu nuget.org](#how-to-delete-my-nugetorg-account) oddílu a [zaregistrovat nový účet](individual-accounts.md) s správné uživatelské jméno.

### <a name="how-to-delete-my-nugetorg-account"></a>Jak odstraním svůj účet nuget.org?

Chcete-li odstranit svůj účet, mějte prosím na paměti, že vám doporučujeme převést vlastnictví všechny balíčky, kde jste jediným vlastníkem. Další informace o [Správa vlastníků balíčku](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) o tom, jak to udělat. To vám také pomůže nám ohledně urychlení jejich zpracování vaší žádosti.

> [!Important]
> Odstraňuje se uživatel bude mít za následek následující:
>  1. Odvolat přidružené klíče rozhraní API. 
>  2. Tento účet odeberte jako vlastníka pro všechny balíčky, které podřízené.
>  3. Zrušit přidružení všechny dříve existující rezervace předpony ID, pomocí tohoto účtu.
>  4. Odeberte účet členem jakékoli organizace.
>  5. Vaše uživatelské jméno se vyhradí a nebude moci znovu jeho použití znovu bez naše oprávnění.

Postupujte podle následujících kroků a pokračujte odstranění účtu.
1. [Přihlaste se k nuget.org](https://www.nuget.org/users/account/LogOn) pomocí účtu, který chcete odstranit.
2. Klikněte na tuto adresu url: [ https://www.nuget.org/account/delete ](https://www.nuget.org/account/delete) a postupujte podle pokynů k odeslání žádosti o odstranění účtu.

Naše Zákaznická podpora bude tento požadavek zpracovat a provést odstranění účtu.
