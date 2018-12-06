---
title: Podepsané balíčky
description: Požadavky na podepisování balíčků NuGet.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977508"
---
# <a name="signed-packages"></a>Podepsané balíčky

*NuGet 4.6.0+ a sady Visual Studio 2017 verze 15.6 a novější*

Balíčky NuGet může obsahovat digitální podpis, který poskytuje ochranu proti zmanipulovanou obsah. Tento podpis je vytvořen z certifikát X.509, který také přidává testování konceptů pravosti skutečné zdroji balíčku.

Podepsané balíčky poskytují nejsilnější ověření začátku do konce. Existují dva různé typy podpisů NuGet:
- **Vytváření podpis**. Podpis autora zaručuje, že balíček nebyl změněn od autora podpisu balíčku, bez ohledu na to, z které úložiště nebo co přenosu metodu doručení balíčku. Kromě toho Autor podepsané balíčky poskytnout další ověřovací mechanismus pro publikování kanál nuget.org, protože podpisový certifikát musí být zaregistrované předem. Další informace najdete v tématu [registrace certifikátů](#register-certificate-on-nugetorg).
- **Podpis úložiště**. Podpisy úložiště poskytuje záruku integrity **všechny** balíčků v úložišti, ať už jsou Autor nebo nemají, i když tyto balíčky jsou získány z jiného umístění než původní úložiště, ve kterém byly podepsané.   

Podrobnosti o vytvoření podepsaný balíček Autor najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [přihlašovací příkaz nuget](../tools/cli-ref-sign.md).

> [!Important]
> Podepisování balíčků aktuálně podporuje jenom při použití nuget.exe ve Windows. Ověření podepsaných balíčků aktuálně podporuje jenom při použití nuget.exe nebo Visual Studio na Windows.

## <a name="certificate-requirements"></a>Požadavky na certifikát

Podepisování balíčků vyžaduje certifikát, který je speciální typ certifikátu, který je platný pro podpis kódu `id-kp-codeSigning` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Certifikát musí mít navíc veřejné délka klíče RSA 2048 bitů nebo vyšší.

## <a name="timestamp-requirements"></a>Požadavky na časové razítko

Podepsané balíčky by měl obsahovat časového razítka RFC 3161 zajistit platnost podpisu mimo období platnosti certifikátu podpisu balíčku. Certifikát použitý k podpisu časového razítka musí být platná pro `id-kp-timeStamping` účel [[RFC 5280 části 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Certifikát musí mít navíc veřejné délka klíče RSA 2048 bitů nebo vyšší.

Další technické podrobnosti najdete v [balíček technické specifikace podpis](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Požadavky na podpis na NuGet.org

nuget.org mají další požadavky pro přijetí podepsaný balíček:

- Primární podpis musí být podpis autora.
- Primární podpis musí mít jediné platné časové razítko.
- Certifikátů X.509 pro podpis autora a jeho podpis časového razítka:
  - Musí mít veřejný klíč RSA 2048 bitů nebo vyšší.
  - Musí být v rozsahu období platnosti podle aktuálního času UTC v době ověřování balíčků na nuget.org.
  - Musí být propojeny s důvěryhodnou kořenovou autoritou, která je důvěryhodná pro výchozí na Windows. Balíčky, které jsou podepsané pomocí samostatně vydané certifikáty byly zamítnuty.
  - Musí být platný pro její účel: 
    - Autor podpisový certifikát musí být platný pro podepisování kódu.
    - Certifikát časového razítka musí být platný pro časových razítek.
  - Nesmí být odvolaný při podepisování čas. (Toto video asi knowable při odesílání, takže nuget.org proběhne znovu pravidelně u stav odvolání).
  
  
## <a name="related-articles"></a>Související články

- [Podepisují se balíčky NuGet](../create-packages/Sign-a-Package.md)
- [Instalace podepsaných balíčků](../consume-packages/installing-signed-packages.md)
