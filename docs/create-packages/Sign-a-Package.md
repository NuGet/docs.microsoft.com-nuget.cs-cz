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
# <a name="signing-nuget-packages"></a><span data-ttu-id="f11aa-103">Podepisování balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="f11aa-103">Signing NuGet Packages</span></span>

<span data-ttu-id="f11aa-104">Podepsané balíčky umožňují kontrolu integrity obsahu, která zajišťuje ochranu proti manipulaci s obsahem.</span><span class="sxs-lookup"><span data-stu-id="f11aa-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="f11aa-105">Podpis balíčku také slouží jako jediný zdroj pravdy na skutečný původ balíčku a pravost posilují balíčku pro daného příjemce.</span><span class="sxs-lookup"><span data-stu-id="f11aa-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="f11aa-106">V tomto průvodci se předpokládá, že jste už [vytvořili balíček](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f11aa-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="f11aa-107">Získání certifikátu pro podpis kódu</span><span class="sxs-lookup"><span data-stu-id="f11aa-107">Get a code signing certificate</span></span>

<span data-ttu-id="f11aa-108">Platné certifikáty mohou být získány od veřejné certifikační autority, jako je [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)atd. Úplný seznam certifikačních autorit, které jsou pro Windows důvěryhodné, můžete získat z [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .</span><span class="sxs-lookup"><span data-stu-id="f11aa-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list).</span></span>

<span data-ttu-id="f11aa-109">Pro účely testování můžete použít certifikáty vystavené svým držitelem.</span><span class="sxs-lookup"><span data-stu-id="f11aa-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="f11aa-110">Balíčky podepsané pomocí certifikátů vydaných svým držitelem ale neakceptuje NuGet.org. Další informace o [Vytvoření testovacího certifikátu](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="f11aa-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="f11aa-111">Exportovat soubor certifikátu</span><span class="sxs-lookup"><span data-stu-id="f11aa-111">Export the certificate file</span></span>

* <span data-ttu-id="f11aa-112">Existující certifikát můžete exportovat do binárního formátu DER pomocí Průvodce exportem certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f11aa-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Průvodce exportem certifikátu](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="f11aa-114">Certifikát můžete také exportovat pomocí [příkazu Exportovat-Certificate PowerShell](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="f11aa-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="f11aa-115">Podepsat balíček</span><span class="sxs-lookup"><span data-stu-id="f11aa-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="f11aa-116">Vyžaduje nuget.exe 4.6.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f11aa-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="f11aa-117">Brzy se dotnet.exe podpora [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="f11aa-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="f11aa-118">Podepište balíček pomocí [znaku NuGet](../reference/cli-reference/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="f11aa-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="f11aa-119">Poskytovatel certifikátu často poskytuje adresu URL serveru pro časová razítka, kterou můžete použít pro `Timestamper` volitelné argumenty zobrazit výše.</span><span class="sxs-lookup"><span data-stu-id="f11aa-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="f11aa-120">Projděte si dokumentaci ke svému poskytovateli nebo podporu pro tuto adresu URL služby.</span><span class="sxs-lookup"><span data-stu-id="f11aa-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="f11aa-121">Můžete použít certifikát, který je k dispozici v úložišti certifikátů, nebo použít certifikát ze souboru.</span><span class="sxs-lookup"><span data-stu-id="f11aa-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="f11aa-122">Viz reference k rozhraní příkazového řádku pro [znak NuGet](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="f11aa-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="f11aa-123">Podepsané balíčky by měly obsahovat časové razítko, aby se zajistilo, že signatura zůstane platná, i když vypršela platnost podpisového certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f11aa-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="f11aa-124">V opačném případě bude operace podepsání [Upozornění](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="f11aa-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="f11aa-125">Můžete zobrazit podrobnosti o podpisu daného balíčku pomocí [ověření NuGet](../reference/cli-reference/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="f11aa-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="f11aa-126">Registrace certifikátu v NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f11aa-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="f11aa-127">K publikování podepsaného balíčku je třeba nejprve zaregistrovat certifikát pomocí NuGet.org. Certifikát budete potřebovat jako `.cer` soubor v binárním formátu der.</span><span class="sxs-lookup"><span data-stu-id="f11aa-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="f11aa-128">[Přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se k NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f11aa-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="f11aa-129">Přejít na `Account settings` (nebo `Manage Organization` **>** `Edit Organization` Pokud chcete zaregistrovat certifikát s účtem organizace).</span><span class="sxs-lookup"><span data-stu-id="f11aa-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organization` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="f11aa-130">Rozbalte `Certificates` část a vyberte `Register new` .</span><span class="sxs-lookup"><span data-stu-id="f11aa-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="f11aa-131">Vyhledejte a vyberte soubor certifikát, který byl dříve exportován.</span><span class="sxs-lookup"><span data-stu-id="f11aa-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="f11aa-132">![Registrované certifikáty](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="f11aa-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="f11aa-133">**Poznámka**</span><span class="sxs-lookup"><span data-stu-id="f11aa-133">**Note**</span></span>
* <span data-ttu-id="f11aa-134">Jeden uživatel může odeslat více certifikátů a stejný certifikát může registrovat více uživatelů.</span><span class="sxs-lookup"><span data-stu-id="f11aa-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="f11aa-135">Jakmile má uživatel zaregistrován certifikát, všechna budoucí odeslání balíčku **musí** být podepsána jedním z certifikátů.</span><span class="sxs-lookup"><span data-stu-id="f11aa-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="f11aa-136">Viz [Správa požadavků na podepisování pro váš balíček v NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg) .</span><span class="sxs-lookup"><span data-stu-id="f11aa-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="f11aa-137">Uživatelé taky můžou z účtu odebrat registrovaný certifikát.</span><span class="sxs-lookup"><span data-stu-id="f11aa-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="f11aa-138">Po odebrání certifikátu se při odeslání nezdaří nové balíčky podepsané tímto certifikátem.</span><span class="sxs-lookup"><span data-stu-id="f11aa-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="f11aa-139">Existující balíčky to neovlivní.</span><span class="sxs-lookup"><span data-stu-id="f11aa-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f11aa-140">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="f11aa-140">Publish the package</span></span>

<span data-ttu-id="f11aa-141">Nyní jste připraveni balíček publikovat do NuGet.org. Viz [publikování balíčků](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f11aa-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="f11aa-142">Vytvořit testovací certifikát</span><span class="sxs-lookup"><span data-stu-id="f11aa-142">Create a test certificate</span></span>

<span data-ttu-id="f11aa-143">Pro účely testování můžete použít certifikáty vystavené svým držitelem.</span><span class="sxs-lookup"><span data-stu-id="f11aa-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="f11aa-144">Pokud chcete vytvořit certifikát vystavený svým držitelem, použijte [příkaz prostředí PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="f11aa-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="f11aa-145">Tento příkaz vytvoří testovací certifikát, který je k dispozici v osobním úložišti certifikátů aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="f11aa-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="f11aa-146">Úložiště certifikátů můžete otevřít tak, že spustíte `certmgr.msc` zobrazení nově vytvořeného certifikátu.</span><span class="sxs-lookup"><span data-stu-id="f11aa-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="f11aa-147">NuGet.org nepřijímá balíčky podepsané certifikáty s certifikátem vydaným svým držitelem.</span><span class="sxs-lookup"><span data-stu-id="f11aa-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="f11aa-148">Správa požadavků na podepisování pro váš balíček na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f11aa-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="f11aa-149">[Přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se k NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f11aa-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="f11aa-150">Přejít ke `Manage Packages`  
    ![ konfiguraci podepsaných podpisů balíčků](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="f11aa-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="f11aa-151">Pokud jste jediným vlastníkem balíčku, je požadováno podepisování, tj. k podepisování a publikování balíčků do NuGet.org můžete použít kterýkoli z registrovaných certifikátů.</span><span class="sxs-lookup"><span data-stu-id="f11aa-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="f11aa-152">Pokud má balíček více vlastníků, můžete ve výchozím nastavení použít k podepsání tohoto balíčku "kterýkoli" certifikát vlastníka.</span><span class="sxs-lookup"><span data-stu-id="f11aa-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="f11aa-153">Jako spoluvlastník balíčku můžete potlačit "any" se svým držitelem nebo jiným spoluvlastníky, aby to byl povinný podpis.</span><span class="sxs-lookup"><span data-stu-id="f11aa-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="f11aa-154">Pokud nastavíte vlastníka, který nemá žádný registrovaný certifikát, budou povoleny nepodepsané balíčky.</span><span class="sxs-lookup"><span data-stu-id="f11aa-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="f11aa-155">Podobně platí, že pokud je vybrána možnost libovolná pro balíček, kde má jeden vlastník certifikát zaregistrovaný a jiný vlastník nemá zaregistrovaný certifikát, pak NuGet.org přijme buď podepsaný balíček s podpisem registrovaným v jednom z jeho vlastníků nebo nepodepsaného balíčku (protože u jednoho z vlastníků není zaregistrován žádný certifikát).</span><span class="sxs-lookup"><span data-stu-id="f11aa-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="f11aa-156">Související články</span><span class="sxs-lookup"><span data-stu-id="f11aa-156">Related articles</span></span>

- [<span data-ttu-id="f11aa-157">Správa rozsahu důvěryhodnosti balíčků</span><span class="sxs-lookup"><span data-stu-id="f11aa-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="f11aa-158">Reference na podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="f11aa-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)