---
title: Transformace zdrojového a konfiguračního souboru pro balíčky NuGet
description: Podrobnosti o možnosti balíčků NuGet pro transformaci zdrojového kódu a konfiguračních souborů (XML) po instalaci.
author: JonDouglas
ms.author: jodou
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 5bd0e409f527fb668008204fb16ad002f4784c46
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774588"
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformace zdrojového kódu a konfiguračních souborů

**Transformace zdrojového kódu** aplikuje jednosměrnou náhradu tokenu na soubory v balíčku `content` nebo `contentFiles` složce ( `content` pro zákazníky používající `packages.config` a `contentFiles` pro `PackageReference` ) při instalaci balíčku, kde tokeny odkazují na [Vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)sady Visual Studio. To umožňuje vložit soubor do oboru názvů projektu, nebo upravit kód, který by obvykle přešel do `global.asax` projektu ASP.NET.

**Transformace konfiguračního souboru** umožňuje upravit soubory, které již existují v cílovém projektu, například `web.config` a `app.config` . Balíček může například potřebovat přidat položku do `modules` oddílu v konfiguračním souboru. Tato transformace se provádí zahrnutím speciálních souborů do balíčku, které popisují oddíly, které se mají přidat do konfiguračních souborů. Při odinstalaci balíčku se tyto změny projeví opačným způsobem transformace.

## <a name="specifying-source-code-transformations"></a>Určení transformací zdrojového kódu

1. Soubory, které chcete vložit z balíčku do projektu, se musí nacházet v rámci balíčků `content` a `contentFiles` složek. Například pokud chcete, aby byl soubor s názvem `ContosoData.cs` nainstalován do `Models` složky cílového projektu, musí být uvnitř `content\Models` `contentFiles\{lang}\{tfm}\Models` složek a v balíčku.

1. Pokud chcete, aby NuGet při instalaci nahradil nahrazení tokenu, připojí se `.pp` k názvu souboru zdrojového kódu. Po instalaci nebude mít tento soubor `.pp` příponu.

    Chcete-li například transformovat v `ContosoData.cs` , pojmenujte soubor v balíčku `ContosoData.cs.pp` . Po instalaci se zobrazí jako `ContosoData.cs` .

1. V souboru se zdrojovým kódem použijte tokeny nerozlišující malá a velká písmena formuláře `$token$` k označení hodnot, které má NuGet nahradit vlastnostmi projektu:

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

    Při instalaci nahrazuje NuGet za `$rootnamespace$` `Fabrikam` předpokladu, že cílový projekt má kořenový obor názvů `Fabrikam` .

`$rootnamespace$`Token je nejčastěji používaná vlastnost projektu. všechny ostatní jsou uvedeny ve [vlastnostech projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Je třeba mít na vědomí, že některé vlastnosti mohou být specifické pro typ projektu.

## <a name="specifying-config-file-transformations"></a>Určení transformací konfiguračního souboru

Jak je popsáno v následujících částech, lze transformaci konfiguračního souboru provést dvěma způsoby:

- Zahrnutí `app.config.transform` a `web.config.transform` soubory do `content` složky balíčku, kde `.transform` rozšíření informuje NuGet, že tyto soubory obsahují soubor XML pro sloučení s existujícími konfiguračními soubory při instalaci balíčku. Při odinstalaci balíčku je stejný kód XML odstraněn.
- Přidejte `app.config.install.xdt` `web.config.install.xdt` soubory do `content` složky balíčku pomocí [syntaxe XDT](/previous-versions/aspnet/dd465326(v=vs.110)) a popište požadované změny. Pomocí této možnosti můžete také začlenit `.uninstall.xdt` soubor, který vrátí zpět změny, když se balíček odebere z projektu.

> [!Note]
> Transformace nejsou aplikovány na `.config` soubory, na které se odkazuje jako na odkaz v aplikaci Visual Studio.

Výhodou použití XDT je, že místo pouhého sloučení dvou statických souborů poskytuje syntaxi pro manipulaci s strukturou modelu DOM XML pomocí elementu a atributu odpovídajícího pomocí úplné podpory XPath. XDT pak může přidat, aktualizovat nebo odebrat prvky, umístit nové prvky do konkrétního umístění nebo nahradit/odebrat prvky (včetně podřízených uzlů). Díky tomu je snadné vytvořit odinstalační transformace, které při instalaci balíčku provedly zpět všechny transformace.

### <a name="xml-transforms"></a>Transformace XML

`app.config.transform`A `web.config.transform` ve `content` složce balíčku obsahují pouze prvky, které mají být sloučeny do existujících `app.config` souborů a souborů projektu `web.config` .

Předpokládejme například, že projekt zpočátku obsahuje následující obsah v `web.config` :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Chcete-li přidat `MyNuModule` prvek do `modules` oddílu při instalaci balíčku, vytvořte `web.config.transform` soubor ve `content` složce balíčku, který vypadá takto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Po instalaci balíčku NuGet se `web.config` zobrazí následující:

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

Všimněte si, že NuGet nenahradil `modules` oddíl, právě ho sloučil do nového záznamu přidáním pouze nových elementů a atributů. NuGet nemění žádné existující prvky ani atributy.

Po odinstalaci balíčku NuGet znovu prohledá `.transform` soubory a odebere prvky, které obsahuje, z příslušných `.config` souborů. Všimněte si, že tento proces nebude mít vliv na žádné řádky v `.config` souboru, které upravíte po instalaci balíčku.

V několika složitějších příkladech balíčky [protokolování chyb a obslužné rutiny pro balíček ASP.NET (knihovny elmah)](https://www.nuget.org/packages/elmah/) přidávají mnoho položek do `web.config` , které se po odinstalaci balíčku znovu odeberou.

Pokud si chcete prohlédnout svůj `web.config.transform` soubor, Stáhněte si z výše uvedeného odkazu balíček knihovny elmah, změňte rozšíření balíčku z `.nupkg` na a `.zip` pak ho otevřete `content\web.config.transform` v tomto souboru ZIP.

Chcete-li zobrazit efekt instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v aplikaci Visual Studio (šablona je v dialogovém okně Nový projekt v části **Visual C# > web** ) a vyberte prázdnou aplikaci ASP.NET. Otevřete `web.config` a zobrazte jeho počáteční stav. Pak klikněte pravým tlačítkem na projekt, vyberte **Spravovat balíčky NuGet**, vyhledejte knihovny elmah v NuGet.org a nainstalujte nejnovější verzi. Všimněte si všech změn v `web.config` . Nyní balíček odinstalujte a uvidíte, že `web.config` se vrátí do předchozího stavu.

### <a name="xdt-transforms"></a>Transformace XDT

> [!Note]
> Jak je uvedeno v [části problémy s kompatibilitou balíčku v dokumentaci pro migraci z nástroje `packages.config` do `PackageReference` ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformace, jak je popsáno níže, jsou podporovány pouze v nástroji `packages.config` . Pokud do svého balíčku přidáte následující soubory, příjemci, kteří používají váš balíček, nebudou `PackageReference` mít použité transformace (v [této ukázce](https://github.com/NuGet/Samples/tree/master/XDTransformExample) se dozvíte, jak pomocí XDT transformovat práci `PackageReference` ).

Konfigurační soubory můžete upravovat pomocí [syntaxe XDT](/previous-versions/aspnet/dd465326(v=vs.110)). Tokeny NuGet můžete také nahradit [vlastnostmi projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) zahrnutím názvu vlastnosti v rámci `$` oddělovačů (bez rozlišení velkých a malých písmen).

Například následující `app.config.install.xdt` soubor bude vkládat `appSettings` element do `app.config` obsahující `FullPath` `FileName` hodnoty, a `ActiveConfigurationSettings` z projektu:

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

Pro jiný příklad Předpokládejme, že projekt zpočátku obsahuje následující obsah `web.config` :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Chcete-li `MyNuModule` `modules` během instalace balíčku přidat element do oddílu, bude `web.config.install.xdt` obsahovat následující:

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

Po instalaci balíčku `web.config` bude vypadat takto:

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

Chcete-li odebrat pouze `MyNuModule` prvek během odinstalace balíčku, `web.config.uninstall.xdt` soubor by měl obsahovat následující:

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