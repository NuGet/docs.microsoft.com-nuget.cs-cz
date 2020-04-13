---
title: Použití nuget.serveru k hostování informačních kanálů NuGet
description: Jak vytvořit a hostovat informační kanál balíčku NuGet na libovolném serveru se spuštěnou službou IIS pomocí souboru NuGet.Server, čímž jsou balíčky zpřístupněny prostřednictvím protokolů HTTP a OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059523"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server je balíček poskytovaný službou .NET Foundation, který vytváří ASP.NET aplikaci, která může hostovat zdroj balíčků na libovolném serveru se službou IIS. Jednoduše řečeno, NuGet.Server zpřístupňuje složku na serveru prostřednictvím HTTP(S) (konkrétně OData). Je snadné nastavit a je nejlepší pro jednoduché scénáře.

1. Vytvořte prázdnou ASP.NET webovou aplikaci v sadě Visual Studio a přidejte do ní balíček NuGet.Server.
1. Nakonfigurujte `Packages` složku v aplikaci a přidejte balíčky.
1. Nasazení aplikace na vhodný server.

Následující části podrobně procházejí tímto procesem pomocí jazyka C#.

Máte-li další dotazy týkající se nuget.server, vytvořte problém na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Vytvoření a nasazení webové aplikace ASP.NET pomocí serveru NuGet.Server

1. V sadě Visual Studio vyberte **soubor > nový > project**, vyhledejte "ASP.NET webovou aplikaci (.NET Framework)", vyberte odpovídající šablonu pro C#.

    ![Výběr šablony webového projektu rozhraní .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. Nastavte **framework** na ".NET Framework 4.6".

    ![Nastavení cílového rámce pro nový projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Pojmenujte aplikaci jiný *název* než NuGet.Server, vyberte OK a v dalším dialogovém okně vyberte **prázdnou** šablonu a pak vyberte **OK**.

    ![Výběr prázdného webového projektu](media/Hosting_02-NuGet.Server-Empty.png)

1. Klikněte pravým tlačítkem myši na projekt a vyberte **spravovat balíčky NuGet**.

1. V unovém rozhraní Správce balíčků vyberte kartu **Procházet** a pak vyhledejte a nainstalujte nejnovější verzi balíčku NuGet.Server, pokud cílíte na rozhraní .NET Framework 4.6. (Můžete jej také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server`.) Při přijetí výzvy přijměte licenční podmínky.

    ![Instalace balíčku NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. Instalace nuget.serveru převede prázdnou webovou aplikaci na zdroj balíčku. Nainstaluje řadu dalších balíčků, vytvoří `Packages` složku v aplikaci a `web.config` upraví zahrnout další nastavení (podrobnosti naleznete v komentářích v tomto souboru).

    > [!Important]
    > Pečlivě `web.config` zkontrolujte po NuGet.Server balíček dokončil své změny tohoto souboru. NuGet.Server nemusí přepsat existující prvky, ale místo toho vytvořit duplicitní prvky. Tyto duplikáty způsobí "Vnitřní chyba serveru" při pozdějším pokusu o spuštění projektu. Například pokud `web.config` vaše `<compilation debug="true" targetFramework="4.5.2" />` obsahuje před instalací NuGet.Server, balíček není přepsat, `<compilation debug="true" targetFramework="4.6" />`ale vloží druhý . V takovém případě odstraňte prvek se starší verzí frameworku.

1. Spusťte web místně v sadě Visual Studio (pomocí **ladění > spustit bez ladění** nebo Ctrl+F5). Domovská stránka obsahuje adresy URL zdroje balíčků, jak je znázorněno níže. Pokud se zobrazí chyby, pečlivě zkontrolujte `web.config` duplicitní prvky, jak je uvedeno dříve.

    ![Výchozí domovská stránka aplikace s NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  Při prvním spuštění aplikace NuGet.Server restrukturalizuje `Packages` složku tak, aby obsahovala složku pro každý balíček. To odpovídá [rozložení místního úložiště](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) zavedené s NuGet 3.3 ke zlepšení výkonu. Při přidávání dalšíbalíčky, pokračovat v následující struktuře.

1. Po otestování místního nasazení nasaďte aplikaci do jakékoli jiné interní nebo externí lokality podle potřeby.

1. Po nasazení `http://<domain>`do , bude adresa URL, kterou `http://<domain>/nuget`používáte pro zdroj balíčku .

## <a name="adding-packages-to-the-feed-externally"></a>Externí přidávání balíků do informačního kanálu

Po spuštění webu NuGet.Server můžete přidat balíčky pomocí [nuget push](../reference/cli-reference/cli-ref-push.md) za předpokladu, že nastavíte hodnotu klíče rozhraní API v aplikaci `web.config`.

Po instalaci balíčku NuGet.Server `web.config` obsahuje `appSetting/apiKey` prázdnou hodnotu:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Pokud `apiKey` je vynechánnebo prázdný, odesílání balíčků do informačního kanálu je zakázáno.

Chcete-li tuto funkci `apiKey` povolit, nastavte hodnotu (v ideálním `appSettings/requireApiKey` případě silné `true`heslo) a přidejte klíč volaný s hodnotou :

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Pokud je server již zabezpečený nebo jinak nepotřebujete klíč rozhraní API (například při použití `requireApiKey` privátního serveru v místní týmové síti), můžete nastavit na . `false` Všechny uživatele s přístupem k serveru pak mohou vymísťovat balíčky.

Počínaje nuget.server 3.0.0, url pro odesílání `http://<domain>/nuget`balíčků byla změna na . Před vydáním verze 3.0.0 byla `http://<domain>/api/v2/package`adresa URL push .

S NuGet 3.2.1 a novější, `/api/v2/package` tato starší `/nuget` adresa URL `enableLegacyPushRoute: true` je povolena kromě`NuGetODataConfig.cs` ve výchozím nastavení prostřednictvím možnosti v spouštěcí konfiguraci (ve výchozím nastavení). Všimněte si, že tato funkce nefunguje, pokud více informačních kanálů jsou hostovány ve stejném projektu.

## <a name="removing-packages-from-the-feed"></a>Odebrání balíčků z informačního kanálu

S NuGet.Server [nuget delete](../reference/cli-reference/cli-ref-delete.md) příkaz odebere balíček z úložiště za předpokladu, že zahrnete klíč rozhraní API s komentářem.

Pokud chcete změnit chování, aby delist balíček místo (ponechat `enableDelisting` k `web.config` dispozici pro obnovení balíčku), změňte klíč v true.

## <a name="configuring-the-packages-folder"></a>Konfigurace složky Balíčky

Pomocí `NuGet.Server` položky 1.5 a novějšímůžete přizpůsobit `appSettings/packagesPath` složku `web.config`balíčku pomocí hodnoty v části :

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath`může být absolutní nebo virtuální cesta.

Pokud `packagesPath` je vynechánnebo ponechán prázdný, složka `~/Packages`balíčky je výchozí .

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Zpřístupnění balíčků při publikování webové aplikace

Chcete-li balíčky zpřístupnit v informačním kanálu při `.nupkg` publikování aplikace `Packages` na server, přidejte jednotlivé soubory do složky v sadě Visual Studio a potom nastavte každý z nich **akce sestavení** na **obsah** a kopírovat **do výstupního adresáře** **ke kopírování vždy**:

![Kopírování balíčků do složky Balíčky v projektu](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Poznámky k verzi

Poznámky k verzi pro NuGet.Server jsou k dispozici na [stránce vydání GitHubu](https://github.com/NuGet/NuGet.Server/releases).
To zahrnuje podrobnosti o opravách chyb a nových funkcích, které jsou přidány.

## <a name="nugetserver-support"></a>Podpora nuget.server

Další nápovědu pomocí souboru NuGet.Server získáte vytvořením problému v aplikaci [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).
