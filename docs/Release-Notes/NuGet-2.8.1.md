---
title: "Poznámky k verzi NuGet 2.8.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 2.8.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.8.1 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-281-release-notes"></a>Poznámky k verzi NuGet 2.8.1

[Poznámky k verzi NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet ve verzi 2.8.2 poznámky k verzi](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 byla vydána 2. dubna 2014.

## <a name="notable-features-in-the-release"></a>Upozorňují na důležité funkce ve verzi

### <a name="support-for-windows-phone-81-projects"></a>Podpora pro projekty Windows Phone 8.1
Tato verze podporuje nyní následující nové monikery framework cíl které se dají použít na cíl Windows Phone 8.1 projekty:

* WindowsPhone81 / WP81 (pro projekty založeného na technologii Silverlight pro Windows Phone)
* WindowsPhoneApp81 / WPA81 (pro projekty založené na WinRT aplikací Windows Phone)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aktualizuje se rozšíření prostředí WebMatrix NuGet
Tato verze aktualizuje klienta NuGet nalezen ve službě WebMatrix k [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 a přináší s funkce jako je například XDT transformace. Je důležité, 2.6.1 základní aktualizace umožňuje, aby klient služby WebMatrix instalace balíčků NuGet, které obsahují novějších verzích `.nuspec` schématu, která zahrnuje balíčků ASP.NET NuGet.

Další informace o aktualizaci rozšíření prostředí WebMatrix, zjistěte, jaké konkrétní [poznámky k verzi](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Opravy chyb
Kromě těchto funkcích tato verze NuGet obsahuje ostatní opravy chyb. Nebyly 16 celkový problémy řešeny v verze. Úplný seznam pracovní položky pevná ve NuGet 2.8.1, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping pomocí sady Visual Studio "14" CTP
V sadě Visual Studio "14" CTP vydala 2014 3. června je dodáván NuGet 2.8.1 v poli. Funkce se podporují zůstávají v nominální s další 2.8.1 VSIXes, jako je třeba pro Visual Studio 2013.
