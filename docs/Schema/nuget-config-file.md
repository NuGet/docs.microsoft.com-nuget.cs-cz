---
title: Odkaz na soubor NuGet.Config | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odkaz na soubor NuGet.Config včetně konfigurace, bindingRedirects, packageRestore, řešení a packageSource oddíly."
keywords: "Soubor NuGet.Config, referenci na konfigurační NuGet, možnosti konfigurace NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 97f19239bcfb7a1c3a3b9b53ea11d73c8b339079
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="33eca-104">Odkaz na soubor nuget.config.</span><span class="sxs-lookup"><span data-stu-id="33eca-104">NuGet.Config reference</span></span>

<span data-ttu-id="33eca-105">Chování NuGet je řízena nastavením v různých `NuGet.Config` souborů, jak je popsáno v [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="33eca-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="33eca-106">`NuGet.Config`je soubor XML obsahující nejvyšší úrovni `<configuration>` uzlu, který pak obsahuje část prvky popsané v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="33eca-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="33eca-107">Každý oddíl obsahuje nula nebo více `<add>` prvky s `key` a `value` atributy.</span><span class="sxs-lookup"><span data-stu-id="33eca-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="33eca-108">Najdete v článku [příklady konfiguračního souboru](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="33eca-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="33eca-109">Následující názvy nastavení jsou velká a malá písmena a můžete použít hodnoty [proměnné prostředí](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="33eca-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="33eca-110">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="33eca-110">In this topic:</span></span>

- [<span data-ttu-id="33eca-111">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="33eca-111">config section</span></span>](#config-section)
- [<span data-ttu-id="33eca-112">část bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="33eca-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="33eca-113">část packageRestore</span><span class="sxs-lookup"><span data-stu-id="33eca-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="33eca-114">část řešení</span><span class="sxs-lookup"><span data-stu-id="33eca-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="33eca-115">[Balíček zdrojové oddíly](#package-source-sections): - [packageSources](#packagesources)</span><span class="sxs-lookup"><span data-stu-id="33eca-115">[Package source sections](#package-source-sections): -[packageSources](#packagesources)</span></span>
  - [<span data-ttu-id="33eca-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="33eca-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="33eca-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="33eca-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="33eca-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="33eca-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="33eca-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="33eca-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="33eca-120">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="33eca-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="33eca-121">Příklad konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="33eca-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="33eca-122">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="33eca-122">config section</span></span>

<span data-ttu-id="33eca-123">Obsahuje nastavení různé konfigurace, které se dá nastavit pomocí [ `nuget config` příkaz](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="33eca-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="33eca-124">Poznámka: `dependencyVersion` a `repositoryPath` se vztahují pouze na projektů pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="33eca-124">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="33eca-125">`globalPackagesFolder`platí pouze pro projekty PackageReference formátu.</span><span class="sxs-lookup"><span data-stu-id="33eca-125">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="33eca-126">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-126">Key</span></span> | <span data-ttu-id="33eca-127">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-128">dependencyVersion (`packages.config` pouze)</span><span class="sxs-lookup"><span data-stu-id="33eca-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="33eca-129">Výchozí `DependencyVersion` hodnotu pro instalaci balíčku, obnovení a aktualizace, když `-DependencyVersion` přepínač není zadán přímo.</span><span class="sxs-lookup"><span data-stu-id="33eca-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="33eca-130">Tato hodnota se používá také pomocí uživatelského rozhraní Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="33eca-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="33eca-131">Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="33eca-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="33eca-132">globalPackagesFolder (projekty nepoužíváte `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="33eca-132">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="33eca-133">Umístění složky výchozí globální balíčky.</span><span class="sxs-lookup"><span data-stu-id="33eca-133">The location of the default global packages folder.</span></span> <span data-ttu-id="33eca-134">Výchozí hodnota je `%USERPROFILE%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="33eca-134">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="33eca-135">Relativní cesta mohou být používány specifické pro projekt `Nuget.Config` soubory.</span><span class="sxs-lookup"><span data-stu-id="33eca-135">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="33eca-136">repositoryPath (`packages.config` pouze)</span><span class="sxs-lookup"><span data-stu-id="33eca-136">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="33eca-137">Umístění, v němž instalace balíčků NuGet místo výchozího `$(Solutiondir)/packages` složky.</span><span class="sxs-lookup"><span data-stu-id="33eca-137">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="33eca-138">Relativní cesta mohou být používány specifické pro projekt `Nuget.Config` soubory.</span><span class="sxs-lookup"><span data-stu-id="33eca-138">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="33eca-139">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="33eca-139">defaultPushSource</span></span> | <span data-ttu-id="33eca-140">Určuje adresu URL nebo cestu zdroje balíčku, který se má použít jako výchozí pro operace nebyly nalezeny žádné jiné zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="33eca-140">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="33eca-141">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="33eca-141">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="33eca-142">Nastavení proxy serveru používat při připojování ke zdroji balíčků; `http_proxy` by měl být ve formátu `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="33eca-142">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="33eca-143">Hesla se šifrují a nelze ji přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="33eca-143">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="33eca-144">Pro `no_proxy`, hodnota je čárkami oddělený seznam domén Nepoužívat proxy server.</span><span class="sxs-lookup"><span data-stu-id="33eca-144">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="33eca-145">Případně můžete http_proxy a no_proxy proměnných prostředí pro tyto hodnoty.</span><span class="sxs-lookup"><span data-stu-id="33eca-145">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="33eca-146">Další podrobnosti najdete v tématu [nastavení proxy serveru NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="33eca-146">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="33eca-147">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="33eca-147">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="33eca-148">část bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="33eca-148">bindingRedirects section</span></span>

<span data-ttu-id="33eca-149">Nakonfiguruje, jestli NuGet nemá přesměrování vazby automatické při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="33eca-149">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="33eca-150">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-150">Key</span></span> | <span data-ttu-id="33eca-151">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-151">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-152">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="33eca-152">skip</span></span> | <span data-ttu-id="33eca-153">Logická hodnota, která určuje, jestli chcete vynechat přesměrování vazby automatické.</span><span class="sxs-lookup"><span data-stu-id="33eca-153">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="33eca-154">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="33eca-154">The default is false.</span></span> |

<span data-ttu-id="33eca-155">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="33eca-155">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="33eca-156">část packageRestore</span><span class="sxs-lookup"><span data-stu-id="33eca-156">packageRestore section</span></span>

<span data-ttu-id="33eca-157">*Ignorovat v 2.7 +*</span><span class="sxs-lookup"><span data-stu-id="33eca-157">*Ignored in 2.7+*</span></span>

<span data-ttu-id="33eca-158">Ovládací prvky obnovení balíčků během sestavení.</span><span class="sxs-lookup"><span data-stu-id="33eca-158">Controls package restore during builds.</span></span>

| <span data-ttu-id="33eca-159">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-159">Key</span></span> | <span data-ttu-id="33eca-160">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-160">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-161">povoleno</span><span class="sxs-lookup"><span data-stu-id="33eca-161">enabled</span></span> | <span data-ttu-id="33eca-162">Logická hodnota, která určuje, zda NuGet můžete provádět automatického obnovení.</span><span class="sxs-lookup"><span data-stu-id="33eca-162">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="33eca-163">Můžete také nastavit `EnableNuGetPackageRestore` proměnnou prostředí s hodnotou `True` místo nastavení tohoto klíče v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="33eca-163">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="33eca-164">automatická</span><span class="sxs-lookup"><span data-stu-id="33eca-164">automatic</span></span> | <span data-ttu-id="33eca-165">Logická hodnota, která určuje, zda NuGet měli kontrolovat chybějící balíčky během sestavení.</span><span class="sxs-lookup"><span data-stu-id="33eca-165">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="33eca-166">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="33eca-166">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="33eca-167">část řešení</span><span class="sxs-lookup"><span data-stu-id="33eca-167">solution section</span></span>

<span data-ttu-id="33eca-168">Ovládací prvky jestli `packages` složku řešení je součástí zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="33eca-168">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="33eca-169">Tato část funguje pouze v `Nuget.Config` souborů ve složce řešení.</span><span class="sxs-lookup"><span data-stu-id="33eca-169">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="33eca-170">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-170">Key</span></span> | <span data-ttu-id="33eca-171">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-171">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-172">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="33eca-172">disableSourceControlIntegration</span></span> | <span data-ttu-id="33eca-173">Logická hodnota, která určuje, zda ignorovat složce balíčků při práci se službou správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="33eca-173">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="33eca-174">Výchozí hodnota je False.</span><span class="sxs-lookup"><span data-stu-id="33eca-174">The default value is false.</span></span> |

<span data-ttu-id="33eca-175">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="33eca-175">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="33eca-176">Části zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="33eca-176">Package source sections</span></span>

<span data-ttu-id="33eca-177">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, A `disabledPackageSources` všechny pracovní dohromady a nakonfigurujte, jak funguje NuGet s úložiště balíčku během instalace, obnovení a operace aktualizace.</span><span class="sxs-lookup"><span data-stu-id="33eca-177">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="33eca-178">[ `nuget sources` Příkaz](../tools/cli-ref-sources.md) se obvykle používá ke správě těchto nastavení, s výjimkou `apikeys` kterou spravují pomocí [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="33eca-178">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="33eca-179">Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="33eca-179">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="33eca-180">packageSources</span><span class="sxs-lookup"><span data-stu-id="33eca-180">packageSources</span></span>

<span data-ttu-id="33eca-181">Zobrazí seznam všech zdrojů známé balíčku.</span><span class="sxs-lookup"><span data-stu-id="33eca-181">Lists all known package sources.</span></span>

| <span data-ttu-id="33eca-182">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-182">Key</span></span> | <span data-ttu-id="33eca-183">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-183">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-184">(název přiřadit do zdroje balíčku)</span><span class="sxs-lookup"><span data-stu-id="33eca-184">(name to assign to the package source)</span></span> | <span data-ttu-id="33eca-185">Cesta nebo adresa URL zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="33eca-185">The path or URL of the package source.</span></span> |

<span data-ttu-id="33eca-186">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="33eca-186">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="33eca-187">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="33eca-187">packageSourceCredentials</span></span>

<span data-ttu-id="33eca-188">Ukládá uživatelská jména a hesla pro zdroje, obvykle zadaným `-username` a `-password` přepne s `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="33eca-188">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="33eca-189">Hesla jsou ve výchozím nastavení zašifrované, pokud `-storepasswordincleartext` je také možnost použít.</span><span class="sxs-lookup"><span data-stu-id="33eca-189">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="33eca-190">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-190">Key</span></span> | <span data-ttu-id="33eca-191">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-192">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="33eca-192">username</span></span> | <span data-ttu-id="33eca-193">Uživatelské jméno pro tento zdroj ve formátu prostého textu.</span><span class="sxs-lookup"><span data-stu-id="33eca-193">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="33eca-194">Heslo</span><span class="sxs-lookup"><span data-stu-id="33eca-194">password</span></span> | <span data-ttu-id="33eca-195">Zašifrované heslo pro zdroj.</span><span class="sxs-lookup"><span data-stu-id="33eca-195">The encrypted password for the source.</span></span> |
| <span data-ttu-id="33eca-196">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="33eca-196">cleartextpassword</span></span> | <span data-ttu-id="33eca-197">Nezašifrované heslo pro zdroj.</span><span class="sxs-lookup"><span data-stu-id="33eca-197">The unencrypted password for the source.</span></span> |

<span data-ttu-id="33eca-198">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="33eca-198">**Example:**</span></span>

<span data-ttu-id="33eca-199">V konfiguračním souboru `<packageSourceCredentials>` element obsahuje podřízené uzly pro každý název příslušným zdrojovým (s nahrazením mezer v názvu `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="33eca-199">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="33eca-200">To znamená zdrojů s názvem "Contoso" a "Test zdroj", konfigurační soubor obsahuje následující při použití šifrovaných hesel:</span><span class="sxs-lookup"><span data-stu-id="33eca-200">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="33eca-201">Při použití nešifrovaná hesla:</span><span class="sxs-lookup"><span data-stu-id="33eca-201">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="33eca-202">apikeys</span><span class="sxs-lookup"><span data-stu-id="33eca-202">apikeys</span></span>

<span data-ttu-id="33eca-203">Ukládá klíče pro zdroje, které používají rozhraní API klíče ověřování, jako sada [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="33eca-203">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="33eca-204">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-204">Key</span></span> | <span data-ttu-id="33eca-205">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-205">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-206">(adresa URL zdroje)</span><span class="sxs-lookup"><span data-stu-id="33eca-206">(source URL)</span></span> | <span data-ttu-id="33eca-207">Šifrovaný klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="33eca-207">The encrypted API key.</span></span> |

<span data-ttu-id="33eca-208">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="33eca-208">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="33eca-209">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="33eca-209">disabledPackageSources</span></span>

<span data-ttu-id="33eca-210">Identifikovat aktuálně zakázané zdroje.</span><span class="sxs-lookup"><span data-stu-id="33eca-210">Identified currently disabled sources.</span></span> <span data-ttu-id="33eca-211">Může být prázdná.</span><span class="sxs-lookup"><span data-stu-id="33eca-211">May be empty.</span></span>

| <span data-ttu-id="33eca-212">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-212">Key</span></span> | <span data-ttu-id="33eca-213">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-214">(název zdroje)</span><span class="sxs-lookup"><span data-stu-id="33eca-214">(name of source)</span></span> | <span data-ttu-id="33eca-215">Logická hodnota určující, zda je neaktivní zdroj.</span><span class="sxs-lookup"><span data-stu-id="33eca-215">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="33eca-216">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="33eca-216">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="33eca-217">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="33eca-217">activePackageSource</span></span>

<span data-ttu-id="33eca-218">*(jenom 2.x; nepoužívané v 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="33eca-218">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="33eca-219">Identifikuje ke zdroji aktuálně aktivní, nebo označuje agregace všech zdrojů.</span><span class="sxs-lookup"><span data-stu-id="33eca-219">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="33eca-220">Key</span><span class="sxs-lookup"><span data-stu-id="33eca-220">Key</span></span> | <span data-ttu-id="33eca-221">Hodnota</span><span class="sxs-lookup"><span data-stu-id="33eca-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="33eca-222">(název zdroje) nebo`All`</span><span class="sxs-lookup"><span data-stu-id="33eca-222">(name of source) or `All`</span></span> | <span data-ttu-id="33eca-223">Pokud klíč je název zdroje, hodnota je zdrojová cesta nebo adresa URL.</span><span class="sxs-lookup"><span data-stu-id="33eca-223">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="33eca-224">Pokud `All`, hodnota by měla být `(Aggregate source)` kombinovat všechny zdroje balíčků, které jinak nejsou zakázány.</span><span class="sxs-lookup"><span data-stu-id="33eca-224">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="33eca-225">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="33eca-225">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="33eca-226">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="33eca-226">Using environment variables</span></span>

<span data-ttu-id="33eca-227">Můžete použít proměnné prostředí v `NuGet.Config` hodnoty (NuGet 3.4 +) k aplikování nastavení na dobu běhu.</span><span class="sxs-lookup"><span data-stu-id="33eca-227">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="33eca-228">Například pokud `HOME` proměnná prostředí v systému Windows je nastavená na `c:\users\username`, pak hodnota `%HOME%\NuGetRepository` v konfiguraci souboru přeloží na `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="33eca-228">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="33eca-229">Podobně pokud `HOME` na Mac/Linux je nastavena na `/home/myStuff`, pak `$HOME/NuGetRepository` v konfiguraci souboru přeloží na `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="33eca-229">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="33eca-230">Pokud není nalezena proměnná prostředí, používá NuGet literálovou hodnotou z konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="33eca-230">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="33eca-231">Příklad konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="33eca-231">Example config file</span></span>

<span data-ttu-id="33eca-232">Dole je příklad `NuGet.Config` soubor, který znázorňuje několik nastavení:</span><span class="sxs-lookup"><span data-stu-id="33eca-232">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
