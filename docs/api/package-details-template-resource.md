---
title: Šablona adresy URL s podrobnostmi balíčku, API NuGet
description: Šablona adresa URL podrobností balíčku umožňuje klientům zobrazit v uživatelském rozhraní webový odkaz na další podrobnosti balíčku.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610961"
---
# <a name="package-details-url-template"></a>Šablona adresy URL s podrobnostmi balíčku

Je možné, že klient vytvoří adresu URL, kterou může uživatel použít k zobrazení dalších podrobností o balíčku ve webovém prohlížeči. To je užitečné, když zdroj balíčku chce zobrazit další informace o balíčku, který se nemusí vejít do rozsahu, který se zobrazí v klientské aplikaci NuGet.

Prostředek použitý k vytvoření této adresy URL je prostředek `PackageDetailsUriTemplate`, který se našel v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použijí se následující hodnoty `@type`:

hodnota @type                     | Poznámky
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Počáteční verze

## <a name="url-template"></a>Šablona adresy URL

Adresa URL následujícího rozhraní API je hodnota vlastnosti `@id` přidružená k jedné z výše uvedených `@type` hodnot prostředku.

## <a name="http-methods"></a>Metody HTTP

I když klient nemá v úmyslu vytvářet požadavky na adresu URL podrobností balíčku jménem uživatele, měla by webová stránka podporovat metodu `GET`, aby bylo možné snadno otevřít otevřenou adresu URL ve webovém prohlížeči.

## <a name="construct-the-url"></a>Vytvoření adresy URL

Vzhledem k známému ID a verzi balíčku může implementace klienta vytvořit adresu URL používanou pro přístup k webovému rozhraní. Implementace klienta by měla zobrazit tuto vytvořenou adresu URL (nebo odkaz na odkaz) pro uživatele, který jim umožní otevřít webový prohlížeč na adresu URL a získat další informace o balíčku. Obsah stránky s podrobnostmi balíčku je určený implementací serveru.

Adresa URL musí být absolutní adresa URL a schéma (protokol) musí být HTTPS.

Hodnota `@id` v indexu služby je řetězec adresy URL obsahující následující zástupné tokeny:

### <a name="url-placeholders"></a>Zástupné symboly adresy URL

Name        | Typ    | Požadováno | Poznámky
----------- | ------- | -------- | -----
`{id}`      | odkazy řetězců  | Ne       | ID balíčku, pro který se mají získat podrobnosti
`{version}` | odkazy řetězců  | Ne       | Verze balíčku, pro který se mají získat podrobnosti

Server by měl přijmout `{id}` a `{version}` hodnoty s libovolným písmenem. Kromě toho by neměl být server citlivý na to, jestli je verze [normalizovaná](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers). Jinými slovy, server by měl přijímat také nenormalizované verze.

Například šablona s podrobnostmi balíčku NuGet. org vypadá takto:

    https://www.nuget.org/packages/{id}/{version}

Pokud implementace klienta potřebuje zobrazit odkaz na podrobnosti balíčku pro NuGet. 4.3.0 správy verzí, vytvoří následující adresu URL a poskytne jí uživateli:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
