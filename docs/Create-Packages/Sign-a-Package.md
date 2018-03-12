---
title: "Podepisování balíčků NuGet | Microsoft Docs"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Vysvětluje, jak podepsaný balíčků slouží k povolení ověření obsahu integrity."
keywords: "Balíček NuGet podepisování NuGet zabezpečení, vytváření balíčků podepsané"
ms.reviewer:
- karann-msft
- anangaur
ms.openlocfilehash: 226b2af13a4559dfc7266e941617dca25ccd2245
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/08/2018
---
# <a name="signing-nuget-packages"></a>Podepisování balíčků NuGet

Podpis balíčku je proces, který zajistí, že balíček nebyl změněn od svého vytvoření.

## <a name="prerequisites"></a>Požadavky

1. Balíček ( `.nupkg` souboru) pro přihlášení. V tématu [vytváření balíčku](creating-a-package.md).

1. nuget.exe 4.6.0 nebo novější. V tématu Jak [nainstalovat rozhraní příkazového řádku NuGet](../install-nuget-client-tools.md#nugetexe-cli).

1. [Certifikát pro podpis kódu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

> [!Warning]
> NuGet.org aktuálně nepřijímá podepsané balíčky. Můžete si balíčky pro publikování vlastních informačních kanálů.

## <a name="sign-a-package"></a>Podepisování balíčku

K podepsání balíčku, použijte [nuget přihlašovací](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Jak je popsáno v reference k příkazu, můžete použít k dispozici certifikát v úložišti certifikátů nebo použití certifikátu ze souboru.

### <a name="common-problems-when-signing-a-package"></a>Běžné problémy při podpis balíčku

- Certifikát není platný pro podepisování kódu. Je nutné zajistit, že zadaný certifikát má odpovídající rozšířené použití klíče (EKU 1.3.6.1.5.5.7.3.3).
- Certifikát nesplňuje požadavky na základní jako podpisový algoritmus RSA, SHA-256 nebo veřejné klíče 2048 bitů nebo vyšší.
- Platnost certifikátu vypršela nebo je odvolaný.
- Časové razítko serveru nesplňuje požadavky na certifikát.

> [!Note]
> Podepsané balíčky by měla obsahovat časovým razítkem a ujistěte se, že podpis bude platný, pokud vypršela platnost podpisového certifikátu. Vytvořit operace přihlášení [upozornění NU3002](../reference/Errors-and-Warnings.md#nu3002) při přihlašování bez časového razítka.

## <a name="verify-a-signed-package"></a>Ověřte podepsaného balíčku

Použití [nuget ověřte](../tools/cli-ref-verify.md) zobrazíte podrobnosti o identifikaci daného balíčku:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Nainstalujte podepsaného balíčku

Podepsané balíčky nevyžadují žádnou zvláštní akci má být nainstalována. ale pokud obsah byla změněna, protože byl podepsán, instalace se zablokuje a vytvoří [chyba NU3008](../reference/Errors-and-Warnings.md#nu3008).

> [!Warning]
> Balíčky s nedůvěryhodnými certifikáty podepsané, jsou považovány za jako nepodepsané a jsou nainstalovány bez žádná upozornění ani chyby jako jakýkoli jiný balíček bez znaménka.

## <a name="see-also"></a>Viz také

[Podepsané balíčky odkaz](../reference/Signed-Packages-Reference.md)
