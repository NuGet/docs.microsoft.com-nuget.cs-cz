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
# <a name="signed-packages"></a><span data-ttu-id="0399c-104">Podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="0399c-104">Signed packages</span></span>

<span data-ttu-id="0399c-105">*NuGet 4.6.0+ a Visual Studio 2017 verze 15.6 a novější*</span><span class="sxs-lookup"><span data-stu-id="0399c-105">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="0399c-106">Balíčky NuGet může obsahovat digitální podpis, který poskytuje ochranu proti zmanipulovanou obsah.</span><span class="sxs-lookup"><span data-stu-id="0399c-106">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="0399c-107">Tento podpis vytváří z certifikát X.509, který také přidá pravosti důkazy skutečné počátek balíčku.</span><span class="sxs-lookup"><span data-stu-id="0399c-107">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="0399c-108">Podepsané balíčky poskytují nejvyšší ověření začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="0399c-108">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="0399c-109">Podpisu Autor zaručuje, že balíčku nezměnil od autora podpisu balíčku, bez ohledu z které úložiště nebo co přenosu Metoda doručení balíčku.</span><span class="sxs-lookup"><span data-stu-id="0399c-109">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="0399c-110">Příjemci, kteří potřebují uzamčené prostředí může vyžadovat balíčky podepsané certifikátem pro konkrétní autora.</span><span class="sxs-lookup"><span data-stu-id="0399c-110">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="0399c-111">Kromě toho Autor podepsané balíčky poskytnout další ověřovací mechanismus pro publikování kanál nuget.org, protože podpisový certifikát musí být zaregistrovaný předem.</span><span class="sxs-lookup"><span data-stu-id="0399c-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="0399c-112">Podrobnosti o vytváření podepsaného balíčku najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [příkaz přihlašovací nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="0399c-112">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="0399c-113">nuget.org v současné době nepřijímá podepsané balíčky.</span><span class="sxs-lookup"><span data-stu-id="0399c-113">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="0399c-114">Můžete si balíčky pro publikování vlastních informačních kanálů.</span><span class="sxs-lookup"><span data-stu-id="0399c-114">You can sign packages for publishing to custom feeds.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="0399c-115">Požadavky na certifikát</span><span class="sxs-lookup"><span data-stu-id="0399c-115">Certificate requirements</span></span>

<span data-ttu-id="0399c-116">Podpis balíčku vyžaduje certifikát, který je speciálnímu typu certifikátu, který je platný pro podepisování kódu `id-kp-codeSigning` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="0399c-116">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="0399c-117">Kromě toho musí mít certifikát veřejné délka klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="0399c-117">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="0399c-118">Získat certifikát pro podpis kódu</span><span class="sxs-lookup"><span data-stu-id="0399c-118">Get a code signing certificate</span></span>

<span data-ttu-id="0399c-119">Platné certifikáty je možné získat od veřejné certifikační autority jako:</span><span class="sxs-lookup"><span data-stu-id="0399c-119">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="0399c-120">Symantec</span><span class="sxs-lookup"><span data-stu-id="0399c-120">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="0399c-121">DigiCert</span><span class="sxs-lookup"><span data-stu-id="0399c-121">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="0399c-122">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="0399c-122">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="0399c-123">Globální přihlášení</span><span class="sxs-lookup"><span data-stu-id="0399c-123">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="0399c-124">Comodo</span><span class="sxs-lookup"><span data-stu-id="0399c-124">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="0399c-125">Certum</span><span class="sxs-lookup"><span data-stu-id="0399c-125">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="0399c-126">Úplný seznam certifikačních autorit, které jsou důvěryhodné v systému Windows můžete získat z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="0399c-126">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="0399c-127">Vytvoření testovacího certifikátu</span><span class="sxs-lookup"><span data-stu-id="0399c-127">Create a test certificate</span></span>

<span data-ttu-id="0399c-128">Pro účely testování můžete svým vydaných certifikátů.</span><span class="sxs-lookup"><span data-stu-id="0399c-128">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="0399c-129">Chcete-li vytvořit certifikát vystavený, použijte [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) příkaz prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0399c-129">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="0399c-130">Tento příkaz vytvoří testovací certifikát k dispozici v úložišti osobních certifikátů aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="0399c-130">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="0399c-131">Úložiště certifikátů můžete otevřít tak, že spustíte `certmgr.msc` zobrazíte nově vytvořený certifikát.</span><span class="sxs-lookup"><span data-stu-id="0399c-131">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="0399c-132">Požadavky na časové razítko</span><span class="sxs-lookup"><span data-stu-id="0399c-132">Timestamp requirements</span></span>

<span data-ttu-id="0399c-133">Podepsané balíčky by měla obsahovat časové razítko RFC 3161 zajistit platnost podpisu nad rámec balíček podepisování doby platnosti certifikátu.</span><span class="sxs-lookup"><span data-stu-id="0399c-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="0399c-134">Musí být platná pro certifikát používaný k podepisování časové razítko `id-kp-timeStamping` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="0399c-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="0399c-135">Kromě toho musí mít certifikát veřejné délka klíče RSA 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="0399c-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="0399c-136">Další technické podrobnosti naleznete v [balíček technických specifikací podpis](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (Githubu).</span><span class="sxs-lookup"><span data-stu-id="0399c-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
