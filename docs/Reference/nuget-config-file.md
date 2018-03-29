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
# <a name="nugetconfig-reference"></a>Odkaz na soubor nuget.config.

Chování NuGet je řízena nastavením v různých `NuGet.Config` souborů, jak je popsáno v [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md).

`NuGet.Config` je soubor XML obsahující nejvyšší úrovni `<configuration>` uzlu, který pak obsahuje část prvky popsané v tomto tématu. Každý oddíl obsahuje nula nebo více `<add>` prvky s `key` a `value` atributy. Najdete v článku [příklady konfiguračního souboru](#example-config-file). Následující názvy nastavení jsou velká a malá písmena a můžete použít hodnoty [proměnné prostředí](#using-environment-variables).

V tomto tématu:

- [konfigurační oddíl](#config-section)
- [část bindingRedirects](#bindingredirects-section)
- [část packageRestore](#packagerestore-section)
- [část řešení](#solution-section)
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

Obsahuje nastavení různé konfigurace, které se dá nastavit pomocí [ `nuget config` příkaz](../tools/cli-ref-config.md).

`dependencyVersion` a `repositoryPath` se vztahují pouze na projektů pomocí `packages.config`. `globalPackagesFolder` platí pouze pro projekty PackageReference formátu.

| Key | Hodnota |
| --- | --- |
| dependencyVersion (`packages.config` pouze) | Výchozí `DependencyVersion` hodnotu pro instalaci balíčku, obnovení a aktualizace, když `-DependencyVersion` přepínač není zadán přímo. Tato hodnota se používá také pomocí uživatelského rozhraní Správce balíčků NuGet. Hodnoty jsou `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (pouze pomocí PackageReference projekty) | Umístění složky výchozí globální balíčky. Výchozí hodnota je `%userprofile%\.nuget\packages` (Windows) nebo `~/.nuget/packages` (Mac/Linux). Relativní cesta mohou být používány specifické pro projekt `Nuget.Config` soubory. Toto nastavení je přepsat proměnnou prostředí NUGET_PACKAGES, která má přednost před. |
| repositoryPath (`packages.config` pouze) | Umístění, v němž instalace balíčků NuGet místo výchozího `$(Solutiondir)/packages` složky. Relativní cesta mohou být používány specifické pro projekt `Nuget.Config` soubory. Toto nastavení je přepsat proměnnou prostředí NUGET_PACKAGES, která má přednost před. |
| defaultPushSource | Určuje adresu URL nebo cestu zdroje balíčku, který se má použít jako výchozí pro operace nebyly nalezeny žádné jiné zdroje balíčku. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Nastavení proxy serveru používat při připojování ke zdroji balíčků; `http_proxy` by měl být ve formátu `http://<username>:<password>@<domain>`. Hesla se šifrují a nelze ji přidat ručně. Pro `no_proxy`, hodnota je čárkami oddělený seznam domén Nepoužívat proxy server. Případně můžete http_proxy a no_proxy proměnných prostředí pro tyto hodnoty. Další podrobnosti najdete v tématu [nastavení proxy serveru NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |

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

Nakonfiguruje, jestli NuGet nemá přesměrování vazby automatické při instalaci balíčku.

| Key | Hodnota |
| --- | --- |
| Přeskočit | Logická hodnota, která určuje, jestli chcete vynechat přesměrování vazby automatické. Výchozí hodnota je false. |

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
| povoleno | Logická hodnota, která určuje, zda NuGet můžete provádět automatického obnovení. Můžete také nastavit `EnableNuGetPackageRestore` proměnnou prostředí s hodnotou `True` místo nastavení tohoto klíče v konfiguračním souboru. |
| automatická | Logická hodnota, která určuje, zda NuGet měli kontrolovat chybějící balíčky během sestavení. |

**Příklad**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>část řešení

Ovládací prvky jestli `packages` složku řešení je součástí zdrojového kódu. Tato část funguje pouze v `Nuget.Config` souborů ve složce řešení.

| Key | Hodnota |
| --- | --- |
| disableSourceControlIntegration | Logická hodnota, která určuje, zda ignorovat složce balíčků při práci se službou správy zdrojového kódu. Výchozí hodnota je False. |

**Příklad**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Části zdroje balíčku

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, A `disabledPackageSources` všechny pracovní dohromady a nakonfigurujte, jak funguje NuGet s úložiště balíčku během instalace, obnovení a operace aktualizace.

[ `nuget sources` Příkaz](../tools/cli-ref-sources.md) se obvykle používá ke správě těchto nastavení, s výjimkou `apikeys` kterou spravují pomocí [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).

Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Zobrazí seznam všech zdrojů známé balíčku. Pořadí je ignorován během operace obnovení a s žádným projektem v PackageReference formátu. Pořadí zdrojů pro instalace respektuje NuGet a aktualizovat operace s projekty pomocí `packages.config`.

| Key | Hodnota |
| --- | --- |
| (název přiřadit do zdroje balíčku) | Cesta nebo adresa URL zdroje balíčku. |

**Příklad**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Ukládá uživatelská jména a hesla pro zdroje, obvykle zadaným `-username` a `-password` přepne s `nuget sources`. Hesla jsou ve výchozím nastavení zašifrované, pokud `-storepasswordincleartext` je také možnost použít.

| Key | Hodnota |
| --- | --- |
| Uživatelské jméno | Uživatelské jméno pro tento zdroj ve formátu prostého textu. |
| Heslo | Zašifrované heslo pro zdroj. |
| cleartextpassword | Nezašifrované heslo pro zdroj. |

**Příklad:**

V konfiguračním souboru `<packageSourceCredentials>` element obsahuje podřízené uzly pro každý název příslušným zdrojovým (s nahrazením mezer v názvu `_x0020_`). To znamená zdrojů s názvem "Contoso" a "Test zdroj", konfigurační soubor obsahuje následující při použití šifrovaných hesel:

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

Ukládá klíče pro zdroje, které používají rozhraní API klíče ověřování, jako sada [ `nuget setapikey` příkaz](../tools/cli-ref-setapikey.md).

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

Identifikovat aktuálně zakázané zdroje. Může být prázdná.

| Key | Hodnota |
| --- | --- |
| (název zdroje) | Logická hodnota určující, zda je neaktivní zdroj. |

**Příklad:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(jenom 2.x; nepoužívané v 3.x+)*

Identifikuje ke zdroji aktuálně aktivní, nebo označuje agregace všech zdrojů.

| Key | Hodnota |
| --- | --- |
| (název zdroje) nebo `All` | Pokud klíč je název zdroje, hodnota je zdrojová cesta nebo adresa URL. Pokud `All`, hodnota by měla být `(Aggregate source)` kombinovat všechny zdroje balíčků, které jinak nejsou zakázány. |

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

Můžete použít proměnné prostředí v `NuGet.Config` hodnoty (NuGet 3.4 +) k aplikování nastavení na dobu běhu.

Například pokud `HOME` proměnná prostředí v systému Windows je nastavená na `c:\users\username`, pak hodnota `%HOME%\NuGetRepository` v konfiguraci souboru přeloží na `c:\users\username\NuGetRepository`.

Podobně pokud `HOME` na Mac/Linux je nastavena na `/home/myStuff`, pak `$HOME/NuGetRepository` v konfiguraci souboru přeloží na `/home/myStuff/NuGetRepository`.

Pokud není nalezena proměnná prostředí, používá NuGet literálovou hodnotou z konfiguračního souboru.

## <a name="example-config-file"></a>Příklad konfiguračního souboru

Dole je příklad `NuGet.Config` soubor, který znázorňuje několik nastavení:

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
