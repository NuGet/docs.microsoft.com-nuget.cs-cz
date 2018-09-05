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
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="c1b51-103">Transformace zdrojového kódu a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="c1b51-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="c1b51-104">Pro projekty používající `packages.config`NuGet podporuje schopnost provádět transformace ke zdrojovému kódu a konfigurační soubory v balíčku nainstalovat a odinstalovat časy.</span><span class="sxs-lookup"><span data-stu-id="c1b51-104">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="c1b51-105">Pouze transformace zdrojového kódu se použijí při instalaci balíčku v projektu pomocí [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="c1b51-105">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="c1b51-106">A **zdrojového kódu transformace** platí jednosměrné nahrazování tokenů pro soubory v balíčku `content` nebo `contentFiles` složky (`content` pro zákazníky, kteří používají `packages.config` a `contentFiles` pro `PackageReference`) při instalaci balíčku, kde tokeny odkazují sady Visual Studio [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="c1b51-106">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="c1b51-107">Díky tomu můžete vložit soubor do oboru názvů v projektu nebo upravit kód, který by obvykle přejděte do `global.asax` v projektu aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c1b51-107">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="c1b51-108">A **transformace souboru config** umožňuje upravovat soubory, které již existují v cílový projekt, například `web.config` a `app.config`.</span><span class="sxs-lookup"><span data-stu-id="c1b51-108">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="c1b51-109">Například může být nutné přidat položku pro váš balíček `modules` oddílu v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="c1b51-109">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="c1b51-110">Tato transformace provádí včetně speciální souborů v balíčku, které popisují oddíly pro přidání konfiguračních souborů.</span><span class="sxs-lookup"><span data-stu-id="c1b51-110">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="c1b51-111">Při odinstalaci balíčku, tyto změny budou stejně se pak vrátit zpět, takže jde obousměrný transformace.</span><span class="sxs-lookup"><span data-stu-id="c1b51-111">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="c1b51-112">Určení zdrojového kódu transformace</span><span class="sxs-lookup"><span data-stu-id="c1b51-112">Specifying source code transformations</span></span>

1. <span data-ttu-id="c1b51-113">Soubory, které chcete vložit do projektu z balíčku musí být umístěn v balíčku `content` a `contentFiles` složek.</span><span class="sxs-lookup"><span data-stu-id="c1b51-113">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="c1b51-114">Například, pokud chcete soubor s názvem `ContosoData.cs` nainstalovaný v `Models` složek na cílový projekt, musí se nacházet uvnitř `content\Models` a `contentFiles\{lang}\{tfm}\Models` složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="c1b51-114">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="c1b51-115">Chcete-li dát pokyn použít náhradních tokenů v době instalace balíčků NuGet, přidejte `.pp` k názvu souboru zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="c1b51-115">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="c1b51-116">Po dokončení instalace, soubor nebude mít `.pp` rozšíření.</span><span class="sxs-lookup"><span data-stu-id="c1b51-116">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="c1b51-117">Například, aby transformace v `ContosoData.cs`, název souboru v balíčku `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="c1b51-117">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="c1b51-118">Po dokončení instalace se zobrazí jako `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="c1b51-118">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="c1b51-119">V souboru zdrojového kódu používat velká a malá písmena tokeny ve formátu `$token$` k označení hodnoty by měly nahradit tento NuGet s vlastnostmi projektu:</span><span class="sxs-lookup"><span data-stu-id="c1b51-119">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="c1b51-120">Po instalaci, nahradí NuGet `$rootnamespace$` s `Fabrikam` za předpokladu, že cílový projekt uživatele, jejichž kořenový obor názvů se `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="c1b51-120">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="c1b51-121">`$rootnamespace$` Token je vlastnost nejčastěji používané projektu; všechny ostatní jsou uvedeny v [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="c1b51-121">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="c1b51-122">Mějte na paměti, samozřejmě, že některé vlastnosti můžou být specifické pro daný typ projektu.</span><span class="sxs-lookup"><span data-stu-id="c1b51-122">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="c1b51-123">Určení transformace souboru config</span><span class="sxs-lookup"><span data-stu-id="c1b51-123">Specifying config file transformations</span></span>

<span data-ttu-id="c1b51-124">Jak je popsáno v následující části, transformace souboru konfigurace lze provést dvěma způsoby:</span><span class="sxs-lookup"><span data-stu-id="c1b51-124">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="c1b51-125">Zahrnout `app.config.transform` a `web.config.transform` soubory vašeho balíčku `content` složku, ve kterém `.transform` rozšíření informuje NuGet, že tyto soubory obsahují kód XML ke sloučení s existujícími soubory konfigurace při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="c1b51-125">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="c1b51-126">Při odinstalaci balíčku, odebere se tento stejný XML.</span><span class="sxs-lookup"><span data-stu-id="c1b51-126">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="c1b51-127">Zahrnout `app.config.install.xdt` a `web.config.install.xdt` soubory vašeho balíčku `content` složky, pomocí [XDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx) k popisu požadované změny.</span><span class="sxs-lookup"><span data-stu-id="c1b51-127">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="c1b51-128">Pomocí této možnosti můžete také zahrnout `.uninstall.xdt` souboru můžete vrátit změny, když balíček se odebere z projektu.</span><span class="sxs-lookup"><span data-stu-id="c1b51-128">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="c1b51-129">Transformace se nepoužije `.config` soubory na něho odkazovat jako na odkaz v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1b51-129">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="c1b51-130">Výhodou použití XDT je, že místo jednoduše sloučení dvou statické soubory, poskytuje syntaxi pro manipulaci s strukturu pomocí elementu a atribut párování pomocí plná podpora jazyka XPath modelu DOM jazyka XML.</span><span class="sxs-lookup"><span data-stu-id="c1b51-130">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="c1b51-131">XDT můžete pak přidat, aktualizovat, nebo odebrat prvky, umístěte nové prvky v konkrétním umístění nebo nahrazení nebo odebrat prvky (včetně podřízených uzlů).</span><span class="sxs-lookup"><span data-stu-id="c1b51-131">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="c1b51-132">To umožňuje jednoduché vytvoření odinstalovat transformací, které zrušíte všechny transformace provést během instalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="c1b51-132">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="c1b51-133">Transformace XML</span><span class="sxs-lookup"><span data-stu-id="c1b51-133">XML transforms</span></span>

<span data-ttu-id="c1b51-134">`app.config.transform` a `web.config.transform` v balíčku `content` složka obsahovat pouze prvky ke sloučení do existujícího projektu `app.config` a `web.config` soubory.</span><span class="sxs-lookup"><span data-stu-id="c1b51-134">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="c1b51-135">Jako příklad předpokládejme, že projekt zpočátku obsahuje následující obsah `web.config`:</span><span class="sxs-lookup"><span data-stu-id="c1b51-135">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="c1b51-136">Přidat `MyNuModule` elementu `modules` části během instalace balíčku, vytvořte `web.config.transform` souborů v balíčku `content` složku, která vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="c1b51-136">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="c1b51-137">Po instalaci balíčku NuGet `web.config` bude vypadat následovně:</span><span class="sxs-lookup"><span data-stu-id="c1b51-137">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="c1b51-138">Všimněte si, že se nepovedlo nahradit NuGet `modules` části, je právě sloučili novou položku do ní přidáním pouze nové prvky a atributy.</span><span class="sxs-lookup"><span data-stu-id="c1b51-138">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="c1b51-139">NuGet nedojde ke změně žádné stávající elementy nebo atributy.</span><span class="sxs-lookup"><span data-stu-id="c1b51-139">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="c1b51-140">Po odinstalaci balíčku NuGet se zaměřuje `.transform` soubory znovu a obsahuje prvky odeberete z příslušné `.config` soubory.</span><span class="sxs-lookup"><span data-stu-id="c1b51-140">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="c1b51-141">Všimněte si, že tento proces nebude mít vliv na všechny řádky `.config` soubor, který můžete upravit po instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="c1b51-141">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="c1b51-142">Jako podrobnější příklad [chyba protokolovací moduly a obslužné rutiny pro technologie ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) balíček přidává mnoho položek do `web.config`, které jsou znovu odebrány při odinstalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="c1b51-142">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="c1b51-143">Prozkoumat její `web.config.transform` soubor, stáhněte si balíček ELMAH z výše uvedeného odkazu, změna rozšíření balíčku z `.nupkg` k `.zip`a pak otevřete `content\web.config.transform` v daném souboru ZIP.</span><span class="sxs-lookup"><span data-stu-id="c1b51-143">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="c1b51-144">Pokud chcete posoudit účinek parametru instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v sadě Visual Studio (šablony je pod **Visual C# > Web** v dialogovém okně Nový projekt) a vyberte prázdnou aplikaci ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c1b51-144">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="c1b51-145">Otevřít `web.config` zobrazíte jeho počátečního stavu.</span><span class="sxs-lookup"><span data-stu-id="c1b51-145">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="c1b51-146">Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**vyhledat ELMAH na nuget.org a nainstalujte nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="c1b51-146">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="c1b51-147">Všimněte si, že všechny změny `web.config`.</span><span class="sxs-lookup"><span data-stu-id="c1b51-147">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="c1b51-148">Teď odinstalovat balíček a uvidíte `web.config` vrátit do předchozího stavu.</span><span class="sxs-lookup"><span data-stu-id="c1b51-148">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="c1b51-149">Transformuje XDT</span><span class="sxs-lookup"><span data-stu-id="c1b51-149">XDT transforms</span></span>

<span data-ttu-id="c1b51-150">Můžete upravit konfigurační soubory pomocí [XDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1b51-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="c1b51-151">Je také možné nahradit tokeny s NuGet [vlastnosti projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) zahrnutím název vlastnosti v rámci `$` dají (velká a malá písmena).</span><span class="sxs-lookup"><span data-stu-id="c1b51-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="c1b51-152">Například následující `app.config.install.xdt` vloží soubor `appSettings` elementu do `app.config` obsahující `FullPath`, `FileName`, a `ActiveConfigurationSettings` hodnoty z projektu:</span><span class="sxs-lookup"><span data-stu-id="c1b51-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="c1b51-153">Další příklad předpokládejme, že projekt zpočátku obsahuje následující obsah `web.config`:</span><span class="sxs-lookup"><span data-stu-id="c1b51-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="c1b51-154">Přidat `MyNuModule` elementu `modules` části během balíček nainstalovat, balíčku `web.config.install.xdt` by obsahovat následující:</span><span class="sxs-lookup"><span data-stu-id="c1b51-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="c1b51-155">Po instalaci balíčku, `web.config` bude vypadat například takto:</span><span class="sxs-lookup"><span data-stu-id="c1b51-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="c1b51-156">Odebrání pouze `MyNuModule` element během odinstalace balíčku `web.config.uninstall.xdt` soubor by měl obsahovat následující:</span><span class="sxs-lookup"><span data-stu-id="c1b51-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
