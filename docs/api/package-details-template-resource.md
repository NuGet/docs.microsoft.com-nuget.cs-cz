---
title: Sbalit podrobnosti o adresu URL šablony NuGet rozhraní API
description: Šablona adresy URL podrobnosti balíčku umožňuje klientům zobrazovat v jejich uživatelského rozhraní webového odkaz na další podrobnosti o balíčku
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638086"
---
# <a name="package-details-url-template"></a>Šablona adresy URL podrobnosti balíčku

Je možné pro klienta sestavit adresu URL, která je možné uživatele zobrazíte další podrobnosti balíčku ve webovém prohlížeči. To je užitečné, pokud chce zobrazit další informace o balíčku, který se nemusí vejde v rámci oboru co klientská aplikace NuGet zobrazuje zdroje balíčku.

Je použit k sestavení tuto adresu URL prostředku `PackageDetailsUriTemplate` prostředek se nenašel v [index služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnoty:

@type Hodnota                     | Poznámky
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Počáteční verze

## <a name="url-template"></a>Adresa URL šablony

Adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty.

## <a name="http-methods"></a>Metody HTTP

I když klient není určen tak, aby adresa URL balíčku podrobnosti žádosti jménem uživatele, by měly podporovat webové stránky `GET` metoda umožňující kliknutí na adresu URL snadno otevřít ve webovém prohlížeči.

## <a name="construct-the-url"></a>Vytvořit adresu URL

Zadané ID známých balíčku a verzi, implementace klienta můžete vytvořit adresu URL pro přístup k webovým rozhraním. Implementace klienta pro uživatele, kterým otevřete webový prohlížeč na adresu URL a další informace o balíčku zobrazeno tento konstruovaný adresy URL (nebo prokliknutelný odkaz). Obsah stránky s podrobnostmi balíčku je určeno implementaci serveru.

Adresa URL musí být absolutní adresu URL a schéma (protokolu) musí být HTTPS.

Hodnota `@id` ve službě index je řetězec adresy URL obsahující některý z následujících tokeny zástupný symbol:

### <a name="url-placeholders"></a>Adresa URL zástupné symboly

Název        | Type    | Požadováno | Poznámky
----------- | ------- | -------- | -----
`{id}`      | odkazy řetězců  | Ne       | ID balíčku získat podrobnosti pro
`{version}` | odkazy řetězců  | Ne       | Verze balíčku získat podrobnosti pro

Server by měl přijmout `{id}` a `{version}` hodnoty všechny velká a malá písmena. Kromě toho by neměl být citlivé na tom, jestli je verze serveru [normalizované](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). Jinými slovy, by měla přijímat server také přijímat nenormalizovaný verze.

Například šablona podrobnosti balíčku nuget.org vypadá například takto:

    https://www.nuget.org/packages/{id}/{version}

Pokud implementace klienta zobrazí odkaz na podrobné informace balíčku pro NuGet.Versioning 4.3.0, to by vytvořit následující adresu URL a poskytují uživateli:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
