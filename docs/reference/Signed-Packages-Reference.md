---
title: Podepsané balíčky
description: Požadavky na podepisování balíčku NuGet
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508797"
---
# <a name="signed-packages"></a>Podepsané balíčky

*NuGet 4.6.0 + a Visual Studio 2017 verze 15,6 a novější*

Balíčky NuGet můžou obsahovat digitální podpis, který poskytuje ochranu proti úmyslnému obsahu. Tento podpis je vytvořený z certifikátu X. 509, který taky do skutečného původce balíčku přidá ověření pravosti.

Podepsané balíčky poskytují nejsilnější kompletní ověřování. Existují dva různé typy signatur NuGet:
- **Podpis autora** Podpis autora zaručuje, že balíček se nezměnil od autora podpisu balíčku bez ohledu na to, ze kterého úložiště nebo jakou metodu transportu balíček doručí. Navíc balíčky podepsané autorem poskytují pro kanál publikování nuget.org dodatečný mechanismus ověřování, protože podpisový certifikát musí být zaregistrovaný předem. Další informace najdete v tématu [Registrace certifikátů](#signature-requirements-on-nugetorg).
- **Podpis úložiště** Signatury úložiště poskytují záruku integrity pro **všechny** balíčky v úložišti bez ohledu na to, jestli jsou autorem podepsané, nebo ne, a to i v případě, že se tyto balíčky získávají z jiného umístění, než je původní úložiště, ve kterém byly podepsané.   

Podrobnosti o vytvoření balíčku podepsaného autorem najdete v tématu [podepisování balíčků](../create-packages/Sign-a-package.md) a [příkaz NuGet Sign](../reference/cli-reference/cli-ref-sign.md). Signatury balíčků můžete ověřit pomocí příkazů [dotnet NuGet ověřit](/dotnet/core/tools/dotnet-nuget-verify) nebo [NuGet ověřit](../reference/cli-reference/cli-ref-verify.md) .

> [!Important]
> Vytváření podpisových balíčků je v tuto chvíli podporované jenom v nuget.exe ve Windows. Všechny balíčky nahrané do nuget.org se ale automaticky podepisují jako úložiště.

## <a name="certificate-requirements"></a>Požadavky na certifikáty

Podepisování balíčků vyžaduje certifikát pro podpis kódu, což je zvláštní typ certifikátu, který je platný pro `id-kp-codeSigning` účely [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Certifikát navíc musí mít délku veřejného klíče RSA 2048 bitů nebo vyšší.

## <a name="timestamp-requirements"></a>Požadavky na časové razítko

Podepsané balíčky by měly zahrnovat časové razítko RFC 3161 k zajištění platnosti podpisu mimo období platnosti podpisového certifikátu balíčku. Certifikát použitý k podepsání časového razítka musí být platný pro `id-kp-timeStamping` účely [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Certifikát navíc musí mít délku veřejného klíče RSA 2048 bitů nebo vyšší.

Další technické podrobnosti najdete v [technické specifikaci signatury balíčku](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Požadavky na podpis na NuGet.org

nuget.org má další požadavky na přijetí podepsaného balíčku:

- Primární signatura musí být podpis autora.
- Primární podpis musí mít jedno platné časové razítko.
- Certifikáty X. 509 pro podpis autora i podpis časového razítka:
  - Musí mít veřejný klíč RSA (2048) nebo vyšší.
  - Musí spadat do období platnosti za aktuální čas UTC v době ověření balíčku v nuget.org.
  - Musí být zřetězené s důvěryhodnou kořenovou autoritou, která je ve Windows ve výchozím nastavení důvěryhodná. Balíčky podepsané pomocí certifikátů vystavených svým držitelem jsou odmítnuty.
  - Musí být platný pro svůj účel: 
    - Podpisový certifikát autora musí být platný pro podepisování kódu.
    - Certifikát časového razítka musí být platný pro časová razítka.
  - Nesmí být odvoláno v době podepisování. (To nemusí být knowable v době odeslání, takže nuget.org pravidelně znovu kontroluje stav odvolání).
  
  
## <a name="related-articles"></a>Související články

- [Podepisování balíčků NuGet](../create-packages/Sign-a-Package.md)
- [Ověření podepsaných balíčků pomocí rozhraní příkazového řádku dotnet](/dotnet/core/tools/dotnet-nuget-verify)
- [Ověření podepsaných balíčků pomocí nuget.exe](../reference/cli-reference/cli-ref-verify.md)
- [Správa rozsahu důvěryhodnosti balíčků](../consume-packages/installing-signed-packages.md)
