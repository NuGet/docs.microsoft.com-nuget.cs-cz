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
# <a name="nugetconfig-reference"></a>odkaz na soubor nuget.config

Chování Nugetu je řízena nastavením v různých `NuGet.Config` soubory, jak je popsáno v [konfigurace chování Nugetu](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` je soubor XML obsahující na nejvyšší úrovni `<configuration>` uzlu, který pak obsahuje část prvky popsané v tomto tématu. Každý oddíl obsahuje nula nebo více položek. Zobrazit [příklady konfiguračního souboru](#example-config-file). Názvy nastavení rozlišují velikost písmen a můžete použít hodnoty [proměnné prostředí](#using-environment-variables).

V tomto tématu:

- [konfigurační oddíl](#config-section)
- [část bindingRedirects](#bindingredirects-section)
- [část packageRestore](#packagerestore-section)
- [oddíl řešení](#solution-section)
- [Balíček zdrojové oddíly](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [část trustedSigners](#trustedsigners-section)
- [Použití proměnných prostředí](#using-environment-variables)
- [Příklad konfiguračního souboru](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>konfigurační oddíl

Obsahuje nastavení různé konfigurace, které lze nastavit pomocí [ `nuget config` příkaz](../tools/cli-ref-config.md).

`dependencyVersion` a `repositoryPath` platí pouze pro projekty pomocí `packages.config`. `globalPackagesFolder` platí pouze pro projekty ve formátu PackageReference.

| Key | Value |
| --- | --- |
| dependencyVersion (`packages.config` jenom) | Výchozí hodnota `DependencyVersion` hodnotu pro instalaci balíčku, obnovení a aktualizace, když `-DependencyVersion` přepínač není zadán přímo. Tato hodnota se používá také pomocí uživatelského rozhraní Správce balíčků NuGet. Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (projekty pouze pomocí PackageReference) | Umístění složky globálních balíčků výchozí. Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux). Relativní cesta lze použít v projektu konkrétní `nuget.config` soubory. Toto nastavení je přepsán NUGET_PACKAGES proměnné prostředí, která má přednost. |
| repositoryPath (`packages.config` jenom) | Umístění, ve kterém k instalaci balíčků NuGet místo výchozího `$(Solutiondir)/packages` složky. Relativní cesta lze použít v projektu konkrétní `nuget.config` soubory. Toto nastavení je přepsán NUGET_PACKAGES proměnné prostředí, která má přednost. |
| defaultPushSource | Určuje adresu URL nebo cestu zdroje balíčku, který se použije jako výchozí, pokud se nenajdou žádné jiné zdroje balíčků pro operaci. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Nastavení proxy serveru mají používat při připojování ke zdrojům balíčků; `http_proxy` by měl být ve formátu `http://<username>:<password>@<domain>`. Hesla jsou zašifrované a nelze ji přidat ručně. Pro `no_proxy`, hodnota je čárkou oddělený seznam domén obejít proxy server. Můžete také použít proměnné prostředí http_proxy a no_proxy pro tyto hodnoty. Další podrobnosti najdete v tématu [nastavení proxy serveru NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Určuje režim ověřování pro ověřování podpisů balíčků pro instalaci balíčků a obnovení. Hodnoty jsou `accept`, `require`. Výchozí hodnota je `accept`.

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

## <a name="bindingredirects-section"></a>část bindingRedirects

Konfiguruje, zda NuGet nepodporuje automatické přesměrování vazby při instalaci balíčku.

| Key | Hodnota |
| --- | --- |
| Přeskočit | Logická hodnota označující, zda se mají přeskočit automatické přesměrování vazby. Výchozí hodnota je false. |

**Příklad**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>část packageRestore

Ovládací prvky obnovení balíčků během sestavení.

| Key | Value |
| --- | --- |
| Povoleno | Logická hodnota označující, zda NuGet můžete provést automatické obnovení. Můžete také nastavit `EnableNuGetPackageRestore` proměnnou prostředí s hodnotou `True` namísto nastavení tohoto klíče v konfiguračním souboru. |
| automatická | Logická hodnota označující, zda NuGet by měla kontrolovat chybějící balíčky během sestavení. |

**Příklad**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>oddíl řešení

Ovládací prvky, zda `packages` složka řešení je součástí správy zdrojového kódu. Tato část funguje pouze v `nuget.config` soubory ve složce řešení.

| Key | Value |
| --- | --- |
| disableSourceControlIntegration | Logická hodnota označující, jestli se má ignorovat složku packages při práci se správou zdrojového kódu. Výchozí hodnota je False. |

**Příklad**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Části zdroje balíčku

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` a `trustedSigners` veškerou práci dohromady a nakonfigurujte, jak NuGet pracuje s úložišť balíčků během instalace, obnovení a operace aktualizace.

[ `nuget sources` Příkaz](../tools/cli-ref-sources.md) se obecně používají tato nastavení můžete spravovat, s výjimkou `apikeys` spravovaném pomocí [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md), a `trustedSigners` spravovaném použití [ `nuget trusted-signers` příkaz](../tools/cli-ref-trusted-signers.md).

Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Uvádí všechny zdroje balíčků známé. Pořadí je ignorována během operace obnovení a s žádným projektem formátu PackageReference. Pořadí zdrojů pro instalace respektuje NuGet a aktualizovat operace s projekty pomocí `packages.config`.

| Key | Value |
| --- | --- |
| (název přiřazení ke zdroji balíčku) | Cesta nebo adresa URL zdroje balíčku. |

**Příklad**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Ukládá uživatelská jména a hesla pro zdroje, obvykle se zadává `-username` a `-password` přepínače s `nuget sources`. Hesla jsou ve výchozím nastavení zašifrované, pokud `-storepasswordincleartext` možnost je také použít.

| Key | Value |
| --- | --- |
| uživatelské jméno | Uživatelské jméno pro zdroj ve formátu prostého textu. |
| heslo | Šifrované heslo pro zdroj. |
| cleartextpassword | Nezašifrované heslo pro zdroj. |

**Příklad:**

V konfiguračním souboru `<packageSourceCredentials>` prvek obsahuje podřízené uzly pro každý název příslušným zdrojovým (s nahrazením mezer v názvu `_x0020_`). To znamená, že u zdrojů s názvem "Contoso" a "Zdroj testu" konfigurační soubor obsahuje následující při použití šifrovaná hesla:

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

Při použití nešifrovaná hesla:

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

Ukládá klíče pro zdroje, které používají ověřování pomocí klíče rozhraní API, jak se [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).

| Key | Value |
| --- | --- |
| (adresa URL zdroje) | Šifrovaný klíč rozhraní API. |

**Příklad**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Zjištěné zdroje aktuálně zakázáno. Může být prázdný.

| Key | Value |
| --- | --- |
| (název zdroje) | Logická hodnota označující, zda zdroj je zakázáno. |

**Příklad:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(pouze 2.x; zastaralé v 3.x+)*

Identifikuje zdroj aktuálně aktivní nebo označuje souhrn všech zdrojů.

| Key | Hodnota |
| --- | --- |
| (název zdroje) nebo `All` | Pokud klíč je název zdroje, hodnota je zdrojová cesta nebo adresa URL. Pokud `All`, hodnotou by měla být `(Aggregate source)` kombinovat všechny zdroje balíčků, které jinak nejsou zakázané. |

**Příklad**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a>část trustedSigners

Úložiště důvěryhodných podepisující osoby, které umožňují balíček při instalaci nebo obnovování. Tento seznam nemůže být prázdný, pokud uživatel nastaví `signatureValidationMode` k `require`. 

Tato část je možné aktualizovat pomocí [ `nuget trusted-signers` příkaz](../tools/cli-ref-trusted-signers.md).

**Schéma**:

Důvěryhodné podepisující osoba má kolekci `certificate` položky, které zařadit všechny certifikáty, které identifikují dané podepisující osoba. Důvěryhodné podepisující osoba může být buď `Author` nebo `Repository`.

Důvěryhodný *úložiště* také určuje `serviceIndex` úložiště (který musí být platný `https` identifikátor uri) a volitelně můžete zadat středníkem oddělený seznam `owners` omezit ještě více který je důvěryhodný z tohoto konkrétního úložiště.

Jsou podporované hashovací algoritmy používané pro otisku certifikátu `SHA256`, `SHA384` a `SHA512`.

Pokud `certificate` Určuje `allowUntrustedRoot` jako `true` daný certifikát řetězce na nedůvěryhodném kořenu může při sestavování řetězu certifikátů jako součást ověření podpisu.

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

## <a name="using-environment-variables"></a>Použití proměnných prostředí

Můžete použít proměnné prostředí v `nuget.config` hodnoty (NuGet 3.4 +) k aplikování nastavení běhu.

Například pokud `HOME` proměnné prostředí na Windows nastavená na `c:\users\username`, pak hodnota `%HOME%\NuGetRepository` v konfiguraci souboru přeloží na `c:\users\username\NuGetRepository`.

Podobně pokud `HOME` na Mac/Linux je nastavena na `/home/myStuff`, pak `%HOME%/NuGetRepository` v konfiguraci souboru přeloží na `/home/myStuff/NuGetRepository`.

Pokud není nalezena proměnné prostředí, používá NuGet hodnota literálu z konfiguračního souboru.

## <a name="example-config-file"></a>Příklad konfiguračního souboru

Tady je příklad `nuget.config` soubor, který ukazuje několik položek nastavení:

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
