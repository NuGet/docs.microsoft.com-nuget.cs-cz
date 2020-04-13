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
# <a name="manage-package-trust-boundaries"></a>Správa rozsahu důvěryhodnosti balíčků

Podepsané balíčky nevyžadují žádnou konkrétní akci, která má být nainstalována; Pokud však byl obsah od podepsání změněn, je instalace blokována chybou [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Balíčky podepsané nedůvěryhodnými certifikáty jsou považovány za nepodepsané a jsou nainstalovány bez upozornění nebo chyb jako jakýkoli jiný nepodepsaný balíček.

## <a name="configure-package-signature-requirements"></a>Konfigurace požadavků na podpis balíčku

> [!Note]
> Vyžaduje NuGet 4.9.0+ a Visual Studio verze 15.9 a novější v systému Windows

Můžete nakonfigurovat, jak klienti NuGet ověřují podpisy balíčků `signatureValidationMode` nastavením `require` na v souboru [nuget.config](../reference/nuget-config-file.md) pomocí příkazu. [`nuget config`](../reference/cli-reference/cli-ref-config.md)

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Tento režim ověří, zda jsou všechny balíčky podepsány libovolným certifikátem důvěryhodným v souboru. `nuget.config` Tento soubor umožňuje určit, kteří autoři a/nebo repozitáře jsou důvěryhodné na základě otisku prstu certifikátu.

### <a name="trust-package-author"></a>Důvěryhodný autor balíčku

Chcete-li důvěřovat balíčkům [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) založeným na `author` podpisu autora, nastavte vlastnost v souboru nuget.config pomocí příkazu.

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
>Pomocí `nuget.exe` [příkazu verify](../reference/cli-reference/cli-ref-verify.md) `SHA256` získáte hodnotu otisku prstu certifikátu.


### <a name="trust-all-packages-from-a-repository"></a>Důvěřovat všem balíčkům z úložiště

Chcete-li důvěřovat balíčkům založeným na podpisu úložiště, `repository` použijte prvek:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Důvěřovat vlastníkům balíčků

Podpisy úložiště obsahují další metadata k určení vlastníků balíčku v době odeslání. Balíčky z úložiště můžete omezit na základě seznamu vlastníků:

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

Pokud balíček obsahuje více vlastníků a některý z těchto vlastníků je v seznamu důvěryhodných, instalace balíčku bude úspěšná.

### <a name="untrusted-root-certificates"></a>Nedůvěryhodné kořenové certifikáty

V některých situacích můžete chtít povolit ověření pomocí certifikátů, které nejsou řetězové k důvěryhodnému kořenu v místním počítači. `allowUntrustedRoot` Atribut můžete přizpůsobit toto chování.

### <a name="sync-repository-certificates"></a>Certifikáty úložiště synchronizace

Úložiště balíčků by měla oznámit certifikáty, které používají ve svém [indexu služeb](../api/service-index.md). Nakonec úložiště tyto certifikáty aktualizuje, například po vypršení platnosti certifikátu. V takovém případě budou klienti s konkrétními zásadami vyžadovat aktualizaci konfigurace tak, aby zahrnovala nově přidaný certifikát. Důvěryhodné podepisující autory přidružené k úložišti `nuget.exe` můžete snadno upgradovat pomocí [příkazu synchronizace důvěryhodných podepisujících](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).

### <a name="schema-reference"></a>Odkaz na schéma

Úplný odkaz na schéma pro zásady klienta naleznete v [odkazu nuget.config.](../reference/nuget-config-file.md#trustedsigners-section)

## <a name="related-articles"></a>Související články

- [Podepisování balíčků NuGet](../create-packages/Sign-a-Package.md)
- [Odkaz na podepsané balíčky](../reference/Signed-Packages-Reference.md)
