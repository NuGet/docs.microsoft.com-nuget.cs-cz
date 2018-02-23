---
title: "Zdroj a konfiguračním souboru transformace pro balíčky NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Podrobnosti na možnost pro balíčky NuGet pro transformaci zdrojového kódu a konfigurační soubory (XML) při instalaci."
keywords: "Instalace balíčku NuGet, transformace balíčku NuGet, úprava konfiguračních souborů, úprava zdrojového kódu"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 8bcf054a497e1069a11f96ba675853fb0f2ed667
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/20/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="9e61f-104">Transformace zdrojového kódu a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="9e61f-104">Transforming source code and configuration files</span></span>

<span data-ttu-id="9e61f-105">Pro projekty pomocí `packages.config`, NuGet podporuje schopnost provádět transformace ke zdrojovému kódu a konfigurační soubory v balíčku instalaci a odinstalaci časy.</span><span class="sxs-lookup"><span data-stu-id="9e61f-105">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="9e61f-106">Transformace se nepoužívají při instalaci balíčku do projektu pomocí [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="9e61f-106">Transformations are not applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="9e61f-107">A **zdrojového kódu transformace** jednosměrný tokenu nahrazení se vztahují na soubory v balíčku `content` složku, když je balíček nainstalován, kde najdete tokeny pro Visual Studio [projektu vlastnosti](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) .</span><span class="sxs-lookup"><span data-stu-id="9e61f-107">A **source code transformation** applies one-way token replacement to files in the package's `content` folder when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="9e61f-108">To umožňuje vložit soubor do projektu obor názvů nebo přizpůsobit kód, který obvykle přejde do `global.asax` v projektu aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9e61f-108">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="9e61f-109">A **transformace souboru config** umožňuje upravit soubory, které již existují v cílovém projektu, například `web.config` a `app.config`.</span><span class="sxs-lookup"><span data-stu-id="9e61f-109">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="9e61f-110">Například může být nutné přidat položku, kterou chcete vašeho balíčku `modules` oddíl v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="9e61f-110">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="9e61f-111">Tato transformace je potřeba včetně speciální soubory v balíčku, který popisuje oddíly pro přidání konfiguračních souborů.</span><span class="sxs-lookup"><span data-stu-id="9e61f-111">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="9e61f-112">Při odinstalaci balíčku, tyto změny budou stejně jsou pak vrátit zpět, provedení to obousměrný transformace.</span><span class="sxs-lookup"><span data-stu-id="9e61f-112">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="9e61f-113">Určení transformace zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="9e61f-113">Specifying source code transformations</span></span>

1. <span data-ttu-id="9e61f-114">Soubory, které chcete vložit z balíčku do projektu musí být umístěn v balíčku `content` složky.</span><span class="sxs-lookup"><span data-stu-id="9e61f-114">Files that you want to insert from the package into the project must be located within the package's `content` folder.</span></span> <span data-ttu-id="9e61f-115">Například, pokud chcete do souboru s názvem `ContosoData.cs` být nainstalovaný v `Models` složky cílový projekt, musí být uvnitř `content\Models` složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e61f-115">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` folder in the package.</span></span>

1. <span data-ttu-id="9e61f-116">Dáte pokyn, aby správci balíčků NuGet použít token nahrazení během instalace, připojte `.pp` k názvu souboru zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="9e61f-116">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="9e61f-117">Po instalaci, soubor nebude mít `.pp` rozšíření.</span><span class="sxs-lookup"><span data-stu-id="9e61f-117">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="9e61f-118">Například aby transformace ve `ContosoData.cs`, název souboru v balíčku `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="9e61f-118">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="9e61f-119">Po instalaci se zobrazí jako `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="9e61f-119">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="9e61f-120">V souboru se zdrojovým kódem, použijte velká a malá písmena tokeny ve formátu `$token$` k určení hodnoty by měl tento NuGet nahraďte vlastností projektu:</span><span class="sxs-lookup"><span data-stu-id="9e61f-120">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="9e61f-121">Po instalaci, nahradí NuGet `$rootnamespace$` s `Fabrikam` za předpokladu, že cílový projekt elementu, jehož kořenový obor názvů je `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="9e61f-121">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="9e61f-122">`$rootnamespace$` Token je vlastnost nejčastěji používané projektu; všechny ostatní jsou uvedeny v [projektu vlastnosti](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="9e61f-122">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="9e61f-123">Mějte na paměti, samozřejmě platí, že některé vlastnosti může být specifické pro daný typ projektu.</span><span class="sxs-lookup"><span data-stu-id="9e61f-123">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="9e61f-124">Určení transformace souboru config</span><span class="sxs-lookup"><span data-stu-id="9e61f-124">Specifying config file transformations</span></span>

<span data-ttu-id="9e61f-125">Jak je popsáno v následujících částech, konfigurační soubor transformace lze provést dvěma způsoby:</span><span class="sxs-lookup"><span data-stu-id="9e61f-125">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="9e61f-126">Zahrnout `app.config.transform` a `web.config.transform` soubory do balíčku `content` složku, kde `.transform` rozšíření informuje NuGet, že tyto soubory obsahují soubor XML sloučit s existující konfigurační soubory, když je balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="9e61f-126">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="9e61f-127">Při odinstalaci balíčku, odeberou se tento stejný XML.</span><span class="sxs-lookup"><span data-stu-id="9e61f-127">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="9e61f-128">(NuGet 2.6 a novější) Zahrnout `app.config.install.xdt` a `web.config.install.xdt` soubory do balíčku `content` složky, pomocí [XDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx) k popisu požadované změny.</span><span class="sxs-lookup"><span data-stu-id="9e61f-128">(NuGet 2.6 and later) Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="9e61f-129">Pomocí této možnosti můžete použít také `.uninstall.xdt` souboru můžete vrátit změny, pokud balíček je odebrán z projektu.</span><span class="sxs-lookup"><span data-stu-id="9e61f-129">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="9e61f-130">Transformace se nepoužije `.config` souborů, který je odkazováno jako na odkaz v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e61f-130">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="9e61f-131">Výhodou použití XDT je, že místo jednoduše sloučení dvou statické soubory, poskytuje syntaxi pro manipulaci s strukturu DOM XML pomocí elementu a atributu odpovídající pomocí plnou podporu jazyka XPath.</span><span class="sxs-lookup"><span data-stu-id="9e61f-131">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="9e61f-132">XDT můžete pak přidat, aktualizovat, nebo odeberte elementy, umístit nové prvky v určitém místě nebo nahradit nebo odebrat elementy (včetně podřízených uzlů).</span><span class="sxs-lookup"><span data-stu-id="9e61f-132">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="9e61f-133">Díky tomu přehledné vytvořit odinstalovat transformace, které se zpět na všechny transformace provést během instalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e61f-133">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="9e61f-134">Transformace XML.</span><span class="sxs-lookup"><span data-stu-id="9e61f-134">XML transforms</span></span>

<span data-ttu-id="9e61f-135">`app.config.transform` a `web.config.transform` v balíčku na `content` složka obsahovat pouze elementy sloučit do projektu existující `app.config` a `web.config` soubory.</span><span class="sxs-lookup"><span data-stu-id="9e61f-135">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="9e61f-136">Jako příklad předpokládejme projekt původně obsahuje následující obsah `web.config`:</span><span class="sxs-lookup"><span data-stu-id="9e61f-136">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="9e61f-137">Chcete-li přidat `MyNuModule` elementu, který chcete `modules` během instalace balíčku, vytvořte `web.config.transform` souboru v balíčku `content` složky, která vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="9e61f-137">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="9e61f-138">Po instalaci balíčku, NuGet `web.config` bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="9e61f-138">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="9e61f-139">Všimněte si, že nebyla nahradit NuGet `modules` části, je právě sloučit nový záznam do ní přidáním pouze nové elementy a atributy.</span><span class="sxs-lookup"><span data-stu-id="9e61f-139">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="9e61f-140">NuGet nezmění žádné existující elementy nebo atributy.</span><span class="sxs-lookup"><span data-stu-id="9e61f-140">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="9e61f-141">Při odinstalaci balíčku NuGet prozkoumá `.transform` soubory znovu a obsahuje prvky odeberete z příslušné `.config` soubory.</span><span class="sxs-lookup"><span data-stu-id="9e61f-141">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="9e61f-142">Všimněte si, že tento proces nebude mít vliv na všechny řádky `.config` soubor, který upravíte po instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e61f-142">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="9e61f-143">Jako v příkladu rozsáhlejší [moduly protokolování chyb a obslužné rutiny pro technologii ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) přidává balíček mnoho položky do `web.config`, které jsou znovu odebrány při odinstalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e61f-143">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="9e61f-144">Pro zjištění jeho `web.config.transform` soubor, stáhněte si balíček ELMAH z výše uvedený odkaz, změňte rozšíření balíčku z `.nupkg` k `.zip`a pak otevřete `content\web.config.transform` v tomto souboru ZIP.</span><span class="sxs-lookup"><span data-stu-id="9e61f-144">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="9e61f-145">Informace o účinku instalace a odinstalace balíčku, vytvořte nový projekt ASP.NET v sadě Visual Studio (šablona je pod **Visual C# > Web** v dialogovém okně Nový projekt) a vyberte prázdnou aplikaci ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9e61f-145">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="9e61f-146">Otevřete `web.config` zobrazíte počátečního stavu.</span><span class="sxs-lookup"><span data-stu-id="9e61f-146">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="9e61f-147">Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**, vyhledejte ELMAH na nuget.org a nainstalujte nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="9e61f-147">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="9e61f-148">Všimněte si, všechny změny do `web.config`.</span><span class="sxs-lookup"><span data-stu-id="9e61f-148">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="9e61f-149">Teď má být balíček odinstalován a zobrazí `web.config` vrátit do předchozího stavu.</span><span class="sxs-lookup"><span data-stu-id="9e61f-149">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="9e61f-150">Transformuje XDT</span><span class="sxs-lookup"><span data-stu-id="9e61f-150">XDT transforms</span></span>

<span data-ttu-id="9e61f-151">S NuGet 2.6 nebo novější, můžete upravit konfigurační soubory pomocí [XDT syntaxe](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e61f-151">With NuGet 2.6 and later, you can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="9e61f-152">Můžete taky nechat NuGet nahradit tokeny se [projektu vlastnosti](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) zahrnutím název vlastnosti v rámci `$` delimeters (velká a malá písmena).</span><span class="sxs-lookup"><span data-stu-id="9e61f-152">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="9e61f-153">Například následující `app.config.install.xdt` vloží soubor `appSettings` element do `app.config` obsahující `FullPath`, `FileName`, a `ActiveConfigurationSettings` hodnoty z projektu:</span><span class="sxs-lookup"><span data-stu-id="9e61f-153">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="9e61f-154">Další příklad předpokládejme projekt původně obsahuje následující obsah `web.config`:</span><span class="sxs-lookup"><span data-stu-id="9e61f-154">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="9e61f-155">Chcete-li přidat `MyNuModule` elementu, který chcete `modules` nainstalovat části během balíčku, balíčku `web.config.install.xdt` by obsahovat následující:</span><span class="sxs-lookup"><span data-stu-id="9e61f-155">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="9e61f-156">Po instalaci balíčku, `web.config` bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="9e61f-156">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="9e61f-157">Pro odebrání pouze `MyNuModule` element během odinstalace balíčku `web.config.uninstall.xdt` soubor by měl obsahovat následující:</span><span class="sxs-lookup"><span data-stu-id="9e61f-157">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
