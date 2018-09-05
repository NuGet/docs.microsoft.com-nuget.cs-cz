---
title: Obsah balíčku NuGet rozhraní API
description: Základní adresa balíček je jednoduché rozhraní pro načítání samotném balíčku.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547151"
---
# <a name="package-content"></a>Balíček obsahu

Je možné ke generování adresy URL načíst obsah libovolného balíčku (souboru .nupkg) pomocí rozhraní API V3. Prostředek, který používá pro načtení balíčku obsahu je `PackageBaseAddress` prostředek se nenašel v [index služby](service-index.md). Tento prostředek také umožňuje zjišťování všech verzí balíčku uvedené nebo neuvedené v seznamu.

Tento prostředek se obvykle označuje jako buď "balíček základní adresa" nebo "ploché kontejneru".

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnota se používá:

@type Hodnota              | Poznámky
------------------------ | -----
PackageBaseAddress/3.0.0 | Počáteční verze

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přidružená k výše uvedených prostředků `@type` hodnotu. V následujícím dokumentu, zástupný symbol základní adresa URL `{@id}` se použije.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL, které jsou součástí zdroje podpory registrace metody HTTP `GET` a `HEAD`.

## <a name="enumerate-package-versions"></a>Výčet verzí balíčků

Pokud klient zná ID balíčku a chcete zjistit, které balíček verze balíčku zdroj nemá k dispozici, klient může vytvořit předvídatelné adresu URL se vytvořit výčet všech verzí balíčků. Tento seznam je určena být "výpis adresáře" pro balíček obsahu API, které jsou uvedené níže.

> [!Note]
> Tento seznam obsahuje obě verze uvedené a neuvedené v seznamu balíčků.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry žádosti

Název     | V     | Typ    | Požadováno | Poznámky
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adresa URL    | odkazy řetězců  | Ano      | ID balíčku, malá písmena

`LOWER_ID` Hodnotu ID požadovaný balíček psané malými písmeny pomocí pravidel implementované. NET společnosti [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

### <a name="response"></a>Odpověď

Pokud zdroj balíčku má žádné verze ID zadaného balíčku, je vrácen stavový kód 404.

Pokud zdroj balíčku má jednu nebo více verzí, vrátí se kód stavový kód 200. Text odpovědi je objekt JSON s následující vlastnost:

Název     | Typ             | Požadováno | Poznámky
-------- | ---------------- | -------- | -----
verze | pole řetězců | Ano      | Balíček ID, které jsou k dispozici

Řetězce ve `versions` pole jsou všechny psané malými písmeny, [normalizovat řetězce verze NuGet](../reference/package-versioning.md#normalized-version-numbers). Řetězce verze neobsahuje žádné SemVer 2.0.0 metadat sestavení.

Cílem je, že verze řetězce nalezen v tomto poli je možné verbatim pro `LOWER_VERSION` tokenů najdete v následujících koncových bodů.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Stáhnout obsah balíčku (.nupkg)

Pokud klient zná ID balíčku a verzi a chce stáhnout obsah balíčku, potřebují jenom vytvořit následující adresu URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parametry žádosti

Název          | V     | Typ   | Požadováno | Poznámky
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Adresa URL    | odkazy řetězců | Ano      | ID balíčku, malá písmena
LOWER_VERSION | Adresa URL    | odkazy řetězců | Ano      | Verze balíčku, normalizovaná a psané malými písmeny

Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
Metoda.

`LOWER_VERSION` Se verze balíčku požadovaného normalizuje pomocí verze Nugetu [normalizace pravidla](../reference/package-versioning.md#normalized-version-numbers). To znamená, že v tomto případě je třeba vyloučit tato sestavení metadata, která je povolena ve specifikaci SemVer 2.0.0.

### <a name="response-body"></a>Text odpovědi

Pokud balíček existuje ve zdroji balíčku, vrátí se kód stavový kód 200. Text odpovědi bude samotného obsahu balíčku.

Pokud balíček na zdroj balíčku neexistuje, vrátí se stavový kód 404.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Ukázková odpověď

Binární datový proud, který je .nupkg pro Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Stáhnout manifest balíčku (souboru .nuspec)

Pokud klient zná ID balíčku a verzi a chce, aby se stáhnout manifest balíčku, potřebují jenom vytvořit následující adresu URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parametry žádosti

Název          | V     | Typ    | Požadováno | Poznámky
------------- | ------ | ------- | -------- | -----
LOWER_ID      | Adresa URL    | odkazy řetězců  | Ano      | ID balíčku, malá písmena
LOWER_VERSION | Adresa URL    | integer | Ano      | Verze balíčku, normalizovaná a psané malými písmeny

Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET společnosti [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

`LOWER_VERSION` Se verze balíčku požadovaného normalizuje pomocí verze Nugetu [normalizace pravidla](../reference/package-versioning.md#normalized-version-numbers). To znamená, že v tomto případě je třeba vyloučit tato sestavení metadata, která je povolena ve specifikaci SemVer 2.0.0.

### <a name="response-body"></a>Text odpovědi

Pokud balíček existuje ve zdroji balíčku, vrátí se kód stavový kód 200. Text odpovědi bude manifest balíčku, který je souboru .nuspec obsažené v odpovídající .nupkg. Souboru .nuspec je dokument XML.

Pokud balíček na zdroj balíčku neexistuje, vrátí se stavový kód 404.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Ukázková odpověď

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
