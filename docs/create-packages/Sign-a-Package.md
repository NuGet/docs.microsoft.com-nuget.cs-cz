---
title: Podepisování balíčků NuGet
description: Vysvětluje, jak lze pomocí podepsaných balíčků povolit ověření integrity obsahu.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 85a862852761b68db882abdc1ca0e84d83d95f07
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317639"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="1ac54-103">Podepisování balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="1ac54-103">Signing NuGet Packages</span></span>

<span data-ttu-id="1ac54-104">Podepsané balíčky umožňují kontrolu integrity obsahu, která zajišťuje ochranu proti manipulaci s obsahem.</span><span class="sxs-lookup"><span data-stu-id="1ac54-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="1ac54-105">Podpis balíčku také slouží jako jediný zdroj pravdy na skutečný původ balíčku a pravost posilují balíčku pro daného příjemce.</span><span class="sxs-lookup"><span data-stu-id="1ac54-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="1ac54-106">V tomto průvodci se předpokládá, že jste už [vytvořili balíček](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="1ac54-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="1ac54-107">Získání certifikátu pro podpis kódu</span><span class="sxs-lookup"><span data-stu-id="1ac54-107">Get a code signing certificate</span></span>

<span data-ttu-id="1ac54-108">Platné certifikáty mohou být získány od veřejné certifikační autority, jako je [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)atd. Úplný seznam certifikačních autorit, které jsou pro Windows důvěryhodné, můžete [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners)získat z.</span><span class="sxs-lookup"><span data-stu-id="1ac54-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="1ac54-109">Pro účely testování můžete použít certifikáty vystavené svým držitelem.</span><span class="sxs-lookup"><span data-stu-id="1ac54-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="1ac54-110">Balíčky podepsané pomocí certifikátů vydaných svým držitelem ale neakceptuje NuGet.org. Další informace o [Vytvoření testovacího certifikátu](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="1ac54-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="1ac54-111">Exportovat soubor certifikátu</span><span class="sxs-lookup"><span data-stu-id="1ac54-111">Export the certificate file</span></span>

* <span data-ttu-id="1ac54-112">Existující certifikát můžete exportovat do binárního formátu DER pomocí Průvodce exportem certifikátu.</span><span class="sxs-lookup"><span data-stu-id="1ac54-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Průvodce exportem certifikátu](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="1ac54-114">Certifikát můžete také exportovat pomocí [příkazu Exportovat-Certificate PowerShell](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="1ac54-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="1ac54-115">Podepsat balíček</span><span class="sxs-lookup"><span data-stu-id="1ac54-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="1ac54-116">Vyžaduje NuGet. exe 4.6.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="1ac54-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="1ac54-117">Podepište balíček pomocí [znaku NuGet](../reference/cli-reference/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="1ac54-117">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="1ac54-118">Poskytovatel certifikátu často poskytuje adresu URL serveru pro časová razítka, kterou můžete použít pro `Timestamper` volitelné argumenty zobrazit výše.</span><span class="sxs-lookup"><span data-stu-id="1ac54-118">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="1ac54-119">Projděte si dokumentaci ke svému poskytovateli nebo podporu pro tuto adresu URL služby.</span><span class="sxs-lookup"><span data-stu-id="1ac54-119">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="1ac54-120">Můžete použít certifikát, který je k dispozici v úložišti certifikátů, nebo použít certifikát ze souboru.</span><span class="sxs-lookup"><span data-stu-id="1ac54-120">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="1ac54-121">Viz reference k rozhraní příkazového řádku pro [znak NuGet](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="1ac54-121">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="1ac54-122">Podepsané balíčky by měly obsahovat časové razítko, aby se zajistilo, že signatura zůstane platná, i když vypršela platnost podpisového certifikátu.</span><span class="sxs-lookup"><span data-stu-id="1ac54-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="1ac54-123">V opačném případě bude operace podepsání [Upozornění](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="1ac54-123">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="1ac54-124">Můžete zobrazit podrobnosti o podpisu daného balíčku pomocí [ověření NuGet](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="1ac54-124">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="1ac54-125">Registrace certifikátu v NuGet.org</span><span class="sxs-lookup"><span data-stu-id="1ac54-125">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="1ac54-126">K publikování podepsaného balíčku je třeba nejprve zaregistrovat certifikát pomocí NuGet.org. Certifikát budete potřebovat jako `.cer` soubor v binárním formátu der.</span><span class="sxs-lookup"><span data-stu-id="1ac54-126">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="1ac54-127">[](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Přihlaste se k NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="1ac54-127">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="1ac54-128">Přejít na `Account settings` (nebo `Manage Organization` **>** Pokudchcetezaregistrovatcertifikáts`Edit Organziation` účtem organizace).</span><span class="sxs-lookup"><span data-stu-id="1ac54-128">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="1ac54-129">Rozbalte část a vyberte `Register new`. `Certificates`</span><span class="sxs-lookup"><span data-stu-id="1ac54-129">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="1ac54-130">Vyhledejte a vyberte soubor certifikát, který byl dříve exportován.</span><span class="sxs-lookup"><span data-stu-id="1ac54-130">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="1ac54-131">![Registrované certifikáty](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="1ac54-131">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="1ac54-132">**Poznámka**</span><span class="sxs-lookup"><span data-stu-id="1ac54-132">**Note**</span></span>
* <span data-ttu-id="1ac54-133">Jeden uživatel může odeslat více certifikátů a stejný certifikát může registrovat více uživatelů.</span><span class="sxs-lookup"><span data-stu-id="1ac54-133">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="1ac54-134">Jakmile má uživatel zaregistrován certifikát, všechna budoucí odeslání balíčku **musí** být podepsána jedním z certifikátů.</span><span class="sxs-lookup"><span data-stu-id="1ac54-134">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="1ac54-135">Viz [Správa požadavků na podepisování pro váš balíček v NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg) .</span><span class="sxs-lookup"><span data-stu-id="1ac54-135">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="1ac54-136">Uživatelé taky můžou z účtu odebrat registrovaný certifikát.</span><span class="sxs-lookup"><span data-stu-id="1ac54-136">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="1ac54-137">Po odebrání certifikátu se při odeslání nezdaří nové balíčky podepsané tímto certifikátem.</span><span class="sxs-lookup"><span data-stu-id="1ac54-137">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="1ac54-138">Existující balíčky to neovlivní.</span><span class="sxs-lookup"><span data-stu-id="1ac54-138">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="1ac54-139">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="1ac54-139">Publish the package</span></span>

<span data-ttu-id="1ac54-140">Nyní jste připraveni balíček publikovat do NuGet.org. Viz [publikování balíčků](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="1ac54-140">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="1ac54-141">Vytvořit testovací certifikát</span><span class="sxs-lookup"><span data-stu-id="1ac54-141">Create a test certificate</span></span>

<span data-ttu-id="1ac54-142">Pro účely testování můžete použít certifikáty vystavené svým držitelem.</span><span class="sxs-lookup"><span data-stu-id="1ac54-142">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="1ac54-143">Pokud chcete vytvořit certifikát vystavený svým držitelem, použijte [příkaz prostředí PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="1ac54-143">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="1ac54-144">Tento příkaz vytvoří testovací certifikát, který je k dispozici v osobním úložišti certifikátů aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="1ac54-144">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="1ac54-145">Úložiště certifikátů můžete otevřít tak, že spustíte `certmgr.msc` zobrazení nově vytvořeného certifikátu.</span><span class="sxs-lookup"><span data-stu-id="1ac54-145">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="1ac54-146">NuGet.org nepřijímá balíčky podepsané certifikáty s certifikátem vydaným svým držitelem.</span><span class="sxs-lookup"><span data-stu-id="1ac54-146">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="1ac54-147">Správa požadavků na podepisování pro váš balíček na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="1ac54-147">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="1ac54-148">[](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Přihlaste se k NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="1ac54-148">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="1ac54-149">Přejít ke `Manage Packages`  
   konfiguraci podepsanýchpodpisůbalíčků![](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="1ac54-149">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="1ac54-150">Pokud jste jediným vlastníkem balíčku, je požadováno podepisování, tj. k podepisování a publikování balíčků do NuGet.org můžete použít kterýkoli z registrovaných certifikátů.</span><span class="sxs-lookup"><span data-stu-id="1ac54-150">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="1ac54-151">Pokud má balíček více vlastníků, můžete ve výchozím nastavení použít k podepsání tohoto balíčku "kterýkoli" certifikát vlastníka.</span><span class="sxs-lookup"><span data-stu-id="1ac54-151">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="1ac54-152">Jako spoluvlastník balíčku můžete potlačit "any" se svým držitelem nebo jiným spoluvlastníky, aby to byl povinný podpis.</span><span class="sxs-lookup"><span data-stu-id="1ac54-152">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="1ac54-153">Pokud nastavíte vlastníka, který nemá žádný registrovaný certifikát, budou povoleny nepodepsané balíčky.</span><span class="sxs-lookup"><span data-stu-id="1ac54-153">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="1ac54-154">Podobně platí, že pokud je vybrána možnost libovolná pro balíček, kde jeden vlastník má registrovaný certifikát a jiný vlastník nemá zaregistrován žádný certifikát, NuGet.org přijme buď podepsaný balíček s podpisem registrovaným jedním z jeho vlastníků nebo Nepodepsaný balíček (protože u jednoho z vlastníků není zaregistrovaný žádný certifikát).</span><span class="sxs-lookup"><span data-stu-id="1ac54-154">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="1ac54-155">Související články</span><span class="sxs-lookup"><span data-stu-id="1ac54-155">Related articles</span></span>

- [<span data-ttu-id="1ac54-156">Správa rozsahu důvěryhodnosti balíčků</span><span class="sxs-lookup"><span data-stu-id="1ac54-156">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="1ac54-157">Reference na podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="1ac54-157">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
