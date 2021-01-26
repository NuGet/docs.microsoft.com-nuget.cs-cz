---
title: Poznámky k verzi NuGet 2.8.1
description: Poznámky k verzi pro NuGet 2.8.1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776772"
---
# <a name="nuget-281-release-notes"></a>Poznámky k verzi NuGet 2.8.1

Zpráva k [vydání verze](../release-notes/nuget-2.8.md)  |  NuGet 2,8 [Poznámky k verzi NuGet ve verzi 2.8.2](../release-notes/nuget-2.8.2.md)

2.8.1 NuGet byl vydaný 2. dubna 2014.

## <a name="notable-features-in-the-release"></a>Významné funkce v této verzi

### <a name="support-for-windows-phone-81-projects"></a>Podpora pro projekty Windows Phone 8,1
Tato verze teď podporuje následující nové monikery cílového rozhraní, které se dají použít k cílení na projekty Windows Phone 8,1:

* WindowsPhone81/WP81 (pro projekty Windows Phone založené na technologii Silverlight)
* WindowsPhoneApp81/WPA81 (pro projekty aplikací Windows Phone založené na WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aktualizace rozšíření WebMatrix NuGet
Tato verze aktualizuje klienta NuGet, který se našel v WebMatrixu, do [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 a přináší funkce IT, jako jsou třeba transformace xdt. Důležitější je, že aktualizace 2.6.1 Core umožňuje klientovi WebMatrix instalovat balíčky NuGet, které obsahují novější verze `.nuspec` schématu, včetně balíčků nuget ASP.NET.

Další informace o aktualizaci rozšíření WebMatrix najdete v těchto [poznámkách k verzi](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Opravy chyb
Kromě těchto funkcí obsahuje tato verze NuGet i další opravy chyb. V této verzi bylo vyřešeno 16 celkových problémů. Úplný seznam pracovních položek opravených ve 2.8.1 NuGet najdete v [přehledu problémů NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Redodávka pomocí sady Visual Studio "14" CTP
V aplikaci Visual Studio "14" CTP vydané 3. června 2014 se do boxu dodává 2.8.1 NuGet. Funkce, které podporují, zůstávají stejné jako jiné 2.8.1 VSIX, jako je ta pro Visual Studio 2013.
