---
title: Podepsané balíčky
description: Požadavky na podepisování balíčků NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020509"
---
# <a name="signed-packages"></a>Podepsané balíčky

*NuGet 4.6.0+ a sady Visual Studio 2017 verze 15.6 a novější*

Balíčky NuGet může obsahovat digitální podpis, který poskytuje ochranu proti zmanipulovanou obsah. Tento podpis je vytvořen z certifikát X.509, který také přidává testování konceptů pravosti skutečné zdroji balíčku.

Podepsané balíčky poskytují nejsilnější ověření začátku do konce. Existují dva různé typy podpisů NuGet:
- **Vytváření podpis**. Podpis autora zaručuje, že balíček nebyl změněn od autora podpisu balíčku, bez ohledu na to, z které úložiště nebo co přenosu metodu doručení balíčku. Kromě toho Autor podepsané balíčky poskytnout další ověřovací mechanismus pro publikování kanál nuget.org, protože podpisový certifikát musí být zaregistrované předem. Další informace najdete v tématu [registrace certifikátů](#register-certificate-on-nugetorg).
- **Podpis úložiště**. Podpisy úložiště poskytuje záruku integrity **všechny** balíčků v úložišti, ať už jsou Autor nebo nemají, i když tyto balíčky jsou získány z jiného umístění než původní úložiště, ve kterém byly podepsané.   

Podrobnosti o vytvoření podepsaný balíček Autor najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [přihlašovací příkaz nuget](../tools/cli-ref-sign.md).

> [!Important]
> Podepisování balíčků aktuálně podporuje jenom při použití nuget.exe ve Windows. Ověření podepsaných balíčků aktuálně podporuje jenom při použití nuget.exe nebo Visual Studio na Windows.

## <a name="certificate-requirements"></a>Požadavky na certifikát

Podepisování balíčků vyžaduje certifikát, který je speciální typ certifikátu, který je platný pro podpis kódu `id-kp-codeSigning` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Certifikát musí mít navíc veřejné délka klíče RSA 2048 bitů nebo vyšší.

## <a name="get-a-code-signing-certificate"></a>Získat certifikát pro podpis kódu

Platné certifikáty lze získat od veřejné certifikační autority, jako jsou:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Globální přihlašování](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Úplný seznam certifikačních autorit důvěryhodná pro Windows můžou pocházet od [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Vytvoření testovacího certifikátu

Pro účely testování můžete použít samostatně vydané certifikáty. Chcete-li vytvořit certifikát vystavený, použijte [příkazu Powershellu New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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
> nuget.org nepřijímá žádné balíčky podepsané pomocí samostatně vydané certifikáty.

## <a name="timestamp-requirements"></a>Požadavky na časové razítko

Podepsané balíčky by měl obsahovat časového razítka RFC 3161 zajistit platnost podpisu mimo období platnosti certifikátu podpisu balíčku. Certifikát použitý k podpisu časového razítka musí být platná pro `id-kp-timeStamping` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Certifikát musí mít navíc veřejné délka klíče RSA 2048 bitů nebo vyšší.

Další technické podrobnosti najdete v [balíček technické specifikace podpis](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Požadavky na podpis na nuget.org

nuget.org mají další požadavky pro přijetí podepsaný balíček:

- Primární podpis musí být podpis autora.
- Primární podpis musí mít jediné platné časové razítko.
- Certifikátů X.509 pro podpis autora a jeho podpis časového razítka:
  - Musí mít veřejný klíč RSA 2048 bitů nebo vyšší.
  - Musí být v rozsahu období platnosti podle aktuálního času UTC v době ověřování balíčků na nuget.org.
  - Musí být propojeny s důvěryhodnou kořenovou autoritou, která je důvěryhodná pro výchozí na Windows. Balíčky, které jsou podepsané pomocí samostatně vydané certifikáty byly zamítnuty.
  - Musí být platný pro její účel: 
    - Autor podpisový certifikát musí být platný pro podepisování kódu.
    - Certifikát časového razítka musí být platný pro časových razítek.
  - Nesmí být odvolaný při podepisování čas. (Toto video asi knowable při odesílání, takže nuget.org proběhne znovu pravidelně u stav odvolání).

## <a name="register-certificate-on-nugetorg"></a>Zaregistrovat certifikát na nuget.org

Odeslat podepsaný balíček, musíte nejprve zaregistrovat certifikát s nuget.org. Budete potřebovat certifikát jako `.cer` soubor ve formátu binární kódování DER. Existující certifikát, který můžete exportovat do formátu binární kódování DER s použitím Průvodce exportem certifikátu.

![Průvodce exportem certifikátu](media/CertificateExportWizard.png)

Pokročilí uživatelé mohou exportovat certifikát pomocí [příkazu Powershellu Export certifikátu](/powershell/module/pkiclient/export-certificate.md).

Chcete-li zaregistrovat certifikát s nuget.org, přejděte na `Certificates` části na `Account settings` stránky (nebo stránku nastavení organizace) a vyberte `Register new certificate`.

![Certifikáty registrované](media/registered-certs.png)

> [!Tip]
> Jeden uživatel může odeslat svoji, že více certifikátů a stejný certifikát může být registrováno více uživatelů.

Jakmile uživatel certifikát zaregistrovaný, všechny příspěvky budoucí balíček **musí** být podepsány pomocí jednoho z certifikátů.

Uživatelé mohou také odebírat registrovaný certifikát z účtu. Po odebrání certifikát v odesílání selhat balíčky podepsaným tímto certifikátem. Nemají vliv na existující balíčky.

## <a name="configure-package-signing-requirements"></a>Konfigurovat požadavky na podepisování balíčku

Pokud jste jediným vlastníkem balíček, jsou požadované podepisující osoba. To znamená slouží všechny certifikáty registrované k podepisování balíčků a odesílání do nuget.org.

Pokud balíček obsahuje více vlastníkům, ve výchozím nastavení, "Libovolné" vlastník certifikáty lze použít k podpisu balíčku. Jako spoluvlastníka balíček můžete přepsat "Žádný" sami se sebou nebo jakékoli jiné spoluvlastník bude požadované podepisující osoba. Pokud provedete vlastníka, který nemá žádné certifikát zaregistrovaný, budou mít povolený balíčky bez znaménka. 

Podobně, pokud výchozí "Libovolné" výběru balíčky, kde má certifikát zaregistrovaný jednoho vlastníka a dalšího vlastníka nemá žádné certifikát zaregistrovaný, pak nuget.org přijímá podepsaný balíček s podpisem registrovaných jednoho ze svých vlastníků nebo bez znaménka balíček (protože jeden z vlastníků nemá žádné certifikát zaregistrovaný).

![Konfigurace podepsaných balíčků](media/configure-package-signers.png)
