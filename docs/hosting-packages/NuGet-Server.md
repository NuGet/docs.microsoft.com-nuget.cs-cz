---
title: Použití NuGet. Server k hostování kanálů NuGet
description: Postup vytvoření a hostování informačního kanálu balíčku NuGet na jakémkoli serveru se službou IIS pomocí NuGet. Server, zpřístupnění balíčků prostřednictvím protokolu HTTP a OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 82b353450ff1da23a17e5b1c6a825ad32782bf75
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610595"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet. Server je balíček poskytovaný rozhraním .NET Foundation, který vytváří aplikaci ASP.NET, která může hostovat kanál balíčku na jakémkoli serveru, na kterém je spuštěna služba IIS. Jednoduše řečeno, NuGet. server zpřístupňuje složku na serveru prostřednictvím protokolu HTTP (konkrétně OData). U jednoduchých scénářů se snadno nastavuje a je nejvhodnější.

1. Vytvořte prázdnou webovou aplikaci v ASP.NET v aplikaci Visual Studio a přidejte do ní balíček NuGet. Server.
1. Nakonfigurujte složku `Packages` v aplikaci a přidejte balíčky.
1. Nasaďte aplikaci na vhodný server.

Následující části podrobně popisují tento proces pomocí nástroje C#.

Pokud máte další dotazy k NuGet. Server, vytvořte problém na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Vytvoření a nasazení webové aplikace v ASP.NET pomocí NuGet. Server

1. V sadě Visual Studio vyberte **soubor > nový > projekt**, vyhledejte "ASP.NET", vyberte šablonu **ASP.NET Web Application (.NET Framework)** pro C#a nastavte **rozhraní** na ".NET Framework 4,6":

    ![Nastavení cílové architektury pro nový projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Poskytněte aplikaci vhodný *jiný* název než NuGet. Server, vyberte OK a v dalším dialogovém okně vyberte **prázdnou** šablonu a pak vyberte **OK**.

1. Klikněte pravým tlačítkem na projekt a vyberte **Spravovat balíčky NuGet**.

1. V uživatelském rozhraní Správce balíčků vyberte kartu **Procházet** a pak vyhledejte a nainstalujte nejnovější verzi balíčku NuGet. Server, pokud cílíte .NET Framework 4,6. (Můžete ji také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.) Pokud se zobrazí výzva, přijměte licenční podmínky.

    ![Instalace balíčku NuGet. Server](media/Hosting_02-NuGet.Server-Package.png)

1. Instalace NuGet. Server převede prázdnou webovou aplikaci na zdroj balíčku. Nainstaluje celou řadu dalších balíčků, vytvoří v aplikaci složku `Packages` a upraví `web.config` tak, aby zahrnovala další nastavení (podrobnosti najdete v komentářích v tomto souboru).

    > [!Important]
    > Pečlivě zkontrolujte `web.config` poté, co balíček NuGet. Server dokončil změny v tomto souboru. NuGet. Server nemůže přepsat existující prvky, ale místo toho vytvoří duplicitní prvky. Tyto duplicity způsobí při pozdějším spuštění projektu "interní chybu serveru". Pokud například `web.config` obsahuje `<compilation debug="true" targetFramework="4.5.2" />` před instalací NuGet. Server, balíček ho nepřepíše, ale vloží druhý `<compilation debug="true" targetFramework="4.6" />`. V takovém případě odstraňte element se starší verzí rozhraní .NET Framework.

1. Chcete-li zpřístupnit balíčky v informačním kanálu při publikování aplikace na server, přidejte jednotlivé soubory `.nupkg` do složky `Packages` v sadě Visual Studio a pak nastavte každou **akci sestavení** na **obsah** a **Kopírovat do výstupního adresáře** .  **vždy**:

    ![Kopírování balíčků do složky Packages v projektu](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Místní spuštění webu v aplikaci Visual Studio (použití **ladění > spustit bez ladění** nebo CTRL + F5). Domovská stránka poskytuje adresy URL kanálu balíčku, jak je znázorněno níže. Pokud se zobrazí chyby, pečlivě zkontrolujte `web.config` pro duplicitní prvky, které jsou uvedeny dříve v kroku 5.

    ![Výchozí domovská stránka aplikace s NuGet. Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Kliknutím **sem** v oblasti uvedené výše zobrazíte kanál OData pro balíčky.

1. Při prvním spuštění aplikace NuGet. Server restrukturuje složku `Packages` tak, aby obsahovala složku pro každý balíček. To odpovídá [rozložení místního úložiště](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) zavedenému pomocí NuGet 3,3 pro zlepšení výkonu. Při přidávání dalších balíčků pokračujte podle této struktury.

1. Po otestování místního nasazení Nasaďte aplikaci na jakoukoli jinou interní nebo externí lokalitu podle potřeby.

1. Po nasazení na `http://<domain>`se adresa URL, kterou použijete pro zdroj balíčku, `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Konfigurace složky balíčků

U `NuGet.Server` 1,5 a novějších verzí můžete složku balíčku přesněji konfigurovat pomocí `appSetting/packagesPath` hodnoty v `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` může být absolutní nebo virtuální cesta.

Pokud je `packagesPath` vynechána nebo je ponecháno prázdné, složka Packages je výchozí `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Přidávají se balíčky do externího kanálu externě.

Po spuštění serveru NuGet. Server můžete balíčky přidat pomocí [nabízených oznámení NuGet](../reference/cli-reference/cli-ref-push.md) , pokud nastavíte hodnotu klíče rozhraní API v `web.config`.

Po instalaci balíčku NuGet. Server `web.config` obsahuje prázdnou `appSetting/apiKey` hodnotu:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Pokud je hodnota `apiKey` vynechána nebo je prázdná, je zablokováno vkládání balíčků do informačního kanálu.

Pokud chcete tuto funkci povolit, nastavte `apiKey` na hodnotu (ideálně silné heslo) a přidejte klíč s názvem `appSettings/requireApiKey` s hodnotou `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Pokud je váš server už zabezpečený nebo pokud nepotřebujete klíč rozhraní API (například při použití privátního serveru v místní týmové síti), můžete nastavit `requireApiKey` na `false`. Všichni uživatelé s přístupem k serveru pak můžou nabízet balíčky.

## <a name="removing-packages-from-the-feed"></a>Odebírají se balíčky z informačního kanálu.

Pomocí NuGet. Server odebere příkaz [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) balíček z úložiště, do kterého jste zadali klíč rozhraní API s komentářem.

Pokud chcete změnit chování pro devýpis balíčku (nechat ho k dispozici pro obnovení balíčku), změňte `enableDelisting` klíč v `web.config` na hodnotu true.

## <a name="nugetserver-support"></a>Podpora NuGet. Server

Pokud chcete další nápovědu k používání NuGet. Server, vytvořte problém na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).