---
title: NuGet.org často kladené otázky
description: Běžné otázky a odpovědi pro práci s galerií NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428903"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org často kladené otázky

## <a name="license-terms"></a>Licenční podmínky

**Jaké jsou výchozí licenční podmínky, pokud balíček neposkytuje konkrétní licenční informace?**

Každý balíček se řídí podmínkami, které jsou součástí balíčku. Před přístupem, stažením nebo získáním balíčků byste si měli přečíst příslušné podmínky. V NuGet.org použijte odkaz **Informace o licenci** na stránce balíčku.

Pokud balíček nespecifikuje licenční podmínky, obraťte se přímo na vlastníky balíčku pomocí odkazu **Vlastníci kontaktů** na stránce balíčku NuGet.org. Společnost Microsoft vám nelicencuje žádné duševní vlastnictví od poskytovatelů balíčků třetích stran a není odpovědná za informace poskytnuté třetími stranami.

## <a name="managing-packages-on-nugetorg"></a>Správa balíčků na NuGet.org

**Mohu po nahrání upravit metadata balíčku?**

NuGet doporučuje všechny balíčky, které mají být podepsány. Princip návrhu podepisování balíčků je, že podepsaný obsah balíčku musí být neměnný, který zahrnuje nuspec. Úprava metadat balíčku má za následek změny nuspec, zrušení existujících podpisů. Doporučujeme upravit existující pracovní postupy tak, aby po vytvoření balíčku nevyžadovaly úpravy metadat balíčku.

Všimněte si, že závislosti uvedené pro váš balíček jsou generovány automaticky ze samotného balíčku a nelze je upravovat.

Kromě toho nahrávání balíčků do [int.nugettest.org](https://int.nugettest.org) je skvělý způsob, jak otestovat a ověřit balíček bez zpřístupnění balíčku ve veřejné galerii. Koncový bod rozhraní API:https://apiint.nugettest.org/v3/index.json

**Mohu odstranit balíček publikovaný do NuGet.org?**

Obecně nepodporujeme odstranění balíčku publikovaného do NuGet.org. Přečtěte si více o našich [zásadách pro mazání balíčků](policies/deleting-packages.md).

**Je možné rezervovat názvy pro balíčky, které budou zveřejněny v budoucnu?**

Ano. ID pro balíčky v [NuGet.org](https://www.nuget.org/) můžete rezervovat tak, že požádáte o předponu ID balíčku pro váš účet. Chcete-li požádat o předponu ID balíku, postupujte podle pokynů v [dokumentaci](id-prefix-reservation.md).

**Jak mohu požadovat vlastnictví balíčků ?**

Viz [Správa vlastníků balíčků na NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Jak mám jednat s vlastníkem balíčku, který porušuje moji softwarovou licenci?**

Doporučujeme komunitě NuGet spolupracovat na řešení všech sporů, které mohou vzniknout mezi vlastníky balíčků a vlastníky jiného softwaru. Vytvořili jsme [proces řešení sporů,](policies/dispute-resolution.md) který je třeba sledovat, než požádáme NuGet.org administrátory, aby se přimlouvali.

**Doporučujeme nahrát testovací balíčky do NuGet.org?**

Pro účely testování můžete použít [int.nugettest.org](https://int.nugettest.org)nebo alternativní veřejné NuGet servery, jako [je myget.org](https://myget.org) nebo [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Všimněte si, že balíčky nahrané do int.nugettest.org nemusí být zachovány.

**Jaká je maximální velikost balíčků, které mohu nahrát do NuGet.org?**

NuGet.org umožňuje balíčky až 250 MB, ale doporučujeme zachovat balíčky pod 1 MB, pokud je to možné, a pomocí závislostí propojit balíčky dohromady. Jako palec balíčky obsahují pouze jedno sestavení, aby se zabránilo kolizím.

NuGet používá HTTP ke stažení balíčků, takže větší balíčky mají vyšší pravděpodobnost neúspěšných instalací než menší.

Je možné sdílet závislosti mezi více balíčků, takže celková velikost stahování pro spotřebitele balíčků NuGet menší.

Závislosti jsou většinou statické a nikdy se nemění. Při opravě chyby v kódu nemusí být nutné aktualizovat závislosti. Pokud sdružete závislosti, skončíte reshipping větší balíčky pokaždé. Rozdělením balíčků NuGet do souvisejících závislostí jsou upgrady mnohem jemněji odstupňované pro spotřebitele vašeho balíčku.

## <a name="nugetorg-not-accessible"></a>NuGet.org není přístupné

**Proč nemohu stahovat balíčky z balíčků nebo nahrát balíčky do NuGet.org?**

Nejprve se ujistěte, že používáte nejnovější verze NuGet. Pokud tato verze nadále selhat, [obraťte se na podporu](https://www.nuget.org/policies/Contact) a poskytnout další informace o řešení potíží připojení, včetně:

- Verze NuGet, kterou používáte
- Zdroje balíčků, které používáte
- Protokol obnovení s podrobnou podrobností
- MTR nebo Šumař stopy (viz níže)
- Vaše zeměpisná oblast
- Zda je váš počítač za proxy nebo firewallem?
- Je váš počítač umístěný v datovém centru poskytovatelů cloudu (Azure, AWS atd.)? Pokud ano, uveďte prosím jméno poskytovatele a regionu.

*Chcete-li zachytit MTR:*

- Stáhnout [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download).
- Zadejte `api.nuget.org` jako název hostitele a klepněte na tlačítko **Start**.
- Počkejte, až se sloupec **Odesláno** >= 100.

    ![Zachycení mtr](media/mtr.png)

- Zkopírujte text do schránky.

*Chcete-li zachytit Šumař:*

- Nainstalujte nejnovější verzi [Fiddler](https://www.telerik.com/download/fiddler).
- Spusťte Fiddler a zakažte zachytávání provozu pomocí nabídky **Soubor > zachytávání provozu.**
- Odeberte všechny relace (vyberte všechny položky v seznamu, stiskněte klávesu **Delete).**
- Nakonfigurujte Šumař pro zachycení přenosu HTTPS kontrolou **dešifrování https provozu** na kartě **HTTPS** v nabídce Nástroje **> Fiddler.**
- Zavřete Visual Studio.
- Povolte nabídku **Soubor > zachytávání provozu.**
- Spusťte visual studio nebo nuget.exe .exe a proveďte akce, které nefungují. Provoz generovaný těmito akcemi by se měl zobrazit v Fiddleru.
- Po spuštění akcí použijte k uložení zachycených relací **soubor > uložit > všechny relace.**

Poznámka: může být nutné `HTTP_PROXY` nastavit proměnnou prostředí `http://127.0.0.1:8888` pro směrování NuGet přenosy přes Šumař.

Pokud se to nepodaří, zkuste [tipy uvedené v tomto StackOverflow post](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>správa účtu NuGet.org

### <a name="how-to-recover-nugetorg-password-login"></a>Jak obnovit NuGet.org heslo přihlášení?

Upozorňujeme, že [přihlášení NuGet.org hesla bylo ukončeno](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) a jediný způsob, jak se přihlásit k NuGet.org, je pomocí osobního účtu Microsoft (MSA) nebo účtu Azure Active Directory (AAD). V případě, že nemáte přístup k přidruženým účtům MSA/AAD, možná budete muset použít přihlašovací jméno hesla pro obnovení vašeho NuGet.org účtu. V takovém případě postupujte podle následujících kroků.
- **Požadavek:** Budete muset mít přístup k e-mailu, který je spojen s účtem, pro který je třeba obnovit heslo.
- Přejít na [stránku Zapomenuté heslo](https://www.nuget.org/account/ForgotPassword)
- Zadejte **e-mailovou** adresu, která je přidružena k účtu NuGet.org, který chcete obnovit.
- Klepněte na tlačítko **Odeslat.**
- Obdržíte e-mail na zadaný účet e-mailové adresy s odkazem na resetování hesla. Klikněte na tento odkaz a nastavte nové heslo. Pokud nemůžete najít poštu, zkontrolujte složku "nevyžádaná pošta".
- Poté, co udělal, můžete se nyní přihlásit s uživatelským jménem / heslem na NuGet.
- Chcete-li se přihlásit pomocí uživatelského jména/hesla, použijte odkaz **Přihlásit se pomocí Nuget.org účtu** na přihlašovací stránce NuGet.org [.](https://www.nuget.org/users/account/LogOn)

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Který účet Microsoft je propojený s mým NuGet.org účtem?

Pokud jste zapomněli, který účet Microsoft je přidružen k vašemu účtu NuGet.org, požádejte o pomoc následující kroky.
1. Přejděte na [NuGet.org přihlašovací stránku](https://www.nuget.org/users/account/LogOn) a klikněte na **potřebujete pomoc přihlášení?**
1. Zobrazí se vyskakovací dialogové okno pro pomoc. Podle pokynů v tomto dialogovém okně porozumíte přidruženým účtům Microsoft pro váš účet NuGet.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Jak změnit účet Microsoft, který používám pro NuGet.org přihlášení?
Pokud chcete změnit účet Microsoft pro NuGet.org uživatele, postupujte podle následujících kroků. Řekněme, že váš `account1@outlook.com` účet Microsoft s e-mailem je spojen s vaším NuGet.org účtem s uživatelským jménem `MyNuGetAccount`. Chcete změnit přihlašovací údaje na jiný účet Microsoft pomocí e-mailu`account2@outlook.com`
1. Po kliknutí na **přihlásit**se u `account1@outlook.com` společnosti Microsoft se přihlaste pomocí **aktuálně přidruženého účtu Microsoft,** tedy na [přihlašovací stránce.](https://www.nuget.org/users/account/LogOn)
1. Po přihlášení přejděte na stránku [nastavení účtu.](https://www.nuget.org/account)
1. Rozbalte oddíl **pro přihlašovací účet**. Klikněte na tlačítko **Změnit účet.**
1. Nyní budete přesměrováni na přihlašovací stránku společnosti Microsoft. Přihlaste se pomocí účtu, který chcete změnit na `account2@outlook.com`účet, tj. **Poznámka:** Možná budete muset kliknout na **Odhlásit se a přihlásit se pomocí jiného účtu** během přihlašování, abyste se mohli přihlásit pomocí jiného účtu Microsoft.
1. Pokud se vám níže zobrazí chyba, další podrobnosti najdete v [tématu Účet Microsoft je propojený s jiným NuGet.org účtu.](#microsoft-account-is-linked-with-another-nugetorg-account)
    >_Aktualizace účtu Microsoft na účet <account2@outlook.com>'account2 '. K tomu může dojít, pokud je již propojen s jiným účtem NuGet. Další informace získáte od podpory._

1. Po úspěšném přihlášení pomocí druhého účtu budete přesměrováni zpět na stránku nastavení účtu NuGet.org a nyní byste měli vidět nový účet Microsoft přidružený jako přihlašovací účet. Do budoucna byste měli použít tento účet při přihlášení k NuGet.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Účet Microsoft je propojen s jiným NuGet.org účtem.

Pokud jste se pokusili změnit své přihlášení společnosti Microsoft a viděli chybu níže:
> _Aktualizace účtu Microsoft na účet <account2@outlook.com>'account2 '. K tomu může dojít, pokud je již propojen s jiným účtem NuGet. Další informace získáte od podpory._

Řekněme, že jste se pokoušeli `account1@outlook.com` změnit přihlášení k `MyNuGetAccount1` účtu Microsoft pro `account2@outlook.com`NuGet.org uživatele s uživatelským jménem na jiný účet Microsoft s e-mailem . A vidíte chybu výše.

**Co znamená výše uvedená chyba?**

To znamená, že existuje další NuGet.org účet, který je spojen s účtem Microsoft, který se pokoušíte změnit na příklad výše, účet Microsoft s e-mailem `<account2@outlook.com>` je spojen s jiným NuGet.org účtem, řekněme s uživatelským jménem `MyNuGetAccount2`.

Přidružené přihlášení pomocí účtu Microsoft, který je propojený s jiným účtem NuGet.org, nemůžete změnit.

**Zapomněl jsem, že mám jiný účet NuGet.org, jak zjistím, který NuGet.org účet to je?**

Přihlaste se pomocí druhého účtu Microsoft na [přihlašovací stránce](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "přihlašovací stránka"). Tím se přihlásíte k účtu NuGet.org, který je aktuálně přidružen k druhému účtu Microsoft. Poté můžete zobrazit nahrané balíčky a provést správu účtu v tomto účtu.

**Nestarám se o tento druhý NuGet.org účet, chci změnit své přihlašovací jméno pro první NuGet.org účet s druhým účtem Microsoft. Co mám dělat?**

Pokud se nechcete starat o druhý účet NuGet.org a přesto chcete znovu `account2@outlook.com`použít přidružený účet Microsoft s e-mailem . 

Spojení mezi účtem Microsoft a NuGet.org účet můžete uvolnit odstraněním účtu NuGet.org.
1. Podle pokynů [odstraňte uživatele](#how-to-delete-my-nugetorg-account) pro `MyNuGetAccount2`druhý NuGet.org účet . 
1. Po odstranění tohoto účtu můžete zopakovat postup [změny přihlášení k účtu Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Počkej, tendruhý účet mě taky zajímá. Nechci tento účet ztratit, ale změnit své přidružené přihlašovací údaje k účtu pro první účet.**

Budete muset vytvořit / použít třetí účet Microsoft, `account3@outlook.com`řekněme, s e-mailem . 
1. Nejprve byste se měli přihlásit pomocí druhého účtu Microsoft, `account2@outlook.com` na NuGet.org. Podle výše uvedených kroků změňte přidružená přihlášení a přidružte třetí účet Microsoft k tomuto účtu NuGet.org.
1. Po dokončení může být váš `account2@outlook.com` druhý účet Microsoft s e-mailem zdarma spojen s vaším prvním účtem NuGet.org `MyNuGetAccount1`. Chcete-li změnit přihlášení společnosti Microsoft na druhý účet Microsoft, postupujte stejným způsobem výše.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Přihlášení pomocí účtu Microsoft mi ukáže, že můj e-mail je propojený s jiným účtem Microsoft.

Pokud jste se pokusili přihlásit pomocí účtu `account1@outlook.com` Microsoft, řekněme pomocí e-mailu a zobrazí se chyba jako níže:
> _Účet s e-mailem 'account1@outlook.com' je propojen s jiným účtem Microsoft._
>
> _Pokud chcete propojený účet Microsoft aktualizovat, můžete tak učinit na stránce nastavení účtu._

**Co znamená výše uvedená chyba?**

Při vytvoření účtu na NuGet.org je k tomuto účtu přidružena komunikační e-mailová adresa. Obvykle je to stejné jako e-mailová adresa, která se používá pro přidružený účet Microsoft. Můžete však zadat jinou e-mailovou adresu pro komunikaci. Takže technicky byste mohli mít jiný účet `account2@outlook.com` Microsoft, řekněme s tím, `account1@outlook.com`že je propojen s NuGet.org účet s komunikační e-mailovou adresou jako .

Takže výše uvedená chyba znamená, že již `account1@outlook.com` existuje NuGet.org účet s komunikační e-mailovou adresou, ale je spojen s jiným účtem Microsoft s e-mailem, **který není** `account1@outlook.com`.

**Jak zjistím, který účet Microsoft je propojený s tímto NuGet.org účtem?**

Pomocí toku [pomoci při přihlášení](#which-microsoft-account-is-linked-to-my-nugetorg-account) byste měli zjistit, který účet Microsoft `account1@outlook.com`je propojen s účtem NuGet.org s e-mailovou adresou .

**Chci přepsat tento účet pomocí účtu Microsoft**

Postupujte podle pokynů v části [Nelze použít přihlášení k Microsoftu, jak lze obnovit](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) oddíl NuGet.org účtu a přidružit váš účet Microsoft k existujícímu účtu NuGet.org.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Nelze použít přihlášení společnosti Microsoft, jak mohu obnovit svůj účet NuGet.org?

Pokud jste se [pokusili](#which-microsoft-account-is-linked-to-my-nugetorg-account) použít pomoc při přihlášení a nemáte přístup k účtu Microsoft, který je přidružen k vašemu účtu NuGet.org, postupujte podle následujících kroků a propojte nový účet Microsoft se svým účtem NuGet.org.
1. **Požadavek**: Budete potřebovat přístup k účtu Microsoft, který není spojen s žádnými existujícími účty NuGet.org. Pokud ho nemáte, můžete ho [vytvořit.](https://signup.live.com)
2. Pokud jste zapomněli své uživatelské jméno a heslo pro svůj účet NuGet.org, [postupujte podle pokynů k obnovení přihlašovacího jména hesla](#how-to-recover-nugetorg-password-login).
3. [Přihlaste se k NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) pomocí uživatelského jména/ hesla.
4. Po přihlášení se zobrazí vyskakovací dialog jako níže. Toto je dialogové okno pro přerušení platnosti hesla.
5. **Poznámka:** Ignorujte instrukce pro přihlášení pomocí zadaného účtu Microsoft. Nyní můžete svůj účet NuGet.org propojit s jakýmkoli jiným přihlášením společnosti Microsoft.
6. Klikněte na tlačítko **Přihlásit se u Microsoftu** a přihlásit se pomocí účtu Microsoft, ke kterému máte přístup, jak je uvedeno v kroku 1.
7. Váš účet bude nyní propojen s novým účtem Microsoft, který můžete použít k přihlášení k NuGet.org do budoucna.

    ![Dialogové okno Propojení msa](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Jak změnit svůj účet NuGet.org na organizaci?

Pokud chcete svůj účet transformovat na organizaci a tento účet je již přidružen k přihlášení k účtu Microsoft, postupujte podle pokynů uvedených v dokumentaci pro [organizace na nuget org](organizations-on-nuget-org.md).

Pokud však váš účet NuGet.org není přidružený nebo propojený s účtem Microsoft, můžete tento účet transformovat na organizaci podle následujících kroků.
1. **Požadavek**: Musíte mít individuální účet nejprve vytvořen na NuGet.org, které mají být použity jako správce na účtu organizace. Pokud ho nemáte, [vytvořte si nový NuGet.org účet](individual-accounts.md)
2. Postupujte [podle pokynů k obnovení vašeho hesla pro](#how-to-recover-nugetorg-password-login) váš účet NuGet.org, pokud nemáte heslo pro něj, pokud ano, přeskočte tento krok.
3. [Přihlaste se k NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) pomocí uživatelského jména/ hesla.
4. Po přihlášení se zobrazí vyskakovací dialog jako níže. Toto je dialogové okno pro přerušení platnosti hesla. 
    > [!Important]
    > Toto dialogové okno ignorujte, **neklikejte** na tlačítko **Přihlásit se pomocí microsoftu.**

5. Přejděte [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)na . To vám umožní převést účet NuGet.org na organizaci bez propojení s účtem Microsoft.
6. Zadejte uživatelské jméno správce pro svůj osobní účet NuGet.org účet/účet, který jste vytvořili v kroku 1.
7. Podle pokynů dokončete transformaci tohoto účtu na organizaci.

    ![Dialogové okno Propojení msa](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>NuGet.org problémy s přihlášením k účtům AAD s nespravovaným tenantem?

Pokud se při toku přihlášení s doménou e-mailového účtu () zobrazí chyba jako níže,@yourdomain.compřečtěte si níže uvedený postup, jak obnovit svůj NuGet.org účet.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Co je to nespravovaný stav věc během přihlášení? A proč se to děje teď?** 

Váš účet se zdá být dříve zaregistrován jako osobní účet Microsoft a fungoval dobře, ale teď to vypadá, že váš účet byl zaregistrován jako "Nespravovaný" tenant ve službě Azure Active Directory (služba identit, kterou používáme k ověření účtů Microsoft). 

K tomu mohlo dojít, pokud jste @yourdomain.com se vy nebo někdo z vaší organizace (s e-mailovou adresou) zaregistrovali u jedné z integrovaných služeb AAD nebo provedli [samoobslužnou registraci pro službu Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup), která vytvoří takového klienta "Nespravovaný" pro použitou doménu účtu Microsoft(@yourdomain.com v takovém případě). 

**Co mohu udělat pro obnovení účtu?**

V tuto chvíli neexistuje způsob, jak pro nás (NuGet.org) k ověření účtů s takovými účty klienta "Nespravované" ve službě Azure Active directory. Hledáme lepší způsob, jak ověřit tyto účty.

Pokud se chcete přihlásit k NuGet.org@yourdomain.compomocí svého účtu Microsoft( ), vy (nebo správce vaší společnosti) budete muset nárokovat vlastnictví@yourdomain.comAAD tím, že provedete ověření DNS, abyste ověřili uživatele pomocí e-mailové adresy " ". Postupujte podle pokynů pro [převzetí správce domén](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover) dokumentované hostova Active directory. Jakmile je to hotovo, vaše normální přihlášení by mělo začít fungovat.

**Nechci dělat všechno, co je jiný způsob, jak obnovit svůj účet?**

Můžete [si vytvořit](https://www.microsoft.com/account) nový účet Microsoft (s @yourdomain.come-mailem, ke kterým **není** přidružen). Postupujte podle pokynů uvedených v části [Obnovení NuGet.org účtu.](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Jak změním uživatelské jméno svého účtu NuGet.org?

To nemůžeš. V rámci zásad nepovolujeme změnu uživatelských jmen. To je také narušující změna pro uživatele, kteří mohou mít definované [zásady důvěryhodnosti balíčku na základě vlastníka balíčku](../consume-packages/installing-signed-packages.md#trust-package-owners). Jediný způsob, jak změnit své uživatelské jméno, je vytvořit nový účet s požadovaným uživatelským jménem. Doporučujeme odstranit svůj stávající účet před vytvořením nového účtu, jinak nebudete moci svůj registrovaný účet Microsoft znovu použít.
> [!Important]
> Odstraněním uživatele bude **reserve** stále `username`rezervovat . Nebudete moci znovu použít stejné uživatelské jméno znovu, a **to zahrnuje změnu střev**. Jako příklad, pokud jste vytvořili `mycoolname` uživatele s uživatelským `MyCoolName`jménem a chcete to změnit na (změny písmen), nebude možné po odstranění uživatele.

Postupujte podle kroků uvedených v [části odstranit svůj NuGet.org účet](#how-to-delete-my-nugetorg-account) a [zaregistrovat nový účet](individual-accounts.md) se správným uživatelským jménem.

### <a name="how-to-delete-my-nugetorg-account"></a>Jak smazat můj účet NuGet.org?

Chcete-li svůj účet smazat, doporučujeme převést vlastnictví všech balíčků, ve kterých jste jediným vlastníkem. Můžete si přečíst další informace o [správě vlastníků balíčků](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg) o tom, jak to udělat. To nám také pomůže urychlit vaši žádost.

Pokud chcete svůj účet transformovat na organizaci, postupujte podle pokynů uvedených v [části Transformace účtu NuGet.org na organizaci](#how-to-transform-my-nugetorg-account-to-an-organization).

> [!Important]
> Odstraněníuživatele bude mít za následek následující:
>  1. Vaše uživatelské jméno bude rezervováno a nikdo ho nebude moci znovu použít k vytvoření individuálního účtu nebo účtu organizace.
>  1. Odvolat přidružené klíče rozhraní API. 
>  1. Odeberte účet jako vlastník pro všechny podřízené balíčky.
>  1. Oddělit všechny dříve existující rezervace předpony ID s tímto účtem.
>  1. Odeberte účet jako člena všech organizací.

Pokračujte v odstraňování účtu následujícím postupem.
1. [Přihlaste se k NuGet.org](https://www.nuget.org/users/account/LogOn) s účtem, který chcete smazat.
2. Klikněte na [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) tuto adresu URL: a postupujte podle pokynů k odeslání žádosti o odstranění účtu.

Naše zákaznická podpora zpracuje tento požadavek a provede smazání účtu.
