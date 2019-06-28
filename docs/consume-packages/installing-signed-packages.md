---
title: Spravovat hranice vztahu důvěryhodnosti balíčku
description: Popisuje postup instalace NuGet podepsané balíčky a konfiguraci podpis balíčku důvěryhodných nastavení.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 8da57dc295ea78f2eb183226fc9b2f4a37e3f5db
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426625"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="4b571-103">Spravovat hranice vztahu důvěryhodnosti balíčku</span><span class="sxs-lookup"><span data-stu-id="4b571-103">Manage package trust boundaries</span></span>

<span data-ttu-id="4b571-104">Podepsané balíčky nevyžadují žádnou konkrétní akci má být nainstalována. ale pokud obsah se změnila, protože byla podepsána, instalace se zablokuje s chybou [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="4b571-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="4b571-105">Nedůvěryhodné certifikáty podepsané balíčky jsou považovány za jako bez znaménka a jsou nainstalovány bez žádná upozornění ani chyby, stejně jako jiné balíčky bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="4b571-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="4b571-106">Konfigurovat požadavky na podpis balíčku</span><span class="sxs-lookup"><span data-stu-id="4b571-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="4b571-107">Vyžaduje NuGet 4.9.0+ a sady Visual Studio verzi 15.9 a později na Windows</span><span class="sxs-lookup"><span data-stu-id="4b571-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="4b571-108">Můžete nakonfigurovat, jak NuGet – klienti ověřují podpisů balíčků tak, že nastavíte `signatureValidationMode` k `require` v [nuget.config](../reference/nuget-config-file.md) soubor pomocí [ `nuget config` ](../tools/cli-ref-config.md) příkazu.</span><span class="sxs-lookup"><span data-stu-id="4b571-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../tools/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="4b571-109">Tento režim se ověří, že všechny balíčky jsou podepsány některý z certifikátů v důvěryhodné `nuget.config` souboru.</span><span class="sxs-lookup"><span data-stu-id="4b571-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="4b571-110">Tento soubor umožňuje určit, které autoři a/nebo úložiště jsou důvěryhodné podle otisk certifikátu.</span><span class="sxs-lookup"><span data-stu-id="4b571-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="4b571-111">Důvěřovat autora balíčku</span><span class="sxs-lookup"><span data-stu-id="4b571-111">Trust package author</span></span>

<span data-ttu-id="4b571-112">Důvěřovat balíčky, které jsou založeny na použití podpis autora [ `trusted-signers` ](../tools/cli-ref-trusted-signers.md) příkazu nastavte `author` vlastnost v nuget.config.</span><span class="sxs-lookup"><span data-stu-id="4b571-112">To trust packages based on the author signature use the [`trusted-signers`](../tools/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
><span data-ttu-id="4b571-113">Použití `nuget.exe` [ověřte příkaz](../tools/cli-ref-verify.md) zobrazíte `SHA256` hodnotu otisk certifikátu.</span><span class="sxs-lookup"><span data-stu-id="4b571-113">Use the `nuget.exe` [verify command](../tools/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="4b571-114">Důvěřovat všechny balíčky z úložiště</span><span class="sxs-lookup"><span data-stu-id="4b571-114">Trust all packages from a repository</span></span>

<span data-ttu-id="4b571-115">Důvěřovat balíčky, které jsou založeny na použití podpisu úložiště `repository` element:</span><span class="sxs-lookup"><span data-stu-id="4b571-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="4b571-116">Důvěřovat vlastníky balíčku</span><span class="sxs-lookup"><span data-stu-id="4b571-116">Trust Package Owners</span></span>

<span data-ttu-id="4b571-117">Podpisy úložiště zahrnují další metadata, chcete-li určit vlastníky balíčku v okamžiku odeslání.</span><span class="sxs-lookup"><span data-stu-id="4b571-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="4b571-118">Můžete omezit balíčky z úložiště na základě seznamu vlastníků:</span><span class="sxs-lookup"><span data-stu-id="4b571-118">You can restrict packages from a repository based on a list of owners:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

<span data-ttu-id="4b571-119">Pokud balíček obsahuje více vlastníkům a některou z těchto vlastníci je v seznamu důvěryhodných, bude úspěšné instalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="4b571-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="4b571-120">Nedůvěryhodné certifikáty kořenové</span><span class="sxs-lookup"><span data-stu-id="4b571-120">Untrusted Root certificates</span></span>

<span data-ttu-id="4b571-121">V některých situacích můžete povolit ověřování pomocí certifikátů, které nejsou zřetězené s důvěryhodným kořenovým v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="4b571-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="4b571-122">Můžete použít `allowUntrustedRoot` atributů k přizpůsobení tohoto chování.</span><span class="sxs-lookup"><span data-stu-id="4b571-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="4b571-123">Synchronizace úložiště certifikátů</span><span class="sxs-lookup"><span data-stu-id="4b571-123">Sync repository certificates</span></span>

<span data-ttu-id="4b571-124">Úložiště balíčku by měl oznamujeme certifikáty se používají v jejich [index služby](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4b571-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="4b571-125">Nakonec bude úložiště aktualizovat tyto certifikáty, třeba když tomuto certifikátu vyprší platnost.</span><span class="sxs-lookup"><span data-stu-id="4b571-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="4b571-126">Pokud k tomu dojde, klienti s konkrétní zásady budou vyžadovat aktualizaci v konfiguraci zahrnout nově přidané certifikátu.</span><span class="sxs-lookup"><span data-stu-id="4b571-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="4b571-127">Budete moct snadno upgradovat podepsaných důvěryhodným přidružit k úložišti pomocí `nuget.exe` [důvěryhodné podepisující osoby synchronizovat příkaz](../tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span><span class="sxs-lookup"><span data-stu-id="4b571-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="4b571-128">Schéma – referenční informace</span><span class="sxs-lookup"><span data-stu-id="4b571-128">Schema reference</span></span>

<span data-ttu-id="4b571-129">Odkaz na kompletní schématu pro zásady klienta najdete v [odkaz na soubor nuget.config](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="4b571-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="4b571-130">Související články</span><span class="sxs-lookup"><span data-stu-id="4b571-130">Related articles</span></span>

- [<span data-ttu-id="4b571-131">Podepisují se balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="4b571-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="4b571-132">Podepsané balíčky odkaz</span><span class="sxs-lookup"><span data-stu-id="4b571-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
