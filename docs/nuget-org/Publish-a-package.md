---
title: Jak publikovat balíček NuGet
description: Podrobné pokyny pro publikování balíčku NuGet na nuget.org nebo privátní kanály a jak spravovat vlastnictví balíčků na nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 6d183100a8319b517347567f34d276e94eb4e15d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427572"
---
# <a name="publishing-packages"></a>Publikování balíčků

Po vytvoření balíčku a mít vaše `.nupkg` soubor spolupráce, je jednoduchý proces, aby byla k dispozici pro jiné vývojáře veřejně nebo soukromě:

- Veřejné balíčky jsou k dispozici pro všechny vývojáře globálně až [nuget.org](https://www.nuget.org/packages/manage/upload) jak je popsáno v tomto článku (vyžaduje NuGet 4.1.0+).
- Privátní balíčky jsou k dispozici pouze tým nebo organizace, hostováním buď sdílené, privátní server NuGet [Azure artefakty](https://www.visualstudio.com/docs/package/nuget/publish), nebo jiného úložiště, jako je například myget, ProGet, Nexus úložiště a Artifactory. Další podrobnosti najdete v tématu [hostování balíčků přehled](../hosting-packages/overview.md).

Tento článek se týká publikování do nuget.org; publikování artefaktů Azure, najdete v části [správy balíčků](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikování na nuget.org

Pro nuget.org musíte se přihlásit pomocí účtu Microsoft, pomocí kterého budete požádáni o registraci účtu s nuget.org. Také se můžete přihlásit pomocí účtu nuget.org, vytvořena pomocí starší verze portálu.

![NuGet přihlášení umístění](media/publish_NuGetSignIn.png)

V dalším kroku můžete buď nahrání balíčku prostřednictvím webového portálu nuget.org, push na nuget.org z příkazového řádku (vyžaduje `nuget.exe` 4.1.0+), nebo publikovat jako součást procesu CI/CD DevOps službami Azure, jak je popsáno v následujících částech.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Webový portál: na kartě nahrání balíčků na nuget.org

1. Vyberte **nahrát** v horní nabídce nuget.org a přejděte do umístění balíčku.

    ![Nahrání balíčků na nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org informuje, pokud název balíčku je k dispozici. Pokud není, změňte identifikátor balíčku v projektu, sestavte znovu a zkuste nahrát znovu.

1. Pokud název balíčku je k dispozici, se otevře nuget.org **ověřte** oddílu, ve kterém můžete zkontrolovat metadat z manifestu balíčku. Chcete-li změnit některý z metadat, upravte svůj projekt (soubor projektu nebo `.nuspec` souboru), znovu sestavit, znovu vytvořte balíček a odešlete znovu.

1. V části **Import dokumentaci** můžete vložit Markdownu, přejděte na svoje dokumenty pomocí adresy URL nebo nahrát soubor dokumentace.

1. Když je připraven všechny informace, vyberte **odeslat** tlačítko

### <a name="command-line"></a>Příkazový řádek

Push balíčků na nuget.org je nutné použít [nuget.exe verze 4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [NuGet protokoly](../api/nuget-protocols.md). Budete také potřebovat klíče rozhraní API, která je vytvořena na nuget.org.

#### <a name="create-api-keys"></a>Vytvoření klíče rozhraní API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikování pomocí nuget dotnet nasdílení změn

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikování pomocí nuget nasdílení změn

1. Na příkazovém řádku spusťte následující příkaz a nahraďte `<your_API_key>` pomocí klíče získané z webu nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Tento příkaz uloží klíč rozhraní API v konfiguraci Nugetu tak, že potřebujete opakujte tento krok znovu ve stejném počítači.

1. Nahrání balíčku do Galerie NuGet pomocí následujícího příkazu:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikovat podepsané balíčky

Odeslat podepsaný balíčků, je nutné nejprve [zaregistrovat certifikát](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) používá k podepisování balíčků. 

> [!Warning]
> nuget.org odmítne balíčky, které splňují není [podepsaný balíček požadavky](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Ověření balíčku a indexování

Balíčky nuget.org do této oblasti podstupovali několik ověření, jako jsou antivirové kontroly. (Všech balíčků na nuget.org jsou pravidelně kontrolovány.)

Když tento balíček prošel všechny ověřovací kontroly, může trvat nějakou dobu se indexovat a zobrazí ve výsledcích hledání. Po dokončení indexování obdržíte e-mail s potvrzením, že byl balíček úspěšně publikovala. Pokud balíček selhání kontroly ověřování, na stránce podrobností balíčku se aktualizuje a zobrazí související chyby a také obdržíte e-mail s upozorněním můžete o něm.

Ověření balíčku a indexování obvykle trvá méně než 15 minut. Pokud o publikování balíčku trvá déle, než se očekávalo, navštivte [status.nuget.org](https://status.nuget.org/) ke kontrole, pokud nuget.org dochází k žádné přerušení. Pokud jsou všechny systémy provozní a balíčku nebyla úspěšně publikována do jedné hodiny, přihlaste se prosím na nuget.org a kontaktujte nás přes odkaz na podporu se obraťte se na stránce balíček pro.

Pokud chcete zobrazit stav balíčku, vyberte **spravovat balíčky** pod názvem vašeho účtu na nuget.org. Po dokončení ověření obdržíte e-mail s potvrzením.

Všimněte si, že může trvat nějakou dobu vašeho balíčku indexovat a zobrazí ve výsledcích hledání tam, kde ostatní můžete najít, během této doby se zobrazí následující zpráva na stránce balíček:

![Zpráva oznamující, že balíček ještě nebyla publikována.](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Služby Azure DevOps (CI/CD)

Pokud vložíte balíčků na nuget.org jako součást procesu průběžnou integraci a nasazování pomocí služby Azure DevOps, je nutné použít `nuget.exe` 4.1 nebo vyšší v úlohách NuGet. Podrobnosti najdete na [pomocí nejnovějšího balíčku NuGet ve vašem buildu](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blogu Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Správa vlastníků balíčků na nuget.org

I když každý balíček NuGet `.nuspec` soubor definuje autory balíčku, galerie nuget.org nepoužívá tato metadata k definování vlastnictví. Místo toho nuget.org přiřadí osobě, která publikuje balíček počáteční vlastnictví. Toto je balíček prostřednictvím uživatelského rozhraní nuget.org přihlášeného uživatele nebo uživatele, jehož klíč rozhraní API byla použita s `nuget SetApiKey` nebo `nuget push`.

Všechny vlastníky balíčku máte úplná oprávnění pro balíček, včetně přidání a odebrání dalších vlastníků a publikování aktualizací.

Chcete-li změnit vlastnictví balíčku, postupujte takto:

1. Přihlaste se k nuget.org pomocí účtu, který je aktuálním vlastníkem balíčku.
1. Vyberte název svého účtu, vyberte **spravovat balíčky**a rozbalte **publikovat balíčky**.
1. Vyberte balíček, který chcete spravovat a potom na pravé straně vyberte **Spravovat vlastníky**.

Zde máte několik možností:

1. Odebrat všechny vlastníka uvedený v části **aktuální vlastníky**.
1. Přidat vlastníka pod **přidat vlastníka** zadáním jejich uživatelskému jménu, zprávu, a výběrem **přidat**. Tato akce odešle e-mailu na tuto novou spoluvlastník s odkazem na potvrzení. Po potvrzení, tato osoba má úplná oprávnění k přidání a odebrání vlastníků. (Dokud není potvrzené, **aktuální vlastníky** čekající na schválení pro tuto osobu, která určuje části.)
1. Převést vlastnictví (jako v části k nesprávnému účtu byl při publikování změny vlastnictví nebo balíčku), přidejte nového vlastníka a po jejich ověření, že vlastnictví, můžete odebrat ze seznamu.

Přiřazení vlastnictví společnosti nebo skupiny, vytvořte účet nuget.org pomocí e-mailový alias, který je předán členům týmu odpovídající. Například různé balíčky Microsoft ASP.NET jsou společné vlastnictví [microsoft](http://nuget.org/profiles/microsoft) a [aspnet](http://nuget.org/profiles/aspnet) účty, které jednoduše tyto aliasy.

### <a name="recovering-package-ownership"></a>Obnovení balíčku vlastnictví

Balíček v některých případech nemusí mít aktivní vlastníka. Například původního vlastníka ještě zbývá společnosti, která vytvoří balíček, nuget.org přihlašovací údaje budou ztraceny, nebo předchozí chyby v galerii ponechat ownerless balíček.

Pokud jsou právoplatného vlastníka balíčku a potřebujete znovu získat vlastnictví, použijte [kontaktní formulář](https://www.nuget.org/policies/Contact) na nuget.org vysvětlit vaší situaci týmu NuGet. My potom postupujte podle procesu ověřit vlastnictví balíček, včetně pokusu o nalezení stávající vlastník prostřednictvím adresy URL projektu daného balíčku, Twitter, e-mailu nebo jiným způsobem. Ale když nic jiného nepomůže, vám můžeme poslat nové pozvánky stát vlastníkem.
