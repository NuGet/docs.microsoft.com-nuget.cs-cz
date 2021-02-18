---
title: Odkaz na soubor nuget.config
description: NuGet.Config odkaz na soubor včetně oddílů config, bindingRedirects, packageRestore, Solution a packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 60626a5a2a261241e0dce34421f73a86d815e454
ms.sourcegitcommit: aeb9072f2fcaca73dc9de05b7fd643f1aa7c5821
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/18/2021
ms.locfileid: "101101340"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="cbe2b-103">Odkaz na nuget.config</span><span class="sxs-lookup"><span data-stu-id="cbe2b-103">nuget.config reference</span></span>

<span data-ttu-id="cbe2b-104">Chování NuGet se řídí podle nastavení v různých `NuGet.Config` `nuget.config` souborech nebo, jak je popsáno v tématu [běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="cbe2b-105">`nuget.config` je soubor XML obsahující uzel nejvyšší úrovně `<configuration>` , který pak obsahuje prvky oddílu popsané v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="cbe2b-106">Každý oddíl obsahuje nula nebo více položek.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-106">Each section contains zero or more items.</span></span> <span data-ttu-id="cbe2b-107">Podívejte se na [příklady konfiguračního souboru](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="cbe2b-108">U názvů nastavení se nerozlišují malá a velká písmena a hodnoty můžou používat [proměnné prostředí](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="cbe2b-109">konfigurační oddíl</span><span class="sxs-lookup"><span data-stu-id="cbe2b-109">config section</span></span>

<span data-ttu-id="cbe2b-110">Obsahuje různá nastavení konfigurace, která lze nastavit pomocí [ `nuget config` příkazu](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="cbe2b-111">`dependencyVersion` a `repositoryPath` platí pouze pro projekty pomocí `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="cbe2b-112">`globalPackagesFolder` platí jenom pro projekty, které používají formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="cbe2b-113">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-113">Key</span></span> | <span data-ttu-id="cbe2b-114">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-115">dependencyVersion ( `packages.config` pouze)</span><span class="sxs-lookup"><span data-stu-id="cbe2b-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="cbe2b-116">Výchozí `DependencyVersion` hodnota pro instalaci balíčku, obnovení a aktualizaci, když `-DependencyVersion` přepínač není zadán přímo</span><span class="sxs-lookup"><span data-stu-id="cbe2b-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="cbe2b-117">Tuto hodnotu používá také uživatelské rozhraní Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="cbe2b-118">Hodnoty jsou `Lowest` , `HighestPatch` , `HighestMinor` , `Highest` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="cbe2b-119">globalPackagesFolder (projekty používající pouze PackageReference)</span><span class="sxs-lookup"><span data-stu-id="cbe2b-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="cbe2b-120">Umístění výchozí složky globálních balíčků.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-120">The location of the default global packages folder.</span></span> <span data-ttu-id="cbe2b-121">Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="cbe2b-122">Relativní cestu lze použít v souborech specifických pro projekt `nuget.config` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="cbe2b-123">Toto nastavení je přepsáno `NUGET_PACKAGES` proměnnou prostředí, která má přednost.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-123">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="cbe2b-124">repositoryPath ( `packages.config` pouze)</span><span class="sxs-lookup"><span data-stu-id="cbe2b-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="cbe2b-125">Místo, kde se mají instalovat balíčky NuGet místo výchozí `$(Solutiondir)/packages` složky</span><span class="sxs-lookup"><span data-stu-id="cbe2b-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="cbe2b-126">Relativní cestu lze použít v souborech specifických pro projekt `nuget.config` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="cbe2b-127">Toto nastavení je přepsáno `NUGET_PACKAGES` proměnnou prostředí, která má přednost.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-127">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="cbe2b-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="cbe2b-128">defaultPushSource</span></span> | <span data-ttu-id="cbe2b-129">Určuje adresu URL nebo cestu ke zdroji balíčku, který má být použit jako výchozí, pokud pro operaci nebyly nalezeny žádné jiné zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="cbe2b-130">http_proxy http_proxy. uživatelské http_proxy. Password no_proxy</span><span class="sxs-lookup"><span data-stu-id="cbe2b-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="cbe2b-131">Nastavení proxy serveru, které se má použít při připojování ke zdrojům balíčků; `http_proxy` by měl být ve formátu `http://<username>:<password>@<domain>` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="cbe2b-132">Hesla jsou šifrovaná a nelze je přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="cbe2b-133">V případě je `no_proxy` Tato hodnota čárkami oddělený seznam domén, které proxy server obejít.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="cbe2b-134">Pro tyto hodnoty můžete alternativně použít proměnné prostředí http_proxy a no_proxy.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="cbe2b-135">Další podrobnosti najdete v tématu [nastavení proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="cbe2b-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="cbe2b-136">signatureValidationMode</span></span> | <span data-ttu-id="cbe2b-137">Určuje režim ověřování, který se používá k ověření signatur balíčků pro instalaci balíčku a obnovení.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="cbe2b-138">Hodnoty jsou `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="cbe2b-139">Výchozí hodnota je `accept` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-139">Defaults to `accept`.</span></span>

<span data-ttu-id="cbe2b-140">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="cbe2b-141">oddíl bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="cbe2b-141">bindingRedirects section</span></span>

<span data-ttu-id="cbe2b-142">Nakonfiguruje, jestli NuGet při instalaci balíčku automaticky přesměrovává vazby.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="cbe2b-143">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-143">Key</span></span> | <span data-ttu-id="cbe2b-144">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-145">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="cbe2b-145">skip</span></span> | <span data-ttu-id="cbe2b-146">Logická hodnota označující, zda se má přeskočit automatický přesměrování vazby</span><span class="sxs-lookup"><span data-stu-id="cbe2b-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="cbe2b-147">Výchozí hodnotou je hodnota false.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-147">The default is false.</span></span> |

<span data-ttu-id="cbe2b-148">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="cbe2b-149">oddíl packageRestore</span><span class="sxs-lookup"><span data-stu-id="cbe2b-149">packageRestore section</span></span>

<span data-ttu-id="cbe2b-150">Řídí obnovení balíčku během sestavení.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="cbe2b-151">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-151">Key</span></span> | <span data-ttu-id="cbe2b-152">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-153">enabled</span><span class="sxs-lookup"><span data-stu-id="cbe2b-153">enabled</span></span> | <span data-ttu-id="cbe2b-154">Logická hodnota označující, zda může NuGet provádět automatické obnovení.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="cbe2b-155">Můžete také nastavit `EnableNuGetPackageRestore` proměnnou prostředí s hodnotou `True` místo nastavení tohoto klíče v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="cbe2b-156">automatická</span><span class="sxs-lookup"><span data-stu-id="cbe2b-156">automatic</span></span> | <span data-ttu-id="cbe2b-157">Logická hodnota označující, zda má NuGet při sestavení kontrolovat chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="cbe2b-158">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="cbe2b-159">oddíl řešení</span><span class="sxs-lookup"><span data-stu-id="cbe2b-159">solution section</span></span>

<span data-ttu-id="cbe2b-160">Určuje, zda `packages` je složka řešení obsažena ve správě zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="cbe2b-161">Tato část funguje pouze v `nuget.config` souborech ve složce řešení.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="cbe2b-162">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-162">Key</span></span> | <span data-ttu-id="cbe2b-163">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="cbe2b-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="cbe2b-165">Logická hodnota označující, zda se má při práci se správou zdrojových kódů ignorovat složku balíčků.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="cbe2b-166">Výchozí hodnota je False.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-166">The default value is false.</span></span> |

<span data-ttu-id="cbe2b-167">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="cbe2b-168">Zdrojové oddíly balíčku</span><span class="sxs-lookup"><span data-stu-id="cbe2b-168">Package source sections</span></span>

<span data-ttu-id="cbe2b-169">`packageSources` `packageSourceCredentials` `apikeys` `activePackageSource` `disabledPackageSources` `trustedSigners` Všechny pracují společně, aby nakonfigurovali, jak NuGet funguje s úložištěmi balíčku během operací instalace, obnovení a aktualizace.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="cbe2b-170">[ `nuget sources` Příkaz](../reference/cli-reference/cli-ref-sources.md) se obecně používá ke správě těchto nastavení, s výjimkou toho, že `apikeys` je spravován pomocí [ `nuget setapikey` příkazu](../reference/cli-reference/cli-ref-setapikey.md)a `trustedSigners` který je spravován pomocí [ `nuget trusted-signers` příkazu](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="cbe2b-171">Všimněte si, že zdrojová adresa URL pro nuget.org je `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="cbe2b-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="cbe2b-172">packageSources</span></span>

<span data-ttu-id="cbe2b-173">Zobrazí seznam všech známých zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-173">Lists all known package sources.</span></span> <span data-ttu-id="cbe2b-174">Pořadí se ignoruje během operací obnovení a s jakýmkoli projektem pomocí formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="cbe2b-175">NuGet respektuje pořadí zdrojů pro operace instalace a aktualizace s projekty pomocí `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="cbe2b-176">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-176">Key</span></span> | <span data-ttu-id="cbe2b-177">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-178">(název, který se má přiřadit ke zdroji balíčku)</span><span class="sxs-lookup"><span data-stu-id="cbe2b-178">(name to assign to the package source)</span></span> | <span data-ttu-id="cbe2b-179">Cesta nebo adresa URL zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="cbe2b-180">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="cbe2b-181">Když `<clear />` je pro daný uzel k dispozici, NuGet ignoruje dříve definované hodnoty konfigurace pro tento uzel.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="cbe2b-182">[Přečtěte si další informace o použití nastavení](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="cbe2b-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="cbe2b-183">packageSourceCredentials</span></span>

<span data-ttu-id="cbe2b-184">Ukládá uživatelská jména a hesla pro zdroje, obvykle zadané s `-username` `-password` přepínači a s `nuget sources` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="cbe2b-185">Hesla jsou zašifrována ve výchozím nastavení, pokud `-storepasswordincleartext` není použita ani tato možnost.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="cbe2b-186">Volitelně lze pomocí přepínače zadat platné typy ověřování `-validauthenticationtypes` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="cbe2b-187">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-187">Key</span></span> | <span data-ttu-id="cbe2b-188">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-189">username</span><span class="sxs-lookup"><span data-stu-id="cbe2b-189">username</span></span> | <span data-ttu-id="cbe2b-190">Uživatelské jméno pro zdroj v prostém textu.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="cbe2b-191">heslo</span><span class="sxs-lookup"><span data-stu-id="cbe2b-191">password</span></span> | <span data-ttu-id="cbe2b-192">Šifrované heslo pro zdroj</span><span class="sxs-lookup"><span data-stu-id="cbe2b-192">The encrypted password for the source.</span></span> <span data-ttu-id="cbe2b-193">Šifrovaná hesla jsou podporována pouze v systému Windows a lze je dešifrovat pouze v případě, že se používají ve stejném počítači a prostřednictvím stejného uživatele jako původní šifrování.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="cbe2b-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="cbe2b-194">cleartextpassword</span></span> | <span data-ttu-id="cbe2b-195">Nešifrované heslo zdroje</span><span class="sxs-lookup"><span data-stu-id="cbe2b-195">The unencrypted password for the source.</span></span> <span data-ttu-id="cbe2b-196">Poznámka: proměnné prostředí lze použít pro lepší zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="cbe2b-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="cbe2b-197">validauthenticationtypes</span></span> | <span data-ttu-id="cbe2b-198">Čárkami oddělený seznam platných typů ověřování pro tento zdroj.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="cbe2b-199">Tuto hodnotu nastavte na, `basic` Pokud server inzeruje protokol NTLM nebo vyjednávat a vaše přihlašovací údaje se musí poslat pomocí základního mechanismu, například při použití Pat s místními Azure DevOps Server.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="cbe2b-200">Mezi další platné hodnoty patří `negotiate` ,, `kerberos` `ntlm` a `digest` , ale tyto hodnoty jsou pravděpodobně užitečné.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="cbe2b-201">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="cbe2b-201">**Example:**</span></span>

<span data-ttu-id="cbe2b-202">V konfiguračním souboru `<packageSourceCredentials>` element obsahuje podřízené uzly pro každý platný název zdroje (mezery v názvu jsou nahrazeny řetězcem `_x0020_` ).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="cbe2b-203">To znamená, že pro zdroje s názvem "contoso" a "zdroj testu" obsahuje konfigurační soubor při použití šifrovaných hesel následující:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="cbe2b-204">Při použití nezašifrovaných hesel uložených v proměnné prostředí:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-204">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="cbe2b-205">Při použití nezašifrovaných hesel:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="cbe2b-206">Kromě toho lze zadat platné metody ověřování:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-206">Additionally, valid authentication methods can be supplied:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="cbe2b-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="cbe2b-207">apikeys</span></span>

<span data-ttu-id="cbe2b-208">Ukládá klíče pro zdroje, které používají ověřování pomocí klíče rozhraní API, jak je nastaveno pomocí [ `nuget setapikey` příkazu](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="cbe2b-209">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-209">Key</span></span> | <span data-ttu-id="cbe2b-210">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-211">(zdrojová adresa URL)</span><span class="sxs-lookup"><span data-stu-id="cbe2b-211">(source URL)</span></span> | <span data-ttu-id="cbe2b-212">Šifrovaný klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-212">The encrypted API key.</span></span> |

<span data-ttu-id="cbe2b-213">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="cbe2b-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="cbe2b-214">disabledPackageSources</span></span>

<span data-ttu-id="cbe2b-215">Identifikovány aktuálně zakázané zdroje.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-215">Identified currently disabled sources.</span></span> <span data-ttu-id="cbe2b-216">Může být prázdné.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-216">May be empty.</span></span>

| <span data-ttu-id="cbe2b-217">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-217">Key</span></span> | <span data-ttu-id="cbe2b-218">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-219">(název zdroje)</span><span class="sxs-lookup"><span data-stu-id="cbe2b-219">(name of source)</span></span> | <span data-ttu-id="cbe2b-220">Logická hodnota označující, zda je zdroj zakázán.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="cbe2b-221">**Příklad:**</span><span class="sxs-lookup"><span data-stu-id="cbe2b-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="cbe2b-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="cbe2b-222">activePackageSource</span></span>

<span data-ttu-id="cbe2b-223">*(pouze 2. x; zastaralé v 3. x +)*</span><span class="sxs-lookup"><span data-stu-id="cbe2b-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="cbe2b-224">Identifikuje aktuálně aktivní zdroj nebo označuje agregaci všech zdrojů.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="cbe2b-225">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-225">Key</span></span> | <span data-ttu-id="cbe2b-226">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-227">(název zdroje) nebo `All`</span><span class="sxs-lookup"><span data-stu-id="cbe2b-227">(name of source) or `All`</span></span> | <span data-ttu-id="cbe2b-228">Pokud je klíč názvem zdroje, hodnota je zdrojová cesta nebo adresa URL.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="cbe2b-229">Pokud `All` by měla být hodnota `(Aggregate source)` pro kombinování všech zdrojů balíčků, které nejsou jinak zakázané.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="cbe2b-230">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="cbe2b-231">oddíl trustedSigners</span><span class="sxs-lookup"><span data-stu-id="cbe2b-231">trustedSigners section</span></span>

<span data-ttu-id="cbe2b-232">Ukládá důvěryhodné podepisující osoby používané k povolení balíčku při instalaci nebo obnovení.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="cbe2b-233">Tento seznam nemůže být prázdný, pokud je uživatel nastaven `signatureValidationMode` na `require` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="cbe2b-234">Tuto část lze aktualizovat pomocí [ `nuget trusted-signers` příkazu](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="cbe2b-235">**Schéma:**</span><span class="sxs-lookup"><span data-stu-id="cbe2b-235">**Schema**:</span></span>

<span data-ttu-id="cbe2b-236">Důvěryhodný podpis má kolekci `certificate` položek, které zařadí všechny certifikáty identifikující daného podepisujícího.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="cbe2b-237">Důvěryhodný podpis může být buď `Author` nebo `Repository` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="cbe2b-238">Důvěryhodné *úložiště* také určuje `serviceIndex` úložiště (které musí být platný `https` identifikátor URI) a může volitelně zadat středníkem oddělený seznam, `owners` který omezí ještě více uživatelů, kteří jsou z daného konkrétního úložiště považováni za důvěryhodné.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="cbe2b-239">Podporované algoritmy hash používané pro otisk certifikátu jsou `SHA256` `SHA384` a `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="cbe2b-240">Pokud `certificate` `allowUntrustedRoot` `true` je jako daný certifikát povoleno řetězení k nedůvěryhodnému kořenovému adresáři při sestavování řetězu certifikátů v rámci ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="cbe2b-241">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-241">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="cbe2b-242">oddíl fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="cbe2b-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="cbe2b-243">*(3.5 +)* Poskytuje způsob, jak předinstalovat balíčky, aby nedošlo k tomu, že by se v případě nalezení balíčku v záložních složkách prováděla žádná práce.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="cbe2b-244">Záložní složky balíčku mají stejnou složku a strukturu souborů jako globální složka balíčku: *. nupkg* je k dispozici a jsou extrahovány všechny soubory.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="cbe2b-245">Logika vyhledávání pro tuto konfiguraci je:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="cbe2b-246">Pokud chcete zjistit, jestli je balíček/verze už stažený, vyhledejte globální složku balíčku.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="cbe2b-247">Vyhledejte shodu balíčku/verze v záložních složkách.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="cbe2b-248">Pokud je vyhledávání úspěšné, není nutné stahovat žádné soubory.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="cbe2b-249">Pokud se shoda nenajde, vyhledá NuGet zdroje souborů, potom zdroje http a pak stáhne balíčky.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="cbe2b-250">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-250">Key</span></span> | <span data-ttu-id="cbe2b-251">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-252">(název záložní složky)</span><span class="sxs-lookup"><span data-stu-id="cbe2b-252">(name of fallback folder)</span></span> | <span data-ttu-id="cbe2b-253">Cesta k záložní složce</span><span class="sxs-lookup"><span data-stu-id="cbe2b-253">Path to fallback folder.</span></span> |

<span data-ttu-id="cbe2b-254">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="cbe2b-255">oddíl packageManagement</span><span class="sxs-lookup"><span data-stu-id="cbe2b-255">packageManagement section</span></span>

<span data-ttu-id="cbe2b-256">Nastaví výchozí formát správy balíčků, buď *packages.config* , nebo PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="cbe2b-257">Projekty ve stylu sady SDK vždycky používají PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="cbe2b-258">Klíč</span><span class="sxs-lookup"><span data-stu-id="cbe2b-258">Key</span></span> | <span data-ttu-id="cbe2b-259">Hodnota</span><span class="sxs-lookup"><span data-stu-id="cbe2b-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="cbe2b-260">formát</span><span class="sxs-lookup"><span data-stu-id="cbe2b-260">format</span></span> | <span data-ttu-id="cbe2b-261">Logická hodnota označující výchozí formát správy balíčků.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="cbe2b-262">Pokud `1` je formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="cbe2b-263">Pokud `0` je formát *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="cbe2b-264">zakázaný</span><span class="sxs-lookup"><span data-stu-id="cbe2b-264">disabled</span></span> | <span data-ttu-id="cbe2b-265">Logická hodnota označující, zda se při první instalaci balíčku má zobrazit výzva k výběru výchozího formátu balíčku.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="cbe2b-266">`False` skryje výzvu.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="cbe2b-267">**Příklad**:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="cbe2b-268">Použití proměnných prostředí</span><span class="sxs-lookup"><span data-stu-id="cbe2b-268">Using environment variables</span></span>

<span data-ttu-id="cbe2b-269">Pokud `nuget.config` chcete použít nastavení v době běhu, můžete použít proměnné prostředí v hodnotách (NuGet 3.4 +).</span><span class="sxs-lookup"><span data-stu-id="cbe2b-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="cbe2b-270">Například pokud `HOME` je proměnná prostředí ve Windows nastavená na `c:\users\username` , pak hodnota `%HOME%\NuGetRepository` v konfiguračním souboru se přeloží na `c:\users\username\NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="cbe2b-271">Všimněte si, že je nutné použít proměnné prostředí ve stylu systému Windows (začíná a končí v%) i v systému Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="cbe2b-272">`$HOME/NuGetRepository`V konfiguračním souboru se nebude překládat.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="cbe2b-273">V systému Mac/Linux hodnota `%HOME%/NuGetRepository` se bude překládat na `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="cbe2b-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="cbe2b-274">Pokud se proměnná prostředí nenajde, NuGet použije hodnotu literálu z konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="cbe2b-275">Například `%MY_UNDEFINED_VAR%/NuGetRepository` bude vyřešen jako `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="cbe2b-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="cbe2b-276">Následující tabulka zobrazuje syntaxi proměnných lnstalování a podporu oddělovače cest pro NuGet.Config soubory.</span><span class="sxs-lookup"><span data-stu-id="cbe2b-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="cbe2b-277">Podpora proměnné prostředí NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="cbe2b-277">NuGet.Config environment variable support</span></span>

| <span data-ttu-id="cbe2b-278">Syntax</span><span class="sxs-lookup"><span data-stu-id="cbe2b-278">Syntax</span></span> | <span data-ttu-id="cbe2b-279">Oddělovač adresářů</span><span class="sxs-lookup"><span data-stu-id="cbe2b-279">Dir separator</span></span> | <span data-ttu-id="cbe2b-280">nuget.exe Windows</span><span class="sxs-lookup"><span data-stu-id="cbe2b-280">Windows nuget.exe</span></span> | <span data-ttu-id="cbe2b-281">dotnet.exe Windows</span><span class="sxs-lookup"><span data-stu-id="cbe2b-281">Windows dotnet.exe</span></span> | <span data-ttu-id="cbe2b-282">nuget.exe Mac (v mono)</span><span class="sxs-lookup"><span data-stu-id="cbe2b-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="cbe2b-283">dotnet.exe Mac</span><span class="sxs-lookup"><span data-stu-id="cbe2b-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="cbe2b-284">Yes</span><span class="sxs-lookup"><span data-stu-id="cbe2b-284">Yes</span></span> | <span data-ttu-id="cbe2b-285">Yes</span><span class="sxs-lookup"><span data-stu-id="cbe2b-285">Yes</span></span> | <span data-ttu-id="cbe2b-286">Yes</span><span class="sxs-lookup"><span data-stu-id="cbe2b-286">Yes</span></span> | <span data-ttu-id="cbe2b-287">Yes</span><span class="sxs-lookup"><span data-stu-id="cbe2b-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="cbe2b-288">Yes</span><span class="sxs-lookup"><span data-stu-id="cbe2b-288">Yes</span></span> | <span data-ttu-id="cbe2b-289">Yes</span><span class="sxs-lookup"><span data-stu-id="cbe2b-289">Yes</span></span> | <span data-ttu-id="cbe2b-290">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-290">No</span></span> | <span data-ttu-id="cbe2b-291">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="cbe2b-292">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-292">No</span></span> | <span data-ttu-id="cbe2b-293">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-293">No</span></span> | <span data-ttu-id="cbe2b-294">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-294">No</span></span> | <span data-ttu-id="cbe2b-295">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="cbe2b-296">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-296">No</span></span> | <span data-ttu-id="cbe2b-297">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-297">No</span></span> | <span data-ttu-id="cbe2b-298">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-298">No</span></span> | <span data-ttu-id="cbe2b-299">No</span><span class="sxs-lookup"><span data-stu-id="cbe2b-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="cbe2b-300">Ukázkový konfigurační soubor</span><span class="sxs-lookup"><span data-stu-id="cbe2b-300">Example config file</span></span>

<span data-ttu-id="cbe2b-301">Níže je příklad `nuget.config` souboru, který ilustruje několik nastavení včetně volitelných parametrů:</span><span class="sxs-lookup"><span data-stu-id="cbe2b-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
