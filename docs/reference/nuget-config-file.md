---
title: Odkaz na soubor nuget.config
description: Odkaz na soubor NuGet.Config včetně konfigurace, bindingRedirects, packageRestore, řešení a packageSource oddíly.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911085"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="6ce02-103">odkaz na soubor nuget.config</span><span class="sxs-lookup"><span data-stu-id="6ce02-103">nuget.config reference</span></span>

<span data-ttu-id="6ce02-104">Chování Nugetu je řízena nastavením v různých `NuGet.Config` soubory, jak je popsáno v [konfigurace chování Nugetu](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6ce02-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="6ce02-105">`nuget.config` je soubor XML obsahující na nejvyšší úrovni `<configuration>` uzlu, který pak obsahuje část prvky popsané v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="6ce02-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="6ce02-106">Každý oddíl obsahuje nula nebo více položek.</span><span class="sxs-lookup"><span data-stu-id="6ce02-106">Each section contains zero or more items.</span></span> <span data-ttu-id="6ce02-107">Zobrazit [příklady konfiguračního souboru](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="6ce02-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="6ce02-108">Názvy nastavení rozlišují velikost písmen a můžete použít hodnoty [proměnné prostředí](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="6ce02-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="6ce02-109">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="6ce02-109">In this topic:</span></span>

- [<span data-ttu-id="6ce02-110">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="6ce02-110">config section</span></span>](#config-section)
- [<span data-ttu-id="6ce02-111">část bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="6ce02-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="6ce02-112">část packageRestore</span><span class="sxs-lookup"><span data-stu-id="6ce02-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="6ce02-113">oddíl řešení</span><span class="sxs-lookup"><span data-stu-id="6ce02-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="6ce02-114">[Balíček zdrojové oddíly](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="6ce02-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="6ce02-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="6ce02-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="6ce02-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="6ce02-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="6ce02-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="6ce02-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="6ce02-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="6ce02-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="6ce02-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="6ce02-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="6ce02-120">část trustedSigners</span><span class="sxs-lookup"><span data-stu-id="6ce02-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="6ce02-121">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="6ce02-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="6ce02-122">Příklad konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="6ce02-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="6ce02-123">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="6ce02-123">config section</span></span>

<span data-ttu-id="6ce02-124">Obsahuje nastavení různé konfigurace, které lze nastavit pomocí [ `nuget config` příkaz](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="6ce02-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="6ce02-125">`dependencyVersion` a `repositoryPath` platí pouze pro projekty pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="6ce02-126">`globalPackagesFolder` platí pouze pro projekty ve formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6ce02-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="6ce02-127">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-127">Key</span></span> | <span data-ttu-id="6ce02-128">Value</span><span class="sxs-lookup"><span data-stu-id="6ce02-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-129">dependencyVersion (`packages.config` jenom)</span><span class="sxs-lookup"><span data-stu-id="6ce02-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="6ce02-130">Výchozí hodnota `DependencyVersion` hodnotu pro instalaci balíčku, obnovení a aktualizace, když `-DependencyVersion` přepínač není zadán přímo.</span><span class="sxs-lookup"><span data-stu-id="6ce02-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="6ce02-131">Tato hodnota se používá také pomocí uživatelského rozhraní Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="6ce02-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="6ce02-132">Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="6ce02-133">globalPackagesFolder (projekty pouze pomocí PackageReference)</span><span class="sxs-lookup"><span data-stu-id="6ce02-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="6ce02-134">Umístění složky globálních balíčků výchozí.</span><span class="sxs-lookup"><span data-stu-id="6ce02-134">The location of the default global packages folder.</span></span> <span data-ttu-id="6ce02-135">Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6ce02-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="6ce02-136">Relativní cesta lze použít v projektu konkrétní `nuget.config` soubory.</span><span class="sxs-lookup"><span data-stu-id="6ce02-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6ce02-137">Toto nastavení je přepsán NUGET_PACKAGES proměnné prostředí, která má přednost.</span><span class="sxs-lookup"><span data-stu-id="6ce02-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6ce02-138">repositoryPath (`packages.config` jenom)</span><span class="sxs-lookup"><span data-stu-id="6ce02-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="6ce02-139">Umístění, ve kterém k instalaci balíčků NuGet místo výchozího `$(Solutiondir)/packages` složky.</span><span class="sxs-lookup"><span data-stu-id="6ce02-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="6ce02-140">Relativní cesta lze použít v projektu konkrétní `nuget.config` soubory.</span><span class="sxs-lookup"><span data-stu-id="6ce02-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6ce02-141">Toto nastavení je přepsán NUGET_PACKAGES proměnné prostředí, která má přednost.</span><span class="sxs-lookup"><span data-stu-id="6ce02-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6ce02-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="6ce02-142">defaultPushSource</span></span> | <span data-ttu-id="6ce02-143">Určuje adresu URL nebo cestu zdroje balíčku, který se použije jako výchozí, pokud se nenajdou žádné jiné zdroje balíčků pro operaci.</span><span class="sxs-lookup"><span data-stu-id="6ce02-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="6ce02-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="6ce02-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="6ce02-145">Nastavení proxy serveru mají používat při připojování ke zdrojům balíčků; `http_proxy` by měl být ve formátu `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="6ce02-146">Hesla jsou zašifrované a nelze ji přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="6ce02-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="6ce02-147">Pro `no_proxy`, hodnota je čárkou oddělený seznam domén obejít proxy server.</span><span class="sxs-lookup"><span data-stu-id="6ce02-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="6ce02-148">Můžete také použít proměnné prostředí http_proxy a no_proxy pro tyto hodnoty.</span><span class="sxs-lookup"><span data-stu-id="6ce02-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="6ce02-149">Další podrobnosti najdete v tématu [nastavení proxy serveru NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="6ce02-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="6ce02-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="6ce02-150">signatureValidationMode</span></span> | <span data-ttu-id="6ce02-151">Určuje režim ověřování pro ověřování podpisů balíčků pro instalaci balíčků a obnovení.</span><span class="sxs-lookup"><span data-stu-id="6ce02-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="6ce02-152">Hodnoty jsou `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="6ce02-153">Výchozí hodnota je `accept`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-153">Defaults to `accept`.</span></span>

<span data-ttu-id="6ce02-154">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="6ce02-155">část bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="6ce02-155">bindingRedirects section</span></span>

<span data-ttu-id="6ce02-156">Konfiguruje, zda NuGet nepodporuje automatické přesměrování vazby při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="6ce02-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="6ce02-157">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-157">Key</span></span> | <span data-ttu-id="6ce02-158">Hodnota</span><span class="sxs-lookup"><span data-stu-id="6ce02-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-159">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="6ce02-159">skip</span></span> | <span data-ttu-id="6ce02-160">Logická hodnota označující, zda se mají přeskočit automatické přesměrování vazby.</span><span class="sxs-lookup"><span data-stu-id="6ce02-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="6ce02-161">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="6ce02-161">The default is false.</span></span> |

<span data-ttu-id="6ce02-162">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="6ce02-163">část packageRestore</span><span class="sxs-lookup"><span data-stu-id="6ce02-163">packageRestore section</span></span>

<span data-ttu-id="6ce02-164">Ovládací prvky obnovení balíčků během sestavení.</span><span class="sxs-lookup"><span data-stu-id="6ce02-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="6ce02-165">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-165">Key</span></span> | <span data-ttu-id="6ce02-166">Value</span><span class="sxs-lookup"><span data-stu-id="6ce02-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-167">Povoleno</span><span class="sxs-lookup"><span data-stu-id="6ce02-167">enabled</span></span> | <span data-ttu-id="6ce02-168">Logická hodnota označující, zda NuGet můžete provést automatické obnovení.</span><span class="sxs-lookup"><span data-stu-id="6ce02-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="6ce02-169">Můžete také nastavit `EnableNuGetPackageRestore` proměnnou prostředí s hodnotou `True` namísto nastavení tohoto klíče v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="6ce02-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="6ce02-170">automatická</span><span class="sxs-lookup"><span data-stu-id="6ce02-170">automatic</span></span> | <span data-ttu-id="6ce02-171">Logická hodnota označující, zda NuGet by měla kontrolovat chybějící balíčky během sestavení.</span><span class="sxs-lookup"><span data-stu-id="6ce02-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="6ce02-172">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="6ce02-173">oddíl řešení</span><span class="sxs-lookup"><span data-stu-id="6ce02-173">solution section</span></span>

<span data-ttu-id="6ce02-174">Ovládací prvky, zda `packages` složka řešení je součástí správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="6ce02-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="6ce02-175">Tato část funguje pouze v `nuget.config` soubory ve složce řešení.</span><span class="sxs-lookup"><span data-stu-id="6ce02-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="6ce02-176">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-176">Key</span></span> | <span data-ttu-id="6ce02-177">Value</span><span class="sxs-lookup"><span data-stu-id="6ce02-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="6ce02-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="6ce02-179">Logická hodnota označující, jestli se má ignorovat složku packages při práci se správou zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="6ce02-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="6ce02-180">Výchozí hodnota je False.</span><span class="sxs-lookup"><span data-stu-id="6ce02-180">The default value is false.</span></span> |

<span data-ttu-id="6ce02-181">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="6ce02-182">Části zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="6ce02-182">Package source sections</span></span>

<span data-ttu-id="6ce02-183">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` a `trustedSigners` veškerou práci dohromady a nakonfigurujte, jak NuGet pracuje s úložišť balíčků během instalace, obnovení a operace aktualizace.</span><span class="sxs-lookup"><span data-stu-id="6ce02-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="6ce02-184">[ `nuget sources` Příkaz](../tools/cli-ref-sources.md) se obecně používají tato nastavení můžete spravovat, s výjimkou `apikeys` spravovaném pomocí [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md), a `trustedSigners` spravovaném použití [ `nuget trusted-signers` příkaz](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="6ce02-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="6ce02-185">Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="6ce02-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="6ce02-186">packageSources</span></span>

<span data-ttu-id="6ce02-187">Uvádí všechny zdroje balíčků známé.</span><span class="sxs-lookup"><span data-stu-id="6ce02-187">Lists all known package sources.</span></span> <span data-ttu-id="6ce02-188">Pořadí je ignorována během operace obnovení a s žádným projektem formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6ce02-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="6ce02-189">Pořadí zdrojů pro instalace respektuje NuGet a aktualizovat operace s projekty pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="6ce02-190">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-190">Key</span></span> | <span data-ttu-id="6ce02-191">Value</span><span class="sxs-lookup"><span data-stu-id="6ce02-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-192">(název přiřazení ke zdroji balíčku)</span><span class="sxs-lookup"><span data-stu-id="6ce02-192">(name to assign to the package source)</span></span> | <span data-ttu-id="6ce02-193">Cesta nebo adresa URL zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="6ce02-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="6ce02-194">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="6ce02-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="6ce02-195">packageSourceCredentials</span></span>

<span data-ttu-id="6ce02-196">Ukládá uživatelská jména a hesla pro zdroje, obvykle se zadává `-username` a `-password` přepínače s `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="6ce02-197">Hesla jsou ve výchozím nastavení zašifrované, pokud `-storepasswordincleartext` možnost je také použít.</span><span class="sxs-lookup"><span data-stu-id="6ce02-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="6ce02-198">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-198">Key</span></span> | <span data-ttu-id="6ce02-199">Value</span><span class="sxs-lookup"><span data-stu-id="6ce02-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-200">uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="6ce02-200">username</span></span> | <span data-ttu-id="6ce02-201">Uživatelské jméno pro zdroj ve formátu prostého textu.</span><span class="sxs-lookup"><span data-stu-id="6ce02-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="6ce02-202">heslo</span><span class="sxs-lookup"><span data-stu-id="6ce02-202">password</span></span> | <span data-ttu-id="6ce02-203">Šifrované heslo pro zdroj.</span><span class="sxs-lookup"><span data-stu-id="6ce02-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="6ce02-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="6ce02-204">cleartextpassword</span></span> | <span data-ttu-id="6ce02-205">Nezašifrované heslo pro zdroj.</span><span class="sxs-lookup"><span data-stu-id="6ce02-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="6ce02-206">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="6ce02-206">**Example:**</span></span>

<span data-ttu-id="6ce02-207">V konfiguračním souboru `<packageSourceCredentials>` prvek obsahuje podřízené uzly pro každý název příslušným zdrojovým (s nahrazením mezer v názvu `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="6ce02-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="6ce02-208">To znamená, že u zdrojů s názvem "Contoso" a "Zdroj testu" konfigurační soubor obsahuje následující při použití šifrovaná hesla:</span><span class="sxs-lookup"><span data-stu-id="6ce02-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="6ce02-209">Při použití nešifrovaná hesla:</span><span class="sxs-lookup"><span data-stu-id="6ce02-209">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="6ce02-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="6ce02-210">apikeys</span></span>

<span data-ttu-id="6ce02-211">Ukládá klíče pro zdroje, které používají ověřování pomocí klíče rozhraní API, jak se [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="6ce02-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="6ce02-212">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-212">Key</span></span> | <span data-ttu-id="6ce02-213">Value</span><span class="sxs-lookup"><span data-stu-id="6ce02-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-214">(adresa URL zdroje)</span><span class="sxs-lookup"><span data-stu-id="6ce02-214">(source URL)</span></span> | <span data-ttu-id="6ce02-215">Šifrovaný klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6ce02-215">The encrypted API key.</span></span> |

<span data-ttu-id="6ce02-216">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="6ce02-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="6ce02-217">disabledPackageSources</span></span>

<span data-ttu-id="6ce02-218">Zjištěné zdroje aktuálně zakázáno.</span><span class="sxs-lookup"><span data-stu-id="6ce02-218">Identified currently disabled sources.</span></span> <span data-ttu-id="6ce02-219">Může být prázdný.</span><span class="sxs-lookup"><span data-stu-id="6ce02-219">May be empty.</span></span>

| <span data-ttu-id="6ce02-220">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-220">Key</span></span> | <span data-ttu-id="6ce02-221">Value</span><span class="sxs-lookup"><span data-stu-id="6ce02-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-222">(název zdroje)</span><span class="sxs-lookup"><span data-stu-id="6ce02-222">(name of source)</span></span> | <span data-ttu-id="6ce02-223">Logická hodnota označující, zda zdroj je zakázáno.</span><span class="sxs-lookup"><span data-stu-id="6ce02-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="6ce02-224">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="6ce02-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="6ce02-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="6ce02-225">activePackageSource</span></span>

<span data-ttu-id="6ce02-226">*(pouze 2.x; zastaralé v 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="6ce02-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="6ce02-227">Identifikuje zdroj aktuálně aktivní nebo označuje souhrn všech zdrojů.</span><span class="sxs-lookup"><span data-stu-id="6ce02-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="6ce02-228">Key</span><span class="sxs-lookup"><span data-stu-id="6ce02-228">Key</span></span> | <span data-ttu-id="6ce02-229">Hodnota</span><span class="sxs-lookup"><span data-stu-id="6ce02-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ce02-230">(název zdroje) nebo `All`</span><span class="sxs-lookup"><span data-stu-id="6ce02-230">(name of source) or `All`</span></span> | <span data-ttu-id="6ce02-231">Pokud klíč je název zdroje, hodnota je zdrojová cesta nebo adresa URL.</span><span class="sxs-lookup"><span data-stu-id="6ce02-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="6ce02-232">Pokud `All`, hodnotou by měla být `(Aggregate source)` kombinovat všechny zdroje balíčků, které jinak nejsou zakázané.</span><span class="sxs-lookup"><span data-stu-id="6ce02-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="6ce02-233">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="6ce02-234">část trustedSigners</span><span class="sxs-lookup"><span data-stu-id="6ce02-234">trustedSigners section</span></span>

<span data-ttu-id="6ce02-235">Úložiště důvěryhodných podepisující osoby, které umožňují balíček při instalaci nebo obnovování.</span><span class="sxs-lookup"><span data-stu-id="6ce02-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="6ce02-236">Tento seznam nemůže být prázdný, pokud uživatel nastaví `signatureValidationMode` k `require`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="6ce02-237">Tato část je možné aktualizovat pomocí [ `nuget trusted-signers` příkaz](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="6ce02-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="6ce02-238">**Schéma**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-238">**Schema**:</span></span>

<span data-ttu-id="6ce02-239">Důvěryhodné podepisující osoba má kolekci `certificate` položky, které zařadit všechny certifikáty, které identifikují dané podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="6ce02-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="6ce02-240">Důvěryhodné podepisující osoba může být buď `Author` nebo `Repository`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="6ce02-241">Důvěryhodný *úložiště* také určuje `serviceIndex` úložiště (který musí být platný `https` identifikátor uri) a volitelně můžete zadat středníkem oddělený seznam `owners` omezit ještě více který je důvěryhodný z tohoto konkrétního úložiště.</span><span class="sxs-lookup"><span data-stu-id="6ce02-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="6ce02-242">Jsou podporované hashovací algoritmy používané pro otisku certifikátu `SHA256`, `SHA384` a `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="6ce02-243">Pokud `certificate` Určuje `allowUntrustedRoot` jako `true` daný certifikát řetězce na nedůvěryhodném kořenu může při sestavování řetězu certifikátů jako součást ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="6ce02-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="6ce02-244">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="6ce02-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="6ce02-245">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="6ce02-245">Using environment variables</span></span>

<span data-ttu-id="6ce02-246">Můžete použít proměnné prostředí v `nuget.config` hodnoty (NuGet 3.4 +) k aplikování nastavení běhu.</span><span class="sxs-lookup"><span data-stu-id="6ce02-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="6ce02-247">Například pokud `HOME` proměnné prostředí na Windows nastavená na `c:\users\username`, pak hodnota `%HOME%\NuGetRepository` v konfiguraci souboru přeloží na `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="6ce02-248">Podobně pokud `HOME` na Mac/Linux je nastavena na `/home/myStuff`, pak `%HOME%/NuGetRepository` v konfiguraci souboru přeloží na `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="6ce02-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="6ce02-249">Pokud není nalezena proměnné prostředí, používá NuGet hodnota literálu z konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="6ce02-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="6ce02-250">Příklad konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="6ce02-250">Example config file</span></span>

<span data-ttu-id="6ce02-251">Tady je příklad `nuget.config` soubor, který ukazuje několik položek nastavení:</span><span class="sxs-lookup"><span data-stu-id="6ce02-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
