---
title: Odkaz na soubor NuGet. config
description: Odkaz na soubor NuGet. config včetně oddílů config, bindingRedirects, packageRestore, Solution a packageSource
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: b03bb8da0191a679671e5898ac70fff2024d52f2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317222"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="29f09-103">Referenční dokumentace NuGet. config</span><span class="sxs-lookup"><span data-stu-id="29f09-103">nuget.config reference</span></span>

<span data-ttu-id="29f09-104">Chování NuGet se řídí nastavením v různých `NuGet.Config` souborech, jak je popsáno v tématu [běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="29f09-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="29f09-105">`nuget.config`je soubor XML obsahující uzel nejvyšší úrovně `<configuration>` , který pak obsahuje prvky oddílu popsané v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="29f09-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="29f09-106">Každý oddíl obsahuje nula nebo více položek.</span><span class="sxs-lookup"><span data-stu-id="29f09-106">Each section contains zero or more items.</span></span> <span data-ttu-id="29f09-107">Podívejte se na [příklady konfiguračního souboru](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="29f09-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="29f09-108">U názvů nastavení se nerozlišují malá a velká písmena a hodnoty můžou používat [proměnné prostředí](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="29f09-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="29f09-109">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="29f09-109">In this topic:</span></span>

- [<span data-ttu-id="29f09-110">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="29f09-110">config section</span></span>](#config-section)
- [<span data-ttu-id="29f09-111">oddíl bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="29f09-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="29f09-112">oddíl packageRestore</span><span class="sxs-lookup"><span data-stu-id="29f09-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="29f09-113">oddíl řešení</span><span class="sxs-lookup"><span data-stu-id="29f09-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="29f09-114">[Zdrojové oddíly balíčku](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="29f09-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="29f09-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="29f09-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="29f09-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="29f09-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="29f09-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="29f09-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="29f09-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="29f09-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="29f09-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="29f09-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="29f09-120">oddíl trustedSigners</span><span class="sxs-lookup"><span data-stu-id="29f09-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="29f09-121">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="29f09-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="29f09-122">Ukázkový konfigurační soubor</span><span class="sxs-lookup"><span data-stu-id="29f09-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="29f09-123">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="29f09-123">config section</span></span>

<span data-ttu-id="29f09-124">Obsahuje různá nastavení konfigurace, která lze nastavit pomocí [ `nuget config` příkazu](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="29f09-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="29f09-125">`dependencyVersion`a `repositoryPath` platí pouze pro projekty pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="29f09-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="29f09-126">`globalPackagesFolder`platí jenom pro projekty, které používají formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="29f09-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="29f09-127">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-127">Key</span></span> | <span data-ttu-id="29f09-128">Hodnota</span><span class="sxs-lookup"><span data-stu-id="29f09-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-129">dependencyVersion (`packages.config` pouze)</span><span class="sxs-lookup"><span data-stu-id="29f09-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="29f09-130">Výchozí `DependencyVersion` hodnota pro instalaci balíčku, obnovení a aktualizaci, `-DependencyVersion` když přepínač není zadán přímo</span><span class="sxs-lookup"><span data-stu-id="29f09-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="29f09-131">Tuto hodnotu používá také uživatelské rozhraní Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="29f09-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="29f09-132">Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor`, .`Highest`</span><span class="sxs-lookup"><span data-stu-id="29f09-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="29f09-133">globalPackagesFolder (projekty používající pouze PackageReference)</span><span class="sxs-lookup"><span data-stu-id="29f09-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="29f09-134">Umístění výchozí složky globálních balíčků.</span><span class="sxs-lookup"><span data-stu-id="29f09-134">The location of the default global packages folder.</span></span> <span data-ttu-id="29f09-135">Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="29f09-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="29f09-136">Relativní cestu lze použít v souborech specifických `nuget.config` pro projekt.</span><span class="sxs-lookup"><span data-stu-id="29f09-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="29f09-137">Toto nastavení je přepsáno proměnnou prostředí NUGET_PACKAGES, která má přednost.</span><span class="sxs-lookup"><span data-stu-id="29f09-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="29f09-138">repositoryPath (`packages.config` pouze)</span><span class="sxs-lookup"><span data-stu-id="29f09-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="29f09-139">Místo, kde se mají instalovat balíčky NuGet místo výchozí `$(Solutiondir)/packages` složky</span><span class="sxs-lookup"><span data-stu-id="29f09-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="29f09-140">Relativní cestu lze použít v souborech specifických `nuget.config` pro projekt.</span><span class="sxs-lookup"><span data-stu-id="29f09-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="29f09-141">Toto nastavení je přepsáno proměnnou prostředí NUGET_PACKAGES, která má přednost.</span><span class="sxs-lookup"><span data-stu-id="29f09-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="29f09-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="29f09-142">defaultPushSource</span></span> | <span data-ttu-id="29f09-143">Určuje adresu URL nebo cestu ke zdroji balíčku, který má být použit jako výchozí, pokud pro operaci nebyly nalezeny žádné jiné zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="29f09-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="29f09-144">http_proxy http_proxy. User http_proxy. Password NO_PROXY</span><span class="sxs-lookup"><span data-stu-id="29f09-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="29f09-145">Nastavení proxy serveru, které se má použít při připojování ke zdrojům balíčků; by měl být ve formátu `http://<username>:<password>@<domain>`. `http_proxy`</span><span class="sxs-lookup"><span data-stu-id="29f09-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="29f09-146">Hesla jsou šifrovaná a nelze je přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="29f09-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="29f09-147">`no_proxy`V případě je tato hodnota čárkami oddělený seznam domén, které proxy server obejít.</span><span class="sxs-lookup"><span data-stu-id="29f09-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="29f09-148">Pro tyto hodnoty můžete alternativně použít proměnné prostředí http_proxy a NO_PROXY.</span><span class="sxs-lookup"><span data-stu-id="29f09-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="29f09-149">Další podrobnosti najdete v tématu [nastavení proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="29f09-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="29f09-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="29f09-150">signatureValidationMode</span></span> | <span data-ttu-id="29f09-151">Určuje režim ověřování, který se používá k ověření signatur balíčků pro instalaci balíčku a obnovení.</span><span class="sxs-lookup"><span data-stu-id="29f09-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="29f09-152">Hodnoty jsou `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="29f09-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="29f09-153">Výchozí hodnota je `accept`.</span><span class="sxs-lookup"><span data-stu-id="29f09-153">Defaults to `accept`.</span></span>

<span data-ttu-id="29f09-154">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="29f09-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="29f09-155">oddíl bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="29f09-155">bindingRedirects section</span></span>

<span data-ttu-id="29f09-156">Nakonfiguruje, jestli NuGet při instalaci balíčku automaticky přesměrovává vazby.</span><span class="sxs-lookup"><span data-stu-id="29f09-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="29f09-157">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-157">Key</span></span> | <span data-ttu-id="29f09-158">Value</span><span class="sxs-lookup"><span data-stu-id="29f09-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-159">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="29f09-159">skip</span></span> | <span data-ttu-id="29f09-160">Logická hodnota označující, zda se má přeskočit automatický přesměrování vazby</span><span class="sxs-lookup"><span data-stu-id="29f09-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="29f09-161">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="29f09-161">The default is false.</span></span> |

<span data-ttu-id="29f09-162">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="29f09-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="29f09-163">oddíl packageRestore</span><span class="sxs-lookup"><span data-stu-id="29f09-163">packageRestore section</span></span>

<span data-ttu-id="29f09-164">Řídí obnovení balíčku během sestavení.</span><span class="sxs-lookup"><span data-stu-id="29f09-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="29f09-165">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-165">Key</span></span> | <span data-ttu-id="29f09-166">Value</span><span class="sxs-lookup"><span data-stu-id="29f09-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-167">enabled</span><span class="sxs-lookup"><span data-stu-id="29f09-167">enabled</span></span> | <span data-ttu-id="29f09-168">Logická hodnota označující, zda může NuGet provádět automatické obnovení.</span><span class="sxs-lookup"><span data-stu-id="29f09-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="29f09-169">Můžete také nastavit `EnableNuGetPackageRestore` proměnnou prostředí s `True` hodnotou místo nastavení tohoto klíče v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="29f09-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="29f09-170">automatická</span><span class="sxs-lookup"><span data-stu-id="29f09-170">automatic</span></span> | <span data-ttu-id="29f09-171">Logická hodnota označující, zda má NuGet při sestavení kontrolovat chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="29f09-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="29f09-172">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="29f09-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="29f09-173">oddíl řešení</span><span class="sxs-lookup"><span data-stu-id="29f09-173">solution section</span></span>

<span data-ttu-id="29f09-174">Určuje, zda `packages` je složka řešení obsažena ve správě zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="29f09-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="29f09-175">Tato část funguje pouze v `nuget.config` souborech ve složce řešení.</span><span class="sxs-lookup"><span data-stu-id="29f09-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="29f09-176">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-176">Key</span></span> | <span data-ttu-id="29f09-177">Hodnota</span><span class="sxs-lookup"><span data-stu-id="29f09-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="29f09-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="29f09-179">Logická hodnota označující, zda se má při práci se správou zdrojových kódů ignorovat složku balíčků.</span><span class="sxs-lookup"><span data-stu-id="29f09-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="29f09-180">Výchozí hodnota je False.</span><span class="sxs-lookup"><span data-stu-id="29f09-180">The default value is false.</span></span> |

<span data-ttu-id="29f09-181">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="29f09-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="29f09-182">Zdrojové oddíly balíčku</span><span class="sxs-lookup"><span data-stu-id="29f09-182">Package source sections</span></span>

<span data-ttu-id="29f09-183">Všechnypracují`packageSourceCredentials`společně `packageSources` ,`apikeys` abynakonfigurovali,jakNuGetfungujesúložištěmibalíčkuběhemoperacíinstalace,obnoveníaaktualizace`activePackageSource`. `disabledPackageSources` `trustedSigners`</span><span class="sxs-lookup"><span data-stu-id="29f09-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="29f09-184">[ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `apikeys` `trustedSigners` [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md) [ Příkaz`nuget sources` ](../reference/cli-reference/cli-ref-sources.md) se obecně používá ke správě těchto nastavení, s výjimkou toho, že je spravován pomocí příkazu a který je spravován pomocí příkazu.</span><span class="sxs-lookup"><span data-stu-id="29f09-184">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="29f09-185">Všimněte si, že zdrojová adresa URL pro `https://api.nuget.org/v3/index.json`NuGet.org je.</span><span class="sxs-lookup"><span data-stu-id="29f09-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="29f09-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="29f09-186">packageSources</span></span>

<span data-ttu-id="29f09-187">Zobrazí seznam všech známých zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="29f09-187">Lists all known package sources.</span></span> <span data-ttu-id="29f09-188">Pořadí se ignoruje během operací obnovení a s jakýmkoli projektem pomocí formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="29f09-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="29f09-189">NuGet respektuje pořadí zdrojů pro operace instalace a aktualizace s projekty pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="29f09-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="29f09-190">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-190">Key</span></span> | <span data-ttu-id="29f09-191">Value</span><span class="sxs-lookup"><span data-stu-id="29f09-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-192">(název, který se má přiřadit ke zdroji balíčku)</span><span class="sxs-lookup"><span data-stu-id="29f09-192">(name to assign to the package source)</span></span> | <span data-ttu-id="29f09-193">Cesta nebo adresa URL zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="29f09-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="29f09-194">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="29f09-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="29f09-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="29f09-195">packageSourceCredentials</span></span>

<span data-ttu-id="29f09-196">Ukládá uživatelská jména a hesla pro zdroje, obvykle zadané s `-username` přepínači a `-password` s `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="29f09-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="29f09-197">Hesla jsou zašifrována ve výchozím `-storepasswordincleartext` nastavení, pokud není použita ani tato možnost.</span><span class="sxs-lookup"><span data-stu-id="29f09-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="29f09-198">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-198">Key</span></span> | <span data-ttu-id="29f09-199">Value</span><span class="sxs-lookup"><span data-stu-id="29f09-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-200">username</span><span class="sxs-lookup"><span data-stu-id="29f09-200">username</span></span> | <span data-ttu-id="29f09-201">Uživatelské jméno pro zdroj v prostém textu.</span><span class="sxs-lookup"><span data-stu-id="29f09-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="29f09-202">password</span><span class="sxs-lookup"><span data-stu-id="29f09-202">password</span></span> | <span data-ttu-id="29f09-203">Šifrované heslo pro zdroj</span><span class="sxs-lookup"><span data-stu-id="29f09-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="29f09-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="29f09-204">cleartextpassword</span></span> | <span data-ttu-id="29f09-205">Nešifrované heslo zdroje</span><span class="sxs-lookup"><span data-stu-id="29f09-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="29f09-206">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="29f09-206">**Example:**</span></span>

<span data-ttu-id="29f09-207">V konfiguračním souboru `<packageSourceCredentials>` element obsahuje podřízené uzly pro každý platný název zdroje (mezery v názvu jsou nahrazeny řetězcem `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="29f09-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="29f09-208">To znamená, že pro zdroje s názvem "contoso" a "zdroj testu" obsahuje konfigurační soubor při použití šifrovaných hesel následující:</span><span class="sxs-lookup"><span data-stu-id="29f09-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="29f09-209">Při použití nezašifrovaných hesel:</span><span class="sxs-lookup"><span data-stu-id="29f09-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="29f09-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="29f09-210">apikeys</span></span>

<span data-ttu-id="29f09-211">Ukládá klíče pro zdroje, které používají ověřování pomocí klíče rozhraní API, jak [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)je nastaveno pomocí příkazu.</span><span class="sxs-lookup"><span data-stu-id="29f09-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="29f09-212">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-212">Key</span></span> | <span data-ttu-id="29f09-213">Hodnota</span><span class="sxs-lookup"><span data-stu-id="29f09-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-214">(zdrojová adresa URL)</span><span class="sxs-lookup"><span data-stu-id="29f09-214">(source URL)</span></span> | <span data-ttu-id="29f09-215">Šifrovaný klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="29f09-215">The encrypted API key.</span></span> |

<span data-ttu-id="29f09-216">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="29f09-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="29f09-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="29f09-217">disabledPackageSources</span></span>

<span data-ttu-id="29f09-218">Identifikovány aktuálně zakázané zdroje.</span><span class="sxs-lookup"><span data-stu-id="29f09-218">Identified currently disabled sources.</span></span> <span data-ttu-id="29f09-219">Může být prázdné.</span><span class="sxs-lookup"><span data-stu-id="29f09-219">May be empty.</span></span>

| <span data-ttu-id="29f09-220">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-220">Key</span></span> | <span data-ttu-id="29f09-221">Value</span><span class="sxs-lookup"><span data-stu-id="29f09-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-222">(název zdroje)</span><span class="sxs-lookup"><span data-stu-id="29f09-222">(name of source)</span></span> | <span data-ttu-id="29f09-223">Logická hodnota označující, zda je zdroj zakázán.</span><span class="sxs-lookup"><span data-stu-id="29f09-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="29f09-224">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="29f09-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="29f09-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="29f09-225">activePackageSource</span></span>

<span data-ttu-id="29f09-226">*(pouze 2. x; zastaralé v 3. x +)*</span><span class="sxs-lookup"><span data-stu-id="29f09-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="29f09-227">Identifikuje aktuálně aktivní zdroj nebo označuje agregaci všech zdrojů.</span><span class="sxs-lookup"><span data-stu-id="29f09-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="29f09-228">Key</span><span class="sxs-lookup"><span data-stu-id="29f09-228">Key</span></span> | <span data-ttu-id="29f09-229">Value</span><span class="sxs-lookup"><span data-stu-id="29f09-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f09-230">(název zdroje) nebo`All`</span><span class="sxs-lookup"><span data-stu-id="29f09-230">(name of source) or `All`</span></span> | <span data-ttu-id="29f09-231">Pokud je klíč názvem zdroje, hodnota je zdrojová cesta nebo adresa URL.</span><span class="sxs-lookup"><span data-stu-id="29f09-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="29f09-232">Pokud `All`by měla být `(Aggregate source)` hodnota pro kombinování všech zdrojů balíčků, které nejsou jinak zakázané.</span><span class="sxs-lookup"><span data-stu-id="29f09-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="29f09-233">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="29f09-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="29f09-234">oddíl trustedSigners</span><span class="sxs-lookup"><span data-stu-id="29f09-234">trustedSigners section</span></span>

<span data-ttu-id="29f09-235">Ukládá důvěryhodné podepisující osoby používané k povolení balíčku při instalaci nebo obnovení.</span><span class="sxs-lookup"><span data-stu-id="29f09-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="29f09-236">Tento seznam nemůže být prázdný, pokud je uživatel `signatureValidationMode` nastaven `require`na.</span><span class="sxs-lookup"><span data-stu-id="29f09-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="29f09-237">Tuto část lze aktualizovat pomocí [ `nuget trusted-signers` příkazu](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="29f09-237">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="29f09-238">**Schéma**:</span><span class="sxs-lookup"><span data-stu-id="29f09-238">**Schema**:</span></span>

<span data-ttu-id="29f09-239">Důvěryhodný podpis má kolekci `certificate` položek, které zařadí všechny certifikáty identifikující daného podepisujícího.</span><span class="sxs-lookup"><span data-stu-id="29f09-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="29f09-240">Důvěryhodný podpis může být buď `Author` `Repository`nebo.</span><span class="sxs-lookup"><span data-stu-id="29f09-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="29f09-241">Důvěryhodné *úložiště* také určuje `serviceIndex` úložiště (které musí být platným `https` identifikátorem URI) a může volitelně zadat středníkem oddělený seznam, který omezí ještě více uživatelů `owners` , kteří jsou z tohoto konkrétního typu považováni za důvěryhodné. úložištì.</span><span class="sxs-lookup"><span data-stu-id="29f09-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="29f09-242">Podporované algoritmy hash používané pro otisk certifikátu jsou `SHA256` `SHA384` a `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="29f09-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="29f09-243">Pokud je jako`true`daný certifikát povoleno řetězení k nedůvěryhodnému kořenovému adresáři při sestavování řetězu certifikátů v rámci ověření podpisu. `allowUntrustedRoot` `certificate`</span><span class="sxs-lookup"><span data-stu-id="29f09-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="29f09-244">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="29f09-244">**Example**:</span></span>

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

## <a name="using-environment-variables"></a><span data-ttu-id="29f09-245">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="29f09-245">Using environment variables</span></span>

<span data-ttu-id="29f09-246">Pokud chcete použít nastavení v době `nuget.config` běhu, můžete použít proměnné prostředí v hodnotách (NuGet 3.4 +).</span><span class="sxs-lookup"><span data-stu-id="29f09-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="29f09-247">Například pokud `HOME` je proměnná prostředí ve Windows nastavená na `c:\users\username` `%HOME%\NuGetRepository` , pak hodnota v konfiguračním souboru se přeloží na `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="29f09-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="29f09-248">Podobně, pokud `HOME` je on Mac/Linux nastavený na `/home/myStuff`, `%HOME%/NuGetRepository` se v konfiguračním souboru přeloží na `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="29f09-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="29f09-249">Pokud se proměnná prostředí nenajde, NuGet použije hodnotu literálu z konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="29f09-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="29f09-250">Ukázkový konfigurační soubor</span><span class="sxs-lookup"><span data-stu-id="29f09-250">Example config file</span></span>

<span data-ttu-id="29f09-251">Níže je příklad `nuget.config` souboru, který ilustruje několik nastavení:</span><span class="sxs-lookup"><span data-stu-id="29f09-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
