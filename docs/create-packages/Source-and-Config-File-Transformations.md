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
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="8ebf2-103">Transformace zdrojového kódu a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="8ebf2-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="8ebf2-104">**Transformace zdrojového kódu** aplikuje jednosměrnou náhradu tokenu na soubory v balíčku `content` nebo `contentFiles` složce ( `content` pro zákazníky používající `packages.config` a `contentFiles` pro `PackageReference` ) při instalaci balíčku, kde tokeny odkazují na [Vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="8ebf2-105">To umožňuje vložit soubor do oboru názvů projektu, nebo upravit kód, který by obvykle přešel do `global.asax` projektu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="8ebf2-106">**Transformace konfiguračního souboru** umožňuje upravit soubory, které již existují v cílovém projektu, například `web.config` a `app.config` .</span><span class="sxs-lookup"><span data-stu-id="8ebf2-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="8ebf2-107">Balíček může například potřebovat přidat položku do `modules` oddílu v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="8ebf2-108">Tato transformace se provádí zahrnutím speciálních souborů do balíčku, které popisují oddíly, které se mají přidat do konfiguračních souborů.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="8ebf2-109">Při odinstalaci balíčku se tyto změny projeví opačným způsobem transformace.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="8ebf2-110">Určení transformací zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="8ebf2-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="8ebf2-111">Soubory, které chcete vložit z balíčku do projektu, se musí nacházet v rámci balíčků `content` a `contentFiles` složek.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="8ebf2-112">Například pokud chcete, aby byl soubor s názvem `ContosoData.cs` nainstalován do `Models` složky cílového projektu, musí být uvnitř `content\Models` `contentFiles\{lang}\{tfm}\Models` složek a v balíčku.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="8ebf2-113">Pokud chcete, aby NuGet při instalaci nahradil nahrazení tokenu, připojí se `.pp` k názvu souboru zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="8ebf2-114">Po instalaci nebude mít tento soubor `.pp` příponu.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="8ebf2-115">Chcete-li například transformovat v `ContosoData.cs` , pojmenujte soubor v balíčku `ContosoData.cs.pp` .</span><span class="sxs-lookup"><span data-stu-id="8ebf2-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="8ebf2-116">Po instalaci se zobrazí jako `ContosoData.cs` .</span><span class="sxs-lookup"><span data-stu-id="8ebf2-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="8ebf2-117">V souboru se zdrojovým kódem použijte tokeny nerozlišující malá a velká písmena formuláře `$token$` k označení hodnot, které má NuGet nahradit vlastnostmi projektu:</span><span class="sxs-lookup"><span data-stu-id="8ebf2-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="8ebf2-118">Při instalaci nahrazuje NuGet za `$rootnamespace$` `Fabrikam` předpokladu, že cílový projekt má kořenový obor názvů `Fabrikam` .</span><span class="sxs-lookup"><span data-stu-id="8ebf2-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="8ebf2-119">`$rootnamespace$`Token je nejčastěji používaná vlastnost projektu. všechny ostatní jsou uvedeny ve [vlastnostech projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="8ebf2-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="8ebf2-120">Je třeba mít na vědomí, že některé vlastnosti mohou být specifické pro typ projektu.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="8ebf2-121">Určení transformací konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="8ebf2-121">Specifying config file transformations</span></span>

<span data-ttu-id="8ebf2-122">Jak je popsáno v následujících částech, lze transformaci konfiguračního souboru provést dvěma způsoby:</span><span class="sxs-lookup"><span data-stu-id="8ebf2-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="8ebf2-123">Zahrnutí `app.config.transform` a `web.config.transform` soubory do `content` složky balíčku, kde `.transform` rozšíření informuje NuGet, že tyto soubory obsahují soubor XML pro sloučení s existujícími konfiguračními soubory při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="8ebf2-124">Při odinstalaci balíčku je stejný kód XML odstraněn.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="8ebf2-125">Přidejte `app.config.install.xdt` `web.config.install.xdt` soubory do `content` složky balíčku pomocí [syntaxe XDT](/previous-versions/aspnet/dd465326(v=vs.110)) a popište požadované změny.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](/previous-versions/aspnet/dd465326(v=vs.110)) to describe the desired changes.</span></span> <span data-ttu-id="8ebf2-126">Pomocí této možnosti můžete také začlenit `.uninstall.xdt` soubor, který vrátí zpět změny, když se balíček odebere z projektu.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="8ebf2-127">Transformace nejsou aplikovány na `.config` soubory, na které se odkazuje jako na odkaz v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="8ebf2-128">Výhodou použití XDT je, že místo pouhého sloučení dvou statických souborů poskytuje syntaxi pro manipulaci s strukturou modelu DOM XML pomocí elementu a atributu odpovídajícího pomocí úplné podpory XPath.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="8ebf2-129">XDT pak může přidat, aktualizovat nebo odebrat prvky, umístit nové prvky do konkrétního umístění nebo nahradit/odebrat prvky (včetně podřízených uzlů).</span><span class="sxs-lookup"><span data-stu-id="8ebf2-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="8ebf2-130">Díky tomu je snadné vytvořit odinstalační transformace, které při instalaci balíčku provedly zpět všechny transformace.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="8ebf2-131">Transformace XML</span><span class="sxs-lookup"><span data-stu-id="8ebf2-131">XML transforms</span></span>

<span data-ttu-id="8ebf2-132">`app.config.transform`A `web.config.transform` ve `content` složce balíčku obsahují pouze prvky, které mají být sloučeny do existujících `app.config` souborů a souborů projektu `web.config` .</span><span class="sxs-lookup"><span data-stu-id="8ebf2-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="8ebf2-133">Předpokládejme například, že projekt zpočátku obsahuje následující obsah v `web.config` :</span><span class="sxs-lookup"><span data-stu-id="8ebf2-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="8ebf2-134">Chcete-li přidat `MyNuModule` prvek do `modules` oddílu při instalaci balíčku, vytvořte `web.config.transform` soubor ve `content` složce balíčku, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="8ebf2-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="8ebf2-135">Po instalaci balíčku NuGet se `web.config` zobrazí následující:</span><span class="sxs-lookup"><span data-stu-id="8ebf2-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="8ebf2-136">Všimněte si, že NuGet nenahradil `modules` oddíl, právě ho sloučil do nového záznamu přidáním pouze nových elementů a atributů.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="8ebf2-137">NuGet nemění žádné existující prvky ani atributy.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="8ebf2-138">Po odinstalaci balíčku NuGet znovu prohledá `.transform` soubory a odebere prvky, které obsahuje, z příslušných `.config` souborů.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="8ebf2-139">Všimněte si, že tento proces nebude mít vliv na žádné řádky v `.config` souboru, které upravíte po instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="8ebf2-140">V několika složitějších příkladech balíčky [protokolování chyb a obslužné rutiny pro balíček ASP.NET (knihovny elmah)](https://www.nuget.org/packages/elmah/) přidávají mnoho položek do `web.config` , které se po odinstalaci balíčku znovu odeberou.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="8ebf2-141">Pokud si chcete prohlédnout svůj `web.config.transform` soubor, Stáhněte si z výše uvedeného odkazu balíček knihovny elmah, změňte rozšíření balíčku z `.nupkg` na a `.zip` pak ho otevřete `content\web.config.transform` v tomto souboru ZIP.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="8ebf2-142">Chcete-li zobrazit efekt instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v aplikaci Visual Studio (šablona je v dialogovém okně Nový projekt v části **Visual C# > web** ) a vyberte prázdnou aplikaci ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="8ebf2-143">Otevřete `web.config` a zobrazte jeho počáteční stav.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="8ebf2-144">Pak klikněte pravým tlačítkem na projekt, vyberte **Spravovat balíčky NuGet**, vyhledejte knihovny elmah v NuGet.org a nainstalujte nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="8ebf2-145">Všimněte si všech změn v `web.config` .</span><span class="sxs-lookup"><span data-stu-id="8ebf2-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="8ebf2-146">Nyní balíček odinstalujte a uvidíte, že `web.config` se vrátí do předchozího stavu.</span><span class="sxs-lookup"><span data-stu-id="8ebf2-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="8ebf2-147">Transformace XDT</span><span class="sxs-lookup"><span data-stu-id="8ebf2-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="8ebf2-148">Jak je uvedeno v [části problémy s kompatibilitou balíčku v dokumentaci pro migraci z nástroje `packages.config` do `PackageReference` ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformace, jak je popsáno níže, jsou podporovány pouze v nástroji `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="8ebf2-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="8ebf2-149">Pokud do svého balíčku přidáte následující soubory, příjemci, kteří používají váš balíček, nebudou `PackageReference` mít použité transformace (v [této ukázce](https://github.com/NuGet/Samples/tree/master/XDTransformExample) se dozvíte, jak pomocí XDT transformovat práci `PackageReference` ).</span><span class="sxs-lookup"><span data-stu-id="8ebf2-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="8ebf2-150">Konfigurační soubory můžete upravovat pomocí [syntaxe XDT](/previous-versions/aspnet/dd465326(v=vs.110)).</span><span class="sxs-lookup"><span data-stu-id="8ebf2-150">You can modify config files using [XDT syntax](/previous-versions/aspnet/dd465326(v=vs.110)).</span></span> <span data-ttu-id="8ebf2-151">Tokeny NuGet můžete také nahradit [vlastnostmi projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) zahrnutím názvu vlastnosti v rámci `$` oddělovačů (bez rozlišení velkých a malých písmen).</span><span class="sxs-lookup"><span data-stu-id="8ebf2-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="8ebf2-152">Například následující `app.config.install.xdt` soubor bude vkládat `appSettings` element do `app.config` obsahující `FullPath` `FileName` hodnoty, a `ActiveConfigurationSettings` z projektu:</span><span class="sxs-lookup"><span data-stu-id="8ebf2-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="8ebf2-153">Pro jiný příklad Předpokládejme, že projekt zpočátku obsahuje následující obsah `web.config` :</span><span class="sxs-lookup"><span data-stu-id="8ebf2-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="8ebf2-154">Chcete-li `MyNuModule` `modules` během instalace balíčku přidat element do oddílu, bude `web.config.install.xdt` obsahovat následující:</span><span class="sxs-lookup"><span data-stu-id="8ebf2-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="8ebf2-155">Po instalaci balíčku `web.config` bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="8ebf2-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="8ebf2-156">Chcete-li odebrat pouze `MyNuModule` prvek během odinstalace balíčku, `web.config.uninstall.xdt` soubor by měl obsahovat následující:</span><span class="sxs-lookup"><span data-stu-id="8ebf2-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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