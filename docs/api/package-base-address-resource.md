---
title: Obsah balíčku, rozhraní API NuGet
description: Základní adresa balíčku je jednoduché rozhraní pro načtení samotného balíčku.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488223"
---
# <a name="package-content"></a>Obsah balíčku

Je možné vygenerovat adresu URL pro načtení obsahu libovolného balíčku (soubor. nupkg) pomocí rozhraní V3 API. Prostředek, který se používá pro načítání obsahu balíčku, `PackageBaseAddress` je prostředek, který se našel v [indexu služby](service-index.md). Tento prostředek také umožňuje zjišťování všech verzí balíčku uvedených v seznamu nebo bez jeho uvedení na seznamu.

Tento prostředek se běžně označuje jako základní adresa balíčku nebo jako "plochý kontejner".

## <a name="versioning"></a>Správa verzí

Použije se `@type` následující hodnota:

@typeosa              | Poznámky
------------------------ | -----
PackageBaseAddress/3.0.0 | Počáteční verze

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti přidružené k uvedené hodnotě prostředku. `@type` V následujícím dokumentu se použije zástupná základní `{@id}` adresa URL.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v registračním prostředku podporují metody `GET` http `HEAD`a.

## <a name="enumerate-package-versions"></a>Zobrazení výčtu verzí balíčků

Pokud klient zná ID balíčku a chce zjistit, které verze balíčků má zdroj balíčku k dispozici, může klient sestavit předvídatelné adresy URL pro zobrazení výčtu všech verzí balíčků. Tento seznam má být "výpis adresáře" pro rozhraní API obsahu balíčku, který je uveden níže.

> [!Note]
> Tento seznam obsahuje uvedené i neuvedené verze balíčků.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry žádosti

Name     | V     | type    | Požadováno | Poznámky
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adresa URL    | odkazy řetězců  | ano      | ID balíčku, malá písmena

`LOWER_ID` Hodnota je ID požadovaného balíčku s malými písmeny pomocí pravidel implementovaných pomocí. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metoda netto.

### <a name="response"></a>Odpověď

Pokud zdroj balíčku nemá žádné verze zadaného ID balíčku, vrátí se stavový kód 404.

Pokud má zdroj balíčku jednu nebo více verzí, vrátí se stavový kód 200. Tělo odpovědi je objekt JSON s následující vlastností:

Name     | type             | Požadováno | Poznámky
-------- | ---------------- | -------- | -----
verze | pole řetězců | ano      | Dostupná ID balíčků

Řetězce v `versions` poli jsou všechny s malými písmeny, [normalizované řetězce verze NuGet](../concepts/package-versioning.md#normalized-version-numbers). Řetězce verze neobsahují žádná metadata buildu SemVer 2.0.0.

Záměrem je, aby se pro `LOWER_VERSION` tokeny, které se nacházejí v následujících koncových bodech, používaly doslovné řetězce verze v tomto poli.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Stáhnout obsah balíčku (. nupkg)

Pokud klient zná ID a verzi balíčku a chce stáhnout obsah balíčku, stačí vytvořit následující adresu URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parametry žádosti

Name          | V     | type   | Požadováno | Poznámky
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Adresa URL    | odkazy řetězců | ano      | ID balíčku, malá písmena
LOWER_VERSION | Adresa URL    | odkazy řetězců | ano      | Verze balíčku, normalizovaná a malá

`LOWER_ID` A`LOWER_VERSION` jsou malá pomocí pravidel implementovaných pomocí. SÍŤ[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
Metoda.

Je požadovaná verze balíčku normalizovaná pomocí pravidel normalizace verzí NuGet. [](../concepts/package-versioning.md#normalized-version-numbers) `LOWER_VERSION` To znamená, že v tomto případě musí být vyloučena metadata sestavení, která jsou povolena specifikací SemVer 2.0.0.

### <a name="response-body"></a>Text odpovědi

Pokud balíček existuje ve zdroji balíčku, vrátí se stavový kód 200. Tělo odpovědi bude samotný obsah balíčku.

Pokud balíček ve zdroji balíčku neexistuje, vrátí se stavový kód 404.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Ukázková odpověď

Binární datový proud, který je souborem. nupkg pro Newtonsoft. JSON 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Stáhnout manifest balíčku (. nuspec)

Pokud klient zná ID a verzi balíčku a chce stáhnout manifest balíčku, stačí vytvořit následující adresu URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parametry žádosti

Name          | V     | type   | Požadováno | Poznámky
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Adresa URL    | odkazy řetězců | ano      | ID balíčku, malá písmena
LOWER_VERSION | Adresa URL    | odkazy řetězců | ano      | Verze balíčku, normalizovaná a malá

`LOWER_ID` A`LOWER_VERSION` jsou malá pomocí pravidel implementovaných pomocí. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metoda netto.

Je požadovaná verze balíčku normalizovaná pomocí pravidel normalizace verzí NuGet. [](../concepts/package-versioning.md#normalized-version-numbers) `LOWER_VERSION` To znamená, že v tomto případě musí být vyloučena metadata sestavení, která jsou povolena specifikací SemVer 2.0.0.

### <a name="response-body"></a>Text odpovědi

Pokud balíček existuje ve zdroji balíčku, vrátí se stavový kód 200. Tělo odpovědi bude manifest balíčku, který je soubor. nuspec obsažený v odpovídajícím nupkg. Soubor. nuspec je dokument XML.

Pokud balíček ve zdroji balíčku neexistuje, vrátí se stavový kód 404.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Ukázková odpověď

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
