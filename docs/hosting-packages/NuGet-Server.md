---
title: Použití NuGet.Server k hostování NuGet informační kanály
description: Jak vytvořit a hostovat balíček NuGet kanálu na libovolný server se službou IIS pomocí NuGet.Server, zpřístupnění balíčků prostřednictvím protokolu HTTP a protokolu OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: e99d42744ec860976ae098be94e747ec4bc9a7c6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551953"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server je balíček poskytované .NET Foundation, který vytváří aplikaci ASP.NET, který může hostovat balíček kanálu na libovolném serveru, na kterém běží služby IIS. Jednoduše ale nutné dodat, NuGet.Server zpřístupňuje složky na serveru prostřednictvím protokolu HTTP (S) (konkrétně OData). Je snadné nastavení a je nejvhodnější pro jednoduché scénáře.

1. Vytvořit prázdnou webovou aplikaci ASP.NET v sadě Visual Studio a přidejte do ní balíček NuGet.Server.
1. Konfigurace `Packages` složky v aplikaci a přidání balíčků.
1. Nasaďte aplikaci do vhodný server.

V následujících částech si tento proces podrobně pomocí jazyka C#.

Pokud máte další otázky týkající se NuGet.Server, vytvoření problému na [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Vytvoření a nasazení webové aplikace ASP.NET s NuGet.Server

1. V sadě Visual Studio, vyberte **soubor > Nový > projekt**, vyhledejte "ASP.NET", vyberte **webová aplikace ASP.NET (.NET Framework)** šablony pro C# a sady **Framework** ".NET Framework 4.6":

    ![Nastavení cílový rámec pro nový projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Zadejte vhodný název aplikace *jiných* než NuGet.Server, vyberte OK a v dalším dialogovém okně vyberte **prázdný** šablony, pak vyberte **OK**.

1. Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**.

1. V uživatelském rozhraní Správce balíčků, vyberte **Procházet** kartě pak vyhledávat a instalovat nejnovější verzi balíčku NuGet.Server, pokud se zaměřujete na rozhraní .NET Framework 4.6. (Můžete ho také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.) Pokud se zobrazí výzva, přijměte licenční podmínky.

    ![Instaluje se balíček NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. Prázdná webová aplikace instalace NuGet.Server převede na zdroji balíčku. Nainstaluje celou řadu dalších balíčků, vytvoří `Packages` složky v aplikaci a změní `web.config` zahrnout další nastavení (viz poznámky v tomto souboru podrobnosti).

    > [!Important]
    > Pečlivě zkontrolujte `web.config` po dokončení své změny do tohoto souboru balíčku NuGet.Server. NuGet.Server může přepsat stávající elementy, ale místo toho vytvořit duplicitní prvky. Tyto duplikáty způsobí "vnitřní chyba serveru", když zkusíte později, spusťte projekt. Například pokud vaše `web.config` obsahuje `<compilation debug="true" targetFramework="4.5.2" />` před instalací NuGet.Server balíček nepřepíše ho ale vloží sekundy `<compilation debug="true" targetFramework="4.6" />`. V takovém případě odstraňte prvek starší verze rozhraní framework.

1. K dispozici balíčky v informačním kanálu publikování aplikace na serveru, přidejte všechny `.nupkg` soubory `Packages` složky v sadě Visual Studio, nastavte každé z nich **akce sestavení** k **obsahu**a **kopírovat do výstupního adresáře** k **vždy Kopírovat**:

    ![Balíčky se kopírují do složky balíčků v projektu](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Spuštění tohoto webu místně v sadě Visual Studio (pomocí **ladit > Spustit bez ladění** nebo Ctrl + F5). Domovská stránka obsahuje balíček kanálu adresy URL, jak je znázorněno níže. Pokud se zobrazí chyby, pečlivě zkontrolujte vaše `web.config` pro duplicitní prvky jsou jste si předtím poznamenali v kroku 5.

    ![Výchozí domovskou stránku pro aplikaci s NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Klikněte na **tady** v oblasti zobrazíte kanál OData, které balíčky uvedené výše.

1. Při prvním spuštění aplikace, ke změně struktury NuGet.Server `Packages` složku tak, aby obsahovala složku pro každý balíček. To odpovídá [rozložení místní úložiště](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) představeny s nástrojem NuGet 3.3 ke zlepšení výkonu. Při přidávání dalších balíčků, i nadále tuto strukturu.

1. Jakmile jste otestovali místní nasazení, podle potřeby nasadíte aplikace na další interní nebo externí web.

1. Po nasazení chcete `http://<domain>`, bude mít adresu URL, který používáte pro zdroj balíčku `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Konfigurace složky balíčků

S `NuGet.Server` 1.5 a novější, můžete přesněji řečeno nakonfigurovat pomocí složku balíčku `appSetting/packagesPath` hodnota v `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` může být absolutní nebo virtuální cesta.

Když `packagesPath` je vynechán nebo prázdné, je výchozí složka balíčky `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Přidávají se balíčky do informačního kanálu externě

Jakmile NuGet.Server Web spuštěný, může přidání balíčků s využitím [nuget nabízených](../tools/cli-ref-push.md) za předpokladu, že nastavíte hodnotu klíče rozhraní API v `web.config`.

Po instalaci balíčku NuGet.Server `web.config` obsahuje prázdnou `appSetting/apiKey` hodnotu:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Když `apiKey` je vynechán, nebo prázdná, nahráním balíčky do informačního kanálu je zakázána.

Chcete-li povolit tuto funkci, nastavte `apiKey` na hodnotu (v ideálním případě silné heslo) a přidejte klíč s názvem `appSettings/requireApiKey` s hodnotou `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Pokud váš server je již zabezpečený nebo jinak nepožadujete klíč rozhraní API (například při použití privátní server na místní team sítě), můžete nastavit `requireApiKey` k `false`. Všichni uživatelé s přístupem k serveru pak můžete nabízet balíčky.

## <a name="removing-packages-from-the-feed"></a>Odebrání balíčků z informačního kanálu

S NuGet.Server [nuget odstranit](../tools/cli-ref-delete.md) příkaz odebere balíček z úložiště, za předpokladu, že obsahovat klíč rozhraní API s komentářem.

Pokud chcete změnit chování výmazu místo zápisu balíček (se v něm k dispozici pro obnovení balíčku), změnit `enableDelisting` klíče v `web.config` na hodnotu true.

## <a name="nugetserver-support"></a>Podpora NuGet.Server

Pokud potřebujete další pomoc pomocí NuGet.Server, vytvoření problému na [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).