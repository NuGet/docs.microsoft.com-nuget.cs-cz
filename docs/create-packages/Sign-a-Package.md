---
title: Podepisují se balíčky NuGet
description: Vysvětluje, jak podepsané balíčky je možné povolit ověření obsahu, integrity.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 8bbbc785a50e49530bbbd4e88bbd71a8a7bfe911
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508176"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="a6823-103">Podepisují se balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="a6823-103">Signing NuGet Packages</span></span>

<span data-ttu-id="a6823-104">Podpis balíčku je proces, který zajistí, že balíček nebyl změněn od jeho vytvoření.</span><span class="sxs-lookup"><span data-stu-id="a6823-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6823-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a6823-105">Prerequisites</span></span>

1. <span data-ttu-id="a6823-106">Balíček ( `.nupkg` souboru) pro přihlášení.</span><span class="sxs-lookup"><span data-stu-id="a6823-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="a6823-107">Zobrazit [vytvoření balíčku](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a6823-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="a6823-108">nuget.exe 4.6.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="a6823-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="a6823-109">V tématu Jak [instalace rozhraní příkazového řádku NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="a6823-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="a6823-110">[Certifikát pro podpis kódu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="a6823-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="a6823-111">Podepište balíček</span><span class="sxs-lookup"><span data-stu-id="a6823-111">Sign a package</span></span>

<span data-ttu-id="a6823-112">K podepsání balíčku, použijte [nuget přihlašování](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="a6823-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="a6823-113">Jak je popsáno v informace o příkazech, můžete použít certifikát k dispozici v úložišti certifikátů nebo použití certifikátu ze souboru.</span><span class="sxs-lookup"><span data-stu-id="a6823-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="a6823-114">Běžné problémy při podepisování balíčku</span><span class="sxs-lookup"><span data-stu-id="a6823-114">Common problems when signing a package</span></span>

- <span data-ttu-id="a6823-115">Certifikát není platný pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="a6823-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="a6823-116">Musíte zajistit, že zadaný certifikát má rozšířené použití klíče (EKU 1.3.6.1.5.5.7.3.3) odpovídající.</span><span class="sxs-lookup"><span data-stu-id="a6823-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="a6823-117">Certifikát nesplňuje požadavky na základní například podpisový algoritmus RSA, SHA-256 nebo veřejné klíče 2 048 bitů nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="a6823-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="a6823-118">Certifikátu již vypršela nebo byl odvolán.</span><span class="sxs-lookup"><span data-stu-id="a6823-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="a6823-119">Serveru časového razítka nesplňuje požadavky na certifikát.</span><span class="sxs-lookup"><span data-stu-id="a6823-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="a6823-120">Podepsané balíčky by měly zahrnovat časové razítko, abyste měli jistotu, že podpis zůstává platná, pokud vypršela platnost podpisového certifikátu.</span><span class="sxs-lookup"><span data-stu-id="a6823-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="a6823-121">Vytvořit operace přihlášení [upozornění NU3002](../reference/errors-and-warnings/NU3002.md) při přihlašování bez časového razítka.</span><span class="sxs-lookup"><span data-stu-id="a6823-121">The sign operation produce a [warning NU3002](../reference/errors-and-warnings/NU3002.md) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="a6823-122">Ověřte podepsaný balíček</span><span class="sxs-lookup"><span data-stu-id="a6823-122">Verify a signed package</span></span>

<span data-ttu-id="a6823-123">Použití [ověřte nuget](../tools/cli-ref-verify.md) zobrazíte podrobnosti o podpisu daného balíčku:</span><span class="sxs-lookup"><span data-stu-id="a6823-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="a6823-124">Podepsaný balíček nainstalovat</span><span class="sxs-lookup"><span data-stu-id="a6823-124">Install a signed package</span></span>

<span data-ttu-id="a6823-125">Podepsané balíčky nevyžadují žádnou konkrétní akci má být nainstalována. Pokud ale obsah se změnila, protože byla podepsána, instalace se zablokuje a vytváří [chyba NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="a6823-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="a6823-126">Nedůvěryhodné certifikáty podepsané balíčky jsou považovány za jako bez znaménka a jsou nainstalovány bez žádná upozornění ani chyby, stejně jako jiné balíčky bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="a6823-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="a6823-127">Viz také:</span><span class="sxs-lookup"><span data-stu-id="a6823-127">See also</span></span>

[<span data-ttu-id="a6823-128">Podepsané balíčky odkaz</span><span class="sxs-lookup"><span data-stu-id="a6823-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
