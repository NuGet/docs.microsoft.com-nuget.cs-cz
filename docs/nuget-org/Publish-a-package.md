---
title: Jak publikovat balíček NuGet
description: Podrobné pokyny pro publikování balíčku NuGet pro nuget.org nebo soukromé informační kanály a jak spravovat vlastnictví balíčku na nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429022"
---
# <a name="publishing-packages"></a>Publikování balíčků

Jakmile vytvoříte balíček a `.nupkg` máte soubor v ruce, je to jednoduchý proces, aby byl k dispozici ostatním vývojářům, a to buď veřejně nebo soukromě:

- Veřejné balíčky jsou k dispozici všem vývojářům globálně prostřednictvím [nuget.org](https://www.nuget.org/packages/manage/upload) jak je popsáno v tomto článku (vyžaduje NuGet 4.1.0+).
- Soukromé balíčky jsou k dispozici pouze pro tým nebo organizaci tím, že je hostuje buď sdílená složka, soukromý nugetový server, [artefakty Azure](https://www.visualstudio.com/docs/package/nuget/publish)nebo úložiště třetích stran, jako je myget, ProGet, Nexus Repository a Artifactory. Další podrobnosti naleznete v [tématu Přehled hostování balíčků](../hosting-packages/overview.md).

Tento článek popisuje publikování na nuget.org; pro publikování na Artefakty Azure, najdete v [tématu Správa balíčků](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikovat do nuget.org

V nuget.org se musíte přihlásit pomocí účtu Microsoft, pomocí kterého budete požádáni o registraci účtu u nuget.org. Můžete se také přihlásit pomocí účtu nuget.org vytvořeného pomocí starších verzí portálu.

![Umístění přihlášení NuGet](media/publish_NuGetSignIn.png)

Dále můžete buď nahrát balíček prostřednictvím webového portálu nuget.org, `nuget.exe` nabízený nuget.org z příkazového řádku (vyžaduje 4.1.0+) nebo publikovat jako součást procesu CI/CD prostřednictvím služby Azure DevOps Services, jak je popsáno v následujících částech.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Webový portál: Použijte kartu Nahrát balíček na nuget.org

1. V horní nabídce nuget.org vyberte **Nahrát** a vyhledejte umístění balíčku.

    ![Nahrání balíčku na nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org vám řekne, zda je k dispozici název balíčku. Pokud tomu tak není, změňte identifikátor balíčku v projektu, znovu se stavněte a zkuste nahrát znovu.

1. Pokud je k dispozici název balíčku, otevře nuget.org oddíl **Ověření,** ve kterém můžete zkontrolovat metadata z manifestu balíčku. Chcete-li změnit libovolné z metadat, upravte `.nuspec` projekt (soubor projektu nebo soubor), znovu vytvořit balíček a znovu nahrát.

1. V části **Import dokumentace** můžete vložit Markdown, přejděte na dokumenty s adresou URL nebo nahrajte soubor dokumentace.

1. Až budou všechny informace připravené, vyberte tlačítko **Odeslat.**

### <a name="command-line"></a>Příkazový řádek

Chcete-li vysunout balíčky nuget.org musíte použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [protokoly NuGet](../api/nuget-protocols.md). Potřebujete také klíč rozhraní API, který je vytvořen na nuget.org.

#### <a name="create-api-keys"></a>Vytvořit klíče rozhraní API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikovat pomocí dotnet nuget push

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikovat pomocí nuget push

1. Na příkazovém řádku spusťte `<your_API_key>` následující příkaz, který nahradí klíč získaný z nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Tento příkaz ukládá klíč rozhraní API v konfiguraci NuGet, takže není nutné opakovat tento krok znovu ve stejném počítači.

    > [!NOTE]
    > Klíč rozhraní API se nepoužívá pro ověřování s privátním zdrojem. Odkazovat [ `nuget sources` ](../reference/cli-reference/cli-ref-sources.md) na příkaz pro správu pověření pro ověřování se zdrojem.
    > Klíče rozhraní API lze získat z jednotlivých serverů NuGet. Chcete-li vytvořit a manange APIKeys pro nuget.org naleznete [na publish-api-key](../quickstart/includes/publish-api-key.md)

1. Převelitím balíčku do Galerie NuGet pomocí následujícího příkazu:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikování podepsaných balíčků

Chcete-li odeslat podepsané balíčky, musíte [nejprve zaregistrovat certifikát](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) použitý k podpisu balíčků. 

> [!Warning]
> nuget.org odmítne balíčky, které nesplňují [požadavky podepsaného balíčku](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Ověření a indexování balíčků

Balíčky, které byly posunuty nuget.org, procházejí několika ověřeními, například kontrolami virů. (Všechny balíčky na nuget.org jsou pravidelně kontrolovány.)

Pokud balíček prošel všechny kontroly ověření, může chvíli trvat, než se indexuje a zobrazí se ve výsledcích hledání. Po dokončení indexování obdržíte e-mail s potvrzením, že balíček byl úspěšně publikován. Pokud balíček neprojde kontrolou ověření, stránka podrobností balíčku se aktualizuje, aby se zobrazila přidružená chyba, a obdržíte také e-mail s upozorněním na něj.

Ověření a indexování balíčku obvykle trvá méně než 15 minut. Pokud publikování balíčku trvá déle, než bylo očekáváno, navštivte [status.nuget.org](https://status.nuget.org/) a zkontrolujte, zda nuget.org dochází k přerušení. Pokud jsou všechny systémy funkční a balíček nebyl úspěšně publikován do hodiny, přihlaste se k nuget.org a kontaktujte nás pomocí odkazu Kontaktujte podporu na stránce balíčku.

Pokud chcete zobrazit stav balíčku, vyberte **spravovat balíčky** pod názvem účtu na nuget.org. Po dokončení ověření obdržíte potvrzovací e-mail.

Všimněte si, že může chvíli trvat, než se váš balíček indexuje a zobrazí se ve výsledcích vyhledávání tam, kde ho mohou najít ostatní, během které se na stránce balíčku zobrazí následující zpráva:

![Zpráva označující balíček ještě není publikována](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Služby Azure DevOps (CI/CD)

Pokud vysáváte balíčky nuget.org pomocí služby Azure DevOps `nuget.exe` Services jako součást procesu průběžné integrace/nasazení, musíte použít 4.1 nebo vyšší v nugetových úlohách. Podrobnosti najdete na [použití nejnovější NuGet ve vašem sestavení](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).

## <a name="managing-package-owners-on-nugetorg"></a>Správa vlastníků balíčků na nuget.org

Přestože každý `.nuspec` soubor balíčku NuGet definuje autory balíčku, galerie nuget.org nepoužívá tato metadata k definování vlastnictví. Místo toho nuget.org přiřadí počáteční vlastnictví osobě, která publikuje balíček. Toto je buď přihlášený uživatel, který nahrál balíček prostřednictvím uživatelského rozhraní `nuget SetApiKey` nuget.org, nebo uživatelé, jejichž klíč rozhraní API byl použit s nebo `nuget push`.

Všichni vlastníci balíčku mají úplná oprávnění pro balíček, včetně přidání a odebrání dalších vlastníků a publikování aktualizací.

Chcete-li změnit vlastnictví balíčku, postupujte takto:

1. Přihlaste se k nuget.org s účtem, který je aktuálním vlastníkem balíčku.
1. Vyberte název účtu, vyberte **Spravovat balíčky**a **rozbalte Položku Publikované balíčky**.
1. Vyberte na balíčku, který chcete spravovat, pak na pravé straně vyberte **Spravovat vlastníky**.

Zde máte několik možností:

1. Odeberte všechny vlastníky uvedené v části **Aktuální vlastníci**.
1. V části **Přidat vlastníka** přidejte vlastníka zadáním uživatelského jména, zprávy a výběrem možnosti **Přidat**. Tato akce odešle e-mail novému spoluvlastníkovi s potvrzovacím odkazem. Po potvrzení má tato osoba úplná oprávnění k přidávání a odebírá vlastníky. (Dokud nebude potvrzeno, část **Aktuální vlastníci** označuje čekající schválení pro tuto osobu.)
1. Chcete-li převést vlastnictví (jako když bylo vlastnické právo publikováno nebo byl balíček publikován pod nesprávným účtem), přidejte nového vlastníka a po potvrzení vlastnictví vás může ze seznamu odebrat.

Chcete-li přiřadit vlastnictví společnosti nebo skupině, vytvořte účet nuget.org pomocí e-mailového aliasu, který je předán příslušným členům týmu. Například různé balíčky Microsoft ASP.NET jsou spoluvlastněny účty [Microsoft](https://nuget.org/profiles/microsoft) a [aspnet,](https://nuget.org/profiles/aspnet) které jednoduše takové aliasy.

### <a name="recovering-package-ownership"></a>Obnovení vlastnictví balíčku

V některých případě balíček nemusí mít aktivního vlastníka. Původní vlastník například opustil společnost, která balíček vyrábí, nuget.org pověření jsou ztraceny nebo dřívější chyby v galerii zanechaly balíček bez vlastníka.

Pokud jste právoplatným vlastníkem balíčku a potřebujete znovu získat vlastnictví, použijte [kontaktní formulář](https://www.nuget.org/policies/Contact) na nuget.org vysvětlit vaši situaci týmu NuGet. Poté se řídíme procesem ověření vašeho vlastnictví balíčku, včetně pokusu o nalezení stávajícího vlastníka prostřednictvím adresy URL projektu, Twitteru, e-mailu nebo jiným i jiným způsobem. Ale pokud vše ostatní selže, můžeme vám poslat novou pozvánku, abyste se stali vlastníkem.
