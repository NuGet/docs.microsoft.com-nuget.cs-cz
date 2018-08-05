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
# <a name="signing-nuget-packages"></a>Podepisují se balíčky NuGet

Podpis balíčku je proces, který zajistí, že balíček nebyl změněn od jeho vytvoření.

## <a name="prerequisites"></a>Požadavky

1. Balíček ( `.nupkg` souboru) pro přihlášení. Zobrazit [vytvoření balíčku](creating-a-package.md).

1. nuget.exe 4.6.0 nebo novější. V tématu Jak [instalace rozhraní příkazového řádku NuGet](../install-nuget-client-tools.md#nugetexe-cli).

1. [Certifikát pro podpis kódu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

## <a name="sign-a-package"></a>Podepište balíček

K podepsání balíčku, použijte [nuget přihlašování](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Jak je popsáno v informace o příkazech, můžete použít certifikát k dispozici v úložišti certifikátů nebo použití certifikátu ze souboru.

### <a name="common-problems-when-signing-a-package"></a>Běžné problémy při podepisování balíčku

- Certifikát není platný pro podepisování kódu. Musíte zajistit, že zadaný certifikát má rozšířené použití klíče (EKU 1.3.6.1.5.5.7.3.3) odpovídající.
- Certifikát nesplňuje požadavky na základní například podpisový algoritmus RSA, SHA-256 nebo veřejné klíče 2 048 bitů nebo vyšší.
- Certifikátu již vypršela nebo byl odvolán.
- Serveru časového razítka nesplňuje požadavky na certifikát.

> [!Note]
> Podepsané balíčky by měly zahrnovat časové razítko, abyste měli jistotu, že podpis zůstává platná, pokud vypršela platnost podpisového certifikátu. Vytvořit operace přihlášení [upozornění NU3002](../reference/errors-and-warnings/NU3002.md) při přihlašování bez časového razítka.

## <a name="verify-a-signed-package"></a>Ověřte podepsaný balíček

Použití [ověřte nuget](../tools/cli-ref-verify.md) zobrazíte podrobnosti o podpisu daného balíčku:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Podepsaný balíček nainstalovat

Podepsané balíčky nevyžadují žádnou konkrétní akci má být nainstalována. Pokud ale obsah se změnila, protože byla podepsána, instalace se zablokuje a vytváří [chyba NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Nedůvěryhodné certifikáty podepsané balíčky jsou považovány za jako bez znaménka a jsou nainstalovány bez žádná upozornění ani chyby, stejně jako jiné balíčky bez znaménka.

## <a name="see-also"></a>Viz také:

[Podepsané balíčky odkaz](../reference/Signed-Packages-Reference.md)
