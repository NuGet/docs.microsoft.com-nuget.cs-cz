---
title: "Pomocí NuGet.Server k hostování NuGet kanály | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 45138f80-9717-42c2-8b34-9a1bc1fb3eab
description: "Postup vytvoření a hostování balíčku NuGet informačního kanálu na libovolném serveru služby IIS pomocí NuGet.Server, zpřístupnění balíčků prostřednictvím protokolu HTTP a OData."
keywords: "NuGet kanálu, galerie NuGet vzdálených balíčků informačního kanálu, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f37b9b711a2bc8c39314214113045a6485f297a8
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server je balíček poskytuje základ .NET, který vytvoří aplikace ASP.NET, která může být hostitelem balíčku kanálu na libovolném serveru, který spouští IIS. Jednoduše řečeno, NuGet.Server zpřístupní složky na serveru prostřednictvím protokolu HTTP (S) (konkrétně OData). Je snadno nastavit a je nejvhodnější pro jednoduchého scénáře.

1. Vytvoření prázdné aplikace technologie ASP.NET v sadě Visual Studio a do ní přidejte balíček NuGet.Server.
1. Konfigurace `Packages` složky v aplikaci a přidání balíčků.
1. Nasaďte aplikaci do vhodný server.

V následujících částech provede tento proces podrobně pomocí jazyka C#.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Vytvoření a nasazení webové aplikace ASP.NET s NuGet.Server

1. V sadě Visual Studio, vyberte **soubor > Nový > projekt**, nastavte cílový framework pro rozhraní .NET Framework 4.6 (viz níže), vyhledejte "ASP.NET" a vyberte **webové aplikace ASP.NET (rozhraní .NET Framework)** Šablona pro jazyk C#.

    ![Nastavení cílového rozhraní .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Zadejte vhodný název aplikace *jiných* než NuGet.Server, výběrem OK a v dialogovém okně Další select **prázdný** šablony a vyberte možnost OK.

1. Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**a v uživatelském rozhraní Správce balíčků vyhledávat a instalovat nejnovější verzi balíčku NuGet.Server, pokud jste cílení na rozhraní .NET Framework 4.6. (Můžete ji také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.)

    ![Instalace balíčku NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Pokud webová aplikace cílí rozhraní .NET Framework 4.5.2, je nutné nainstalovat NuGet Server **2.10.3** místo.

1. Instalace NuGet.Server převede prázdné webové aplikace do zdroje balíčku. Vytvoří `Packages` složky v aplikaci a přepíše `web.config` zahrnout další nastavení (viz komentáře v tomto souboru podrobnosti).

1. Balíčky k dispozici při publikování aplikace na server, přidáte jejich `.nupkg` souborů do `Packages` složky v sadě Visual Studio, nastavte jejich **akce sestavení** k **obsahu**a **kopírovat do výstupního adresáře** k **vždy Kopírovat**:

    ![Kopírování balíčků do složky balíčky v projektu](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Spuštění tohoto webu místně v sadě Visual Studio (bez ladění, který je Ctrl + F5). Domovská stránka poskytuje že balíček kanálu adresy URL:

    ![Výchozí domovskou stránku pro aplikaci s NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Klikněte na **sem** v oblasti uvedených výše, pokud chcete zobrazit informační kanál OData balíčků.

1. Při prvním spuštění aplikace, ke změně struktury NuGet.Server `Packages` složky tak, aby obsahovala složku pro každý balíček. To odpovídá [rozložení místní úložiště](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) zavedené NuGet 3.3 ke zlepšení výkonu. Když přidáváte další balíčky, postupujte dál podle tuto strukturu.

1. Jakmile otestujete místní nasazení, nasazení aplikace na jakoukoli jinou lokalitu interních nebo externích podle potřeby.
1. Po nasazení do `http://<domain>`, bude mít adresu URL, který používáte pro zdroj balíčku `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Konfigurace složky balíčků

S `NuGet.Server` verzi 1.5 nebo novější, můžete konkrétně nakonfigurovat složky balíčku pomocí `appSetting/packagesPath` hodnotu `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath`může být absolutní nebo virtuální cesta.

Když `packagesPath` je tento parametr vynechán nebo ponecháno prázdné, je výchozí složka balíčky `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Přidávání balíčků k informačnímu kanálu externě

Jakmile lokalita NuGet.Server běží, můžete přidat nebo odstranit balíčky pomocí nuget.exe za předpokladu, že nastavíte hodnotu klíče rozhraní API v `web.config`.

Po instalaci balíčku NuGet.Server `web.config` obsahuje prázdnou `appSetting/apiKey` hodnotu:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Když `apiKey` je vynechán nebo je prázdné, když zavedete balíčky k informačnímu kanálu zakázáno.

Chcete-li povolit tuto funkci, nastavte `apiKey` na hodnotu (v ideálním případě silné heslo) a přidejte klíč s názvem `appSettings/requireApiKey` s hodnotou `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Pokud váš server je již zabezpečená nebo v opačném případě nepotřebujete klíč rozhraní API (např. při použití privátního serveru v síti místní team), můžete nastavit `requireApiKey` k `false`. Všichni uživatelé s přístupem k serveru můžete pak push nebo odstranit balíčky.