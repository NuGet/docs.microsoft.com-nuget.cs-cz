---
title: "Zdroj a konfiguračním souboru transformace pro balíčky NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20991d69-9e2e-4881-bbf2-96ae634e1872
description: "Podrobnosti na možnost pro balíčky NuGet pro transformaci zdrojového kódu a konfigurační soubory (XML) při instalaci."
keywords: "Instalace balíčku NuGet, transformace balíčku NuGet, úprava konfiguračních souborů, úprava zdrojového kódu"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 89a55716ccbc9043cfce4c7f38ec8ab9a0e2f768
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformace zdrojového kódu a konfiguračních souborů

Pro projekty pomocí `packages.config` nebo `project.json`, NuGet podporuje schopnost provádět transformace ke zdrojovému kódu a konfigurační soubory v balíčku instalaci a odinstalaci časy.

> [!Note]
> Zdroj a konfigurační soubor transformace se nepoužívají při instalaci balíčku do projektu pomocí [odkazů balíčku v souborech projektu](../Consume-Packages/Package-References-in-Project-Files.md). 

A **zdrojového kódu transformace** jednosměrný tokenu nahrazení se vztahují na soubory v balíčku `content` složku, když je balíček nainstalován, kde najdete tokeny pro Visual Studio [projektu vlastnosti](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) . To umožňuje vložit soubor do projektu obor názvů nebo přizpůsobit kód, který obvykle přejde do `global.asax` v projektu aplikace ASP.NET.

A **transformace souboru config** umožňuje upravit soubory, které již existují v cílovém projektu, například `web.config` a `app.config`. Například může být nutné přidat položku, kterou chcete vašeho balíčku `modules` oddíl v konfiguračním souboru. Tato transformace je potřeba včetně speciální soubory v balíčku, který popisuje oddíly pro přidání konfiguračních souborů. Při odinstalaci balíčku, tyto změny budou stejně jsou pak vrátit zpět, provedení to obousměrný transformace.

## <a name="specifying-source-code-transformations"></a>Určení transformace zdrojového kódu

1. Soubory, které chcete vložit z balíčku do projektu musí být umístěn v balíčku `content` složky. Například, pokud chcete do souboru s názvem `ContosoData.cs` být nainstalovaný v `Models` složky cílový projekt, musí být uvnitř `content\Models` složky v balíčku.

1. Dáte pokyn, aby správci balíčků NuGet použít token nahrazení během instalace, připojte `.pp` k názvu souboru zdrojového kódu. Po instalaci, soubor nebude mít `.pp` rozšíření.

    Například aby transformace ve `ContosoData.cs`, název souboru v balíčku `ContosoData.cs.pp`. Po instalaci se zobrazí jako `ContosoData.cs`.

1. V souboru se zdrojovým kódem, použijte velká a malá písmena tokeny ve formátu `$token$` k určení hodnoty by měl tento NuGet nahraďte vlastností projektu:

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

    Po instalaci, nahradí NuGet `$rootnamespace$` s `Fabrikam` za předpokladu, že cílový projekt elementu, jehož kořenový obor názvů je `Fabrikam`.

`$rootnamespace$` Token je vlastnost nejčastěji používané projektu; všechny ostatní jsou uvedeny v [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) dokumentaci na webu MSDN. Mějte na paměti, samozřejmě platí, že některé vlastnosti může být specifické pro daný typ projektu.

## <a name="specifying-config-file-transformations"></a>Určení transformace souboru config

Jak je popsáno v následujících částech, konfigurační soubor transformace lze provést dvěma způsoby:

- Zahrnout `app.config.transform` a `web.config.transform` soubory do balíčku `content` složku, kde `.transform` rozšíření informuje NuGet, že tyto soubory obsahují soubor XML sloučit s existující konfigurační soubory, když je balíček nainstalován. Při odinstalaci balíčku, odeberou se tento stejný XML.
- (NuGet 2.6 a novější) Zahrnout `app.config.install.xdt` a `web.config.install.xdt` soubory do balíčku `content` složky, pomocí [XDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx) k popisu požadované změny. Pomocí této možnosti můžete použít také `.uninstall.xdt` souboru můžete vrátit změny, pokud balíček je odebrán z projektu.

> [!Note]
> Transformace se nepoužije `.config` souborů, který je odkazováno jako na odkaz v sadě Visual Studio.

Výhodou použití XDT je, že místo jednoduše sloučení dvou statické soubory, poskytuje syntaxi pro manipulaci s strukturu DOM XML pomocí elementu a atributu odpovídající pomocí plnou podporu jazyka XPath. XDT můžete pak přidat, aktualizovat, nebo odeberte elementy, umístit nové prvky v určitém místě nebo nahradit nebo odebrat elementy (včetně podřízených uzlů). Díky tomu přehledné vytvořit odinstalovat transformace, které se zpět na všechny transformace provést během instalace balíčku.

### <a name="xml-transforms"></a>Transformace XML.

`app.config.transform` a `web.config.transform` v balíčku na `content` složka obsahovat pouze elementy sloučit do projektu existující `app.config` a `web.config` soubory.

Jako příklad předpokládejme projekt původně obsahuje následující obsah `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

Chcete-li přidat `MyNuModule` elementu, který chcete `modules` během instalace balíčku, vytvořte `web.config.transform` souboru v balíčku `content` složky, která vypadá takto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

Po instalaci balíčku, NuGet `web.config` bude vypadat takto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

Všimněte si, že nebyla nahradit NuGet `modules` části, je právě sloučit nový záznam do ní přidáním pouze nové elementy a atributy. NuGet nezmění žádné existující elementy nebo atributy.

Při odinstalaci balíčku NuGet prozkoumá `.transform` soubory znovu a obsahuje prvky odeberete z příslušné `.config` soubory. Všimněte si, že tento proces nebude mít vliv na všechny řádky `.config` soubor, který upravíte po instalaci balíčku.

Jako v příkladu rozsáhlejší [moduly protokolování chyb a obslužné rutiny pro technologii ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) přidává balíček mnoho položky do `web.config`, které jsou znovu odebrány při odinstalaci balíčku.

Pro zjištění jeho `web.config.transform` soubor, stáhněte si balíček ELMAH z výše uvedený odkaz, změňte rozšíření balíčku z `.nupkg` k `.zip`a pak otevřete `content\web.config.transform` v tomto souboru ZIP.

Informace o účinku instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v sadě Visual Studio (šablona je pod **Visual C# > Web** v dialogovém okně Nový projekt) a vyberte prázdnou aplikaci ASP.NET. Otevřete `web.config` zobrazíte počátečního stavu. Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**, vyhledejte ELMAH na nuget.org a nainstalujte nejnovější verzi. Všimněte si, všechny změny do `web.config`. Teď má být balíček odinstalován a uvidíte `web.config` vrátit do předchozího stavu.

### <a name="xdt-transforms"></a>Transformuje XDT

S NuGet 2.6 nebo novější, můžete upravit konfigurační soubory pomocí [XDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx). Můžete taky nechat NuGet nahradit tokeny se [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) zahrnutím název vlastnosti v rámci `$` delimeters (velká a malá písmena).

Například následující `app.config.install.xdt` vloží soubor `appSettings` element do `app.config` obsahující `FullPath`, `FileName`, a `ActiveConfigurationSettings` hodnoty z projektu:

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

Další příklad předpokládejme projekt původně obsahuje následující obsah `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

Chcete-li přidat `MyNuModule` elementu, který chcete `modules` nainstalovat části během balíčku, balíčku `web.config.install.xdt` by obsahovat následující:

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

Po instalaci balíčku, `web.config` bude vypadat takto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

Pro odebrání pouze `MyNuModule` element během odinstalace balíčku `web.config.uninstall.xdt` soubor by měl obsahovat následující:

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
