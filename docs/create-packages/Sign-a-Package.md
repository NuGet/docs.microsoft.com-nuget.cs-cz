---
title: Podepisování balíčků NuGet
description: Vysvětluje, jak lze podepsané balíčky použít k povolení ověření integrity obsahu.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429001"
---
# <a name="signing-nuget-packages"></a>Podepisování balíčků NuGet

Podepsané balíčky umožňují kontrolu ověření integrity obsahu, která poskytuje ochranu proti manipulaci s obsahem. Podpis balíčku slouží také jako jediný zdroj pravdy o skutečném původu balíčku a posiluje pravost balíčku pro spotřebitele. Tato příručka předpokládá, že jste již [vytvořili balíček](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Získání certifikátu pro podepisování kódu

Platné certifikáty lze získat od veřejné certifikační autority, jako jsou [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)atd. Úplný seznam certifikačních úřadů důvěryhodných systémem [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners)Windows lze získat z aplikace .

Pro účely testování můžete použít certifikáty s vlastním vydáním. Balíčky podepsané pomocí certifikátů vydaných samostatně však nejsou NuGet.org akceptovány. Další informace o [vytvoření testovacího certifikátu](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Export souboru certifikátu

* Existující certifikát můžete exportovat do binárního formátu DER pomocí Průvodce exportem certifikátu.

  ![Průvodce exportem certifikátu](../reference/media/CertificateExportWizard.png)

* Certifikát můžete také exportovat pomocí [příkazu Export-Certificate PowerShell](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Podepište balíček

> [!note]
> Vyžaduje nuget.exe 4.6.0 nebo novější. Dotnet.exe podpora je již brzy - [#7939](https://github.com/NuGet/Home/issues/7939)

Podepište balíček pomocí [nugetového znaku](../reference/cli-reference/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Poskytovatel certifikátu často také poskytuje adresu URL serveru časových razítek, kterou můžete použít pro výše uvedenou povinnou `Timestamper` argumentaci. Obraťte se na dokumentaci a/nebo podporu této adresy URL služby od svého poskytovatele.

* Můžete použít certifikát dostupný v úložišti certifikátů nebo certifikát ze souboru. Viz odkaz na CLI pro [znaménko nuget](../reference/cli-reference/cli-ref-sign.md).
* Podepsané balíčky by měly obsahovat časové razítko, abyste měli jistotu, že podpis zůstane platný i po vypršení platnosti podpisového certifikátu. Jinak bude operace znaku produkovat [upozornění](../reference/errors-and-warnings/NU3002.md).
* Můžete zobrazit podrobnosti o podpisu daného balíčku pomocí [nuget verify](../reference/cli-reference/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Registrace certifikátu na NuGet.org

Chcete-li publikovat podepsaný balíček, musíte nejprve zaregistrovat certifikát u NuGet.org. Certifikát potřebujete jako `.cer` soubor v binárním formátu DER.

1. [Přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se k NuGet.org.
1. Přejděte `Account settings` na `Manage Organization` **>** `Edit Organziation` (nebo pokud chcete certifikát zaregistrovat pomocí účtu organizace).
1. Rozbalte `Certificates` oddíl `Register new`a vyberte .
1. Procházejte a vyberte soubor certficate, který byl exportován dříve.
  ![Registrované certifikáty](../reference/media/registered-certs.png)

**Poznámka**
* Jeden uživatel může odeslat více certifikátů a stejný certifikát může být registrován více uživateli.
* Jakmile má uživatel certifikát registrovaný, **musí** být všechny budoucí odeslání balíčku podepsány jedním z certifikátů. Viz [Správa požadavků na podepisování pro váš balíček na NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Uživatelé mohou také odebrat registrovaný certifikát z účtu. Po odebrání certifikátu se při odeslání nezdaří nové balíčky podepsané tímto certifikátem. Existující balíčky nejsou ovlivněny.

## <a name="publish-the-package"></a>Publikování balíčku

Nyní jste připraveni publikovat balíček NuGet.org. Viz [Publikování balíčků](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Vytvoření testovacího certifikátu

Pro účely testování můžete použít certifikáty s vlastním vydáním. Chcete-li vytvořit certifikát s vlastním vydáním, použijte [příkaz New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).

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

Tento příkaz vytvoří testovací certifikát, který je k dispozici v úložišti osobních certifikátů aktuálního uživatele. Úložiště certifikátů můžete otevřít `certmgr.msc` spuštěním a zobrazit nově vytvořený certifikát.

> [!Warning]
> NuGet.org nepřijímá balíčky podepsané certifikáty vydanými samostatně.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Správa požadavků na podepisování pro váš balíček na NuGet.org
1. [Přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se k NuGet.org.

1. Přejít `Manage Packages`  
    ![na Konfigurovat podepisující balíky](../reference/media/configure-package-signers.png)

* Pokud jste jediným vlastníkem balíčku, jste povinným podepi NuGet.orgsujícím, tj.

* Pokud balíček má více vlastníků, ve výchozím nastavení "Všechny" certifikáty vlastníka lze použít k podpisu balíčku. Jako spoluvlastník balíčku můžete přepsat "Any" se sebou nebo jiným spoluvlastníkem, abyste byli povinni podepisovat. Pokud vytvoříte vlastníka, který nemá žádný certifikát registrovaný, budou povoleny nepodepsané balíčky. 

* Podobně pokud je pro balíček vybrána výchozí možnost "Any", kde má jeden vlastník certifikát registrovaný a jiný vlastník nemá žádný certifikát registrovaný, přijme NuGet.org podepsaný balíček s podpisem registrovaným jedním z jeho vlastníků nebo nepodepsaný balíček (protože jeden z vlastníků nemá žádný certifikát registrovaný).

## <a name="related-articles"></a>Související články

- [Správa rozsahu důvěryhodnosti balíčků](../consume-packages/installing-signed-packages.md)
- [Odkaz na podepsané balíčky](../reference/Signed-Packages-Reference.md)
