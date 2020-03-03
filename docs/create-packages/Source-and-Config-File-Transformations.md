---
title: Transformace zdrojového a konfiguračního souboru pro balíčky NuGet
description: Podrobnosti o možnosti balíčků NuGet pro transformaci zdrojového kódu a konfiguračních souborů (XML) po instalaci.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231172"
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformace zdrojového kódu a konfiguračních souborů

**Transformace zdrojového kódu** aplikuje jednosměrnou náhradu tokenů na soubory ve `content` nebo `contentFiles` složce balíčku (`content` pro zákazníky, kteří používají `packages.config` a `contentFiles` pro `PackageReference`) při instalaci balíčku, kde tokeny odkazují na [Vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)sady Visual Studio. To umožňuje vložit soubor do oboru názvů projektu nebo přizpůsobit kód, který by obvykle přešel do `global.asax` v projektu ASP.NET.

**Transformace konfiguračního souboru** umožňuje upravit soubory, které již existují v cílovém projektu, například `web.config` a `app.config`. Balíček může například potřebovat přidat položku do oddílu `modules` v konfiguračním souboru. Tato transformace se provádí zahrnutím speciálních souborů do balíčku, které popisují oddíly, které se mají přidat do konfiguračních souborů. Při odinstalaci balíčku se tyto změny projeví opačným způsobem transformace.

## <a name="specifying-source-code-transformations"></a>Určení transformací zdrojového kódu

1. Soubory, které chcete vložit z balíčku do projektu, se musí nacházet v rámci `content` a `contentFiles` složky balíčku. Například pokud chcete, aby byl soubor s názvem `ContosoData.cs` nainstalován do `Models` složky cílového projektu, musí být uvnitř `content\Models` a `contentFiles\{lang}\{tfm}\Models` složky v balíčku.

1. Pokud chcete, aby NuGet při instalaci nahradil nahrazení tokenu, přidejte `.pp` k názvu souboru zdrojového kódu. Po instalaci nebude mít tento soubor příponu `.pp`.

    Pokud například chcete transformovat `ContosoData.cs`, pojmenujte soubor v `ContosoData.cs.pp`balíčku. Po instalaci se zobrazí jako `ContosoData.cs`.

1. V souboru zdrojového kódu použijte tokeny nerozlišující malá a velká písmena formuláře `$token$` k označení hodnot, které má NuGet nahradit vlastnostmi projektu:

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

    Při instalaci nahrazuje NuGet `$rootnamespace$` `Fabrikam` za předpokladu, že cílový obor názvů je `Fabrikam`.

Token `$rootnamespace$` je nejčastěji používaná vlastnost projektu; všechny ostatní jsou uvedeny ve [vlastnostech projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Je třeba mít na vědomí, že některé vlastnosti mohou být specifické pro typ projektu.

## <a name="specifying-config-file-transformations"></a>Určení transformací konfiguračního souboru

Jak je popsáno v následujících částech, lze transformaci konfiguračního souboru provést dvěma způsoby:

- Do složky `content` balíčku zahrňte soubory `app.config.transform` a `web.config.transform`, kde rozšíření `.transform` oznamuje, že tyto soubory obsahují kód XML pro sloučení s existujícími konfiguračními soubory při instalaci balíčku. Při odinstalaci balíčku je stejný kód XML odstraněn.
- Přidejte `app.config.install.xdt` a `web.config.install.xdt` soubory do složky `content` balíčku pomocí [syntaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx) k popisu požadovaných změn. Pomocí této možnosti můžete také použít soubor `.uninstall.xdt` pro vrácení změn, když se balíček odebere z projektu.

> [!Note]
> Transformace nejsou aplikovány na `.config` soubory, na které se odkazuje jako na odkaz v aplikaci Visual Studio.

Výhodou použití XDT je, že místo pouhého sloučení dvou statických souborů poskytuje syntaxi pro manipulaci s strukturou modelu DOM XML pomocí elementu a atributu odpovídajícího pomocí úplné podpory XPath. XDT pak může přidat, aktualizovat nebo odebrat prvky, umístit nové prvky do konkrétního umístění nebo nahradit/odebrat prvky (včetně podřízených uzlů). Díky tomu je snadné vytvořit odinstalační transformace, které při instalaci balíčku provedly zpět všechny transformace.

### <a name="xml-transforms"></a>Transformace XML

`app.config.transform` a `web.config.transform` v `content` složce balíčku obsahují pouze prvky, které mají být sloučeny do stávajícího `app.config` a `web.config` souborů projektu.

Předpokládejme například, že projekt zpočátku obsahuje následující obsah v `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Chcete-li přidat prvek `MyNuModule` do oddílu `modules` při instalaci balíčku, vytvořte `web.config.transform` soubor ve složce `content` balíčku, která vypadá takto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Po instalaci balíčku NuGet se `web.config` zobrazí takto:

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

Všimněte si, že NuGet nenahradil oddíl `modules`, právě do něj právě slučuje nový záznam přidáním nových prvků a atributů. NuGet nemění žádné existující prvky ani atributy.

Po odinstalaci balíčku NuGet znovu prohledá soubory `.transform` a odebere prvky, které obsahuje, z příslušných `.config` souborů. Všimněte si, že tento proces nebude mít vliv na žádné řádky v souboru `.config`, které upravíte po instalaci balíčku.

V širším příkladu balíček [protokolování chyb a obslužné rutiny pro ASP.NET (knihovny elmah)](https://www.nuget.org/packages/elmah/) přidává do `web.config`mnoho položek, které se po odinstalaci balíčku znovu odeberou.

Pokud chcete prostudovat svůj `web.config.transform` soubor, Stáhněte si z výše uvedeného odkazu balíček knihovny ELMAH, změňte rozšíření balíčku z `.nupkg` na `.zip`a pak otevřete `content\web.config.transform` v tomto souboru ZIP.

Chcete-li zobrazit efekt instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v aplikaci Visual Studio (šablona je pod položkou  **C# Visual > Web** v dialogovém okně Nový projekt) a vyberte prázdnou aplikaci ASP.NET. Otevřete `web.config`, abyste viděli jeho počáteční stav. Pak klikněte pravým tlačítkem na projekt, vyberte **Spravovat balíčky NuGet**, vyhledejte knihovny elmah v NuGet.org a nainstalujte nejnovější verzi. Všimněte si všech změn `web.config`. Teď balíček odinstalujte a uvidíte `web.config` vrátit se k předchozímu stavu.

### <a name="xdt-transforms"></a>Transformace XDT

> [!Note]
> Jak je uvedeno v [části problémy s kompatibilitou balíčku v dokumentaci pro migraci z `packages.config` na `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), transformace XDT, jak je popsáno níže, jsou podporovány pouze `packages.config`. Pokud do balíčku přidáte následující soubory, příjemci, kteří používají váš balíček s `PackageReference`, nebudou mít použité transformace (v [této ukázce](https://github.com/NuGet/Samples/tree/master/XDTransformExample) se dozvíte, jak XDT pracovat s`PackageReference`).

Konfigurační soubory můžete upravovat pomocí [syntaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx). Můžete také tokeny NuGet nahradit [vlastnostmi projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) zahrnutím názvu vlastnosti v rámci `$` oddělovači (bez rozlišení velkých a malých písmen).

Například následující `app.config.install.xdt` soubor vloží `appSettings` prvek do `app.config` obsahující `FullPath`, `FileName`a `ActiveConfigurationSettings` hodnoty z projektu:

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

Pro jiný příklad Předpokládejme, že projekt zpočátku obsahuje následující obsah v `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Chcete-li přidat `MyNuModule` element do oddílu `modules` při instalaci balíčku, `web.config.install.xdt` balíčku by obsahovala následující:

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

Po instalaci balíčku bude `web.config` vypadat takto:

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

Chcete-li během odinstalace balíčku odebrat pouze prvek `MyNuModule`, soubor `web.config.uninstall.xdt` by měl obsahovat následující:

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
