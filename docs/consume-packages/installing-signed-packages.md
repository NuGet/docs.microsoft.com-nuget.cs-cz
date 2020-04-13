---
title: Správa rozsahu důvěryhodnosti balíčků
description: Popisuje proces instalace podepsaných balíčků NuGet a konfigurace nastavení důvěryhodnosti podpisu balíčku.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428980"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="27e4c-103">Správa rozsahu důvěryhodnosti balíčků</span><span class="sxs-lookup"><span data-stu-id="27e4c-103">Manage package trust boundaries</span></span>

<span data-ttu-id="27e4c-104">Podepsané balíčky nevyžadují žádnou konkrétní akci, která má být nainstalována; Pokud však byl obsah od podepsání změněn, je instalace blokována chybou [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="27e4c-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="27e4c-105">Balíčky podepsané nedůvěryhodnými certifikáty jsou považovány za nepodepsané a jsou nainstalovány bez upozornění nebo chyb jako jakýkoli jiný nepodepsaný balíček.</span><span class="sxs-lookup"><span data-stu-id="27e4c-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="27e4c-106">Konfigurace požadavků na podpis balíčku</span><span class="sxs-lookup"><span data-stu-id="27e4c-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="27e4c-107">Vyžaduje NuGet 4.9.0+ a Visual Studio verze 15.9 a novější v systému Windows</span><span class="sxs-lookup"><span data-stu-id="27e4c-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="27e4c-108">Můžete nakonfigurovat, jak klienti NuGet ověřují podpisy balíčků `signatureValidationMode` nastavením `require` na v souboru [nuget.config](../reference/nuget-config-file.md) pomocí příkazu. [`nuget config`](../reference/cli-reference/cli-ref-config.md)</span><span class="sxs-lookup"><span data-stu-id="27e4c-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="27e4c-109">Tento režim ověří, zda jsou všechny balíčky podepsány libovolným certifikátem důvěryhodným v souboru. `nuget.config`</span><span class="sxs-lookup"><span data-stu-id="27e4c-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="27e4c-110">Tento soubor umožňuje určit, kteří autoři a/nebo repozitáře jsou důvěryhodné na základě otisku prstu certifikátu.</span><span class="sxs-lookup"><span data-stu-id="27e4c-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="27e4c-111">Důvěryhodný autor balíčku</span><span class="sxs-lookup"><span data-stu-id="27e4c-111">Trust package author</span></span>

<span data-ttu-id="27e4c-112">Chcete-li důvěřovat balíčkům [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) založeným na `author` podpisu autora, nastavte vlastnost v souboru nuget.config pomocí příkazu.</span><span class="sxs-lookup"><span data-stu-id="27e4c-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="27e4c-113">Pomocí `nuget.exe` [příkazu verify](../reference/cli-reference/cli-ref-verify.md) `SHA256` získáte hodnotu otisku prstu certifikátu.</span><span class="sxs-lookup"><span data-stu-id="27e4c-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="27e4c-114">Důvěřovat všem balíčkům z úložiště</span><span class="sxs-lookup"><span data-stu-id="27e4c-114">Trust all packages from a repository</span></span>

<span data-ttu-id="27e4c-115">Chcete-li důvěřovat balíčkům založeným na podpisu úložiště, `repository` použijte prvek:</span><span class="sxs-lookup"><span data-stu-id="27e4c-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="27e4c-116">Důvěřovat vlastníkům balíčků</span><span class="sxs-lookup"><span data-stu-id="27e4c-116">Trust Package Owners</span></span>

<span data-ttu-id="27e4c-117">Podpisy úložiště obsahují další metadata k určení vlastníků balíčku v době odeslání.</span><span class="sxs-lookup"><span data-stu-id="27e4c-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="27e4c-118">Balíčky z úložiště můžete omezit na základě seznamu vlastníků:</span><span class="sxs-lookup"><span data-stu-id="27e4c-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="27e4c-119">Pokud balíček obsahuje více vlastníků a některý z těchto vlastníků je v seznamu důvěryhodných, instalace balíčku bude úspěšná.</span><span class="sxs-lookup"><span data-stu-id="27e4c-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="27e4c-120">Nedůvěryhodné kořenové certifikáty</span><span class="sxs-lookup"><span data-stu-id="27e4c-120">Untrusted Root certificates</span></span>

<span data-ttu-id="27e4c-121">V některých situacích můžete chtít povolit ověření pomocí certifikátů, které nejsou řetězové k důvěryhodnému kořenu v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="27e4c-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="27e4c-122">`allowUntrustedRoot` Atribut můžete přizpůsobit toto chování.</span><span class="sxs-lookup"><span data-stu-id="27e4c-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="27e4c-123">Certifikáty úložiště synchronizace</span><span class="sxs-lookup"><span data-stu-id="27e4c-123">Sync repository certificates</span></span>

<span data-ttu-id="27e4c-124">Úložiště balíčků by měla oznámit certifikáty, které používají ve svém [indexu služeb](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="27e4c-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="27e4c-125">Nakonec úložiště tyto certifikáty aktualizuje, například po vypršení platnosti certifikátu.</span><span class="sxs-lookup"><span data-stu-id="27e4c-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="27e4c-126">V takovém případě budou klienti s konkrétními zásadami vyžadovat aktualizaci konfigurace tak, aby zahrnovala nově přidaný certifikát.</span><span class="sxs-lookup"><span data-stu-id="27e4c-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="27e4c-127">Důvěryhodné podepisující autory přidružené k úložišti `nuget.exe` můžete snadno upgradovat pomocí [příkazu synchronizace důvěryhodných podepisujících](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span><span class="sxs-lookup"><span data-stu-id="27e4c-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="27e4c-128">Odkaz na schéma</span><span class="sxs-lookup"><span data-stu-id="27e4c-128">Schema reference</span></span>

<span data-ttu-id="27e4c-129">Úplný odkaz na schéma pro zásady klienta naleznete v [odkazu nuget.config.](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="27e4c-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="27e4c-130">Související články</span><span class="sxs-lookup"><span data-stu-id="27e4c-130">Related articles</span></span>

- [<span data-ttu-id="27e4c-131">Podepisování balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="27e4c-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="27e4c-132">Odkaz na podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="27e4c-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
