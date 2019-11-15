---
title: Správa hranic vztahů důvěryhodnosti balíčku
description: Popisuje proces instalace podepsaných balíčků NuGet a konfigurace nastavení důvěryhodnosti podpisu balíčku.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096853"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="745d4-103">Správa hranic vztahů důvěryhodnosti balíčku</span><span class="sxs-lookup"><span data-stu-id="745d4-103">Manage package trust boundaries</span></span>

<span data-ttu-id="745d4-104">Podepsané balíčky nevyžadují, aby se nainstalovala žádná konkrétní akce. Pokud se ale obsah od svého podepsání změnil, instalace je zablokovaná s chybou [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="745d4-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="745d4-105">Balíčky podepsané pomocí nedůvěryhodných certifikátů se považují za nepodepsané a instalují se bez jakýchkoli upozornění a chyb, jako jakýkoli jiný nepodepsaný balíček.</span><span class="sxs-lookup"><span data-stu-id="745d4-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="745d4-106">Konfigurace požadavků na podpis balíčku</span><span class="sxs-lookup"><span data-stu-id="745d4-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="745d4-107">Vyžaduje NuGet 4.9.0 + a Visual Studio verze 15,9 a novější ve Windows.</span><span class="sxs-lookup"><span data-stu-id="745d4-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="745d4-108">Můžete nakonfigurovat, jak klienti NuGet ověřují signatury balíčků, nastavením `signatureValidationMode` pro `require` v souboru [NuGet. config](../reference/nuget-config-file.md) pomocí příkazu [`nuget config`](../reference/cli-reference/cli-ref-config.md) .</span><span class="sxs-lookup"><span data-stu-id="745d4-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="745d4-109">V tomto režimu se ověří, jestli jsou všechny balíčky podepsané jakýmkoli certifikátem důvěryhodným v souboru `nuget.config`.</span><span class="sxs-lookup"><span data-stu-id="745d4-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="745d4-110">Tento soubor vám umožní určit, které autory nebo úložiště jsou důvěryhodné na základě otisku certifikátu.</span><span class="sxs-lookup"><span data-stu-id="745d4-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="745d4-111">Autor balíčku důvěryhodnosti</span><span class="sxs-lookup"><span data-stu-id="745d4-111">Trust package author</span></span>

<span data-ttu-id="745d4-112">Pro důvěřování balíčkům na základě podpisu autora použijte příkaz [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) pro nastavení vlastnosti `author` v souboru NuGet. config.</span><span class="sxs-lookup"><span data-stu-id="745d4-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="745d4-113">K získání `SHA256` hodnoty otisku certifikátu použijte [příkaz `nuget.exe` Verify](../reference/cli-reference/cli-ref-verify.md) .</span><span class="sxs-lookup"><span data-stu-id="745d4-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="745d4-114">Důvěřovat všem balíčkům z úložiště</span><span class="sxs-lookup"><span data-stu-id="745d4-114">Trust all packages from a repository</span></span>

<span data-ttu-id="745d4-115">K důvěřování balíčkům na základě podpisu úložiště použijte element `repository`:</span><span class="sxs-lookup"><span data-stu-id="745d4-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="745d4-116">Důvěřovat vlastníkům balíčku</span><span class="sxs-lookup"><span data-stu-id="745d4-116">Trust Package Owners</span></span>

<span data-ttu-id="745d4-117">Signatury úložiště obsahují další metadata, která určují vlastníky balíčku v době odeslání.</span><span class="sxs-lookup"><span data-stu-id="745d4-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="745d4-118">Balíčky můžete omezit z úložiště na základě seznamu vlastníků:</span><span class="sxs-lookup"><span data-stu-id="745d4-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="745d4-119">Pokud má balíček více vlastníků a některý z těchto vlastníků je v seznamu důvěryhodných, instalace balíčku bude úspěšná.</span><span class="sxs-lookup"><span data-stu-id="745d4-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="745d4-120">Nedůvěryhodné kořenové certifikáty</span><span class="sxs-lookup"><span data-stu-id="745d4-120">Untrusted Root certificates</span></span>

<span data-ttu-id="745d4-121">V některých situacích možná budete chtít povolit ověřování pomocí certifikátů, které se neřetězí k důvěryhodnému kořenovému adresáři v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="745d4-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="745d4-122">K přizpůsobení tohoto chování můžete použít atribut `allowUntrustedRoot`.</span><span class="sxs-lookup"><span data-stu-id="745d4-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="745d4-123">Synchronizovat certifikáty úložiště</span><span class="sxs-lookup"><span data-stu-id="745d4-123">Sync repository certificates</span></span>

<span data-ttu-id="745d4-124">Úložiště balíčků by měla oznamovat certifikáty, které používají v [indexu služeb](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="745d4-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="745d4-125">Úložiště pak tyto certifikáty aktualizuje, např. po vypršení platnosti certifikátu.</span><span class="sxs-lookup"><span data-stu-id="745d4-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="745d4-126">V takovém případě budou klienti s konkrétními zásadami vyžadovat aktualizaci konfigurace, aby zahrnovala nově přidaný certifikát.</span><span class="sxs-lookup"><span data-stu-id="745d4-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="745d4-127">Důvěryhodné podepsané přidružené k úložišti můžete snadno upgradovat pomocí [příkazu `nuget.exe` důvěryhodných podepsaných synchronizací](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span><span class="sxs-lookup"><span data-stu-id="745d4-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="745d4-128">Odkaz na schéma</span><span class="sxs-lookup"><span data-stu-id="745d4-128">Schema reference</span></span>

<span data-ttu-id="745d4-129">Úplný odkaz na schéma pro zásady klienta najdete v [referenčních informacích k NuGet. config.](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="745d4-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="745d4-130">Související články</span><span class="sxs-lookup"><span data-stu-id="745d4-130">Related articles</span></span>

- [<span data-ttu-id="745d4-131">Podepisování balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="745d4-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="745d4-132">Reference na podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="745d4-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
