---
title: Použití NuGet. Server k hostování kanálů NuGet
description: Postup vytvoření a hostování informačního kanálu balíčku NuGet na jakémkoli serveru se službou IIS pomocí NuGet. Server, zpřístupnění balíčků prostřednictvím protokolu HTTP a OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 7a806e6b586c63c701642c9e43865cb077d7999c
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623042"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet. Server je balíček poskytovaný rozhraním .NET Foundation, který vytváří aplikaci ASP.NET, která může hostovat kanál balíčku na jakémkoli serveru, na kterém je spuštěna služba IIS. Jednoduše řečeno, NuGet. server zpřístupňuje složku na serveru prostřednictvím protokolu HTTP (konkrétně OData). U jednoduchých scénářů se snadno nastavuje a je nejvhodnější.

1. Vytvořte prázdnou webovou aplikaci v ASP.NET v aplikaci Visual Studio a přidejte do ní balíček NuGet. Server.
1. Nakonfigurujte `Packages` složku v aplikaci a přidejte balíčky.
1. Nasaďte aplikaci na vhodný server.

Následující části podrobně popisují tento proces pomocí jazyka C#.

Pokud máte další dotazy k NuGet. Server, vytvořte problém v [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) .

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Vytvoření a nasazení webové aplikace v ASP.NET pomocí NuGet. Server

1. V aplikaci Visual Studio vyberte **soubor > nový > projekt**, vyhledejte "ASP.NET webová aplikace (.NET Framework)", vyberte šablonu pro **jazyk C#**.

    ![Vyberte šablonu .NET Framework webového projektu.](media/Hosting_00-NuGet.Server-ProjectType.png)

1. Nastavte **rozhraní** na ".NET Framework 4,6".

    ![Nastavení cílové architektury pro nový projekt](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Poskytněte aplikaci vhodný *jiný* název než NuGet. Server, vyberte OK a v dalším dialogovém okně vyberte **prázdnou** šablonu a pak vyberte **OK**.

    ![Vyberte prázdný webový projekt.](media/Hosting_02-NuGet.Server-Empty.png)

1. Klikněte pravým tlačítkem na projekt a vyberte **Spravovat balíčky NuGet**.

1. V uživatelském rozhraní Správce balíčků vyberte kartu **Procházet** a pak vyhledejte a nainstalujte nejnovější verzi balíčku NuGet. Server, pokud cílíte .NET Framework 4,6. (Můžete ji také nainstalovat z konzoly Správce balíčků s `Install-Package NuGet.Server` .) Pokud se zobrazí výzva, přijměte licenční podmínky.

    ![Instalace balíčku NuGet. Server](media/Hosting_03-NuGet.Server-Package.png)

1. Instalace NuGet. Server převede prázdnou webovou aplikaci na zdroj balíčku. Nainstaluje celou řadu dalších balíčků, vytvoří `Packages` složku v aplikaci a upraví `web.config` tak, aby zahrnovala další nastavení (podrobnosti najdete v komentářích v tomto souboru).

    > [!Important]
    > Pečlivě zkontrolujte `web.config` , až balíček NuGet. Server dokončí změny tohoto souboru. NuGet. Server nemůže přepsat existující prvky, ale místo toho vytvoří duplicitní prvky. Tyto duplicity způsobí při pozdějším spuštění projektu "interní chybu serveru". Například pokud váš soubor `web.config` obsahuje `<compilation debug="true" targetFramework="4.5.2" />` před instalací NuGet. Server, balíček ho nepřepíše, ale vloží druhý `<compilation debug="true" targetFramework="4.6" />` . V takovém případě odstraňte element se starší verzí rozhraní .NET Framework.

1. Místní spuštění webu v aplikaci Visual Studio (použití **ladění > spustit bez ladění** nebo CTRL + F5). Domovská stránka poskytuje adresy URL kanálu balíčku, jak je znázorněno níže. Pokud se zobrazí chyby, pečlivě zkontrolujte, zda neexistují `web.config` duplicitní prvky, jak bylo uvedeno dříve.

    ![Výchozí domovská stránka aplikace s NuGet. Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  Při prvním spuštění aplikace NuGet. Server restrukturuje `Packages` složku tak, aby obsahovala složku pro každý balíček. To odpovídá [rozložení místního úložiště](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) zavedenému pomocí NuGet 3,3 pro zlepšení výkonu. Při přidávání dalších balíčků pokračujte podle této struktury.

1. Po otestování místního nasazení Nasaďte aplikaci na jakoukoli jinou interní nebo externí lokalitu podle potřeby.

1. Po nasazení do nástroje `http://<domain>` bude adresa URL, kterou použijete pro zdroj balíčku, `http://<domain>/nuget` .

## <a name="adding-packages-to-the-feed-externally"></a>Přidávají se balíčky do externího kanálu externě.

Po spuštění serveru NuGet. Server můžete balíčky přidat pomocí [nabízených oznámení NuGet](../reference/cli-reference/cli-ref-push.md) , pokud nastavíte hodnotu klíče rozhraní API v `web.config` .

Po instalaci balíčku NuGet. Server `web.config` obsahuje prázdná `appSetting/apiKey` hodnota:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Pokud `apiKey` je hodnota vynechána nebo prázdná, je zablokováno vkládání balíčků do informačního kanálu.

Pokud chcete tuto funkci povolit, nastavte na `apiKey` hodnotu (ideálně silné heslo) a přidejte klíč `appSettings/requireApiKey` s názvem s hodnotou `true` :

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Pokud je váš server už zabezpečený nebo pokud nepotřebujete klíč rozhraní API (například při použití privátního serveru v místní týmové síti), můžete nastavit `requireApiKey` na `false` . Všichni uživatelé s přístupem k serveru pak můžou nabízet balíčky.

Počínaje NuGet. Server 3.0.0 se adresa URL pro zatlačení balíčků změnila na `http://<domain>/nuget` . Před vydáním verze 3.0.0 byla adresa URL nabízení `http://<domain>/api/v2/package` .

U NuGet 3.2.1 a novějších verzí je tato starší adresa URL `/api/v2/package` ve výchozím nastavení povolená, a to `/nuget` prostřednictvím `enableLegacyPushRoute: true` Možnosti v konfiguraci spouštění ( `NuGetODataConfig.cs` ve výchozím nastavení). Všimněte si, že tato funkce nefunguje, když je více kanálů hostováno ve stejném projektu.

## <a name="removing-packages-from-the-feed"></a>Odebírají se balíčky z informačního kanálu.

Pomocí NuGet. Server odebere příkaz [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) balíček z úložiště, do kterého jste zadali klíč rozhraní API s komentářem.

Pokud chcete změnit chování pro devýpis balíčku (nechat ho k dispozici pro obnovení balíčku), změňte `enableDelisting` klíč v `web.config` na true.

## <a name="configuring-the-packages-folder"></a>Konfigurace složky balíčků

Pomocí `NuGet.Server` 1,5 a novějších verzí můžete složku balíčku přizpůsobit pomocí `appSettings/packagesPath` hodnoty v `web.config` :

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` může být absolutní nebo virtuální cesta.

Když `packagesPath` je vynecháno nebo je ponecháno prázdné, složka Packages (balíčky) je výchozí `~/Packages` .

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Zpřístupnění balíčků po publikování webové aplikace

Chcete-li zpřístupnit balíčky v informačním kanálu při publikování aplikace na server, přidejte jednotlivé `.nupkg` soubory do `Packages` složky v aplikaci Visual Studio a pak nastavte každou **akci sestavení** na **obsah** a **Kopírovat do výstupního adresáře** **vždy**:

![Kopírování balíčků do složky Packages v projektu](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Zpráva k vydání verze

Poznámky k verzi pro NuGet. Server jsou k dispozici na [stránce verze GitHubu](https://github.com/NuGet/NuGet.Server/releases).
Obsahuje také podrobnosti o opravách chyb a nových funkcích, které jsou přidány.

## <a name="nugetserver-support"></a>Podpora NuGet. Server

Další nápovědu k používání NuGet. Server získáte vytvořením problému v [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) .
