---
title: Transformace zdrojových a konfiguračních souborů pro balíčky NuGet
description: Podrobnosti o schopnosti balíčků NuGet transformovat zdrojový kód a konfigurační (XML) soubory při instalaci.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231172"
---
# <a name="transforming-source-code-and-configuration-files"></a>Transformace zdrojového kódu a konfiguračních souborů

**Transformace zdrojového kódu** použije nahrazení jednosměrného tokenu na `content` `contentFiles` soubory`content` v balíčku `packages.config` `contentFiles` nebo `PackageReference`složce ( pro zákazníky, kteří používají a pro ) při instalaci balíčku, kde tokeny odkazují na [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)sady Visual Studio . To umožňuje vložit soubor do oboru názvů projektu nebo přizpůsobit kód, který `global.asax` by obvykle jít do v ASP.NET projektu.

**Transformace konfiguračního souboru** umožňuje upravit soubory, které `web.config` již `app.config`existují v cílovém projektu, například a . Balíček může být například nutné přidat `modules` položku do oddílu v konfiguračním souboru. Tato transformace se provádí zahrnutím speciální soubory v balíčku, které popisují oddíly přidat do konfiguračních souborů. Při odinstalaci balíčku jsou tyto stejné změny stornovány, což je obousměrná transformace.

## <a name="specifying-source-code-transformations"></a>Určení transformací zdrojového kódu

1. Soubory, které chcete vložit z balíčku do projektu, musí `content` být `contentFiles` umístěny v rámci balíčku a složek. Například pokud chcete, aby `ContosoData.cs` soubor volal `Models` být nainstalován ve složce cílového `content\Models` `contentFiles\{lang}\{tfm}\Models` projektu, musí být uvnitř a složky v balíčku.

1. Chcete-li pokyn NuGet použít nahrazení tokenu v době instalace, připojit `.pp` k názvu souboru zdrojového kódu. Po instalaci nebude mít soubor `.pp` příponu.

    Chcete-li například provést `ContosoData.cs`transformace v aplikace `ContosoData.cs.pp`, pojmenujte soubor v balíčku . Po instalaci se `ContosoData.cs`zobrazí jako .

1. V souboru zdrojového kódu použijte tokeny formuláře `$token$` bez velkých a malých písmen k označení hodnot, které by měl YGet nahradit vlastnostmi projektu:

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

    Po instalaci nuget `$rootnamespace$` nahradí `Fabrikam` za předpokladu, že cílový `Fabrikam`projekt, jehož kořenový obor názvů je .

Token `$rootnamespace$` je nejčastěji používaná vlastnost projektu; všechny ostatní jsou uvedeny ve [vlastnostech projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Mějte samozřejmě na paměti, že některé vlastnosti mohou být specifické pro typ projektu.

## <a name="specifying-config-file-transformations"></a>Určení transformací konfiguračních souborů

Jak je popsáno v následujících částech, transformace konfiguračních souborů lze provést dvěma způsoby:

- Zahrnout `app.config.transform` `web.config.transform` a soubory ve `content` složce balíčku, kde `.transform` rozšíření říká NuGet, že tyto soubory obsahují XML sloučit s existujícími soubory konfigurační konfigurace při instalaci balíčku. Při odinstalaci balíčku je odebrán stejný kód XML.
- Zahrnout `app.config.install.xdt` `web.config.install.xdt` a soubory ve `content` složce balíčku, pomocí [xDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx) popsat požadované změny. Pomocí této možnosti můžete `.uninstall.xdt` také zahrnout soubor pro stornování změn při odebrání balíčku z projektu.

> [!Note]
> Transformace nejsou použity `.config` na soubory odkazované jako odkaz v sadě Visual Studio.

Výhodou použití XDT je, že namísto jednoduchého sloučení dvou statických souborů poskytuje syntaxi pro manipulaci se strukturou XML DOM pomocí porovnávání elementů a atributů pomocí plné podpory XPath. XDT pak můžete přidat, aktualizovat nebo odebrat prvky, umístit nové prvky na určité místo nebo nahradit nebo odebrat prvky (včetně podřízených uzlů). Díky tomu je jednoduché vytvořit odinstalovat transformace, které zálohovat všechny transformace provedené během instalace balíčku.

### <a name="xml-transforms"></a>Transformace XML

Složka `app.config.transform` `web.config.transform` a ve `content` složce balíčku obsahuje pouze ty prvky, `app.config` `web.config` které se mají sloučit do existujících souborů a souborů projektu.

Jako příklad předpokládejme, že projekt zpočátku obsahuje následující obsah v aplikaci `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Chcete-li `MyNuModule` přidat `modules` prvek do oddílu `web.config.transform` během instalace balíčku, `content` vytvořte soubor ve složce balíčku, který vypadá takto:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Po NuGet nainstaluje `web.config` balíček, se zobrazí takto:

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

Všimněte si, že NuGet nenahradil `modules` oddíl, pouze sloučil novou položku do něj přidáním pouze nové prvky a atributy. NuGet nezmění žádné existující prvky nebo atributy.

Při odinstalaci balíčku NuGet znovu `.transform` zkontroluje soubory a odebere prvky, které obsahuje z příslušných `.config` souborů. Všimněte si, že tento proces `.config` nebude mít vliv na všechny řádky v souboru, který upravíte po instalaci balíčku.

Jako rozsáhlejší příklad balíček [Moduly protokolování chyb a obslužné rutiny pro ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) přidá mnoho položek do `web.config`aplikace , které jsou znovu odebrány při odinstalaci balíčku.

Chcete-li `web.config.transform` zkontrolovat jeho soubor, stáhněte balíček ELMAH `.nupkg` z `.zip`výše uvedeného odkazu, změňte příponu balíčku z na a otevřete `content\web.config.transform` jej v tomto souboru ZIP.

Chcete-li zobrazit efekt instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v sadě Visual Studio (šablona je v části **Visual C# > Web** v dialogovém okně Nový projekt) a vyberte prázdnou ASP.NET aplikaci. Otevřít `web.config` zobrazíte počáteční stav. Potom klikněte pravým tlačítkem myši na projekt, vyberte **spravovat balíčky NuGet**, vyhledejte ELMAH na nuget.org a nainstalujte nejnovější verzi. Všimněte si `web.config`všech změn v . Nyní odinstalujte balíček a uvidíte, `web.config` že se vrátíte do jeho předchozího stavu.

### <a name="xdt-transforms"></a>XDT transformace

> [!Note]
> Jak je uvedeno v [části problémy s kompatibilitou `packages.config` balíčků `PackageReference`v dokumentech pro migraci z ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)do `packages.config`, transformace XDT, jak je popsáno níže, jsou podporovány pouze . Pokud přidáte níže uvedené soubory do balíčku, `PackageReference` spotřebitelé pomocí balíčku s nebude mít transformace použít (viz tato`PackageReference` [ukázka,](https://github.com/NuGet/Samples/tree/master/XDTransformExample) aby XDT transformace pracovat s ).

Konfigurační soubory můžete upravit pomocí [syntaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx). Můžete také mít NuGet nahradit tokeny s [vlastnostmi projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) zahrnutím název vlastnosti do `$` oddělovače (malá a velká písmena).

Například `app.config.install.xdt` následující soubor vloží `appSettings` prvek `app.config` do obsahující `FullPath` `FileName`, `ActiveConfigurationSettings` a hodnoty z projektu:

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

Předpokládejme, že projekt zpočátku obsahuje `web.config`následující obsah v aplikaci :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Chcete-li `MyNuModule` přidat `modules` prvek do oddílu během `web.config.install.xdt` instalace balíčku, balíček bude obsahovat následující:

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
    </system.webServer>
</configuration>
```

Chcete-li `MyNuModule` odebrat pouze prvek `web.config.uninstall.xdt` během odinstalace balíčku, soubor by měl obsahovat následující:

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
