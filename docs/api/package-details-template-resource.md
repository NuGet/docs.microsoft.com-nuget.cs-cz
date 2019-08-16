---
title: Šablona adresy URL s podrobnostmi balíčku, API NuGet
description: Šablona adresa URL podrobností balíčku umožňuje klientům zobrazit v uživatelském rozhraní webový odkaz na další podrobnosti balíčku.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 6657536ea6c699a834f57494c66b2a7d741dfcb7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488170"
---
# <a name="package-details-url-template"></a>Šablona adresy URL s podrobnostmi balíčku

Je možné, že klient vytvoří adresu URL, kterou může uživatel použít k zobrazení dalších podrobností o balíčku ve webovém prohlížeči. To je užitečné, když zdroj balíčku chce zobrazit další informace o balíčku, který se nemusí vejít do rozsahu, který se zobrazí v klientské aplikaci NuGet.

Prostředek použitý k vytvoření této adresy URL je prostředek `PackageDetailsUriTemplate` , který se našel v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použijí se `@type` tyto hodnoty:

@typeosa                     | Poznámky
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Počáteční verze

## <a name="url-template"></a>Šablona adresy URL

Adresa URL následujícího rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených hodnot prostředků. `@type`

## <a name="http-methods"></a>Metody HTTP

I když klient nemá v úmyslu vytvářet požadavky na adresu URL podrobností balíčku jménem uživatele, měla by tato webová stránka podporovat `GET` metodu, aby bylo možné snadno otevřít otevřenou webovou stránku ve webovém prohlížeči.

## <a name="construct-the-url"></a>Vytvoření adresy URL

Vzhledem k známému ID a verzi balíčku může implementace klienta vytvořit adresu URL používanou pro přístup k webovému rozhraní. Implementace klienta by měla zobrazit tuto vytvořenou adresu URL (nebo odkaz na odkaz) pro uživatele, který jim umožní otevřít webový prohlížeč na adresu URL a získat další informace o balíčku. Obsah stránky s podrobnostmi balíčku je určený implementací serveru.

Adresa URL musí být absolutní adresa URL a schéma (protokol) musí být HTTPS.

Hodnota `@id` v indexu služby je řetězec adresy URL obsahující kteroukoli z následujících zástupných tokenů:

### <a name="url-placeholders"></a>Zástupné symboly adresy URL

Name        | type    | Požadováno | Poznámky
----------- | ------- | -------- | -----
`{id}`      | odkazy řetězců  | Ne       | ID balíčku, pro který se mají získat podrobnosti
`{version}` | odkazy řetězců  | Ne       | Verze balíčku, pro který se mají získat podrobnosti

Server by měl přijmout `{id}` hodnoty `{version}` a s libovolnými velkými písmeny. Kromě toho by neměl být server citlivý na to, jestli je verze [normalizovaná](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers). Jinými slovy, server by měl přijímat také nenormalizované verze.

Například šablona s podrobnostmi balíčku NuGet. org vypadá takto:

    https://www.nuget.org/packages/{id}/{version}

Pokud implementace klienta potřebuje zobrazit odkaz na podrobnosti balíčku pro NuGet. 4.3.0 správy verzí, vytvoří následující adresu URL a poskytne jí uživateli:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
