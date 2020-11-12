---
title: Podepisování balíčků NuGet
description: Vysvětluje, jak lze pomocí podepsaných balíčků povolit ověření integrity obsahu.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 64b28c29ae3b533bde7c8f41dd38a4ab0a5afef7
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550372"
---
# <a name="signing-nuget-packages"></a>Podepisování balíčků NuGet

Podepsané balíčky umožňují kontrolu integrity obsahu, která zajišťuje ochranu proti manipulaci s obsahem. Podpis balíčku také slouží jako jediný zdroj pravdy na skutečný původ balíčku a pravost posilují balíčku pro daného příjemce. V tomto průvodci se předpokládá, že jste už [vytvořili balíček](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Získání certifikátu pro podpis kódu

Platné certifikáty mohou být získány od veřejné certifikační autority, jako je [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)atd. Úplný seznam certifikačních autorit, které jsou pro Windows důvěryhodné, můžete získat z [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .

Pro účely testování můžete použít certifikáty vystavené svým držitelem. Balíčky podepsané pomocí certifikátů vydaných svým držitelem ale neakceptuje NuGet.org. Další informace o [Vytvoření testovacího certifikátu](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Exportovat soubor certifikátu

* Existující certifikát můžete exportovat do binárního formátu DER pomocí Průvodce exportem certifikátu.

  ![Průvodce exportem certifikátu](../reference/media/CertificateExportWizard.png)

* Certifikát můžete také exportovat pomocí [příkazu Exportovat-Certificate PowerShell](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Podepsat balíček

> [!note]
> Vyžaduje nuget.exe 4.6.0 nebo novější. Brzy se dotnet.exe podpora [#7939](https://github.com/NuGet/Home/issues/7939)

Podepište balíček pomocí [znaku NuGet](../reference/cli-reference/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Poskytovatel certifikátu často poskytuje adresu URL serveru pro časová razítka, kterou můžete použít pro `Timestamper` volitelné argumenty zobrazit výše. Projděte si dokumentaci ke svému poskytovateli nebo podporu pro tuto adresu URL služby.

* Můžete použít certifikát, který je k dispozici v úložišti certifikátů, nebo použít certifikát ze souboru. Viz reference k rozhraní příkazového řádku pro [znak NuGet](../reference/cli-reference/cli-ref-sign.md).
* Podepsané balíčky by měly obsahovat časové razítko, aby se zajistilo, že signatura zůstane platná, i když vypršela platnost podpisového certifikátu. V opačném případě bude operace podepsání [Upozornění](../reference/errors-and-warnings/NU3002.md).
* Můžete zobrazit podrobnosti o podpisu daného balíčku pomocí [ověření NuGet](../reference/cli-reference/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Registrace certifikátu v NuGet.org

K publikování podepsaného balíčku je třeba nejprve zaregistrovat certifikát pomocí NuGet.org. Certifikát budete potřebovat jako `.cer` soubor v binárním formátu der.

1. [Přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se k NuGet.org.
1. Přejít na `Account settings` (nebo `Manage Organization` **>** `Edit Organization` Pokud chcete zaregistrovat certifikát s účtem organizace).
1. Rozbalte `Certificates` část a vyberte `Register new` .
1. Vyhledejte a vyberte soubor certifikát, který byl dříve exportován.
  ![Registrované certifikáty](../reference/media/registered-certs.png)

**Poznámka**
* Jeden uživatel může odeslat více certifikátů a stejný certifikát může registrovat více uživatelů.
* Jakmile má uživatel zaregistrován certifikát, všechna budoucí odeslání balíčku **musí** být podepsána jedním z certifikátů. Viz [Správa požadavků na podepisování pro váš balíček v NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg) .
* Uživatelé taky můžou z účtu odebrat registrovaný certifikát. Po odebrání certifikátu se při odeslání nezdaří nové balíčky podepsané tímto certifikátem. Existující balíčky to neovlivní.

## <a name="publish-the-package"></a>Publikování balíčku

Nyní jste připraveni balíček publikovat do NuGet.org. Viz [publikování balíčků](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Vytvořit testovací certifikát

Pro účely testování můžete použít certifikáty vystavené svým držitelem. Pokud chcete vytvořit certifikát vystavený svým držitelem, použijte [příkaz prostředí PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).

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

Tento příkaz vytvoří testovací certifikát, který je k dispozici v osobním úložišti certifikátů aktuálního uživatele. Úložiště certifikátů můžete otevřít tak, že spustíte `certmgr.msc` zobrazení nově vytvořeného certifikátu.

> [!Warning]
> NuGet.org nepřijímá balíčky podepsané certifikáty s certifikátem vydaným svým držitelem.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Správa požadavků na podepisování pro váš balíček na NuGet.org
1. [Přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se k NuGet.org.

1. Přejít ke `Manage Packages`  
    ![ konfiguraci podepsaných podpisů balíčků](../reference/media/configure-package-signers.png)

* Pokud jste jediným vlastníkem balíčku, je požadováno podepisování, tj. k podepisování a publikování balíčků do NuGet.org můžete použít kterýkoli z registrovaných certifikátů.

* Pokud má balíček více vlastníků, můžete ve výchozím nastavení použít k podepsání tohoto balíčku "kterýkoli" certifikát vlastníka. Jako spoluvlastník balíčku můžete potlačit "any" se svým držitelem nebo jiným spoluvlastníky, aby to byl povinný podpis. Pokud nastavíte vlastníka, který nemá žádný registrovaný certifikát, budou povoleny nepodepsané balíčky. 

* Podobně platí, že pokud je vybrána možnost libovolná pro balíček, kde má jeden vlastník certifikát zaregistrovaný a jiný vlastník nemá zaregistrovaný certifikát, pak NuGet.org přijme buď podepsaný balíček s podpisem registrovaným v jednom z jeho vlastníků nebo nepodepsaného balíčku (protože u jednoho z vlastníků není zaregistrován žádný certifikát).

## <a name="related-articles"></a>Související články

- [Správa rozsahu důvěryhodnosti balíčků](../consume-packages/installing-signed-packages.md)
- [Reference na podepsané balíčky](../reference/Signed-Packages-Reference.md)