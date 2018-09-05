---
title: Ohlásit nevhodné chování adresy URL šablony NuGet rozhraní API
description: Šablona adresy URL sestavy zneužití umožňuje klientům zobrazit odkaz kliknete v jejich uživatelského rozhraní.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549336"
---
# <a name="report-abuse-url-template"></a>Šablona adresy URL sestavy urážlivého příspěvku

Je možné sestavit adresu URL, kterého uživatel k oznámení zneužití o konkrétní balíček klienta. To je užitečné, pokud zdroj balíčku chce umožněte všechny klienta (i 3. stran) delegovat zneužití sestavy ke zdroji balíčku.

Je použit k sestavení tuto adresu URL prostředku `ReportAbuseUriTemplate` prostředek se nenašel v [index služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnoty:

@type Hodnota                       | Poznámky
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | Počáteční verze
ReportAbuseUriTemplate/3.0.0-rc   | Alias `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Adresa URL šablony

Adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty.

## <a name="http-methods"></a>Metody HTTP

I když klient není určena adresa URL sestavy zneužití provádět požadavky jménem uživatele, by měly podporovat webové stránky `GET` metoda umožňující kliknutí na adresu URL snadno otevřít ve webovém prohlížeči.

## <a name="construct-the-url"></a>Vytvořit adresu URL

Zadané ID známých balíčku a verzi, implementace klienta můžete vytvořit adresu URL pro přístup k webovým rozhraním. Implementace klienta pro uživatele, kterým otevřete webový prohlížeč na adresu URL a proveďte všechny nezbytné zneužití sestavy zobrazeno tento konstruovaný adresy URL (nebo prokliknutelný odkaz). Implementace formuláře zneužití sestavy je určeno implementaci serveru.

Hodnota `@id` je řetězec adresy URL obsahující některý z následujících tokeny zástupný symbol:

### <a name="url-placeholders"></a>Adresa URL zástupné symboly

Název        | Typ    | Požadováno | Poznámky
----------- | ------- | -------- | -----
`{id}`      | odkazy řetězců  | Ne       | ID balíčku, který chcete ohlásit příspěvek jako urážlivý
`{version}` | odkazy řetězců  | Ne       | Verze balíčku k oznámení zneužití pro

`{id}` a `{version}` hodnoty interpretovány implementací serveru musí být malá a velká písmena a nikoli citlivá, jestli je normalizovány na verzi.

Například šablona zneužití nuget.org sestavy vypadá například takto:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Pokud implementace klienta potřebuje k zobrazení odkazu do formuláře zneužití sestavy pro NuGet.Versioning 4.3.0, ho by vytvořit následující adresu URL a poskytují uživateli:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
