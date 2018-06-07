---
title: Postup publikování balíčku NuGet
description: Podrobné pokyny pro publikování balíčku NuGet nuget.org nebo privátní informačních kanálů a jak spravovat vlastnictví balíčku na nuget.org.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: eb45ac1574efc79873d2d372f122a3d756e90ee5
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818552"
---
# <a name="publishing-packages"></a>Publikování balíčků

Po vytvoření balíčku a mít vaše `.nupkg` souboru v ručně, je jednoduchý proces, aby byl k dispozici pro ostatní vývojáři veřejných nebo soukromých:

- Veřejné balíčky jsou k dispozici pro všechny vývojáře globálně přes [nuget.org](https://www.nuget.org/packages/manage/upload) jak je popsáno v tomto článku (vyžaduje NuGet 4.1.0+).
- Soukromé balíčky jsou k dispozici pouze tým nebo organizace, hostování je buď sdílenou složku, server privátní NuGet [Visual Studio Team Services balíček Management](https://www.visualstudio.com/docs/package/nuget/publish), nebo jako je například myget ProGet, Nexus úložiště jiných výrobců Úložiště a Artifactory. Další podrobnosti najdete v tématu [hostování přehled balíčky](../hosting-packages/overview.md).

Tento článek se zabývá publikování nuget.org; pro publikování na Visual Studio Team Services, najdete v části [správy balíčků](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikovat do nuget.org

Pro nuget.org musíte se přihlásit s účtem Microsoft, pomocí kterého budete vyzváni k registraci účet s nuget.org. Také se můžete přihlásit pomocí účet nuget.org vytvořené pomocí starší verze portálu.

![Místo přihlášení NuGet](media/publish_NuGetSignIn.png)

Dále můžete buď nahrání balíčku přes webový portál nuget.org, nabízená nuget.org z příkazového řádku (vyžaduje `nuget.exe` 4.1.0+), nebo publikovat v rámci procesu CI/CD prostřednictvím Visual Studio Team Services, jak je popsáno v následujících částech.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Webový portál: karta odeslat balíček v nuget.org

1. Vyberte **nahrát** v horní nabídce nuget.org a přejděte do umístění balíčku.

    ![Nahrání balíčku v nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org zjistíte, zda je název balíčku k dispozici. Pokud není, změnit identifikátor balíčku v projektu, znovu sestavit a opakujte odeslání.

1. Pokud je dostupný název balíčku, otevře se nuget.org **ověřte** části, ve kterém můžete zkontrolovat metadata z manifestu balíčku. Chcete-li změnit některé z metadat, upravte projektu (soubor projektu nebo `.nuspec` soubor), znovu vytvořit, znovu vytvořte balíček a odešlete znovu.

1. V části **Import dokumentaci** můžete vložit Markdownu, přejděte na svoje dokumenty s adresou URL nebo odeslat soubor dokumentace.

1. Když je připraven všechny informace, vyberte **odeslání** tlačítko

### <a name="command-line"></a>Příkazový řádek

K nabízení balíčků nuget.org je nutné použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md). Musíte také klíč rozhraní API, která je vytvořena na nuget.org.

#### <a name="create-api-keys"></a>Vytvoření klíče rozhraní API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikování pomocí nabízených nuget dotnet.

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikování pomocí nabízených nuget

1. Na příkazovém řádku spusťte následující příkaz, nahraďte `<your_API_key>` klíčem získané z nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Tento příkaz uloží klíč rozhraní API v konfiguraci NuGet tak, aby potřebovat opakujte tento krok opakujte na stejném počítači.

1. Nabízená vašeho balíčku Galerie NuGet pomocí následujícího příkazu:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikovat podepsané balíčky

Chcete-li odeslat podepsaný balíčků, je nutné nejprve [zaregistrovat certifikát](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg) použít pro podepisování balíčků. 

> [!Warning]
> nuget.org odmítne balíčky, které si odpovídají [podepsané požadavků balíčku](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Ověřování balíčku a indexování

Balíčky nabídnutých do nuget.org podstoupit několik ověření, jako jsou antivirové kontroly. (Všechny balíčky v nuget.org jsou pravidelně kontrolovány.)

. Když balíček uplynutí všechny ověřovací kontroly, může trvat nějakou dobu se indexovat a zobrazí ve výsledcích hledání. Po dokončení indexování obdržíte e-mail s potvrzením, že byl balíček úspěšně publikovala. Pokud se balíček nezdaří ověřování pravosti, stránce s podrobnostmi o balíčku se aktualizuje a zobrazí související chybu a taky dostane e-mail s upozorněním o něm.

Ověřování balíčku a indexování obvykle trvá v části 15 minut. Pokud balíček publikování trvá déle, než se očekávalo, navštivte [status.nuget.org](https://status.nuget.org/) ke kontrole, pokud nuget.org dochází k žádné přerušení. Pokud jsou všechny systémy provozní a balíčku nebyla publikována úspěšně v rámci hodiny, přihlaste se prosím na nuget.org a kontaktujte nás na stránce balíček pomocí odkazu obraťte se na podporu.

Chcete-li zobrazit stav balíčku, vyberte **spravovat balíčky** pod názvem vašeho účtu na nuget.org. Po dokončení ověření obdržíte e-mail s potvrzením.

Všimněte si, že může trvat nějakou dobu vašeho balíčku indexovat a zobrazit ve výsledcích hledání, kde je během této doby zobrazí se následující zpráva na stránce balíček můžete najít jiné:

![Zpráva oznamující, že balíček ještě není publikována.](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Pokud jste nabízená balíčky nuget.org pomocí Visual Studio Team Services jako součást procesu průběžnou integraci a nasazení, musíte použít `nuget.exe` 4.1 nebo vyšší v úlohách NuGet. Podrobnosti najdete na [pomocí nejnovější NuGet v buildu](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Správa vlastníků balíčku v nuget.org

I když každý balíček NuGet `.nuspec` soubor definuje autoři balíčku, galerie nuget.org nepoužívá aby metadata k definování vlastnictví. Místo toho nuget.org přiřadí počáteční vlastnictví osobě, která publikuje balíček. Toto je balíček prostřednictvím uživatelského rozhraní nuget.org přihlášeného uživatele nebo uživatele, jehož klíč rozhraní API se použila se `nuget SetApiKey` nebo `nuget push`.

Všechny vlastníky balíček mít úplná oprávnění pro daný balíček, včetně přidání a odebrání dalších vlastníci a publikování aktualizací.

Chcete-li změnit vlastnictví balíčku, postupujte takto:

1. Přihlaste se k nuget.org pomocí účtu, který je vlastníkem aktuální balíčku.
1. Vyberte název účtu, vyberte **spravovat balíčky**a rozbalte **publikované balíčky**.
1. Vyberte na balíček, který chcete spravovat a pak na pravé straně vyberte **Spravovat vlastníky**.

Zde máte několik možností:

1. Odeberte všechny vlastníka uvedený v seznamu **aktuální vlastníky**.
1. Přidat vlastníka pod **přidat vlastníka** zadáním uživatelského jména, zprávu, a výběrem **přidat**. Tato akce odešle e-mail na tuto novou spoluvlastník s odkazem potvrzení. Po potvrzení, tento uživatel má úplná oprávnění k přidání a odebrání vlastníky. (Dokud potvrzen, **aktuální vlastníky** části označuje čekající na schválení pro tuto osobu.)
1. Převést vlastnictví (jako když změny vlastnictví nebo balíčku byla publikována v části nesprávný účet), přidejte nový vlastník a po jejich jste potvrzen vlastnictví jejich můžete odebrat ze seznamu.

K přiřazení vlastnictví společnosti nebo skupiny, vytvořte účet nuget.org pomocí alias e-mailu, který se předají odpovídající jednotlivým členům. Například různé Microsoft ASP.NET balíčky jsou společně vlastněny [microsoft](http://nuget.org/profiles/microsoft) a [aspnet](http://nuget.org/profiles/aspnet) účty, které jednoduše takové aliasy.

### <a name="recovering-package-ownership"></a>Obnovení balíčku vlastnictví

Balíček v některých případech nemusí mít aktivní vlastníka. Například si původního vlastníka opustili společnost, která vytvoří balíček, nuget.org přihlašovací údaje budou ztraceny nebo dřívější chyby v galerii zbývajících balíček ownerless.

Pokud jste jeho oprávněný vlastník balíčku a muset znovu získat vlastnictví, použijte [obraťte se na formuláři](https://www.nuget.org/policies/Contact) na nuget.org vysvětlit, vaší konkrétní situace týmu NuGet. Jsme potom postupujte podle procesu ověřit vlastnictví balíčku, včetně pokusu o nalezení vlastník existující prostřednictvím adresy URL projektu balíčku, Twitter, e-mailu nebo jiným způsobem. Ale pokud všechno ostatní selže, může vám můžeme poslat nové pozvání k vlastníka.
