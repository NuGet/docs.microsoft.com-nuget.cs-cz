---
title: Správa rozsahu důvěryhodnosti balíčků
description: Popisuje proces instalace podepsaných balíčků NuGet a konfigurace nastavení důvěryhodnosti podpisu balíčku.
author: JonDouglas
ms.author: jodou
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 596ce330e434253e6fb200aa59ae4e14d47779ed
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774800"
---
# <a name="manage-package-trust-boundaries"></a>Správa rozsahu důvěryhodnosti balíčků

Podepsané balíčky nevyžadují, aby se nainstalovala žádná konkrétní akce. Pokud se ale obsah od svého podepsání změnil, instalace je zablokovaná s chybou [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Balíčky podepsané pomocí nedůvěryhodných certifikátů se považují za nepodepsané a instalují se bez jakýchkoli upozornění a chyb, jako jakýkoli jiný nepodepsaný balíček.

## <a name="configure-package-signature-requirements"></a>Konfigurace požadavků na podpis balíčku

> [!Note]
> Vyžaduje NuGet 4.9.0 + a Visual Studio verze 15,9 a novější ve Windows.

Můžete nakonfigurovat, jak klienti NuGet ověřují signatury balíčků, nastavením `signatureValidationMode` na `require` v souboru [nuget.config](../reference/nuget-config-file.md) pomocí [`nuget config`](../reference/cli-reference/cli-ref-config.md) příkazu.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

V tomto režimu se ověří, jestli jsou všechny balíčky podepsané všemi certifikáty, které jsou v `nuget.config` souboru důvěryhodné. Tento soubor vám umožní určit, které autory nebo úložiště jsou důvěryhodné na základě otisku certifikátu.

### <a name="trust-package-author"></a>Autor balíčku důvěryhodnosti

Pro důvěřování balíčkům na základě podpisu autora použijte [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) příkaz pro nastavení `author` vlastnosti v nuget.config.

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
>`nuget.exe` [](../reference/cli-reference/cli-ref-verify.md) K získání `SHA256` hodnoty otisku certifikátu použijte příkaz Verify.


### <a name="trust-all-packages-from-a-repository"></a>Důvěřovat všem balíčkům z úložiště

K důvěřování balíčkům na základě podpisu úložiště použijte `repository` element:

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

V některých situacích možná budete chtít povolit ověřování pomocí certifikátů, které se neřetězí k důvěryhodnému kořenovému adresáři v místním počítači. `allowUntrustedRoot`K přizpůsobení tohoto chování můžete použít atribut.

### <a name="sync-repository-certificates"></a>Synchronizovat certifikáty úložiště

Úložiště balíčků by měla oznamovat certifikáty, které používají v [indexu služeb](../api/service-index.md). Úložiště pak tyto certifikáty aktualizuje, např. po vypršení platnosti certifikátu. V takovém případě budou klienti s konkrétními zásadami vyžadovat aktualizaci konfigurace, aby zahrnovala nově přidaný certifikát. Důvěryhodné podepsané přidružené k úložišti můžete snadno upgradovat pomocí `nuget.exe` [příkazu pro synchronizaci důvěryhodného přihlášení](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).

### <a name="schema-reference"></a>Odkaz na schéma

Kompletní odkaz na schéma pro zásady klienta najdete v [referenčních informacích onuget.config](../reference/nuget-config-file.md#trustedsigners-section) .

## <a name="related-articles"></a>Související články

- [Podepisování balíčků NuGet](../create-packages/Sign-a-Package.md)
- [Reference na podepsané balíčky](../reference/Signed-Packages-Reference.md)
