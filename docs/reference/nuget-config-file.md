---
title: Odkaz na soubor NuGet. config
description: Odkaz na soubor NuGet. config včetně oddílů config, bindingRedirects, packageRestore, Solution a packageSource
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230523"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="90c46-103">Referenční dokumentace NuGet. config</span><span class="sxs-lookup"><span data-stu-id="90c46-103">nuget.config reference</span></span>

<span data-ttu-id="90c46-104">Chování NuGet se řídí nastavením v různých `NuGet.Config` nebo `nuget.config` souborů, jak je popsáno v tématu [běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="90c46-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="90c46-105">`nuget.config` je soubor XML, který obsahuje uzel `<configuration>` nejvyšší úrovně, který pak obsahuje prvky oddílu popsané v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="90c46-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="90c46-106">Každý oddíl obsahuje nula nebo více položek.</span><span class="sxs-lookup"><span data-stu-id="90c46-106">Each section contains zero or more items.</span></span> <span data-ttu-id="90c46-107">Podívejte se na [příklady konfiguračního souboru](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="90c46-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="90c46-108">U názvů nastavení se nerozlišují malá a velká písmena a hodnoty můžou používat [proměnné prostředí](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="90c46-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="90c46-109">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="90c46-109">config section</span></span>

<span data-ttu-id="90c46-110">Obsahuje různá nastavení konfigurace, která se dají nastavit pomocí [příkazu`nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="90c46-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="90c46-111">`dependencyVersion` a `repositoryPath` se vztahují pouze na projekty používající `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="90c46-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="90c46-112">`globalPackagesFolder` platí jenom pro projekty, které používají formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="90c46-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="90c46-113">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-113">Key</span></span> | <span data-ttu-id="90c46-114">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-115">dependencyVersion (pouze`packages.config`)</span><span class="sxs-lookup"><span data-stu-id="90c46-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="90c46-116">Výchozí hodnota `DependencyVersion` pro instalaci, obnovení a aktualizaci balíčku, když `-DependencyVersion` přepínač není zadán přímo.</span><span class="sxs-lookup"><span data-stu-id="90c46-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="90c46-117">Tuto hodnotu používá také uživatelské rozhraní Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="90c46-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="90c46-118">Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor``Highest`.</span><span class="sxs-lookup"><span data-stu-id="90c46-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="90c46-119">globalPackagesFolder (projekty používající pouze PackageReference)</span><span class="sxs-lookup"><span data-stu-id="90c46-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="90c46-120">Umístění výchozí složky globálních balíčků.</span><span class="sxs-lookup"><span data-stu-id="90c46-120">The location of the default global packages folder.</span></span> <span data-ttu-id="90c46-121">Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="90c46-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="90c46-122">Relativní cestu lze použít v souborech `nuget.config` specifických pro projekt.</span><span class="sxs-lookup"><span data-stu-id="90c46-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="90c46-123">Toto nastavení je přepsáno proměnnou prostředí NUGET_PACKAGES, která má přednost.</span><span class="sxs-lookup"><span data-stu-id="90c46-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="90c46-124">repositoryPath (pouze`packages.config`)</span><span class="sxs-lookup"><span data-stu-id="90c46-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="90c46-125">Místo, kam se mají instalovat balíčky NuGet místo výchozí složky `$(Solutiondir)/packages`</span><span class="sxs-lookup"><span data-stu-id="90c46-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="90c46-126">Relativní cestu lze použít v souborech `nuget.config` specifických pro projekt.</span><span class="sxs-lookup"><span data-stu-id="90c46-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="90c46-127">Toto nastavení je přepsáno proměnnou prostředí NUGET_PACKAGES, která má přednost.</span><span class="sxs-lookup"><span data-stu-id="90c46-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="90c46-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="90c46-128">defaultPushSource</span></span> | <span data-ttu-id="90c46-129">Určuje adresu URL nebo cestu ke zdroji balíčku, který má být použit jako výchozí, pokud pro operaci nebyly nalezeny žádné jiné zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="90c46-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="90c46-130">http_proxy http_proxy. uživatelské http_proxy. Password no_proxy</span><span class="sxs-lookup"><span data-stu-id="90c46-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="90c46-131">Nastavení proxy serveru, které se má použít při připojování ke zdrojům balíčků; `http_proxy` by měl být ve formátu `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="90c46-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="90c46-132">Hesla jsou šifrovaná a nelze je přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="90c46-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="90c46-133">V případě `no_proxy`je tato hodnota čárkami oddělený seznam domén, které proxy server vynechá.</span><span class="sxs-lookup"><span data-stu-id="90c46-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="90c46-134">Pro tyto hodnoty můžete alternativně použít proměnné prostředí http_proxy a no_proxy.</span><span class="sxs-lookup"><span data-stu-id="90c46-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="90c46-135">Další podrobnosti najdete v tématu [nastavení proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="90c46-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="90c46-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="90c46-136">signatureValidationMode</span></span> | <span data-ttu-id="90c46-137">Určuje režim ověřování, který se používá k ověření signatur balíčků pro instalaci balíčku a obnovení.</span><span class="sxs-lookup"><span data-stu-id="90c46-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="90c46-138">Hodnoty jsou `accept``require`.</span><span class="sxs-lookup"><span data-stu-id="90c46-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="90c46-139">Výchozí hodnota je `accept`.</span><span class="sxs-lookup"><span data-stu-id="90c46-139">Defaults to `accept`.</span></span>

<span data-ttu-id="90c46-140">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="90c46-141">oddíl bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="90c46-141">bindingRedirects section</span></span>

<span data-ttu-id="90c46-142">Nakonfiguruje, jestli NuGet při instalaci balíčku automaticky přesměrovává vazby.</span><span class="sxs-lookup"><span data-stu-id="90c46-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="90c46-143">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-143">Key</span></span> | <span data-ttu-id="90c46-144">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-145">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="90c46-145">skip</span></span> | <span data-ttu-id="90c46-146">Logická hodnota označující, zda se má přeskočit automatický přesměrování vazby</span><span class="sxs-lookup"><span data-stu-id="90c46-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="90c46-147">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="90c46-147">The default is false.</span></span> |

<span data-ttu-id="90c46-148">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="90c46-149">oddíl packageRestore</span><span class="sxs-lookup"><span data-stu-id="90c46-149">packageRestore section</span></span>

<span data-ttu-id="90c46-150">Řídí obnovení balíčku během sestavení.</span><span class="sxs-lookup"><span data-stu-id="90c46-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="90c46-151">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-151">Key</span></span> | <span data-ttu-id="90c46-152">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-153">povolené</span><span class="sxs-lookup"><span data-stu-id="90c46-153">enabled</span></span> | <span data-ttu-id="90c46-154">Logická hodnota označující, zda může NuGet provádět automatické obnovení.</span><span class="sxs-lookup"><span data-stu-id="90c46-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="90c46-155">Můžete také nastavit proměnnou prostředí `EnableNuGetPackageRestore` s hodnotou `True` namísto nastavení tohoto klíče v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="90c46-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="90c46-156">automatická</span><span class="sxs-lookup"><span data-stu-id="90c46-156">automatic</span></span> | <span data-ttu-id="90c46-157">Logická hodnota označující, zda má NuGet při sestavení kontrolovat chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="90c46-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="90c46-158">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="90c46-159">oddíl řešení</span><span class="sxs-lookup"><span data-stu-id="90c46-159">solution section</span></span>

<span data-ttu-id="90c46-160">Určuje, zda je `packages` složka řešení zahrnutá ve správě zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="90c46-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="90c46-161">Tato část funguje pouze v `nuget.config` soubory ve složce řešení.</span><span class="sxs-lookup"><span data-stu-id="90c46-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="90c46-162">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-162">Key</span></span> | <span data-ttu-id="90c46-163">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="90c46-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="90c46-165">Logická hodnota označující, zda se má při práci se správou zdrojových kódů ignorovat složku balíčků.</span><span class="sxs-lookup"><span data-stu-id="90c46-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="90c46-166">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="90c46-166">The default value is false.</span></span> |

<span data-ttu-id="90c46-167">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="90c46-168">Zdrojové oddíly balíčku</span><span class="sxs-lookup"><span data-stu-id="90c46-168">Package source sections</span></span>

<span data-ttu-id="90c46-169">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` a `trustedSigners` společně nakonfigurují, jak NuGet funguje s úložištěmi balíčků během operací instalace, obnovení a aktualizace.</span><span class="sxs-lookup"><span data-stu-id="90c46-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="90c46-170">[Příkaz`nuget sources`](../reference/cli-reference/cli-ref-sources.md) se obecně používá ke správě těchto nastavení, s výjimkou `apikeys`, která je spravována pomocí [příkazu`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md), a `trustedSigners`, které je spravováno pomocí [příkazu`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="90c46-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="90c46-171">Všimněte si, že zdrojová adresa URL pro nuget.org je `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="90c46-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="90c46-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="90c46-172">packageSources</span></span>

<span data-ttu-id="90c46-173">Zobrazí seznam všech známých zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="90c46-173">Lists all known package sources.</span></span> <span data-ttu-id="90c46-174">Pořadí se ignoruje během operací obnovení a s jakýmkoli projektem pomocí formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="90c46-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="90c46-175">NuGet respektuje pořadí zdrojů pro operace instalace a aktualizace s projekty pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="90c46-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="90c46-176">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-176">Key</span></span> | <span data-ttu-id="90c46-177">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-178">(název, který se má přiřadit ke zdroji balíčku)</span><span class="sxs-lookup"><span data-stu-id="90c46-178">(name to assign to the package source)</span></span> | <span data-ttu-id="90c46-179">Cesta nebo adresa URL zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="90c46-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="90c46-180">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="90c46-181">Pokud je pro daný uzel k dispozici `<clear />`, NuGet ignoruje dříve definované hodnoty konfigurace pro tento uzel.</span><span class="sxs-lookup"><span data-stu-id="90c46-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="90c46-182">[Přečtěte si další informace o použití nastavení](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="90c46-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="90c46-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="90c46-183">packageSourceCredentials</span></span>

<span data-ttu-id="90c46-184">Ukládá uživatelská jména a hesla pro zdroje, obvykle zadané pomocí `-username` a `-password` přepínačů `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="90c46-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="90c46-185">Pokud není použita možnost `-storepasswordincleartext`, jsou hesla ve výchozím nastavení zašifrována.</span><span class="sxs-lookup"><span data-stu-id="90c46-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="90c46-186">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-186">Key</span></span> | <span data-ttu-id="90c46-187">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-188">uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="90c46-188">username</span></span> | <span data-ttu-id="90c46-189">Uživatelské jméno pro zdroj v prostém textu.</span><span class="sxs-lookup"><span data-stu-id="90c46-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="90c46-190">heslo</span><span class="sxs-lookup"><span data-stu-id="90c46-190">password</span></span> | <span data-ttu-id="90c46-191">Šifrované heslo pro zdroj</span><span class="sxs-lookup"><span data-stu-id="90c46-191">The encrypted password for the source.</span></span> |
| <span data-ttu-id="90c46-192">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="90c46-192">cleartextpassword</span></span> | <span data-ttu-id="90c46-193">Nešifrované heslo zdroje</span><span class="sxs-lookup"><span data-stu-id="90c46-193">The unencrypted password for the source.</span></span> |

<span data-ttu-id="90c46-194">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="90c46-194">**Example:**</span></span>

<span data-ttu-id="90c46-195">V konfiguračním souboru `<packageSourceCredentials>` element obsahuje podřízené uzly pro každý příslušný název zdroje (mezery v názvu jsou nahrazeny `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="90c46-195">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="90c46-196">To znamená, že pro zdroje s názvem "contoso" a "zdroj testu" obsahuje konfigurační soubor při použití šifrovaných hesel následující:</span><span class="sxs-lookup"><span data-stu-id="90c46-196">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="90c46-197">Při použití nezašifrovaných hesel:</span><span class="sxs-lookup"><span data-stu-id="90c46-197">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="90c46-198">apikeys</span><span class="sxs-lookup"><span data-stu-id="90c46-198">apikeys</span></span>

<span data-ttu-id="90c46-199">Ukládá klíče pro zdroje, které používají ověřování pomocí klíče rozhraní API, jak je nastaveno pomocí [příkazu`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="90c46-199">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="90c46-200">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-200">Key</span></span> | <span data-ttu-id="90c46-201">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-201">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-202">(zdrojová adresa URL)</span><span class="sxs-lookup"><span data-stu-id="90c46-202">(source URL)</span></span> | <span data-ttu-id="90c46-203">Šifrovaný klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="90c46-203">The encrypted API key.</span></span> |

<span data-ttu-id="90c46-204">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-204">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="90c46-205">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="90c46-205">disabledPackageSources</span></span>

<span data-ttu-id="90c46-206">Identifikovány aktuálně zakázané zdroje.</span><span class="sxs-lookup"><span data-stu-id="90c46-206">Identified currently disabled sources.</span></span> <span data-ttu-id="90c46-207">Může být prázdné.</span><span class="sxs-lookup"><span data-stu-id="90c46-207">May be empty.</span></span>

| <span data-ttu-id="90c46-208">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-208">Key</span></span> | <span data-ttu-id="90c46-209">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-210">(název zdroje)</span><span class="sxs-lookup"><span data-stu-id="90c46-210">(name of source)</span></span> | <span data-ttu-id="90c46-211">Logická hodnota označující, zda je zdroj zakázán.</span><span class="sxs-lookup"><span data-stu-id="90c46-211">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="90c46-212">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="90c46-212">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="90c46-213">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="90c46-213">activePackageSource</span></span>

<span data-ttu-id="90c46-214">*(pouze 2. x; zastaralé v 3. x +)*</span><span class="sxs-lookup"><span data-stu-id="90c46-214">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="90c46-215">Identifikuje aktuálně aktivní zdroj nebo označuje agregaci všech zdrojů.</span><span class="sxs-lookup"><span data-stu-id="90c46-215">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="90c46-216">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-216">Key</span></span> | <span data-ttu-id="90c46-217">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-218">(název zdroje) nebo `All`</span><span class="sxs-lookup"><span data-stu-id="90c46-218">(name of source) or `All`</span></span> | <span data-ttu-id="90c46-219">Pokud je klíč názvem zdroje, hodnota je zdrojová cesta nebo adresa URL.</span><span class="sxs-lookup"><span data-stu-id="90c46-219">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="90c46-220">Pokud `All`, musí být hodnota `(Aggregate source)` pro kombinování všech zdrojů balíčků, které nejsou jinak zakázány.</span><span class="sxs-lookup"><span data-stu-id="90c46-220">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="90c46-221">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-221">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="90c46-222">oddíl trustedSigners</span><span class="sxs-lookup"><span data-stu-id="90c46-222">trustedSigners section</span></span>

<span data-ttu-id="90c46-223">Ukládá důvěryhodné podepisující osoby používané k povolení balíčku při instalaci nebo obnovení.</span><span class="sxs-lookup"><span data-stu-id="90c46-223">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="90c46-224">Tento seznam nemůže být prázdný, pokud uživatel nastaví `signatureValidationMode` k `require`.</span><span class="sxs-lookup"><span data-stu-id="90c46-224">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="90c46-225">Tuto část lze aktualizovat pomocí [příkazu`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="90c46-225">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="90c46-226">**Schéma**:</span><span class="sxs-lookup"><span data-stu-id="90c46-226">**Schema**:</span></span>

<span data-ttu-id="90c46-227">Důvěryhodný podpis má kolekci `certificate`ch položek, které zařadí všechny certifikáty identifikující daného podepisujícího.</span><span class="sxs-lookup"><span data-stu-id="90c46-227">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="90c46-228">Důvěryhodný podpis může být buď `Author`, nebo `Repository`.</span><span class="sxs-lookup"><span data-stu-id="90c46-228">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="90c46-229">Důvěryhodné *úložiště* také určuje `serviceIndex` pro úložiště (musí to být platný identifikátor URI `https`) a může volitelně zadat středníkem oddělený seznam `owners`, aby bylo možné ještě více omezit, kdo je z tohoto konkrétního úložiště důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="90c46-229">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="90c46-230">Podporované algoritmy hash používané pro otisk certifikátu jsou `SHA256`, `SHA384` a `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="90c46-230">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="90c46-231">Pokud `certificate` specifikuje `allowUntrustedRoot` jako `true` daný certifikát může při vytváření řetězu certifikátů v rámci ověřování podpisů řetězit nedůvěryhodnému kořenovému adresáři.</span><span class="sxs-lookup"><span data-stu-id="90c46-231">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="90c46-232">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-232">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="90c46-233">oddíl fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="90c46-233">fallbackPackageFolders section</span></span>

<span data-ttu-id="90c46-234">*(3.5 +)* Poskytuje způsob, jak předinstalovat balíčky, aby nedošlo k tomu, že by se v případě nalezení balíčku v záložních složkách prováděla žádná práce.</span><span class="sxs-lookup"><span data-stu-id="90c46-234">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="90c46-235">Záložní složky balíčku mají stejnou složku a strukturu souborů jako globální složka balíčku: *. nupkg* je k dispozici a jsou extrahovány všechny soubory.</span><span class="sxs-lookup"><span data-stu-id="90c46-235">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="90c46-236">Logika vyhledávání pro tuto konfiguraci je:</span><span class="sxs-lookup"><span data-stu-id="90c46-236">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="90c46-237">Pokud chcete zjistit, jestli je balíček/verze už stažený, vyhledejte globální složku balíčku.</span><span class="sxs-lookup"><span data-stu-id="90c46-237">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="90c46-238">Vyhledejte shodu balíčku/verze v záložních složkách.</span><span class="sxs-lookup"><span data-stu-id="90c46-238">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="90c46-239">Pokud je vyhledávání úspěšné, není nutné stahovat žádné soubory.</span><span class="sxs-lookup"><span data-stu-id="90c46-239">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="90c46-240">Pokud se shoda nenajde, vyhledá NuGet zdroje souborů, potom zdroje http a pak stáhne balíčky.</span><span class="sxs-lookup"><span data-stu-id="90c46-240">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="90c46-241">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-241">Key</span></span> | <span data-ttu-id="90c46-242">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-242">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-243">(název záložní složky)</span><span class="sxs-lookup"><span data-stu-id="90c46-243">(name of fallback folder)</span></span> | <span data-ttu-id="90c46-244">Cesta k záložní složce</span><span class="sxs-lookup"><span data-stu-id="90c46-244">Path to fallback folder.</span></span> |

<span data-ttu-id="90c46-245">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-245">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="90c46-246">oddíl packageManagement</span><span class="sxs-lookup"><span data-stu-id="90c46-246">packageManagement section</span></span>

<span data-ttu-id="90c46-247">Nastaví výchozí formát správy balíčků, buď *Packages. config* , nebo PackageReference.</span><span class="sxs-lookup"><span data-stu-id="90c46-247">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="90c46-248">Projekty ve stylu sady SDK vždycky používají PackageReference.</span><span class="sxs-lookup"><span data-stu-id="90c46-248">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="90c46-249">Klíč</span><span class="sxs-lookup"><span data-stu-id="90c46-249">Key</span></span> | <span data-ttu-id="90c46-250">Hodnota</span><span class="sxs-lookup"><span data-stu-id="90c46-250">Value</span></span> |
| --- | --- |
| <span data-ttu-id="90c46-251">format</span><span class="sxs-lookup"><span data-stu-id="90c46-251">format</span></span> | <span data-ttu-id="90c46-252">Logická hodnota označující výchozí formát správy balíčků.</span><span class="sxs-lookup"><span data-stu-id="90c46-252">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="90c46-253">Pokud je `1`, formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="90c46-253">If `1`, format is PackageReference.</span></span> <span data-ttu-id="90c46-254">Pokud `0`, formát je *Packages. config*.</span><span class="sxs-lookup"><span data-stu-id="90c46-254">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="90c46-255">zakázaný</span><span class="sxs-lookup"><span data-stu-id="90c46-255">disabled</span></span> | <span data-ttu-id="90c46-256">Logická hodnota označující, zda se při první instalaci balíčku má zobrazit výzva k výběru výchozího formátu balíčku.</span><span class="sxs-lookup"><span data-stu-id="90c46-256">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="90c46-257">`False` skryje výzvu.</span><span class="sxs-lookup"><span data-stu-id="90c46-257">`False` hides the prompt.</span></span> |

<span data-ttu-id="90c46-258">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="90c46-258">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="90c46-259">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="90c46-259">Using environment variables</span></span>

<span data-ttu-id="90c46-260">Pomocí proměnných prostředí v `nuget.config`ch hodnotách (NuGet 3.4 +) můžete použít nastavení v době běhu.</span><span class="sxs-lookup"><span data-stu-id="90c46-260">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="90c46-261">Pokud je například proměnná prostředí `HOME` v systému Windows nastavena na hodnotu `c:\users\username`, hodnota `%HOME%\NuGetRepository` v konfiguračním souboru se přeloží na `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="90c46-261">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="90c46-262">Všimněte si, že je nutné použít proměnné prostředí ve stylu systému Windows (začíná a končí v%) i v systému Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="90c46-262">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="90c46-263">Nastavení `$HOME/NuGetRepository` v konfiguračním souboru nebude vyřešeno.</span><span class="sxs-lookup"><span data-stu-id="90c46-263">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="90c46-264">V systému Mac/Linux bude hodnota `%HOME%\NuGetRepository` překládat na `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="90c46-264">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="90c46-265">Pokud se proměnná prostředí nenajde, NuGet použije hodnotu literálu z konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="90c46-265">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="90c46-266">Ukázkový konfigurační soubor</span><span class="sxs-lookup"><span data-stu-id="90c46-266">Example config file</span></span>

<span data-ttu-id="90c46-267">Níže je příklad `nuget.config` souboru, který ilustruje několik nastavení včetně volitelných parametrů:</span><span class="sxs-lookup"><span data-stu-id="90c46-267">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
