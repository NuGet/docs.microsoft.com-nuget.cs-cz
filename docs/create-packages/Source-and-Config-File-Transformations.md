---
title: Zdrojových a konfiguračních souborů transformace pro balíčky NuGet
description: Podrobnosti o možnost pro balíčky NuGet pro transformaci zdrojový kód a konfigurační soubory (XML) při instalaci.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c2cd61b692b80cdc45fce399483cda3b57d12e5e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547682"
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformace zdrojového kódu a konfiguračních souborů

Pro projekty používající `packages.config`NuGet podporuje schopnost provádět transformace ke zdrojovému kódu a konfigurační soubory v balíčku nainstalovat a odinstalovat časy. Pouze transformace zdrojového kódu se použijí při instalaci balíčku v projektu pomocí [PackageReference](../consume-packages/package-references-in-project-files.md).

A **zdrojového kódu transformace** platí jednosměrné nahrazování tokenů pro soubory v balíčku `content` nebo `contentFiles` složky (`content` pro zákazníky, kteří používají `packages.config` a `contentFiles` pro `PackageReference`) při instalaci balíčku, kde tokeny odkazují sady Visual Studio [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Díky tomu můžete vložit soubor do oboru názvů v projektu nebo upravit kód, který by obvykle přejděte do `global.asax` v projektu aplikace ASP.NET.

A **transformace souboru config** umožňuje upravovat soubory, které již existují v cílový projekt, například `web.config` a `app.config`. Například může být nutné přidat položku pro váš balíček `modules` oddílu v konfiguračním souboru. Tato transformace provádí včetně speciální souborů v balíčku, které popisují oddíly pro přidání konfiguračních souborů. Při odinstalaci balíčku, tyto změny budou stejně se pak vrátit zpět, takže jde obousměrný transformace.

## <a name="specifying-source-code-transformations"></a>Určení zdrojového kódu transformace

1. Soubory, které chcete vložit do projektu z balíčku musí být umístěn v balíčku `content` a `contentFiles` složek. Například, pokud chcete soubor s názvem `ContosoData.cs` nainstalovaný v `Models` složek na cílový projekt, musí se nacházet uvnitř `content\Models` a `contentFiles\{lang}\{tfm}\Models` složky v balíčku.

1. Chcete-li dát pokyn použít náhradních tokenů v době instalace balíčků NuGet, přidejte `.pp` k názvu souboru zdrojového kódu. Po dokončení instalace, soubor nebude mít `.pp` rozšíření.

    Například, aby transformace v `ContosoData.cs`, název souboru v balíčku `ContosoData.cs.pp`. Po dokončení instalace se zobrazí jako `ContosoData.cs`.

1. V souboru zdrojového kódu používat velká a malá písmena tokeny ve formátu `$token$` k označení hodnoty by měly nahradit tento NuGet s vlastnostmi projektu:

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    Po instalaci, nahradí NuGet `$rootnamespace$` s `Fabrikam` za předpokladu, že cílový projekt uživatele, jejichž kořenový obor názvů se `Fabrikam`.

`$rootnamespace$` Token je vlastnost nejčastěji používané projektu; všechny ostatní jsou uvedeny v [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Mějte na paměti, samozřejmě, že některé vlastnosti můžou být specifické pro daný typ projektu.

## <a name="specifying-config-file-transformations"></a>Určení transformace souboru config

Jak je popsáno v následující části, transformace souboru konfigurace lze provést dvěma způsoby:

- Zahrnout `app.config.transform` a `web.config.transform` soubory vašeho balíčku `content` složku, ve kterém `.transform` rozšíření informuje NuGet, že tyto soubory obsahují kód XML ke sloučení s existujícími soubory konfigurace při instalaci balíčku. Při odinstalaci balíčku, odebere se tento stejný XML.
- Zahrnout `app.config.install.xdt` a `web.config.install.xdt` soubory vašeho balíčku `content` složky, pomocí [XDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx) k popisu požadované změny. Pomocí této možnosti můžete také zahrnout `.uninstall.xdt` souboru můžete vrátit změny, když balíček se odebere z projektu.

> [!Note]
> Transformace se nepoužije `.config` soubory na něho odkazovat jako na odkaz v sadě Visual Studio.

Výhodou použití XDT je, že místo jednoduše sloučení dvou statické soubory, poskytuje syntaxi pro manipulaci s strukturu pomocí elementu a atribut párování pomocí plná podpora jazyka XPath modelu DOM jazyka XML. XDT můžete pak přidat, aktualizovat, nebo odebrat prvky, umístěte nové prvky v konkrétním umístění nebo nahrazení nebo odebrat prvky (včetně podřízených uzlů). To umožňuje jednoduché vytvoření odinstalovat transformací, které zrušíte všechny transformace provést během instalace balíčku.

### <a name="xml-transforms"></a>Transformace XML

`app.config.transform` a `web.config.transform` v balíčku `content` složka obsahovat pouze prvky ke sloučení do existujícího projektu `app.config` a `web.config` soubory.

Jako příklad předpokládejme, že projekt zpočátku obsahuje následující obsah `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Přidat `MyNuModule` elementu `modules` části během instalace balíčku, vytvořte `web.config.transform` souborů v balíčku `content` složku, která vypadá takto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Po instalaci balíčku NuGet `web.config` bude vypadat následovně:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Všimněte si, že se nepovedlo nahradit NuGet `modules` části, je právě sloučili novou položku do ní přidáním pouze nové prvky a atributy. NuGet nedojde ke změně žádné stávající elementy nebo atributy.

Po odinstalaci balíčku NuGet se zaměřuje `.transform` soubory znovu a obsahuje prvky odeberete z příslušné `.config` soubory. Všimněte si, že tento proces nebude mít vliv na všechny řádky `.config` soubor, který můžete upravit po instalaci balíčku.

Jako podrobnější příklad [chyba protokolovací moduly a obslužné rutiny pro technologie ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) balíček přidává mnoho položek do `web.config`, které jsou znovu odebrány při odinstalaci balíčku.

Prozkoumat její `web.config.transform` soubor, stáhněte si balíček ELMAH z výše uvedeného odkazu, změna rozšíření balíčku z `.nupkg` k `.zip`a pak otevřete `content\web.config.transform` v daném souboru ZIP.

Pokud chcete posoudit účinek parametru instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v sadě Visual Studio (šablony je pod **Visual C# > Web** v dialogovém okně Nový projekt) a vyberte prázdnou aplikaci ASP.NET. Otevřít `web.config` zobrazíte jeho počátečního stavu. Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**vyhledat ELMAH na nuget.org a nainstalujte nejnovější verzi. Všimněte si, že všechny změny `web.config`. Teď odinstalovat balíček a uvidíte `web.config` vrátit do předchozího stavu.

### <a name="xdt-transforms"></a>Transformuje XDT

Můžete upravit konfigurační soubory pomocí [XDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx). Je také možné nahradit tokeny s NuGet [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) zahrnutím název vlastnosti v rámci `$` dají (velká a malá písmena).

Například následující `app.config.install.xdt` vloží soubor `appSettings` elementu do `app.config` obsahující `FullPath`, `FileName`, a `ActiveConfigurationSettings` hodnoty z projektu:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

Další příklad předpokládejme, že projekt zpočátku obsahuje následující obsah `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Přidat `MyNuModule` elementu `modules` části během balíček nainstalovat, balíčku `web.config.install.xdt` by obsahovat následující:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

Po instalaci balíčku, `web.config` bude vypadat například takto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Odebrání pouze `MyNuModule` element během odinstalace balíčku `web.config.uninstall.xdt` soubor by měl obsahovat následující:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
