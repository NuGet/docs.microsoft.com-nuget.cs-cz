---
title: Zpráva k vydání verze NuGet 2.8.1
description: Zpráva k vydání verze pro NuGet 2.8.1 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545236"
---
# <a name="nuget-281-release-notes"></a>Zpráva k vydání verze NuGet 2.8.1

[Zpráva k vydání verze NuGet 2.8](../release-notes/nuget-2.8.md) | [zpráva k vydání verze NuGet ve verzi 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 byla vydána 2. dubna 2014.

## <a name="notable-features-in-the-release"></a>Důležité funkce ve verzi

### <a name="support-for-windows-phone-81-projects"></a>Podpora pro projekty Windows Phone 8.1
Tato verze podporuje nyní následující nové cílové rozhraní framework zástupných názvů které je možné použít na cíl Windows Phone 8.1 projekty:

* WindowsPhone81 / WP81 (pro projekty založené na technologii Silverlight pro Windows Phone)
* WindowsPhoneApp81 / WPA81 (pro projekty založené na WinRT aplikací Windows Phone)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aktualizace rozšíření prostředí WebMatrix NuGet
Tato verze aktualizuje klienta NuGet v WebMatrix za účelem [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 a přichází s funkcí jako XDT transformace. Důležitější je, 2.6.1 aktualizací core umožňuje klientovi služby WebMatrix instalace balíčků NuGet, které obsahují novějších verzích `.nuspec` schématu, která zahrnuje balíčky NuGet technologie ASP.NET.

Další informace o aktualizaci rozšíření nástroje WebMatrix, zjistěte, jaké konkrétní [poznámky k verzi](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Opravy chyb
Kromě těchto funkcí tato verze NuGet obsahuje ostatní opravy chyb. Došlo k 16 celkový problémy zákazníky a vyřešené ve verzi. Úplný seznam pracovní položky opravených NuGet 2.8.1, prosím zobrazení [NuGet sledování problémů pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping pomocí sady Visual Studio "14" CTP
Ve Visual Studiu "14" CTP vydala 3. června 2014 je v poli dodané NuGet 2.8.1. Funkce se podporují zůstávají v pamětích s další 2.8.1 VSIXes, jako je třeba pro Visual Studio 2013.
