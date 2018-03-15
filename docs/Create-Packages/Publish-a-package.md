---
title: "Postup publikování balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Podrobné pokyny pro publikování balíčku NuGet nuget.org nebo privátní informačních kanálů a jak spravovat vlastnictví balíčku na nuget.org."
keywords: "Publikování balíčku NuGet, publikování balíčku NuGet, vlastnictví balíčku NuGet, publikovat do nuget.org, privátní kanály NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6cb582c036392ae2792f2fa4d307370e91c4f961
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="publishing-packages"></a>Publikování balíčků

Po vytvoření balíčku a mít vaše `.nukpg` souboru v ručně, je jednoduchý proces, aby byl k dispozici pro ostatní vývojáři veřejných nebo soukromých:

- Veřejné balíčky jsou k dispozici pro všechny vývojáře globálně přes [nuget.org](https://www.nuget.org/packages/manage/upload) jak je popsáno v tomto tématu.
- Soukromé balíčky jsou k dispozici pouze tým nebo organizace, hostování je buď sdílenou složku, server privátní NuGet [Visual Studio Team Services balíček Management](https://www.visualstudio.com/docs/package/nuget/publish), nebo jako je například myget ProGet, Nexus úložiště jiných výrobců Úložiště a Artifactory. Další podrobnosti najdete v tématu [hostování přehled balíčky](../hosting-packages/overview.md).

Toto téma popisuje publikování nuget.org; pro publikování na Visual Studio Team Services, najdete v části [správy balíčků](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikovat do nuget.org

Pro nuget.org, musíte nejdřív [zaregistrovat bezplatný účet](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) nebo přihlásit, pokud již zaregistrován:

![NuGet registrace a přihlášení umístění](media/publish_NuGetSignIn.png)

Dále můžete buď nahrání balíčku přes webový portál nuget.org, nabízená nuget.org z příkazového řádku (vyžaduje `nuget.exe` 4.1.0+), nebo publikovat v rámci procesu CI/CD prostřednictvím Visual Studio Team Services, jak je popsáno v následujících částech.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Webový portál: karta odeslat balíček v nuget.org

![Nahrání balíčku s Správce balíčků NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>Příkazový řádek

> [!Important]
> K nabízení balíčků nuget.org je nutné použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).

1. Klikněte na jméno uživatele, přejděte na nastavení svého účtu.
1. V části **klíč rozhraní API**, klikněte na tlačítko **kopírovat do schránky** načíst přístup klíče je nutné v rozhraní příkazového řádku:

    ![Kopírování klíč rozhraní API z nastavení účtu](media/publish_APIKey.png)

1. Na příkazovém řádku spusťte následující příkaz:

    ```cli
    nuget setApiKey Your-API-Key
    ```

    To ukládá klíč rozhraní API na počítači, aby nemusí proveďte tento krok opakujte na stejném počítači.

1. Nabízená vašeho balíčku Galerie NuGet pomocí příkazu:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. Před prováděné veřejný, jsou všechny balíčky nahrán do nuget.org zkontrolovat viry a odmítnuta, pokud nejsou nalezeny žádné viry. Všechny balíčky uvedené v nuget.org také jsou pravidelně kontrolovány.

1. Ve vašem účtu na nuget.org, klikněte na tlačítko **spravovat vlastní balíčky** zobrazíte ten, který jste právě publikovaná; obdržíte e-mail s potvrzením. Všimněte si, že může trvat nějakou dobu vašeho balíčku indexovat a zobrazit ve výsledcích hledání, kde je během této doby zobrazí se následující zpráva na stránce balíček můžete najít jiné:

    ![Zpráva oznamující, že balíček není ještě indexované](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>Ověřování balíčku a indexování

Balíčky nabídnutých do nuget.org podstoupit několik ověření. Když balíček uplynutí všechny ověřovací kontroly, může trvat nějakou dobu se indexovat a zobrazí ve výsledcích hledání. Po dokončení indexování obdržíte e-mail s potvrzením, že byl balíček úspěšně publikovala. Pokud se balíček nezdaří ověřování pravosti, stránce s podrobnostmi o balíčku se aktualizuje a zobrazí související chybu a taky dostane e-mail s upozorněním o něm.

Ověřování balíčku a indexování obvykle trvá v části 15 minut. Pokud balíček publikování trvá déle, než se očekávalo, navštivte [status.nuget.org](https://status.nuget.org/) ke kontrole, pokud nuget.org dochází k žádné přerušení. Pokud jsou všechny systémy provozní a balíčku nebyla publikována úspěšně v rámci hodiny, přihlaste se prosím na nuget.org a kontaktujte nás na stránce balíček pomocí odkazu obraťte se na podporu.

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Pokud jste nabízená balíčky nuget.org pomocí Visual Studio Team Services jako součást procesu průběžnou integraci a nasazení, musíte použít `nuget.exe` 4.1 nebo vyšší v úlohách NuGet. Podrobnosti najdete na [pomocí nejnovější NuGet v buildu](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Správa vlastníků balíčku v nuget.org

I když každý balíček NuGet `.nuspec` soubor definuje autoři balíčku, galerie nuget.org nepoužívá aby metadata k definování vlastnictví. Místo toho nuget.org přiřadí počáteční vlastnictví osobě, která publikuje balíček. Toto je balíček prostřednictvím uživatelského rozhraní nuget.org přihlášeného uživatele nebo uživatele, jehož klíč rozhraní API se použila se `nuget SetApiKey` nebo `nuget push`.

Všechny vlastníky balíček mít úplná oprávnění pro daný balíček, včetně přidání a odebrání dalších vlastníci a publikování aktualizací.

Chcete-li změnit vlastnictví balíčku, postupujte takto:

1. Přihlaste se k nuget.org pomocí účtu, který je vlastníkem aktuální balíčku.
1. Klikněte na své uživatelské jméno, pak na **spravovat vlastní balíčky**, pak na balíčku, kterou chcete spravovat.
1. Klikněte **Spravovat vlastníky** odkaz na levé straně.

Zde máte několik možností:

1. Chcete-li přidat vlastníka, zadejte název účtu jejich NuGet a klikněte na **přidat**. Tím se odešle e-mail do této nové spoluvlastník s odkazem potvrzení. Po potvrzení, tento uživatel má úplná oprávnění k přidání a odebrání vlastníky. (Dokud potvrzen, **Spravovat vlastníky** stránky označuje "čekající na schválení" pro tuto osobu).
1. Odebrat vlastníka, vyberte své jméno na **Spravovat vlastníky** a klikněte na tlačítko **odebrat**.
1. Jednoduše převést vlastnictví (jako když změny vlastnictví nebo balíčku byla publikována v části nesprávný účet), přidejte nový vlastník a po jejich jste potvrzen vlastnictví jejich můžete odebrat ze seznamu.

K přiřazení vlastnictví společnosti nebo skupiny, vytvořte účet nuget.org pomocí alias e-mailu, který se předají odpovídající jednotlivým členům. Například různé Microsoft ASP.NET balíčky jsou společně vlastněny [microsoft](http://nuget.org/profiles/microsoft) a [aspnet](http://nuget.org/profiles/aspnet) účty, které jednoduše takové aliasy.

### <a name="recovering-package-ownership"></a>Obnovení balíčku vlastnictví

Balíček v některých případech nemusí mít aktivní vlastníka. Například si původního vlastníka opustili společnost, která vytvoří balíček, nuget.org přihlašovací údaje budou ztraceny nebo dřívější chyby v galerii zbývajících balíček ownerless.

Pokud jste jeho oprávněný vlastník balíčku a muset znovu získat vlastnictví, použijte [obraťte se na formuláři](https://www.nuget.org/policies/Contact) na nuget.org vysvětlit, vaší konkrétní situace týmu NuGet. Jsme potom postupujte podle procesu ověřit vlastnictví balíčku, včetně pokusu o nalezení vlastník existující prostřednictvím adresy URL projektu balíčku, Twitter, e-mailu nebo jiným způsobem. Ale pokud všechno ostatní selže, může vám můžeme poslat nové pozvání k vlastníka.
