---
title: Pomocí NuGet.Server k hostování NuGet kanály
description: Postup vytvoření a hostování balíčku NuGet informačního kanálu na libovolném serveru služby IIS pomocí NuGet.Server, zpřístupnění balíčků prostřednictvím protokolu HTTP a OData.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: b1ef1764b28631c3032ac23a250dedece7803ae6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817964"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server je balíček poskytuje základ .NET, který vytvoří aplikace ASP.NET, která může být hostitelem balíčku kanálu na libovolném serveru, který spouští IIS. Jednoduše řečeno, NuGet.Server zpřístupní složky na serveru prostřednictvím protokolu HTTP (S) (konkrétně OData). Je snadno nastavit a je nejvhodnější pro jednoduchého scénáře.

1. Vytvoření prázdné aplikace technologie ASP.NET v sadě Visual Studio a do ní přidejte balíček NuGet.Server.
1. Konfigurace `Packages` složky v aplikaci a přidání balíčků.
1. Nasaďte aplikaci do vhodný server.

V následujících částech provede tento proces podrobně pomocí jazyka C#.

Pokud máte další dotazy týkající se NuGet.Server, vytvořit problém na [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Vytvoření a nasazení webové aplikace ASP.NET s NuGet.Server

1. V sadě Visual Studio, vyberte **soubor > Nový > projekt**, vyhledejte "ASP.NET", vyberte **webové aplikace ASP.NET (rozhraní .NET Framework)** šablonu pro C# a sady **Framework** "Rozhraní .NET Framework 4.6":

    ![Nastavení rozhraní target framework pro nový projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Zadejte vhodný název aplikace *jiných* než NuGet.Server, výběrem OK a v dialogovém okně Další select **prázdný** šablony, vyberte **OK**.

1. Klikněte pravým tlačítkem na projekt, vyberte **spravovat balíčky NuGet**.

1. V uživatelském rozhraní Správce balíčků, vyberte **Procházet** kartě, pak vyhledávat a instalovat nejnovější verzi balíčku NuGet.Server, pokud jste cílení na rozhraní .NET Framework 4.6. (Můžete ji také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.) Pokud se zobrazí výzva, přijměte licenční podmínky.

    ![Instalace balíčku NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. Instalace NuGet.Server převede prázdné webové aplikace do zdroje balíčku. Ho nainstaluje celou řadu dalších balíčků, vytvoří `Packages` složky v aplikaci a upravuje `web.config` zahrnout další nastavení (viz komentáře v tomto souboru podrobnosti).

    > [!Important]
    > Pečlivě zkontrolujte `web.config` po dokončení své změny do tohoto souboru balíčku NuGet.Server. NuGet.Server může nepřepíše existující prvky, ale místo toho vytvořte elementy s duplicitním. Tyto duplikáty způsobí, že "vnitřní chyba serveru" při pokusu později, spusťte projekt. Například pokud vaše `web.config` obsahuje `<compilation debug="true" targetFramework="4.5.2" />` před instalací NuGet.Server, nebude ho přepsat balíček, ale vloží druhý `<compilation debug="true" targetFramework="4.6" />`. V takovém případě odstraňte prvek se starší verzí framework.

1. Balíčky k dispozici pro v informačním kanálu publikování aplikace na server, přidejte každý `.nupkg` souborů do `Packages` složky v sadě Visual Studio, nastavte každé z nich je **akce sestavení** k **obsahu**a **kopírovat do výstupního adresáře** k **vždy Kopírovat**:

    ![Kopírování balíčků do složky balíčky v projektu](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Spuštění tohoto webu místně v sadě Visual Studio (pomocí **ladění > Spustit bez ladění** nebo Ctrl + F5). Domovská stránka obsahuje že balíček kanálu adresy URL, jak je uvedeno níže. Pokud se zobrazí chyby, pečlivě zkontrolujte vaše `web.config` pro elementy s duplicitním jsou si předtím poznamenali krokem 5.

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

`packagesPath` může být absolutní nebo virtuální cesta.

Když `packagesPath` je tento parametr vynechán nebo ponecháno prázdné, je výchozí složka balíčky `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Přidávání balíčků k informačnímu kanálu externě

Jakmile lokalita NuGet.Server běží, můžete přidat balíčky pomocí [nuget nabízené](../tools/cli-ref-push.md) za předpokladu, že nastavíte hodnotu klíče rozhraní API v `web.config`.

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

Pokud váš server je již zabezpečená nebo v opačném případě nepotřebujete klíč rozhraní API (např. při použití privátního serveru v síti místní team), můžete nastavit `requireApiKey` k `false`. Všichni uživatelé s přístupem k serveru, můžete pak push balíčky.

## <a name="removing-packages-from-the-feed"></a>Odebrání balíčků z informačního kanálu

S NuGet.Server [nuget odstranit](../tools/cli-ref-delete.md) příkaz odebere balíček z úložiště za předpokladu, že zahrnují klíč rozhraní API s komentářem.

Pokud chcete změnit chování o výmazu zápisu balíček místo (zároveň je nechává k dispozici pro obnovení balíčku), změnit `enableDelisting` klíče v `web.config` na hodnotu true.

## <a name="nugetserver-support"></a>Podpora NuGet.Server

Pokud potřebujete další pomoc pomocí NuGet.Server, vytvořit problém na [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).