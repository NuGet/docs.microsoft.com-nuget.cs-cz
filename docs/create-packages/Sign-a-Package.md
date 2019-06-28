---
title: Podepisují se balíčky NuGet
description: Vysvětluje, jak podepsané balíčky je možné povolit ověření obsahu, integrity.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: abdd06642ccc652527a1a005eda2689ce97df74c
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426810"
---
# <a name="signing-nuget-packages"></a>Podepisují se balíčky NuGet

Podepsané balíčky umožňuje kontroly ověření obsahu, integrity, která poskytuje ochranu proti falšování obsahu. Podpis balíčku také slouží jako jediný zdroj pravdivých informací o skutečné původu balíček a poznámkových bloků zvýší pravosti balíčku pro spotřebitele. Tento průvodce to předpokládá, že už máte [vytvořil balíček](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Získat certifikát pro podpis kódu

Platné certifikáty mohou pocházet od veřejné certifikační autority, jako [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [globální přihlašování](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)atd. Úplný seznam certifikačních autorit důvěryhodná pro Windows můžou pocházet od [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

Pro účely testování můžete použít samostatně vydané certifikáty. Balíčky, které jsou podepsány pomocí samostatně vydané certifikáty nejsou však přijal NuGet.org. Další informace o [vytvoření testovacího certifikátu](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Exportovat soubor certifikátu

* Existující certifikát, který můžete exportovat do formátu binární kódování DER s použitím Průvodce exportem certifikátu.

  ![Průvodce exportem certifikátu](../reference/media/CertificateExportWizard.png)

* Můžete také exportovat certifikát pomocí [příkazu Powershellu Export certifikátu](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Podepište balíček

> [!note]
> Vyžaduje nuget.exe 4.6.0 nebo novější

Podepsání balíčku pomocí [nuget přihlašování](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Poskytovatel certifikátu často také obsahuje adresu URL serveru časového razítka, která vám pomůže `Timestamper` nepovinný argument zobrazit výše. Poraďte se s dokumentaci poskytovatele nebo podporu pro tuto adresu URL služby.

* Můžete použít certifikát k dispozici v úložišti certifikátů nebo použití certifikátu ze souboru. Viz odkaz pro rozhraní příkazového řádku [nuget přihlašování](../tools/cli-ref-sign.md).
* Podepsané balíčky by měly zahrnovat časové razítko, abyste měli jistotu, že podpis zůstává platná, pokud vypršela platnost podpisového certifikátu. Jinak operace přihlášení vytvoří [upozornění](../reference/errors-and-warnings/NU3002.md).
* Můžete zobrazit podrobnosti o podpisu daného balíčku pomocí [ověřte nuget](../tools/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Zaregistrovat certifikát na NuGet.org

Chcete-li publikovat podepsaný balíček, musí nejprve zaregistrovat certifikát s NuGet.org. Budete potřebovat certifikát jako `.cer` soubor ve formátu binární kódování DER.

1. [Přihlaste se](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) na NuGet.org.
1. Přejděte na `Account settings` (nebo `Manage Organization` **>** `Edit Organziation` Pokud byste chtěli zaregistrovat certifikát pomocí účtu organizace).
1. Rozbalte `Certificates` a vyberte `Register new`.
1. Procházet a vyberte soubor certifikát, který jste dříve exportovali.
  ![Certifikáty registrované](../reference/media/registered-certs.png)

**Poznámka**
* Jeden uživatel může odeslat svoji, že více certifikátů a stejný certifikát může být registrováno více uživatelů.
* Jakmile uživatel certifikát zaregistrovaný, všechny příspěvky budoucí balíček **musí** být podepsány pomocí jednoho z certifikátů. Zobrazit [spravovat podepisování požadavky pro vaše balíčků na NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Uživatelé mohou také odebírat registrovaný certifikát z účtu. Po odebrání certifikátu se nezdaří nové balíčky, které jsou podepsané pomocí tohoto certifikátu na odeslání. Nemají vliv na existující balíčky.

## <a name="publish-the-package"></a>Publikování balíčku

Nyní jste připraveni publikovat balíček na NuGet.org. Zobrazit [publikování balíčků](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Vytvoření testovacího certifikátu

Pro účely testování můžete použít samostatně vydané certifikáty. Chcete-li vytvořit certifikát vystavený, použijte [příkazu Powershellu New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

Tento příkaz vytvoří testovací certifikát k dispozici v úložišti osobních certifikátů aktuálního uživatele. Můžete otevřít úložiště certifikátů spuštěním `certmgr.msc` zobrazíte nově vytvořeného certifikátu.

> [!Warning]
> NuGet.org nepřijímá žádné balíčky podepsané pomocí samostatně vydané certifikáty.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Spravovat podepisování požadavky pro vaše balíčků na NuGet.org
1. [Přihlaste se](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) na NuGet.org.

1. Přejděte na `Manage Packages`  
    ![konfigurace podepsaných balíčků](../reference/media/configure-package-signers.png)

* Pokud jste jediným vlastníkem balíček, jsou požadované podepisující osoba to znamená všechny certifikáty registrované můžete použít k podepisování a publikovat vaše balíčky NuGet.org.

* Pokud balíček obsahuje více vlastníkům, ve výchozím nastavení, "Libovolné" vlastník certifikáty lze použít k podpisu balíčku. Jako spoluvlastníka balíček můžete přepsat "Žádný" sami se sebou nebo jakékoli jiné spoluvlastník bude požadované podepisující osoba. Pokud provedete vlastníka, který nemá žádné certifikát zaregistrovaný, budou mít povolený balíčky bez znaménka. 

* Podobně, pokud výchozí "Libovolné" výběru balíčky, kde má certifikát zaregistrovaný jednoho vlastníka a dalšího vlastníka nemá žádné certifikát zaregistrovaný, pak NuGet.org přijímá podepsaný balíček s podpisem registrovaných jednoho ze svých vlastníků nebo bez znaménka balíček (protože jeden z vlastníků nemá žádné certifikát zaregistrovaný).

## <a name="related-articles"></a>Související články

- [Spravovat hranice vztahu důvěryhodnosti balíčku](../consume-packages/installing-signed-packages.md)
- [Podepsané balíčky odkaz](../reference/Signed-Packages-Reference.md)
