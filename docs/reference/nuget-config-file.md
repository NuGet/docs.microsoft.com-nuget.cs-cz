---
title: Odkaz na soubor nuget.config
description: Odkaz na soubor NuGet.Config včetně konfigurace, bindingRedirects, packageRestore, řešení a packageSource oddíly.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 504a48224051265164f9ab183e63fa5e7f5867e6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546912"
---
# <a name="nugetconfig-reference"></a>odkaz na soubor nuget.config

Chování Nugetu je řízena nastavením v různých `NuGet.Config` soubory, jak je popsáno v [konfigurace chování Nugetu](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` je soubor XML obsahující na nejvyšší úrovni `<configuration>` uzlu, který pak obsahuje část prvky popsané v tomto tématu. Každý oddíl obsahuje nula nebo více `<add>` prvky s `key` a `value` atributy. Zobrazit [příklady konfiguračního souboru](#example-config-file). Názvy nastavení rozlišují velikost písmen a můžete použít hodnoty [proměnné prostředí](#using-environment-variables).

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
- [Použití proměnných prostředí](#using-environment-variables)
- [Příklad konfiguračního souboru](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>konfigurační oddíl

Obsahuje nastavení různé konfigurace, které lze nastavit pomocí [ `nuget config` příkaz](../tools/cli-ref-config.md).

`dependencyVersion` a `repositoryPath` platí pouze pro projekty pomocí `packages.config`. `globalPackagesFolder` platí pouze pro projekty ve formátu PackageReference.

| Key | Hodnota |
| --- | --- |
| dependencyVersion (`packages.config` jenom) | Výchozí hodnota `DependencyVersion` hodnotu pro instalaci balíčku, obnovení a aktualizace, když `-DependencyVersion` přepínač není zadán přímo. Tato hodnota se používá také pomocí uživatelského rozhraní Správce balíčků NuGet. Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (projekty pouze pomocí PackageReference) | Umístění složky globálních balíčků výchozí. Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux). Relativní cesta lze použít v projektu konkrétní `nuget.config` soubory. Toto nastavení je přepsán NUGET_PACKAGES proměnné prostředí, která má přednost. |
| repositoryPath (`packages.config` jenom) | Umístění, ve kterém k instalaci balíčků NuGet místo výchozího `$(Solutiondir)/packages` složky. Relativní cesta lze použít v projektu konkrétní `nuget.config` soubory. Toto nastavení je přepsán NUGET_PACKAGES proměnné prostředí, která má přednost. |
| defaultPushSource | Určuje adresu URL nebo cestu zdroje balíčku, který se použije jako výchozí, pokud se nenajdou žádné jiné zdroje balíčků pro operaci. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Nastavení proxy serveru mají používat při připojování ke zdrojům balíčků; `http_proxy` by měl být ve formátu `http://<username>:<password>@<domain>`. Hesla jsou zašifrované a nelze ji přidat ručně. Pro `no_proxy`, hodnota je čárkou oddělený seznam domén obejít proxy server. Můžete také použít proměnné prostředí http_proxy a no_proxy pro tyto hodnoty. Další podrobnosti najdete v tématu [nastavení proxy serveru NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |

**Příklad**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
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

| Key | Hodnota |
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

| Key | Hodnota |
| --- | --- |
| disableSourceControlIntegration | Logická hodnota označující, jestli se má ignorovat složku packages při práci se správou zdrojového kódu. Výchozí hodnota je False. |

**Příklad**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Části zdroje balíčku

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, A `disabledPackageSources` veškerou práci dohromady a nakonfigurujte, jak NuGet pracuje s úložišť balíčků během instalace, obnovení a operace aktualizace.

[ `nuget sources` Příkaz](../tools/cli-ref-sources.md) se obecně používají tato nastavení můžete spravovat, s výjimkou `apikeys` spravovaném pomocí [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).

Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Uvádí všechny zdroje balíčků známé. Pořadí je ignorována během operace obnovení a s žádným projektem formátu PackageReference. Pořadí zdrojů pro instalace respektuje NuGet a aktualizovat operace s projekty pomocí `packages.config`.

| Key | Hodnota |
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

| Key | Hodnota |
| --- | --- |
| uživatelské jméno | Uživatelské jméno pro zdroj ve formátu prostého textu. |
| Heslo | Šifrované heslo pro zdroj. |
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

| Key | Hodnota |
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

| Key | Hodnota |
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
</configuration>
```
