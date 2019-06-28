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
# <a name="signing-nuget-packages"></a><span data-ttu-id="54fb5-103">Podepisují se balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="54fb5-103">Signing NuGet Packages</span></span>

<span data-ttu-id="54fb5-104">Podepsané balíčky umožňuje kontroly ověření obsahu, integrity, která poskytuje ochranu proti falšování obsahu.</span><span class="sxs-lookup"><span data-stu-id="54fb5-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="54fb5-105">Podpis balíčku také slouží jako jediný zdroj pravdivých informací o skutečné původu balíček a poznámkových bloků zvýší pravosti balíčku pro spotřebitele.</span><span class="sxs-lookup"><span data-stu-id="54fb5-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="54fb5-106">Tento průvodce to předpokládá, že už máte [vytvořil balíček](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="54fb5-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="54fb5-107">Získat certifikát pro podpis kódu</span><span class="sxs-lookup"><span data-stu-id="54fb5-107">Get a code signing certificate</span></span>

<span data-ttu-id="54fb5-108">Platné certifikáty mohou pocházet od veřejné certifikační autority, jako [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [globální přihlašování](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)atd. Úplný seznam certifikačních autorit důvěryhodná pro Windows můžou pocházet od [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="54fb5-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="54fb5-109">Pro účely testování můžete použít samostatně vydané certifikáty.</span><span class="sxs-lookup"><span data-stu-id="54fb5-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="54fb5-110">Balíčky, které jsou podepsány pomocí samostatně vydané certifikáty nejsou však přijal NuGet.org. Další informace o [vytvoření testovacího certifikátu](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="54fb5-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="54fb5-111">Exportovat soubor certifikátu</span><span class="sxs-lookup"><span data-stu-id="54fb5-111">Export the certificate file</span></span>

* <span data-ttu-id="54fb5-112">Existující certifikát, který můžete exportovat do formátu binární kódování DER s použitím Průvodce exportem certifikátu.</span><span class="sxs-lookup"><span data-stu-id="54fb5-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Průvodce exportem certifikátu](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="54fb5-114">Můžete také exportovat certifikát pomocí [příkazu Powershellu Export certifikátu](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="54fb5-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="54fb5-115">Podepište balíček</span><span class="sxs-lookup"><span data-stu-id="54fb5-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="54fb5-116">Vyžaduje nuget.exe 4.6.0 nebo novější</span><span class="sxs-lookup"><span data-stu-id="54fb5-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="54fb5-117">Podepsání balíčku pomocí [nuget přihlašování](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="54fb5-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="54fb5-118">Poskytovatel certifikátu často také obsahuje adresu URL serveru časového razítka, která vám pomůže `Timestamper` nepovinný argument zobrazit výše.</span><span class="sxs-lookup"><span data-stu-id="54fb5-118">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="54fb5-119">Poraďte se s dokumentaci poskytovatele nebo podporu pro tuto adresu URL služby.</span><span class="sxs-lookup"><span data-stu-id="54fb5-119">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="54fb5-120">Můžete použít certifikát k dispozici v úložišti certifikátů nebo použití certifikátu ze souboru.</span><span class="sxs-lookup"><span data-stu-id="54fb5-120">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="54fb5-121">Viz odkaz pro rozhraní příkazového řádku [nuget přihlašování](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="54fb5-121">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="54fb5-122">Podepsané balíčky by měly zahrnovat časové razítko, abyste měli jistotu, že podpis zůstává platná, pokud vypršela platnost podpisového certifikátu.</span><span class="sxs-lookup"><span data-stu-id="54fb5-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="54fb5-123">Jinak operace přihlášení vytvoří [upozornění](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="54fb5-123">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="54fb5-124">Můžete zobrazit podrobnosti o podpisu daného balíčku pomocí [ověřte nuget](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="54fb5-124">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="54fb5-125">Zaregistrovat certifikát na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="54fb5-125">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="54fb5-126">Chcete-li publikovat podepsaný balíček, musí nejprve zaregistrovat certifikát s NuGet.org. Budete potřebovat certifikát jako `.cer` soubor ve formátu binární kódování DER.</span><span class="sxs-lookup"><span data-stu-id="54fb5-126">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="54fb5-127">[Přihlaste se](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="54fb5-127">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="54fb5-128">Přejděte na `Account settings` (nebo `Manage Organization` **>** `Edit Organziation` Pokud byste chtěli zaregistrovat certifikát pomocí účtu organizace).</span><span class="sxs-lookup"><span data-stu-id="54fb5-128">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="54fb5-129">Rozbalte `Certificates` a vyberte `Register new`.</span><span class="sxs-lookup"><span data-stu-id="54fb5-129">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="54fb5-130">Procházet a vyberte soubor certifikát, který jste dříve exportovali.</span><span class="sxs-lookup"><span data-stu-id="54fb5-130">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="54fb5-131">![Certifikáty registrované](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="54fb5-131">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="54fb5-132">**Poznámka**</span><span class="sxs-lookup"><span data-stu-id="54fb5-132">**Note**</span></span>
* <span data-ttu-id="54fb5-133">Jeden uživatel může odeslat svoji, že více certifikátů a stejný certifikát může být registrováno více uživatelů.</span><span class="sxs-lookup"><span data-stu-id="54fb5-133">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="54fb5-134">Jakmile uživatel certifikát zaregistrovaný, všechny příspěvky budoucí balíček **musí** být podepsány pomocí jednoho z certifikátů.</span><span class="sxs-lookup"><span data-stu-id="54fb5-134">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="54fb5-135">Zobrazit [spravovat podepisování požadavky pro vaše balíčků na NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="54fb5-135">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="54fb5-136">Uživatelé mohou také odebírat registrovaný certifikát z účtu.</span><span class="sxs-lookup"><span data-stu-id="54fb5-136">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="54fb5-137">Po odebrání certifikátu se nezdaří nové balíčky, které jsou podepsané pomocí tohoto certifikátu na odeslání.</span><span class="sxs-lookup"><span data-stu-id="54fb5-137">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="54fb5-138">Nemají vliv na existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="54fb5-138">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="54fb5-139">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="54fb5-139">Publish the package</span></span>

<span data-ttu-id="54fb5-140">Nyní jste připraveni publikovat balíček na NuGet.org. Zobrazit [publikování balíčků](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="54fb5-140">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="54fb5-141">Vytvoření testovacího certifikátu</span><span class="sxs-lookup"><span data-stu-id="54fb5-141">Create a test certificate</span></span>

<span data-ttu-id="54fb5-142">Pro účely testování můžete použít samostatně vydané certifikáty.</span><span class="sxs-lookup"><span data-stu-id="54fb5-142">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="54fb5-143">Chcete-li vytvořit certifikát vystavený, použijte [příkazu Powershellu New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="54fb5-143">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="54fb5-144">Tento příkaz vytvoří testovací certifikát k dispozici v úložišti osobních certifikátů aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="54fb5-144">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="54fb5-145">Můžete otevřít úložiště certifikátů spuštěním `certmgr.msc` zobrazíte nově vytvořeného certifikátu.</span><span class="sxs-lookup"><span data-stu-id="54fb5-145">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="54fb5-146">NuGet.org nepřijímá žádné balíčky podepsané pomocí samostatně vydané certifikáty.</span><span class="sxs-lookup"><span data-stu-id="54fb5-146">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="54fb5-147">Spravovat podepisování požadavky pro vaše balíčků na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="54fb5-147">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="54fb5-148">[Přihlaste se](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="54fb5-148">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="54fb5-149">Přejděte na `Manage Packages`  
    ![konfigurace podepsaných balíčků](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="54fb5-149">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="54fb5-150">Pokud jste jediným vlastníkem balíček, jsou požadované podepisující osoba to znamená všechny certifikáty registrované můžete použít k podepisování a publikovat vaše balíčky NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="54fb5-150">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="54fb5-151">Pokud balíček obsahuje více vlastníkům, ve výchozím nastavení, "Libovolné" vlastník certifikáty lze použít k podpisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="54fb5-151">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="54fb5-152">Jako spoluvlastníka balíček můžete přepsat "Žádný" sami se sebou nebo jakékoli jiné spoluvlastník bude požadované podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="54fb5-152">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="54fb5-153">Pokud provedete vlastníka, který nemá žádné certifikát zaregistrovaný, budou mít povolený balíčky bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="54fb5-153">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="54fb5-154">Podobně, pokud výchozí "Libovolné" výběru balíčky, kde má certifikát zaregistrovaný jednoho vlastníka a dalšího vlastníka nemá žádné certifikát zaregistrovaný, pak NuGet.org přijímá podepsaný balíček s podpisem registrovaných jednoho ze svých vlastníků nebo bez znaménka balíček (protože jeden z vlastníků nemá žádné certifikát zaregistrovaný).</span><span class="sxs-lookup"><span data-stu-id="54fb5-154">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="54fb5-155">Související články</span><span class="sxs-lookup"><span data-stu-id="54fb5-155">Related articles</span></span>

- [<span data-ttu-id="54fb5-156">Spravovat hranice vztahu důvěryhodnosti balíčku</span><span class="sxs-lookup"><span data-stu-id="54fb5-156">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="54fb5-157">Podepsané balíčky odkaz</span><span class="sxs-lookup"><span data-stu-id="54fb5-157">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
