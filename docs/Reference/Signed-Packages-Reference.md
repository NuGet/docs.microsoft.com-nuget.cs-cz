---
title: Podepsané balíčky odkaz | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Popis funkce balíčky se znaménkem
keywords: Přihlašovací balíčku NuGet, podpisu certifikátu
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a2a338596f7d98ded11da6fb02bafba3521249ab
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="signed-packages"></a>Podepsané balíčky

*NuGet 4.6.0+ a Visual Studio 2017 verze 15.6 a novější*

Balíčky NuGet může obsahovat digitální podpis, který poskytuje ochranu proti zmanipulovanou obsah. Tento podpis vytváří z certifikát X.509, který také přidá pravosti důkazy skutečné počátek balíčku.

Podepsané balíčky poskytují nejvyšší ověření začátku do konce. Podpisu Autor zaručuje, že balíčku nezměnil od autora podpisu balíčku, bez ohledu z které úložiště nebo co přenosu Metoda doručení balíčku.

Příjemci, kteří potřebují uzamčené prostředí může vyžadovat balíčky podepsané certifikátem pro konkrétní autora.

Kromě toho Autor podepsané balíčky poskytnout další ověřovací mechanismus pro publikování kanál nuget.org, protože podpisový certifikát musí být zaregistrovaný předem.

Podrobnosti o vytváření podepsaného balíčku najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [příkaz přihlašovací nuget](../tools/cli-ref-sign.md).

> [!Important]
> nuget.org v současné době nepřijímá podepsané balíčky. Můžete si balíčky pro publikování vlastních informačních kanálů.

## <a name="certificate-requirements"></a>Požadavky na certifikát

Podpis balíčku vyžaduje certifikát, který je speciálnímu typu certifikátu, který je platný pro podepisování kódu `id-kp-codeSigning` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Kromě toho musí mít certifikát veřejné délka klíče RSA 2048 bitů nebo vyšší.

## <a name="get-a-code-signing-certificate"></a>Získat certifikát pro podpis kódu

Platné certifikáty je možné získat od veřejné certifikační autority jako:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Globální přihlášení](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Úplný seznam certifikačních autorit, které jsou důvěryhodné v systému Windows můžete získat z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Vytvoření testovacího certifikátu

Pro účely testování můžete svým vydaných certifikátů. Chcete-li vytvořit certifikát vystavený, použijte [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) příkaz prostředí PowerShell.

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

## <a name="timestamp-requirements"></a>Požadavky na časové razítko

Podepsané balíčky by měla obsahovat časové razítko RFC 3161 zajistit platnost podpisu nad rámec balíček podepisování doby platnosti certifikátu. Musí být platná pro certifikát používaný k podepisování časové razítko `id-kp-timeStamping` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Kromě toho musí mít certifikát veřejné délka klíče RSA 2048 bitů nebo vyšší.

Další technické podrobnosti naleznete v [balíček technických specifikací podpis](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (Githubu).
