---
title: Sestava šablony adres URL pro zneužití, API NuGet
description: Šablona URL pro zneužití sestavy umožňuje klientům zobrazit v uživatelském rozhraní odkaz na zneužití sestavy.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775230"
---
# <a name="report-abuse-url-template"></a>Šablona adresy URL pro zneužití sestavy

Je možné, že klient vytvoří adresu URL, kterou může uživatel použít k nahlášení zneužití k určitému balíčku. To je užitečné, když zdroj balíčku chce povolit všem klientským prostředím (dokonce i třetí straně) delegovat zprávy o zneužití na zdroj balíčku.

Prostředek použitý k vytvoření této adresy URL je prostředek, který se `ReportAbuseUriTemplate` našel v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použijí se tyto `@type` hodnoty:

@type osa                       | Poznámky
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0 – beta | Počáteční verze
ReportAbuseUriTemplate/3.0.0 – RC   | Alias pro `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Šablona adresy URL

Adresa URL následujícího rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených `@type` hodnot prostředků.

## <a name="http-methods"></a>Metody HTTP

I když klient nemá v úmyslu vytvářet požadavky na adresu URL pro zneužití zprávy jménem uživatele, měla by webová stránka podporovat `GET` metodu, aby bylo možné snadno otevřít otevřenou adresu URL ve webovém prohlížeči.

## <a name="construct-the-url"></a>Vytvoření adresy URL

Vzhledem k známému ID a verzi balíčku může implementace klienta vytvořit adresu URL používanou pro přístup k webovému rozhraní. Implementace klienta by měla zobrazit tuto vytvořenou adresu URL (nebo odkaz na odkaz) uživateli, který jim umožní otevřít webový prohlížeč na adresu URL a udělat si veškerou potřebnou zprávu o zneužití. Implementaci formuláře sestavy o zneužití je určeno implementací serveru.

Hodnota `@id` je řetězec adresy URL obsahující kteroukoli z následujících zástupných tokenů:

### <a name="url-placeholders"></a>Zástupné symboly adresy URL

Název        | Typ    | Vyžadováno | Poznámky
----------- | ------- | -------- | -----
`{id}`      | řetězec  | ne       | ID balíčku pro nahlášení zneužití pro
`{version}` | řetězec  | ne       | Verze balíčku pro nahlášení zneužití pro

`{id}`Hodnoty a, které `{version}` jsou interpretovány implementací serveru, musí rozlišovat velká a malá písmena a nerozlišují se, zda je verze normalizována.

Například šablona pro zneužití sestavy NuGet. org vypadá takto:

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Pokud implementace klienta potřebuje zobrazit odkaz na formulář pro zneužití sestav pro NuGet. 4.3.0 správy verzí, vytvoří následující adresu URL a poskytne jí uživateli:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
