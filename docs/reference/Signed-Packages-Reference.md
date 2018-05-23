---
title: Podepsané balíčky
description: Požadavky pro podepisování balíčku NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a>Podepsané balíčky

*NuGet 4.6.0+ a Visual Studio 2017 verze 15.6 a novější*

Balíčky NuGet může obsahovat digitální podpis, který poskytuje ochranu proti zmanipulovanou obsah. Tento podpis vytváří z certifikát X.509, který také přidá pravosti důkazy skutečné počátek balíčku.

Podepsané balíčky poskytují nejvyšší ověření začátku do konce. Podpisu Autor zaručuje, že balíčku nezměnil od autora podpisu balíčku, bez ohledu z které úložiště nebo co přenosu Metoda doručení balíčku.

Kromě toho Autor podepsané balíčky poskytnout další ověřovací mechanismus pro publikování kanál nuget.org, protože podpisový certifikát musí být zaregistrovaný předem. Další informace najdete v tématu [zaregistrovat certifikáty](#register-certificate-on-nugetorg).

Podrobnosti o vytváření podepsaného balíčku najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [příkaz přihlašovací nuget](../tools/cli-ref-sign.md).

> [!Important]
> Podpis balíčku se aktuálně podporuje jenom při použití nuget.exe v systému Windows. Ověření podepsaný balíčků se aktuálně podporuje jenom při použití nuget.exe nebo Visual Studio v systému Windows.

## <a name="certificate-requirements"></a>Požadavky na certifikát

Podpis balíčku vyžaduje certifikát, který je speciálnímu typu certifikátu, který je platný pro podepisování kódu `id-kp-codeSigning` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Kromě toho musí mít certifikát veřejné délka klíče RSA 2048 bitů nebo vyšší.

## <a name="get-a-code-signing-certificate"></a>Získat certifikát pro podpis kódu

Platné certifikáty lze získat od veřejné certifikační autority jako:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Globální přihlášení](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Úplný seznam certifikačních autorit, které jsou důvěryhodné v systému Windows můžete získat z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Vytvoření testovacího certifikátu

Pro účely testování můžete svým vydaných certifikátů. Chcete-li vytvořit certifikát vystavený, použijte [příkazu New-SelfSignedCertificate Powershellu](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Tento příkaz vytvoří testovací certifikát k dispozici v úložišti osobních certifikátů aktuálního uživatele. Úložiště certifikátů můžete otevřít tak, že spustíte `certmgr.msc` zobrazíte nově vytvořený certifikát.

> [!Warning]
> nuget.org nepřijímá balíčky podepsán svým vydaných certifikátů.

## <a name="timestamp-requirements"></a>Požadavky na časové razítko

Podepsané balíčky by měla obsahovat časové razítko RFC 3161 zajistit platnost podpisu nad rámec balíček podepisování doby platnosti certifikátu. Musí být platná pro certifikát používaný k podepisování časové razítko `id-kp-timeStamping` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Kromě toho musí mít certifikát veřejné délka klíče RSA 2048 bitů nebo vyšší.

Další technické podrobnosti naleznete v [balíček technických specifikací podpis](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (Githubu).

## <a name="signature-requirements-on-nugetorg"></a>Požadavky na podpis v nuget.org

nuget.org mají další požadavky pro přijetí podepsaného balíčku:

- Primární podpis musí být podpisu autora.
- Primární podpis musí mít jeden platný časové razítko.
- Certifikáty X.509 pro podpis autora a časové razítko podpis:
  - Musí mít veřejný klíč RSA 2048 bitů nebo vyšší.
  - Musí být v rozsahu období platnosti na aktuální čas UTC během ověřování balíčku na nuget.org.
  - Musí být propojeny s důvěryhodnou kořenovou autoritou, která je důvěryhodná ve výchozím nastavení v systému Windows. Balíčky s samoobslužné vystavené certifikáty podepsané odmítají.
  - Musí být platná pro jeho účel: 
    - Autor podpisový certifikát musí být platná pro podepisování kódu.
    - Certifikát časového razítka musí být platná pro vytvoření časového razítka.
  - Nesmí být odvolaný při podepisování čas. (Nemusí to být knowable během odesílání, takže nuget.org proběhne znovu pravidelně u stav odvolání).

## <a name="register-certificate-on-nugetorg"></a>Registrovat certifikát v nuget.org

Odeslat podepsaný balíček, je nutné nejprve zaregistrovat certifikát s nuget.org. Budete potřebovat certifikát jako `.cer` soubor v binárním formátu DER. Existující certifikát můžete exportovat do binárního formátu DER pomocí Průvodce exportem certifikátu.

![Průvodce exportem certifikátu](media/CertificateExportWizard.png)

Pokročilí uživatelé můžete exportovat certifikát pomocí [příkaz prostředí PowerShell Export certifikátu](/powershell/module/pkiclient/export-certificate.md).

Chcete-li zaregistrovat certifikát s nuget.org, přejděte na `Certificates` části na `Account settings` stránku (nebo organizace nastavení) a vyberte `Register new certificate`.

![Certifikáty registrované](media/registered-certs.png)

> [!Tip]
> Jeden uživatel může odeslat, že více certifikátů a stejný certifikát může být registrováno více uživatelů.

Jakmile uživatel, který má certifikát registrován, všechny budoucí balíček odesílání **musí** být podepsány pomocí jednoho z certifikátů.

Uživatelé mohou také odebrat registrovaný certifikát z účtu. Odebraný certifikát podepsaným tímto certifikátem balíčky nezdaří na odeslání. Ovlivněné nejsou existující balíčky.

## <a name="configure-package-signing-requirements"></a>Konfigurace balíčku požadavky na registraci

Pokud jste pouze vlastník balíčku, se vyžaduje podepisující osoba. To znamená všechny certifikáty registrované můžete použít k podepisování vlastních balíčků a odeslání nuget.org.

Pokud balíček obsahuje více vlastníky, ve výchozím nastavení, certifikáty "Žádné" vlastníka můžete použít k podpisu balíčku. Jako spoluvlastník balíček můžete přepsat "Žádný" sami se sebou nebo jakékoli jiné spoluvlastník být požadované podepisující osoba. Pokud provedete vlastníka, který nemá zaregistrovaný žádný certifikát, budou mít povolený nepodepsaných balíčků. 

Podobně, pokud výchozí možnost "Žádné" pro balíček, kde má jednoho vlastníka certifikát registrován a jiný vlastník nemá zaregistrovaný žádný certifikát, pak nuget.org přijímá podepsaného balíčku podpisem zaregistrován pomocí jednoho z vlastníků nebo Nepodepsaný balíčku (protože jeden z vlastníci není zaregistrovaný žádný certifikát).

![Konfigurace balíčku podepisující osoby](media/configure-package-signers.png)
