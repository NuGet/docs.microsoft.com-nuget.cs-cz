---
title: Jak publikovat balíček NuGet
description: Podrobné pokyny pro publikování balíčku NuGet v nuget.org nebo privátních informačních kanálech a o tom, jak spravovat vlastnictví balíčku v nuget.org.
author: JonDouglas
ms.author: jodou
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 5be7a4d4c31df9f2f4bda7bdb1ff9f4887108578
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775991"
---
# <a name="publishing-packages"></a>Publikování balíčků

Jakmile vytvoříte balíček a máte `.nupkg` soubor v ruce, je to jednoduchý proces, který ho zpřístupní ostatním vývojářům, a to veřejně nebo soukromě:

- Veřejné balíčky jsou zpřístupněny všem vývojářům globálně prostřednictvím [NuGet.org](https://www.nuget.org/packages/manage/upload) , jak je popsáno v tomto článku (vyžaduje NuGet 4.1.0 +).
- Soukromé balíčky jsou k dispozici pouze pro tým nebo organizaci, a to jejich hostováním buď sdílené složky, privátního serveru NuGet, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)nebo úložiště třetí strany, jako je například Myget, ProGet, Nexus úložiště a Artifactory. Další podrobnosti najdete v tématu [Přehled hostujících balíčků](../hosting-packages/overview.md).

Tento článek popisuje publikování na nuget.org. informace o publikování do Azure Artifacts najdete v tématu [Správa balíčků](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikovat na nuget.org

V případě nuget.org se musíte přihlásit pomocí účet Microsoft, se kterým budete požádáni o registraci účtu v nuget.org.

![Přihlašovací umístění NuGet](media/publish_NuGetSignIn.png)

Dále můžete balíček nahrát prostřednictvím webového portálu nuget.org, vložit ho do nuget.org z příkazového řádku (vyžaduje `nuget.exe` 4.1.0 +) nebo publikovat jako součást procesu CI/CD prostřednictvím Azure DevOps Services, jak je popsáno v následujících částech.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Webový portál: použijte kartu nahrát balíček v nuget.org

1. V horní nabídce nuget.org vyberte **nahrát** a vyhledejte umístění balíčku.

    ![Nahrání balíčku na nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org obsahuje informace o tom, jestli je k dispozici název balíčku. Pokud není, změňte identifikátor balíčku v projektu, znovu sestavte a opakujte nahrávání.

1. Pokud je název balíčku k dispozici, nuget.org otevře oddíl **ověření** , ve kterém můžete zkontrolovat metadata z manifestu balíčku. Chcete-li změnit jakoukoli metadata, upravit projekt (soubor projektu nebo `.nuspec` soubor), znovu sestavit, znovu vytvořit balíček a znovu nahrávat.

1. V části **importovat dokumentaci** můžete Markdownu vložit, nasměrovat na své dokumenty pomocí adresy URL nebo nahrát soubor dokumentace.

1. Až budou všechny informace připravené, vyberte tlačítko **Odeslat** .

### <a name="command-line"></a>Příkazový řádek

Pokud chcete nabízet balíčky do nuget.org, budete nejdřív potřebovat klíč rozhraní API, který se vytvoří v nuget.org. Musíte použít buď dotnet.exe (.NET Core), nebo nuget.exe v 4.1.0 nebo novějším, které implementují požadované protokoly NuGet.
Další informace najdete v tématu protokoly [.NET Core](/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads)a [NuGet](../api/nuget-protocols.md).

#### <a name="create-api-keys"></a>Vytvoření klíčů rozhraní API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikování pomocí příkazu dotnet NuGet push

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikování s nabízeným oznámením NuGet

1. Na příkazovém řádku spusťte následující příkaz, kterým nahradíte `<your_API_key>` klíč získaný z NuGet.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Tento příkaz uloží klíč rozhraní API do konfigurace NuGet, takže tento krok nebudete muset opakovat na stejném počítači.

    > [!NOTE]
    > Klíč rozhraní API se nepoužívá pro ověřování pomocí privátního informačního kanálu. Pro správu přihlašovacích údajů pro ověřování ve zdroji použijte [ `nuget sources` příkaz](../reference/cli-reference/cli-ref-sources.md) .
    > Klíče rozhraní API lze získat z jednotlivých serverů NuGet. Informace o vytvoření a manange APIKeys pro nuget.org najdete v tématu [vytvoření klíčů rozhraní API](#create-api-keys).

1. Nahrajte balíček do galerie NuGet pomocí následujícího příkazu:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikovat podepsané balíčky

Chcete-li odeslat podepsané balíčky, je třeba nejprve [zaregistrovat certifikát](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) použitý k podepsání balíčků. 

> [!Warning]
> nuget.org odmítne balíčky, které nesplňují [požadavky na podepsaný balíček](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Ověření a indexování balíčku

Balíčky vložené do nuget.org prošly několika ověřeními, jako jsou například kontroly virů. (Všechny balíčky na nuget.org se pravidelně hledají.)

Po úspěšném provedení všech kontrol balíčku může chvíli trvat, než se bude indexovat a zobrazit ve výsledcích hledání. Po dokončení indexování obdržíte e-mail s potvrzením, že balíček byl úspěšně publikován. Pokud balíček neuspěje při ověření, aktualizuje se stránka s podrobnostmi balíčku, aby se zobrazila přidružená chyba, a obdržíte také e-mail s upozorněním.

Ověření a indexování balíčku obvykle trvá 15 minut. Pokud publikování balíčku trvá déle, než se čekalo, navštivte [status.NuGet.org](https://status.nuget.org/) a ověřte, jestli NuGet.org má nějaké přerušení. Pokud jsou všechny systémy funkční a balíček se do jedné hodiny nepublikoval úspěšně, přihlaste se k nuget.org a kontaktujte nás pomocí odkazu na podporu kontaktů na stránce balíček.

Pokud chcete zobrazit stav balíčku, vyberte **Spravovat balíčky** pod názvem svého účtu v NuGet.org. Po dokončení ověření se zobrazí potvrzovací e-mail.

Všimněte si, že může chvíli trvat, než se váš balíček naindexuje a zobrazí ve výsledcích hledání, kde ho můžou najít jiní uživatelé. v takovém případě se na stránce balíčku zobrazí následující zpráva:

![Zpráva oznamující, že balíček ještě není publikovaný](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

Pokud zadáte balíčky do nuget.org pomocí Azure DevOps Services jako součást procesu kontinuální integrace nebo nasazení, musíte `nuget.exe` v úlohách NuGet použít 4,1 nebo vyšší. Podrobnosti najdete v [části použití nejnovější sady NuGet v sestavení](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Správa vlastníků balíčků na nuget.org

I když každý soubor balíčku NuGet `.nuspec` definuje autory balíčku, galerie NuGet.org nepoužívá tato metadata k definování vlastnictví. Místo toho nuget.org přiřadí počáteční vlastnictví osobě, která balíček zveřejňuje. Toto je buď přihlášený uživatel, který balíček odeslal prostřednictvím uživatelského rozhraní nuget.org, nebo uživatele, jejichž klíč rozhraní API se použil s `nuget SetApiKey` nebo `nuget push` .

Všichni vlastníci balíčku mají úplná oprávnění pro balíček, včetně přidávání a odebírání jiných vlastníků a publikování aktualizací.

Chcete-li změnit vlastnictví balíčku, postupujte následovně:

1. Přihlaste se k nuget.org pomocí účtu, který je aktuálním vlastníkem balíčku.
1. Vyberte název účtu, vyberte **Spravovat balíčky** a rozbalte **publikované balíčky**.
1. Vyberte balíček, který chcete spravovat, a pak na pravé straně vyberte **Spravovat vlastníky**.

Tady máte několik možností:

1. Odeberte všechny vlastníka uvedené v části **aktuální vlastníci**.
1. Přidejte vlastníka do části **Přidat vlastníka** zadáním jeho uživatelského jména, zprávy a výběru možnosti **Přidat**. Tato akce pošle e-mailem tomuto novému spoluvlastníkovi odkaz s potvrzením. Po potvrzení tato osoba má úplná oprávnění k přidávání a odebírání vlastníků. (Až do potvrzení, část **aktuální vlastníci** indikuje, že se čeká na schválení pro tuto osobu.)
1. Pokud chcete přenést vlastnictví (jako při změně vlastnictví nebo balíčku, který se publikoval v nesprávném účtu), přidejte nového vlastníka a jakmile se potvrdí vlastnictví, můžou vás ze seznamu odebrat.

Pokud chcete přiřadit vlastnictví společnosti nebo skupiny, vytvořte účet nuget.org pomocí e-mailového aliasu předaného příslušnému členovi týmu. Například různé balíčky Microsoft ASP.NET jsou spoluvlastněny účty [Microsoft](https://nuget.org/profiles/microsoft) a [ASPNET](https://nuget.org/profiles/aspnet) , které jednoduše odkazují na tyto aliasy.

### <a name="recovering-package-ownership"></a>Obnovování vlastnictví balíčku

V některých případech nemusí mít daný balíček aktivního vlastníka. Původní vlastník například mohl přijít o společnost, která vytvořila balíček, nuget.org přihlašovací údaje nebo předchozí chyby v galerii opustili bez vlastníka balíčku.

Pokud jste vlastníkem balíčku rightful a potřebujete znovu získat vlastnictví, použijte [kontaktní formulář](https://www.nuget.org/policies/Contact) v NuGet.org a vysvětlete svou situaci týmu NuGet. Pak budeme postupovat podle tohoto procesu a ověřit vlastnictví balíčku, včetně pokusu o vyhledání existujícího vlastníka prostřednictvím adresy URL projektu, Twitteru, e-mailu nebo jiného prostředku balíčku. Pokud se ale všechny ostatní selžou, můžeme vám poslat nové pozvánky, abychom se stali vlastníkem.
