---
title: Odkaz na soubor NuGet. config
description: Odkaz na soubor NuGet. config včetně oddílů config, bindingRedirects, packageRestore, Solution a packageSource
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: a2955617b899bfadab42d1ae98dd20c8fc6ddca9
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020054"
---
# <a name="nugetconfig-reference"></a>Referenční dokumentace NuGet. config

Chování NuGet se řídí nastavením v různých `NuGet.Config` souborech, jak je popsáno v tématu [běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config`je soubor XML obsahující uzel nejvyšší úrovně `<configuration>` , který pak obsahuje prvky oddílu popsané v tomto tématu. Každý oddíl obsahuje nula nebo více položek. Podívejte se na [příklady konfiguračního souboru](#example-config-file). U názvů nastavení se nerozlišují malá a velká písmena a hodnoty můžou používat [proměnné prostředí](#using-environment-variables).

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>konfigurační oddíl

Obsahuje různá nastavení konfigurace, která lze nastavit pomocí [ `nuget config` příkazu](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion`a `repositoryPath` platí pouze pro projekty pomocí `packages.config`. `globalPackagesFolder`platí jenom pro projekty, které používají formát PackageReference.

| Key | Value |
| --- | --- |
| dependencyVersion (`packages.config` pouze) | Výchozí `DependencyVersion` hodnota pro instalaci balíčku, obnovení a aktualizaci, `-DependencyVersion` když přepínač není zadán přímo Tuto hodnotu používá také uživatelské rozhraní Správce balíčků NuGet. Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor`, .`Highest` |
| globalPackagesFolder (projekty používající pouze PackageReference) | Umístění výchozí složky globálních balíčků. Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux). Relativní cestu lze použít v souborech specifických `nuget.config` pro projekt. Toto nastavení je přepsáno proměnnou prostředí NUGET_PACKAGES, která má přednost. |
| repositoryPath (`packages.config` pouze) | Místo, kde se mají instalovat balíčky NuGet místo výchozí `$(Solutiondir)/packages` složky Relativní cestu lze použít v souborech specifických `nuget.config` pro projekt. Toto nastavení je přepsáno proměnnou prostředí NUGET_PACKAGES, která má přednost. |
| defaultPushSource | Určuje adresu URL nebo cestu ke zdroji balíčku, který má být použit jako výchozí, pokud pro operaci nebyly nalezeny žádné jiné zdroje balíčků. |
| http_proxy http_proxy. User http_proxy. Password NO_PROXY | Nastavení proxy serveru, které se má použít při připojování ke zdrojům balíčků; by měl být ve formátu `http://<username>:<password>@<domain>`. `http_proxy` Hesla jsou šifrovaná a nelze je přidat ručně. `no_proxy`V případě je tato hodnota čárkami oddělený seznam domén, které proxy server obejít. Pro tyto hodnoty můžete alternativně použít proměnné prostředí http_proxy a NO_PROXY. Další podrobnosti najdete v tématu [nastavení proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Určuje režim ověřování, který se používá k ověření signatur balíčků pro instalaci balíčku a obnovení. Hodnoty jsou `accept`, `require`. Výchozí hodnota je `accept`.

**Příklad**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>oddíl bindingRedirects

Nakonfiguruje, jestli NuGet při instalaci balíčku automaticky přesměrovává vazby.

| Key | Value |
| --- | --- |
| Přeskočit | Logická hodnota označující, zda se má přeskočit automatický přesměrování vazby Výchozí hodnota je false. |

**Příklad**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>oddíl packageRestore

Řídí obnovení balíčku během sestavení.

| Key | Value |
| --- | --- |
| enabled | Logická hodnota označující, zda může NuGet provádět automatické obnovení. Můžete také nastavit `EnableNuGetPackageRestore` proměnnou prostředí s `True` hodnotou místo nastavení tohoto klíče v konfiguračním souboru. |
| automatická | Logická hodnota označující, zda má NuGet při sestavení kontrolovat chybějící balíčky. |

**Příklad**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>oddíl řešení

Určuje, zda `packages` je složka řešení obsažena ve správě zdrojového kódu. Tato část funguje pouze v `nuget.config` souborech ve složce řešení.

| Key | Value |
| --- | --- |
| disableSourceControlIntegration | Logická hodnota označující, zda se má při práci se správou zdrojových kódů ignorovat složku balíčků. Výchozí hodnota je False. |

**Příklad**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Zdrojové oddíly balíčku

Všechnypracují`packageSourceCredentials`společně `packageSources` ,`apikeys` abynakonfigurovali,jakNuGetfungujesúložištěmibalíčkuběhemoperacíinstalace,obnoveníaaktualizace`activePackageSource`. `disabledPackageSources` `trustedSigners`

[ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `apikeys` `trustedSigners` [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md) [ Příkaz`nuget sources` ](../reference/cli-reference/cli-ref-sources.md) se obecně používá ke správě těchto nastavení, s výjimkou toho, že je spravován pomocí příkazu a který je spravován pomocí příkazu.

Všimněte si, že zdrojová adresa URL pro `https://api.nuget.org/v3/index.json`NuGet.org je.

### <a name="packagesources"></a>packageSources

Zobrazí seznam všech známých zdrojů balíčků. Pořadí se ignoruje během operací obnovení a s jakýmkoli projektem pomocí formátu PackageReference. NuGet respektuje pořadí zdrojů pro operace instalace a aktualizace s projekty pomocí `packages.config`.

| Key | Value |
| --- | --- |
| (název, který se má přiřadit ke zdroji balíčku) | Cesta nebo adresa URL zdroje balíčku. |

**Příklad**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Ukládá uživatelská jména a hesla pro zdroje, obvykle zadané s `-username` přepínači a `-password` s `nuget sources`. Hesla jsou zašifrována ve výchozím `-storepasswordincleartext` nastavení, pokud není použita ani tato možnost.

| Key | Value |
| --- | --- |
| username | Uživatelské jméno pro zdroj v prostém textu. |
| password | Šifrované heslo pro zdroj |
| cleartextpassword | Nešifrované heslo zdroje |

**Příklad:**

V konfiguračním souboru `<packageSourceCredentials>` element obsahuje podřízené uzly pro každý platný název zdroje (mezery v názvu jsou nahrazeny řetězcem `_x0020_`). To znamená, že pro zdroje s názvem "contoso" a "zdroj testu" obsahuje konfigurační soubor při použití šifrovaných hesel následující:

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

Při použití nezašifrovaných hesel:

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

### <a name="apikeys"></a>apikeys

Ukládá klíče pro zdroje, které používají ověřování pomocí klíče rozhraní API, jak [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)je nastaveno pomocí příkazu.

| Key | Value |
| --- | --- |
| (zdrojová adresa URL) | Šifrovaný klíč rozhraní API. |

**Příklad**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Identifikovány aktuálně zakázané zdroje. Může být prázdné.

| Key | Value |
| --- | --- |
| (název zdroje) | Logická hodnota označující, zda je zdroj zakázán. |

**Příklad:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(pouze 2. x; zastaralé v 3. x +)*

Identifikuje aktuálně aktivní zdroj nebo označuje agregaci všech zdrojů.

| Key | Value |
| --- | --- |
| (název zdroje) nebo`All` | Pokud je klíč názvem zdroje, hodnota je zdrojová cesta nebo adresa URL. Pokud `All`by měla být `(Aggregate source)` hodnota pro kombinování všech zdrojů balíčků, které nejsou jinak zakázané. |

**Příklad**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a>oddíl trustedSigners

Ukládá důvěryhodné podepisující osoby používané k povolení balíčku při instalaci nebo obnovení. Tento seznam nemůže být prázdný, pokud je uživatel `signatureValidationMode` nastaven `require`na. 

Tuto část lze aktualizovat pomocí [ `nuget trusted-signers` příkazu](../reference/cli-reference/cli-ref-trusted-signers.md).

**Schéma**:

Důvěryhodný podpis má kolekci `certificate` položek, které zařadí všechny certifikáty identifikující daného podepisujícího. Důvěryhodný podpis může být buď `Author` `Repository`nebo.

Důvěryhodné *úložiště* také určuje `serviceIndex` úložiště (které musí být platným `https` identifikátorem URI) a může volitelně zadat středníkem oddělený seznam, který omezí ještě více uživatelů `owners` , kteří jsou z tohoto konkrétního typu považováni za důvěryhodné. úložištì.

Podporované algoritmy hash používané pro otisk certifikátu jsou `SHA256` `SHA384` a `SHA512`.

Pokud je jako`true`daný certifikát povoleno řetězení k nedůvěryhodnému kořenovému adresáři při sestavování řetězu certifikátů v rámci ověření podpisu. `allowUntrustedRoot` `certificate`

**Příklad**:

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

## <a name="fallbackpackagefolders-section"></a>oddíl fallbackPackageFolders

*(3.5 +)* Poskytuje způsob, jak předinstalovat balíčky, aby nedošlo k tomu, že by se v případě nalezení balíčku v záložních složkách prováděla žádná práce. Záložní složky balíčku mají stejnou složku a strukturu souborů jako globální složka balíčku: *. nupkg* je k dispozici a jsou extrahovány všechny soubory.

Logika vyhledávání pro tuto konfiguraci je:

- Pokud chcete zjistit, jestli je balíček/verze už stažený, vyhledejte globální složku balíčku.

- Vyhledejte shodu balíčku/verze v záložních složkách.

Pokud je vyhledávání úspěšné, není nutné stahovat žádné soubory.

Pokud se shoda nenajde, vyhledá NuGet zdroje souborů, potom zdroje http a pak stáhne balíčky.

| Key | Value |
| --- | --- |
| (název záložní složky) | Cesta k záložní složce |

**Příklad**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>oddíl packageManagement

Nastaví výchozí formát správy balíčků, buď *Packages. config* , nebo PackageReference. Projekty ve stylu sady SDK vždycky používají PackageReference.

| Key | Value |
| --- | --- |
| formát | Logická hodnota označující výchozí formát správy balíčků. Pokud `1`je formát PackageReference. Pokud `0`má formát hodnotu *Packages. config*. |
| zakázaný | Logická hodnota označující, zda se při první instalaci balíčku má zobrazit výzva k výběru výchozího formátu balíčku. `False`skryje výzvu. |

**Příklad**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Použití proměnných prostředí

Pokud chcete použít nastavení v době `nuget.config` běhu, můžete použít proměnné prostředí v hodnotách (NuGet 3.4 +).

Například pokud `HOME` je proměnná prostředí ve Windows nastavená na `c:\users\username` `%HOME%\NuGetRepository` , pak hodnota v konfiguračním souboru se přeloží na `c:\users\username\NuGetRepository`.

Podobně, pokud `HOME` je on Mac/Linux nastavený na `/home/myStuff`, `%HOME%/NuGetRepository` se v konfiguračním souboru přeloží na `/home/myStuff/NuGetRepository`.

Pokud se proměnná prostředí nenajde, NuGet použije hodnotu literálu z konfiguračního souboru.

## <a name="example-config-file"></a>Ukázkový konfigurační soubor

Níže je příklad `nuget.config` souboru, který ilustruje několik nastavení:

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
