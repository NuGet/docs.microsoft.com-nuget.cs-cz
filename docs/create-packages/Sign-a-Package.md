---
title: Podepisování balíčků NuGet
description: Vysvětluje, jak podepsaný balíčků slouží k povolení ověření obsahu integrity.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9900db1970a89de129d9074e5900e0aa048101de
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449601"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="7966f-103">Podepisování balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="7966f-103">Signing NuGet Packages</span></span>

<span data-ttu-id="7966f-104">Podpis balíčku je proces, který zajistí, že balíček nebyl změněn od svého vytvoření.</span><span class="sxs-lookup"><span data-stu-id="7966f-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7966f-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7966f-105">Prerequisites</span></span>

1. <span data-ttu-id="7966f-106">Balíček ( `.nupkg` souboru) pro přihlášení.</span><span class="sxs-lookup"><span data-stu-id="7966f-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="7966f-107">V tématu [vytváření balíčku](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="7966f-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="7966f-108">nuget.exe 4.6.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="7966f-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="7966f-109">V tématu Jak [nainstalovat rozhraní příkazového řádku NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="7966f-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="7966f-110">[Certifikát pro podpis kódu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="7966f-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="7966f-111">Podepisování balíčku</span><span class="sxs-lookup"><span data-stu-id="7966f-111">Sign a package</span></span>

<span data-ttu-id="7966f-112">K podepsání balíčku, použijte [nuget přihlašovací](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="7966f-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="7966f-113">Jak je popsáno v reference k příkazu, můžete použít k dispozici certifikát v úložišti certifikátů nebo použití certifikátu ze souboru.</span><span class="sxs-lookup"><span data-stu-id="7966f-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="7966f-114">Běžné problémy při podpis balíčku</span><span class="sxs-lookup"><span data-stu-id="7966f-114">Common problems when signing a package</span></span>

- <span data-ttu-id="7966f-115">Certifikát není platný pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="7966f-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="7966f-116">Je nutné zajistit, že zadaný certifikát má odpovídající rozšířené použití klíče (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="7966f-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="7966f-117">Certifikát nesplňuje požadavky na základní jako podpisový algoritmus RSA, SHA-256 nebo veřejné klíče 2048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="7966f-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="7966f-118">Platnost certifikátu vypršela nebo je odvolaný.</span><span class="sxs-lookup"><span data-stu-id="7966f-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="7966f-119">Časové razítko serveru nesplňuje požadavky na certifikát.</span><span class="sxs-lookup"><span data-stu-id="7966f-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="7966f-120">Podepsané balíčky by měla obsahovat časovým razítkem a ujistěte se, že podpis bude platný, pokud vypršela platnost podpisového certifikátu.</span><span class="sxs-lookup"><span data-stu-id="7966f-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="7966f-121">Vytvořit operace přihlášení [upozornění NU3002](../reference/Errors-and-Warnings.md#nu3002) při přihlašování bez časového razítka.</span><span class="sxs-lookup"><span data-stu-id="7966f-121">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="7966f-122">Ověřte podepsaného balíčku</span><span class="sxs-lookup"><span data-stu-id="7966f-122">Verify a signed package</span></span>

<span data-ttu-id="7966f-123">Použití [nuget ověřte](../tools/cli-ref-verify.md) zobrazíte podrobnosti o identifikaci daného balíčku:</span><span class="sxs-lookup"><span data-stu-id="7966f-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="7966f-124">Nainstalujte podepsaného balíčku</span><span class="sxs-lookup"><span data-stu-id="7966f-124">Install a signed package</span></span>

<span data-ttu-id="7966f-125">Podepsané balíčky nevyžadují žádnou zvláštní akci má být nainstalována. ale pokud obsah byla změněna, protože byl podepsán, instalace se zablokuje a vytvoří [chyba NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="7966f-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="7966f-126">Balíčky s nedůvěryhodnými certifikáty podepsané, jsou považovány za jako nepodepsané a jsou nainstalovány bez žádná upozornění ani chyby jako jakýkoli jiný balíček bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="7966f-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="7966f-127">Viz také</span><span class="sxs-lookup"><span data-stu-id="7966f-127">See also</span></span>

[<span data-ttu-id="7966f-128">Podepsané balíčky odkaz</span><span class="sxs-lookup"><span data-stu-id="7966f-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
