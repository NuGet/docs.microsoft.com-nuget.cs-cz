---
title: Odkaz na soubor NuGet.Config | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Odkaz na soubor NuGet.Config včetně konfigurace, bindingRedirects, packageRestore, řešení a packageSource oddíly.
keywords: Soubor NuGet.Config, referenci na konfigurační NuGet, možnosti konfigurace NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="87b82-104">Odkaz na soubor nuget.config.</span><span class="sxs-lookup"><span data-stu-id="87b82-104">NuGet.Config reference</span></span>

<span data-ttu-id="87b82-105">Chování NuGet je řízena nastavením v různých `NuGet.Config` souborů, jak je popsáno v [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="87b82-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="87b82-106">`NuGet.Config` je soubor XML obsahující nejvyšší úrovni `<configuration>` uzlu, který pak obsahuje část prvky popsané v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="87b82-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="87b82-107">Každý oddíl obsahuje nula nebo více `<add>` prvky s `key` a `value` atributy.</span><span class="sxs-lookup"><span data-stu-id="87b82-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="87b82-108">Najdete v článku [příklady konfiguračního souboru](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="87b82-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="87b82-109">Následující názvy nastavení jsou velká a malá písmena a můžete použít hodnoty [proměnné prostředí](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="87b82-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="87b82-110">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="87b82-110">In this topic:</span></span>

- [<span data-ttu-id="87b82-111">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="87b82-111">config section</span></span>](#config-section)
- [<span data-ttu-id="87b82-112">část bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="87b82-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="87b82-113">část packageRestore</span><span class="sxs-lookup"><span data-stu-id="87b82-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="87b82-114">část řešení</span><span class="sxs-lookup"><span data-stu-id="87b82-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="87b82-115">[Balíček zdrojové oddíly](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="87b82-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="87b82-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="87b82-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="87b82-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="87b82-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="87b82-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="87b82-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="87b82-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="87b82-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="87b82-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="87b82-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="87b82-121">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="87b82-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="87b82-122">Příklad konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="87b82-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="87b82-123">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="87b82-123">config section</span></span>

<span data-ttu-id="87b82-124">Obsahuje nastavení různé konfigurace, které se dá nastavit pomocí [ `nuget config` příkaz](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="87b82-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="87b82-125">`dependencyVersion` a `repositoryPath` se vztahují pouze na projektů pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="87b82-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="87b82-126">`globalPackagesFolder` platí pouze pro projekty PackageReference formátu.</span><span class="sxs-lookup"><span data-stu-id="87b82-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="87b82-127">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-127">Key</span></span> | <span data-ttu-id="87b82-128">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-129">dependencyVersion (`packages.config` pouze)</span><span class="sxs-lookup"><span data-stu-id="87b82-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="87b82-130">Výchozí `DependencyVersion` hodnotu pro instalaci balíčku, obnovení a aktualizace, když `-DependencyVersion` přepínač není zadán přímo.</span><span class="sxs-lookup"><span data-stu-id="87b82-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="87b82-131">Tato hodnota se používá také pomocí uživatelského rozhraní Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="87b82-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="87b82-132">Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="87b82-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="87b82-133">globalPackagesFolder (pouze pomocí PackageReference projekty)</span><span class="sxs-lookup"><span data-stu-id="87b82-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="87b82-134">Umístění složky výchozí globální balíčky.</span><span class="sxs-lookup"><span data-stu-id="87b82-134">The location of the default global packages folder.</span></span> <span data-ttu-id="87b82-135">Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="87b82-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="87b82-136">Relativní cesta mohou být používány specifické pro projekt `Nuget.Config` soubory.</span><span class="sxs-lookup"><span data-stu-id="87b82-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="87b82-137">Toto nastavení je přepsat proměnnou prostředí NUGET_PACKAGES, která má přednost před.</span><span class="sxs-lookup"><span data-stu-id="87b82-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="87b82-138">repositoryPath (`packages.config` pouze)</span><span class="sxs-lookup"><span data-stu-id="87b82-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="87b82-139">Umístění, v němž instalace balíčků NuGet místo výchozího `$(Solutiondir)/packages` složky.</span><span class="sxs-lookup"><span data-stu-id="87b82-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="87b82-140">Relativní cesta mohou být používány specifické pro projekt `Nuget.Config` soubory.</span><span class="sxs-lookup"><span data-stu-id="87b82-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="87b82-141">Toto nastavení je přepsat proměnnou prostředí NUGET_PACKAGES, která má přednost před.</span><span class="sxs-lookup"><span data-stu-id="87b82-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="87b82-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="87b82-142">defaultPushSource</span></span> | <span data-ttu-id="87b82-143">Určuje adresu URL nebo cestu zdroje balíčku, který se má použít jako výchozí pro operace nebyly nalezeny žádné jiné zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="87b82-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="87b82-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="87b82-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="87b82-145">Nastavení proxy serveru používat při připojování ke zdroji balíčků; `http_proxy` by měl být ve formátu `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="87b82-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="87b82-146">Hesla se šifrují a nelze ji přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="87b82-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="87b82-147">Pro `no_proxy`, hodnota je čárkami oddělený seznam domén Nepoužívat proxy server.</span><span class="sxs-lookup"><span data-stu-id="87b82-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="87b82-148">Případně můžete http_proxy a no_proxy proměnných prostředí pro tyto hodnoty.</span><span class="sxs-lookup"><span data-stu-id="87b82-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="87b82-149">Další podrobnosti najdete v tématu [nastavení proxy serveru NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="87b82-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="87b82-150">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="87b82-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="87b82-151">část bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="87b82-151">bindingRedirects section</span></span>

<span data-ttu-id="87b82-152">Nakonfiguruje, jestli NuGet nemá přesměrování vazby automatické při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="87b82-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="87b82-153">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-153">Key</span></span> | <span data-ttu-id="87b82-154">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-155">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="87b82-155">skip</span></span> | <span data-ttu-id="87b82-156">Logická hodnota, která určuje, jestli chcete vynechat přesměrování vazby automatické.</span><span class="sxs-lookup"><span data-stu-id="87b82-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="87b82-157">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="87b82-157">The default is false.</span></span> |

<span data-ttu-id="87b82-158">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="87b82-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="87b82-159">část packageRestore</span><span class="sxs-lookup"><span data-stu-id="87b82-159">packageRestore section</span></span>

<span data-ttu-id="87b82-160">Ovládací prvky obnovení balíčků během sestavení.</span><span class="sxs-lookup"><span data-stu-id="87b82-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="87b82-161">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-161">Key</span></span> | <span data-ttu-id="87b82-162">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-163">povoleno</span><span class="sxs-lookup"><span data-stu-id="87b82-163">enabled</span></span> | <span data-ttu-id="87b82-164">Logická hodnota, která určuje, zda NuGet můžete provádět automatického obnovení.</span><span class="sxs-lookup"><span data-stu-id="87b82-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="87b82-165">Můžete také nastavit `EnableNuGetPackageRestore` proměnnou prostředí s hodnotou `True` místo nastavení tohoto klíče v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="87b82-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="87b82-166">automatická</span><span class="sxs-lookup"><span data-stu-id="87b82-166">automatic</span></span> | <span data-ttu-id="87b82-167">Logická hodnota, která určuje, zda NuGet měli kontrolovat chybějící balíčky během sestavení.</span><span class="sxs-lookup"><span data-stu-id="87b82-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="87b82-168">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="87b82-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="87b82-169">část řešení</span><span class="sxs-lookup"><span data-stu-id="87b82-169">solution section</span></span>

<span data-ttu-id="87b82-170">Ovládací prvky jestli `packages` složku řešení je součástí zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="87b82-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="87b82-171">Tato část funguje pouze v `Nuget.Config` souborů ve složce řešení.</span><span class="sxs-lookup"><span data-stu-id="87b82-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="87b82-172">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-172">Key</span></span> | <span data-ttu-id="87b82-173">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="87b82-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="87b82-175">Logická hodnota, která určuje, zda ignorovat složce balíčků při práci se službou správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="87b82-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="87b82-176">Výchozí hodnota je False.</span><span class="sxs-lookup"><span data-stu-id="87b82-176">The default value is false.</span></span> |

<span data-ttu-id="87b82-177">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="87b82-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="87b82-178">Části zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="87b82-178">Package source sections</span></span>

<span data-ttu-id="87b82-179">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, A `disabledPackageSources` všechny pracovní dohromady a nakonfigurujte, jak funguje NuGet s úložiště balíčku během instalace, obnovení a operace aktualizace.</span><span class="sxs-lookup"><span data-stu-id="87b82-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="87b82-180">[ `nuget sources` Příkaz](../tools/cli-ref-sources.md) se obvykle používá ke správě těchto nastavení, s výjimkou `apikeys` kterou spravují pomocí [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="87b82-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="87b82-181">Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="87b82-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="87b82-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="87b82-182">packageSources</span></span>

<span data-ttu-id="87b82-183">Zobrazí seznam všech zdrojů známé balíčku.</span><span class="sxs-lookup"><span data-stu-id="87b82-183">Lists all known package sources.</span></span> <span data-ttu-id="87b82-184">Pořadí je ignorován během operace obnovení a s žádným projektem v PackageReference formátu.</span><span class="sxs-lookup"><span data-stu-id="87b82-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="87b82-185">Pořadí zdrojů pro instalace respektuje NuGet a aktualizovat operace s projekty pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="87b82-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="87b82-186">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-186">Key</span></span> | <span data-ttu-id="87b82-187">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-188">(název přiřadit do zdroje balíčku)</span><span class="sxs-lookup"><span data-stu-id="87b82-188">(name to assign to the package source)</span></span> | <span data-ttu-id="87b82-189">Cesta nebo adresa URL zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="87b82-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="87b82-190">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="87b82-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="87b82-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="87b82-191">packageSourceCredentials</span></span>

<span data-ttu-id="87b82-192">Ukládá uživatelská jména a hesla pro zdroje, obvykle zadaným `-username` a `-password` přepne s `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="87b82-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="87b82-193">Hesla jsou ve výchozím nastavení zašifrované, pokud `-storepasswordincleartext` je také možnost použít.</span><span class="sxs-lookup"><span data-stu-id="87b82-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="87b82-194">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-194">Key</span></span> | <span data-ttu-id="87b82-195">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-196">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="87b82-196">username</span></span> | <span data-ttu-id="87b82-197">Uživatelské jméno pro tento zdroj ve formátu prostého textu.</span><span class="sxs-lookup"><span data-stu-id="87b82-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="87b82-198">Heslo</span><span class="sxs-lookup"><span data-stu-id="87b82-198">password</span></span> | <span data-ttu-id="87b82-199">Zašifrované heslo pro zdroj.</span><span class="sxs-lookup"><span data-stu-id="87b82-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="87b82-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="87b82-200">cleartextpassword</span></span> | <span data-ttu-id="87b82-201">Nezašifrované heslo pro zdroj.</span><span class="sxs-lookup"><span data-stu-id="87b82-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="87b82-202">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="87b82-202">**Example:**</span></span>

<span data-ttu-id="87b82-203">V konfiguračním souboru `<packageSourceCredentials>` element obsahuje podřízené uzly pro každý název příslušným zdrojovým (s nahrazením mezer v názvu `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="87b82-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="87b82-204">To znamená zdrojů s názvem "Contoso" a "Test zdroj", konfigurační soubor obsahuje následující při použití šifrovaných hesel:</span><span class="sxs-lookup"><span data-stu-id="87b82-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="87b82-205">Při použití nešifrovaná hesla:</span><span class="sxs-lookup"><span data-stu-id="87b82-205">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="87b82-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="87b82-206">apikeys</span></span>

<span data-ttu-id="87b82-207">Ukládá klíče pro zdroje, které používají rozhraní API klíče ověřování, jako sada [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="87b82-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="87b82-208">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-208">Key</span></span> | <span data-ttu-id="87b82-209">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-210">(adresa URL zdroje)</span><span class="sxs-lookup"><span data-stu-id="87b82-210">(source URL)</span></span> | <span data-ttu-id="87b82-211">Šifrovaný klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="87b82-211">The encrypted API key.</span></span> |

<span data-ttu-id="87b82-212">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="87b82-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="87b82-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="87b82-213">disabledPackageSources</span></span>

<span data-ttu-id="87b82-214">Identifikovat aktuálně zakázané zdroje.</span><span class="sxs-lookup"><span data-stu-id="87b82-214">Identified currently disabled sources.</span></span> <span data-ttu-id="87b82-215">Může být prázdná.</span><span class="sxs-lookup"><span data-stu-id="87b82-215">May be empty.</span></span>

| <span data-ttu-id="87b82-216">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-216">Key</span></span> | <span data-ttu-id="87b82-217">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-218">(název zdroje)</span><span class="sxs-lookup"><span data-stu-id="87b82-218">(name of source)</span></span> | <span data-ttu-id="87b82-219">Logická hodnota určující, zda je neaktivní zdroj.</span><span class="sxs-lookup"><span data-stu-id="87b82-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="87b82-220">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="87b82-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="87b82-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="87b82-221">activePackageSource</span></span>

<span data-ttu-id="87b82-222">*(jenom 2.x; nepoužívané v 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="87b82-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="87b82-223">Identifikuje ke zdroji aktuálně aktivní, nebo označuje agregace všech zdrojů.</span><span class="sxs-lookup"><span data-stu-id="87b82-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="87b82-224">Key</span><span class="sxs-lookup"><span data-stu-id="87b82-224">Key</span></span> | <span data-ttu-id="87b82-225">Hodnota</span><span class="sxs-lookup"><span data-stu-id="87b82-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="87b82-226">(název zdroje) nebo `All`</span><span class="sxs-lookup"><span data-stu-id="87b82-226">(name of source) or `All`</span></span> | <span data-ttu-id="87b82-227">Pokud klíč je název zdroje, hodnota je zdrojová cesta nebo adresa URL.</span><span class="sxs-lookup"><span data-stu-id="87b82-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="87b82-228">Pokud `All`, hodnota by měla být `(Aggregate source)` kombinovat všechny zdroje balíčků, které jinak nejsou zakázány.</span><span class="sxs-lookup"><span data-stu-id="87b82-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="87b82-229">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="87b82-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="87b82-230">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="87b82-230">Using environment variables</span></span>

<span data-ttu-id="87b82-231">Můžete použít proměnné prostředí v `NuGet.Config` hodnoty (NuGet 3.4 +) k aplikování nastavení na dobu běhu.</span><span class="sxs-lookup"><span data-stu-id="87b82-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="87b82-232">Například pokud `HOME` proměnná prostředí v systému Windows je nastavená na `c:\users\username`, pak hodnota `%HOME%\NuGetRepository` v konfiguraci souboru přeloží na `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="87b82-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="87b82-233">Podobně pokud `HOME` na Mac/Linux je nastavena na `/home/myStuff`, pak `$HOME/NuGetRepository` v konfiguraci souboru přeloží na `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="87b82-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="87b82-234">Pokud není nalezena proměnná prostředí, používá NuGet literálovou hodnotou z konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="87b82-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="87b82-235">Příklad konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="87b82-235">Example config file</span></span>

<span data-ttu-id="87b82-236">Dole je příklad `NuGet.Config` soubor, který znázorňuje několik nastavení:</span><span class="sxs-lookup"><span data-stu-id="87b82-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
</configuration>
```
