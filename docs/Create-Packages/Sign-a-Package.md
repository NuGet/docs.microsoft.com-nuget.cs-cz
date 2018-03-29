---
title: Podepisování balíčků NuGet | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Vysvětluje, jak podepsaný balíčků slouží k povolení ověření obsahu integrity.
keywords: Balíček NuGet podepisování NuGet zabezpečení, vytváření balíčků podepsané
ms.reviewer:
- karann-msft
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61d90066e8cf75c8f49c7cc9390d45e1cd8afd0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="04b9c-104">Podepisování balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="04b9c-104">Signing NuGet Packages</span></span>

<span data-ttu-id="04b9c-105">Podpis balíčku je proces, který zajistí, že balíček nebyl změněn od svého vytvoření.</span><span class="sxs-lookup"><span data-stu-id="04b9c-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04b9c-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="04b9c-106">Prerequisites</span></span>

1. <span data-ttu-id="04b9c-107">Balíček ( `.nupkg` souboru) pro přihlášení.</span><span class="sxs-lookup"><span data-stu-id="04b9c-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="04b9c-108">V tématu [vytváření balíčku](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="04b9c-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="04b9c-109">nuget.exe 4.6.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="04b9c-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="04b9c-110">V tématu Jak [nainstalovat rozhraní příkazového řádku NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="04b9c-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="04b9c-111">[Certifikát pro podpis kódu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="04b9c-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="04b9c-112">nuget.org aktuálně nepřijímá podepsané balíčky.</span><span class="sxs-lookup"><span data-stu-id="04b9c-112">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="04b9c-113">Můžete si balíčky pro publikování vlastních informačních kanálů.</span><span class="sxs-lookup"><span data-stu-id="04b9c-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="04b9c-114">Podepisování balíčku</span><span class="sxs-lookup"><span data-stu-id="04b9c-114">Sign a package</span></span>

<span data-ttu-id="04b9c-115">K podepsání balíčku, použijte [nuget přihlašovací](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="04b9c-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="04b9c-116">Jak je popsáno v reference k příkazu, můžete použít k dispozici certifikát v úložišti certifikátů nebo použití certifikátu ze souboru.</span><span class="sxs-lookup"><span data-stu-id="04b9c-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="04b9c-117">Běžné problémy při podpis balíčku</span><span class="sxs-lookup"><span data-stu-id="04b9c-117">Common problems when signing a package</span></span>

- <span data-ttu-id="04b9c-118">Certifikát není platný pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="04b9c-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="04b9c-119">Je nutné zajistit, že zadaný certifikát má odpovídající rozšířené použití klíče (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="04b9c-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="04b9c-120">Certifikát nesplňuje požadavky na základní jako podpisový algoritmus RSA, SHA-256 nebo veřejné klíče 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="04b9c-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="04b9c-121">Platnost certifikátu vypršela nebo je odvolaný.</span><span class="sxs-lookup"><span data-stu-id="04b9c-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="04b9c-122">Časové razítko serveru nesplňuje požadavky na certifikát.</span><span class="sxs-lookup"><span data-stu-id="04b9c-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="04b9c-123">Podepsané balíčky by měla obsahovat časovým razítkem a ujistěte se, že podpis bude platný, pokud vypršela platnost podpisového certifikátu.</span><span class="sxs-lookup"><span data-stu-id="04b9c-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="04b9c-124">Vytvořit operace přihlášení [upozornění NU3002](../reference/Errors-and-Warnings.md#nu3002) při přihlašování bez časového razítka.</span><span class="sxs-lookup"><span data-stu-id="04b9c-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="04b9c-125">Ověřte podepsaného balíčku</span><span class="sxs-lookup"><span data-stu-id="04b9c-125">Verify a signed package</span></span>

<span data-ttu-id="04b9c-126">Použití [nuget ověřte](../tools/cli-ref-verify.md) zobrazíte podrobnosti o identifikaci daného balíčku:</span><span class="sxs-lookup"><span data-stu-id="04b9c-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="04b9c-127">Nainstalujte podepsaného balíčku</span><span class="sxs-lookup"><span data-stu-id="04b9c-127">Install a signed package</span></span>

<span data-ttu-id="04b9c-128">Podepsané balíčky nevyžadují žádnou zvláštní akci má být nainstalována. ale pokud obsah byla změněna, protože byl podepsán, instalace se zablokuje a vytvoří [chyba NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="04b9c-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="04b9c-129">Balíčky s nedůvěryhodnými certifikáty podepsané, jsou považovány za jako nepodepsané a jsou nainstalovány bez žádná upozornění ani chyby jako jakýkoli jiný balíček bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="04b9c-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="04b9c-130">Viz také</span><span class="sxs-lookup"><span data-stu-id="04b9c-130">See also</span></span>

[<span data-ttu-id="04b9c-131">Podepsané balíčky odkaz</span><span class="sxs-lookup"><span data-stu-id="04b9c-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
