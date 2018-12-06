---
title: Nainstalujte podepsaný balíček NuGet
description: Popisuje postup instalace NuGet podepsané balíčky a konfiguraci podpis balíčku důvěryhodných nastavení.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977850"
---
# <a name="install-a-signed-package"></a>Podepsaný balíček nainstalovat

Podepsané balíčky nevyžadují žádnou konkrétní akci má být nainstalována. ale pokud obsah se změnila, protože byla podepsána, instalace se zablokuje s chybou [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Nedůvěryhodné certifikáty podepsané balíčky jsou považovány za jako bez znaménka a jsou nainstalovány bez žádná upozornění ani chyby, stejně jako jiné balíčky bez znaménka.

## <a name="configure-package-signature-requirements"></a>Konfigurovat požadavky na podpis balíčku

> [!Note]
> Vyžaduje NuGet 4.9.0+ a sady Visual Studio verzi 15.9 a později na Windows

Můžete nakonfigurovat, jak NuGet – klienti ověřují podpisů balíčků tak, že nastavíte `signatureValidationMode` k `require` v [nuget.config](../reference/nuget-config-file) soubor pomocí [ `nuget config` ](../tools/cli-ref-config) příkazu.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Tento režim se ověří, že všechny balíčky jsou podepsány některý z certifikátů v důvěryhodné `nuget.config` souboru. Tento soubor umožňuje určit, které autoři a/nebo úložiště jsou důvěryhodné podle otisk certifikátu.

### <a name="trust-package-author"></a>Důvěřovat autora balíčku

Důvěřovat balíčky, které jsou založeny na použití podpis autora [ `trusted-signers` ](..tools/cli-ref-trusted-signers) příkazu nastavte `author` vlastnost v nuget.config.

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
>Použití `nuget.exe` [ověřte příkaz](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) zobrazíte `SHA256` hodnotu otisk certifikátu.


### <a name="trust-all-packages-from-a-repository"></a>Důvěřovat všechny balíčky z úložiště

Důvěřovat balíčky, které jsou založeny na použití podpisu úložiště `repository` element:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Důvěřovat vlastníky balíčku

Podpisy úložiště zahrnují další metadata, chcete-li určit vlastníky balíčku v okamžiku odeslání. Můžete omezit balíčky z úložiště na základě seznamu vlastníků:

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

Pokud balíček obsahuje více vlastníkům a některou z těchto vlastníci je v seznamu důvěryhodných, bude úspěšné instalace balíčku.

### <a name="untrusted-root-certificates"></a>Nedůvěryhodné certifikáty kořenové

V některých situacích můžete povolit ověřování pomocí certifikátů, které nejsou zřetězené s důvěryhodným kořenovým v místním počítači. Můžete použít `allowUntrustedRoot` atributů k přizpůsobení tohoto chování.

### <a name="sync-repository-certificates"></a>Synchronizace úložiště certifikátů

Úložiště balíčku by měl oznamujeme certifikáty se používají v jejich [index služby](https://docs.microsoft.com/en-us/nuget/api/service-index). Nakonec bude úložiště aktualizovat tyto certifikáty, třeba když tomuto certifikátu vyprší platnost. Pokud k tomu dojde, klienti s konkrétní zásady budou vyžadovat aktualizaci v konfiguraci zahrnout nově přidané certifikátu. Budete moct snadno upgradovat podepsaných důvěryhodným přidružit k úložišti pomocí `nuget.exe` [důvěryhodné podepisující osoby synchronizovat příkaz](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).

### <a name="schema-reference"></a>Schéma – referenční informace

Odkaz na kompletní schématu pro zásady klienta najdete v [odkaz na soubor nuget.config](/nuget/reference/nuget-config-file#trustedsigners-section)

## <a name="related-articles"></a>Související články

- [Různé způsoby instalace balíčku NuGet](ways-to-install-a-package.md)
- [Podepisují se balíčky NuGet](../create-packages/Sign-a-Package.md)
- [Podepsané balíčky odkaz](../reference/Signed-Packages-Reference.md)
