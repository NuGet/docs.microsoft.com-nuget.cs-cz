---
title: Obsah balíčku NuGet rozhraní API
description: Základní adresa balíčku je jednoduché rozhraní pro načítání balíčku sám sebe.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819174"
---
# <a name="package-content"></a>Obsah balíčku

Je možné ke generování adresy URL se načíst obsah libovolného balíčku (souboru .nupkg v podadresáři) pomocí rozhraní API V3. Je prostředku používaného pro načítání obsahu balíčku `PackageBaseAddress` v nalezen prostředek [indexu služby](service-index.md). Tento prostředek také umožňuje zjišťování všech verzí balíčku, uvedené nebo není uveden v seznamu.

Tento prostředek se obvykle označuje jako buď "balíček základní adresu" nebo "ploché container".

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnota se používá:

@type Hodnota              | Poznámky
------------------------ | -----
PackageBaseAddress/3.0.0 | Původní verze

## <a name="base-url"></a>Základní adresu URL

Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s zmíněnými prostředků `@type` hodnotu. V následujícím dokumentu zástupného textu základní adresa URL `{@id}` se použije.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL v podpory registrace prostředků nalezen metody HTTP `GET` a `HEAD`.

## <a name="enumerate-package-versions"></a>Zobrazení výčtu verze balíčku

Když klient zná ID balíčku a chce zjistit, které balíčku verze balíčku zdroj má k dispozici, klient můžete vytvořit adresu URL předvídatelný výčet všechny verze balíčku. Tento seznam je určené jako "adresářů" pro balíček obsahu API uvedených níže.

> [!Note]
> Tento seznam obsahuje obě verze uvedené a neuvedené balíček.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry žádosti

Název     | V     | Typ    | Požadováno | Poznámky
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adresa URL    | odkazy řetězců  | Ano      | ID balíčku, malá písmena

`LOWER_ID` Hodnota je psané malými písmeny pomocí pravidel implementovaných podle ID požadované balíčku. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.

### <a name="response"></a>Odpověď

Pokud zdroj balíčku má žádné verzích ID zadaný balíček, je vrácen 404 stavový kód.

Pokud zdroj balíčku má jeden nebo více verzí, je vrácen 200 stavový kód. Text odpovědi je objekt JSON s následující vlastnost:

Název     | Typ             | Požadováno | Poznámky
-------- | ---------------- | -------- | -----
verze | Pole řetězců. | Ano      | Balíček ID, které jsou k dispozici

Řetězce v `versions` pole jsou všechny psané malými písmeny, [normalized řetězce verze NuGet](../reference/package-versioning.md#normalized-version-numbers). Řetězce verze neobsahují žádné SemVer 2.0.0 metadata sestavení.

Účelem je, že řetězce verze součástí toto pole lze použít doslovné pro `LOWER_VERSION` tokeny najít v následujících koncových bodů.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Stažení obsahu balíčku (.nupkg)

Pokud klient zná ID balíčku a verze a chce stáhnout obsah balíčku, potřebují jenom vytvořit následující adresu URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parametry žádosti

Název          | V     | Typ   | Požadováno | Poznámky
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Adresa URL    | odkazy řetězců | Ano      | ID balíčku, malá písmena
LOWER_VERSION | Adresa URL    | odkazy řetězců | Ano      | Verze balíčku normalized a psané malými písmeny

Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.

`LOWER_VERSION` Je verze balíčku požadované normalized pomocí verze NuGet [normalizaci pravidla](../reference/package-versioning.md#normalized-version-numbers). To znamená, že aby metadata sestavení, kterou specifikace SemVer 2.0.0 se musí v tomto případě vyloučit.

### <a name="response-body"></a>Text odpovědi

Pokud balíček existuje ve zdroji balíčku, je vrácena 200 stavový kód. Text odpovědi bude obsah balíčku sám sebe.

Pokud balíček neexistuje ve zdroji balíčku, je vrácena 404 stavový kód.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Ukázková odpověď

Binární datový proud, který je .nupkg pro Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Stáhněte manifest balíčku (s příponou .nuspec)

Pokud klient zná ID balíčku a verze a chce stáhnout manifest balíčku, potřebují jenom vytvořit následující adresu URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parametry žádosti

Název          | V     | Typ    | Požadováno | Poznámky
------------- | ------ | ------- | -------- | -----
LOWER_ID      | Adresa URL    | odkazy řetězců  | Ano      | ID balíčku, malá písmena
LOWER_VERSION | Adresa URL    | integer | Ano      | Verze balíčku normalized a psané malými písmeny

Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.

`LOWER_VERSION` Je verze balíčku požadované normalized pomocí verze NuGet [normalizaci pravidla](../reference/package-versioning.md#normalized-version-numbers). To znamená, že aby metadata sestavení, kterou specifikace SemVer 2.0.0 se musí v tomto případě vyloučit.

### <a name="response-body"></a>Text odpovědi

Pokud balíček existuje ve zdroji balíčku, je vrácena 200 stavový kód. Text odpovědi bude manifest balíčku, který je příponou .nuspec obsažené v odpovídající .nupkg. Příponou .nuspec je dokument XML.

Pokud balíček neexistuje ve zdroji balíčku, je vrácena 404 stavový kód.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Ukázková odpověď

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
