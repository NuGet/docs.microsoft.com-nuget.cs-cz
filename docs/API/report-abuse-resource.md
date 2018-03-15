---
title: "Sestavy zneužití URL šablony, NuGet rozhraní API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Šablona sestavy zneužití URL umožňuje klientům zobrazit odkaz v jejich uživatelského rozhraní."
keywords: "Rozhraní API NuGet oznámení zneužití, rozhraní API NuGet souboru předpisy, šablona adresy URL sestavy nuget.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: efbe5704e6e6028f9382fea3fe5ec453f573a2e9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="report-abuse-url-template"></a>Šablona sestavy zneužití adresy URL

Je možné pro klienta sestavit adresu URL, kterého uživatel k oznámení zneužití o určitém balíčku. To je užitečné, když chce zdroj balíčku povolit všechny činnosti klienta (i 3. stran) delegovat zneužití sestavy ke zdroji balíčku.

Je prostředku používaného pro načítání obsahu balíčku `ReportAbuseUriTemplate` v nalezen prostředek [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` se používají hodnoty:

@type Hodnota                       | Poznámky
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | Původní verze
ReportAbuseUriTemplate/3.0.0-rc   | Alias `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Adresa URL šablony

Adresa URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s jedním z výše uvedených prostředků `@type` hodnoty.

## <a name="http-methods"></a>Metody HTTP

I když klient není určen provádět požadavky na adresu URL sestavy zneužití jménem uživatele, musí podporovat webové stránky `GET` metoda umožňující kliknutelnou URL snadno otevřít ve webovém prohlížeči.

## <a name="construct-the-url"></a>Vytvořit adresu URL

Zadané ID známých balíčku a verzi, implementace klienta můžete vytvořit adresu URL používá pro přístup k webovému rozhraní. Implementace klienta by měl zobrazit tento vytvořený adresa URL (nebo prokliknutelný odkaz) uživateli, což jim aby otevřete webový prohlížeč na adresu URL a proveďte všechny nezbytné zneužití sestavy. Implementace formuláře pro hlášení zneužití je určen podle implementaci serveru.

Hodnota `@id` je adresa URL řetězec obsahující všechny následující zástupný symbol tokenů:

### <a name="url-placeholders"></a>Adresa URL zástupné symboly

Název        | Typ    | Požadováno | Poznámky
----------- | ------- | -------- | -----
`{id}`      | odkazy řetězců  | Ne       | ID balíčku k oznámení zneužití pro
`{version}` | odkazy řetězců  | Ne       | Verze balíčku k oznámení zneužití pro

`{id}` a `{version}` hodnoty interpretovány implementací serveru musí být malá a velká písmena a zda je verze normalizovány není citlivé.

Šablona zneužití sestavy nuget.org například vypadá takto:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Pokud implementace klienta potřebuje k zobrazení odkaz na formulář zneužití sestavy NuGet.Versioning 4.3.0, by se vytvořit následující adresu URL a poskytne mu uživateli:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
