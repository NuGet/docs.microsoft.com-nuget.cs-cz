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
# <a name="manage-package-trust-boundaries"></a>Správa hranic vztahů důvěryhodnosti balíčku

Podepsané balíčky nevyžadují, aby se nainstalovala žádná konkrétní akce. Pokud se ale obsah od svého podepsání změnil, instalace je zablokovaná s chybou [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Balíčky podepsané pomocí nedůvěryhodných certifikátů se považují za nepodepsané a instalují se bez jakýchkoli upozornění a chyb, jako jakýkoli jiný nepodepsaný balíček.

## <a name="configure-package-signature-requirements"></a>Konfigurace požadavků na podpis balíčku

> [!Note]
> Vyžaduje NuGet 4.9.0 + a Visual Studio verze 15,9 a novější ve Windows.

Můžete nakonfigurovat, jak klienti NuGet ověřují signatury balíčků, nastavením `signatureValidationMode` pro `require` v souboru [NuGet. config](../reference/nuget-config-file.md) pomocí příkazu [`nuget config`](../reference/cli-reference/cli-ref-config.md) .

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

V tomto režimu se ověří, jestli jsou všechny balíčky podepsané jakýmkoli certifikátem důvěryhodným v souboru `nuget.config`. Tento soubor vám umožní určit, které autory nebo úložiště jsou důvěryhodné na základě otisku certifikátu.

### <a name="trust-package-author"></a>Autor balíčku důvěryhodnosti

Pro důvěřování balíčkům na základě podpisu autora použijte příkaz [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) pro nastavení vlastnosti `author` v souboru NuGet. config.

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
>K získání `SHA256` hodnoty otisku certifikátu použijte [příkaz `nuget.exe` Verify](../reference/cli-reference/cli-ref-verify.md) .


### <a name="trust-all-packages-from-a-repository"></a>Důvěřovat všem balíčkům z úložiště

K důvěřování balíčkům na základě podpisu úložiště použijte element `repository`:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Důvěřovat vlastníkům balíčku

Signatury úložiště obsahují další metadata, která určují vlastníky balíčku v době odeslání. Balíčky můžete omezit z úložiště na základě seznamu vlastníků:

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

Pokud má balíček více vlastníků a některý z těchto vlastníků je v seznamu důvěryhodných, instalace balíčku bude úspěšná.

### <a name="untrusted-root-certificates"></a>Nedůvěryhodné kořenové certifikáty

V některých situacích možná budete chtít povolit ověřování pomocí certifikátů, které se neřetězí k důvěryhodnému kořenovému adresáři v místním počítači. K přizpůsobení tohoto chování můžete použít atribut `allowUntrustedRoot`.

### <a name="sync-repository-certificates"></a>Synchronizovat certifikáty úložiště

Úložiště balíčků by měla oznamovat certifikáty, které používají v [indexu služeb](../api/service-index.md). Úložiště pak tyto certifikáty aktualizuje, např. po vypršení platnosti certifikátu. V takovém případě budou klienti s konkrétními zásadami vyžadovat aktualizaci konfigurace, aby zahrnovala nově přidaný certifikát. Důvěryhodné podepsané přidružené k úložišti můžete snadno upgradovat pomocí [příkazu `nuget.exe` důvěryhodných podepsaných synchronizací](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).

### <a name="schema-reference"></a>Odkaz na schéma

Úplný odkaz na schéma pro zásady klienta najdete v [referenčních informacích k NuGet. config.](../reference/nuget-config-file.md#trustedsigners-section)

## <a name="related-articles"></a>Související články

- [Podepisování balíčků NuGet](../create-packages/Sign-a-Package.md)
- [Reference na podepsané balíčky](../reference/Signed-Packages-Reference.md)
