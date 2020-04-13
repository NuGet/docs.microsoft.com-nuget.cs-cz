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
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="17bbf-103">Transformace zdrojového kódu a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="17bbf-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="17bbf-104">**Transformace zdrojového kódu** použije nahrazení jednosměrného tokenu na `content` `contentFiles` soubory`content` v balíčku `packages.config` `contentFiles` nebo `PackageReference`složce ( pro zákazníky, kteří používají a pro ) při instalaci balíčku, kde tokeny odkazují na [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)sady Visual Studio .</span><span class="sxs-lookup"><span data-stu-id="17bbf-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="17bbf-105">To umožňuje vložit soubor do oboru názvů projektu nebo přizpůsobit kód, který `global.asax` by obvykle jít do v ASP.NET projektu.</span><span class="sxs-lookup"><span data-stu-id="17bbf-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="17bbf-106">**Transformace konfiguračního souboru** umožňuje upravit soubory, které `web.config` již `app.config`existují v cílovém projektu, například a .</span><span class="sxs-lookup"><span data-stu-id="17bbf-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="17bbf-107">Balíček může být například nutné přidat `modules` položku do oddílu v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="17bbf-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="17bbf-108">Tato transformace se provádí zahrnutím speciální soubory v balíčku, které popisují oddíly přidat do konfiguračních souborů.</span><span class="sxs-lookup"><span data-stu-id="17bbf-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="17bbf-109">Při odinstalaci balíčku jsou tyto stejné změny stornovány, což je obousměrná transformace.</span><span class="sxs-lookup"><span data-stu-id="17bbf-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="17bbf-110">Určení transformací zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="17bbf-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="17bbf-111">Soubory, které chcete vložit z balíčku do projektu, musí `content` být `contentFiles` umístěny v rámci balíčku a složek.</span><span class="sxs-lookup"><span data-stu-id="17bbf-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="17bbf-112">Například pokud chcete, aby `ContosoData.cs` soubor volal `Models` být nainstalován ve složce cílového `content\Models` `contentFiles\{lang}\{tfm}\Models` projektu, musí být uvnitř a složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="17bbf-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="17bbf-113">Chcete-li pokyn NuGet použít nahrazení tokenu v době instalace, připojit `.pp` k názvu souboru zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="17bbf-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="17bbf-114">Po instalaci nebude mít soubor `.pp` příponu.</span><span class="sxs-lookup"><span data-stu-id="17bbf-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="17bbf-115">Chcete-li například provést `ContosoData.cs`transformace v aplikace `ContosoData.cs.pp`, pojmenujte soubor v balíčku .</span><span class="sxs-lookup"><span data-stu-id="17bbf-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="17bbf-116">Po instalaci se `ContosoData.cs`zobrazí jako .</span><span class="sxs-lookup"><span data-stu-id="17bbf-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="17bbf-117">V souboru zdrojového kódu použijte tokeny formuláře `$token$` bez velkých a malých písmen k označení hodnot, které by měl YGet nahradit vlastnostmi projektu:</span><span class="sxs-lookup"><span data-stu-id="17bbf-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="17bbf-118">Po instalaci nuget `$rootnamespace$` nahradí `Fabrikam` za předpokladu, že cílový `Fabrikam`projekt, jehož kořenový obor názvů je .</span><span class="sxs-lookup"><span data-stu-id="17bbf-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="17bbf-119">Token `$rootnamespace$` je nejčastěji používaná vlastnost projektu; všechny ostatní jsou uvedeny ve [vlastnostech projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="17bbf-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="17bbf-120">Mějte samozřejmě na paměti, že některé vlastnosti mohou být specifické pro typ projektu.</span><span class="sxs-lookup"><span data-stu-id="17bbf-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="17bbf-121">Určení transformací konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="17bbf-121">Specifying config file transformations</span></span>

<span data-ttu-id="17bbf-122">Jak je popsáno v následujících částech, transformace konfiguračních souborů lze provést dvěma způsoby:</span><span class="sxs-lookup"><span data-stu-id="17bbf-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="17bbf-123">Zahrnout `app.config.transform` `web.config.transform` a soubory ve `content` složce balíčku, kde `.transform` rozšíření říká NuGet, že tyto soubory obsahují XML sloučit s existujícími soubory konfigurační konfigurace při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="17bbf-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="17bbf-124">Při odinstalaci balíčku je odebrán stejný kód XML.</span><span class="sxs-lookup"><span data-stu-id="17bbf-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="17bbf-125">Zahrnout `app.config.install.xdt` `web.config.install.xdt` a soubory ve `content` složce balíčku, pomocí [xDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx) popsat požadované změny.</span><span class="sxs-lookup"><span data-stu-id="17bbf-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="17bbf-126">Pomocí této možnosti můžete `.uninstall.xdt` také zahrnout soubor pro stornování změn při odebrání balíčku z projektu.</span><span class="sxs-lookup"><span data-stu-id="17bbf-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="17bbf-127">Transformace nejsou použity `.config` na soubory odkazované jako odkaz v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17bbf-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="17bbf-128">Výhodou použití XDT je, že namísto jednoduchého sloučení dvou statických souborů poskytuje syntaxi pro manipulaci se strukturou XML DOM pomocí porovnávání elementů a atributů pomocí plné podpory XPath.</span><span class="sxs-lookup"><span data-stu-id="17bbf-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="17bbf-129">XDT pak můžete přidat, aktualizovat nebo odebrat prvky, umístit nové prvky na určité místo nebo nahradit nebo odebrat prvky (včetně podřízených uzlů).</span><span class="sxs-lookup"><span data-stu-id="17bbf-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="17bbf-130">Díky tomu je jednoduché vytvořit odinstalovat transformace, které zálohovat všechny transformace provedené během instalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="17bbf-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="17bbf-131">Transformace XML</span><span class="sxs-lookup"><span data-stu-id="17bbf-131">XML transforms</span></span>

<span data-ttu-id="17bbf-132">Složka `app.config.transform` `web.config.transform` a ve `content` složce balíčku obsahuje pouze ty prvky, `app.config` `web.config` které se mají sloučit do existujících souborů a souborů projektu.</span><span class="sxs-lookup"><span data-stu-id="17bbf-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="17bbf-133">Jako příklad předpokládejme, že projekt zpočátku obsahuje následující obsah v aplikaci `web.config`:</span><span class="sxs-lookup"><span data-stu-id="17bbf-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="17bbf-134">Chcete-li `MyNuModule` přidat `modules` prvek do oddílu `web.config.transform` během instalace balíčku, `content` vytvořte soubor ve složce balíčku, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="17bbf-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="17bbf-135">Po NuGet nainstaluje `web.config` balíček, se zobrazí takto:</span><span class="sxs-lookup"><span data-stu-id="17bbf-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="17bbf-136">Všimněte si, že NuGet nenahradil `modules` oddíl, pouze sloučil novou položku do něj přidáním pouze nové prvky a atributy.</span><span class="sxs-lookup"><span data-stu-id="17bbf-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="17bbf-137">NuGet nezmění žádné existující prvky nebo atributy.</span><span class="sxs-lookup"><span data-stu-id="17bbf-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="17bbf-138">Při odinstalaci balíčku NuGet znovu `.transform` zkontroluje soubory a odebere prvky, které obsahuje z příslušných `.config` souborů.</span><span class="sxs-lookup"><span data-stu-id="17bbf-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="17bbf-139">Všimněte si, že tento proces `.config` nebude mít vliv na všechny řádky v souboru, který upravíte po instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="17bbf-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="17bbf-140">Jako rozsáhlejší příklad balíček [Moduly protokolování chyb a obslužné rutiny pro ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) přidá mnoho položek do `web.config`aplikace , které jsou znovu odebrány při odinstalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="17bbf-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="17bbf-141">Chcete-li `web.config.transform` zkontrolovat jeho soubor, stáhněte balíček ELMAH `.nupkg` z `.zip`výše uvedeného odkazu, změňte příponu balíčku z na a otevřete `content\web.config.transform` jej v tomto souboru ZIP.</span><span class="sxs-lookup"><span data-stu-id="17bbf-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="17bbf-142">Chcete-li zobrazit efekt instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v sadě Visual Studio (šablona je v části **Visual C# > Web** v dialogovém okně Nový projekt) a vyberte prázdnou ASP.NET aplikaci.</span><span class="sxs-lookup"><span data-stu-id="17bbf-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="17bbf-143">Otevřít `web.config` zobrazíte počáteční stav.</span><span class="sxs-lookup"><span data-stu-id="17bbf-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="17bbf-144">Potom klikněte pravým tlačítkem myši na projekt, vyberte **spravovat balíčky NuGet**, vyhledejte ELMAH na nuget.org a nainstalujte nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="17bbf-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="17bbf-145">Všimněte si `web.config`všech změn v .</span><span class="sxs-lookup"><span data-stu-id="17bbf-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="17bbf-146">Nyní odinstalujte balíček a uvidíte, `web.config` že se vrátíte do jeho předchozího stavu.</span><span class="sxs-lookup"><span data-stu-id="17bbf-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="17bbf-147">XDT transformace</span><span class="sxs-lookup"><span data-stu-id="17bbf-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="17bbf-148">Jak je uvedeno v [části problémy s kompatibilitou `packages.config` balíčků `PackageReference`v dokumentech pro migraci z ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)do `packages.config`, transformace XDT, jak je popsáno níže, jsou podporovány pouze .</span><span class="sxs-lookup"><span data-stu-id="17bbf-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="17bbf-149">Pokud přidáte níže uvedené soubory do balíčku, `PackageReference` spotřebitelé pomocí balíčku s nebude mít transformace použít (viz tato`PackageReference` [ukázka,](https://github.com/NuGet/Samples/tree/master/XDTransformExample) aby XDT transformace pracovat s ).</span><span class="sxs-lookup"><span data-stu-id="17bbf-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="17bbf-150">Konfigurační soubory můžete upravit pomocí [syntaxe XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="17bbf-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="17bbf-151">Můžete také mít NuGet nahradit tokeny s [vlastnostmi projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) zahrnutím název vlastnosti do `$` oddělovače (malá a velká písmena).</span><span class="sxs-lookup"><span data-stu-id="17bbf-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="17bbf-152">Například `app.config.install.xdt` následující soubor vloží `appSettings` prvek `app.config` do obsahující `FullPath` `FileName`, `ActiveConfigurationSettings` a hodnoty z projektu:</span><span class="sxs-lookup"><span data-stu-id="17bbf-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="17bbf-153">Předpokládejme, že projekt zpočátku obsahuje `web.config`následující obsah v aplikaci :</span><span class="sxs-lookup"><span data-stu-id="17bbf-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="17bbf-154">Chcete-li `MyNuModule` přidat `modules` prvek do oddílu během `web.config.install.xdt` instalace balíčku, balíček bude obsahovat následující:</span><span class="sxs-lookup"><span data-stu-id="17bbf-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="17bbf-155">Po instalaci balíčku, `web.config` bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="17bbf-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="17bbf-156">Chcete-li `MyNuModule` odebrat pouze prvek `web.config.uninstall.xdt` během odinstalace balíčku, soubor by měl obsahovat následující:</span><span class="sxs-lookup"><span data-stu-id="17bbf-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
