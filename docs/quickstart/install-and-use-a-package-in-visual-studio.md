---
title: Instalace a použití balíčku NuGet v aplikaci Visual Studio
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 1976d1dc7129da4edb44a1346c6ce74ad3e93b1b
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342485"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Rychlý start: Instalace a použití balíčku v aplikaci Visual Studio

Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři. Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky jsou nainstalovány do projektu aplikace Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzoly Správce balíčků. Tento článek popisuje proces použití oblíbeného balíčku [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) a projektu univerzální platforma Windows (UWP). Stejný postup platí pro všechny ostatní projekty .NET nebo .NET Core.

Po instalaci se podívejte na balíček v kódu `using <namespace>` , kde \<obor názvů\> je specifický pro balíček, který používáte. Po provedení odkazu můžete balíček volat prostřednictvím jeho rozhraní API.

> [!Tip]
> **Začínáme s NuGet.org**: Procházení nuget.org je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích. Můžete vyhledat nuget.org přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Požadavky

- Visual Studio 2017 s úlohou vývoje Univerzální platforma Windows nebo
- Visual Studio 2015 Update 3 s nástroji pro univerzální aplikace pro Windows

Edici 2017 Community Edition můžete zdarma nainstalovat z [VisualStudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.

Pokud používáte Visual Studio pro Mac, přečtěte si téma [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough).

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet se dají nainstalovat do libovolného projektu .NET, za předpokladu, že balíček podporuje stejnou cílovou architekturu jako projekt.

Pro tento návod použijte jednoduchou aplikaci pro univerzální platformu Windows (UWP). V aplikaci Visual Studio vytvořte projekt pomocí **> soubor nový projekt...** a vyberte možnost **Windows Universal > prázdná aplikace (univerzální pro Windows)** . Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou verzi a minimální verzi.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček NuGet Newtonsoft. JSON.

Chcete-li nainstalovat balíček, můžete použít buď uživatelské rozhraní Správce balíčků, nebo konzolu Správce balíčků. Při instalaci balíčku zaznamená NuGet závislost v souboru projektu nebo `packages.config` v souboru. Další informace najdete v tématu [Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Uživatelské rozhraní Správce balíčků

1. V Průzkumník řešení klikněte pravým tlačítkem na **odkazy** a vyberte **Spravovat balíčky NuGet**.

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. Jako **zdroj balíčku**zvolte "NuGet.org", vyberte kartu **Procházet** , vyhledejte **Newtonsoft. JSON**, vyberte tento balíček v seznamu a vyberte **instalovat**:

    ![Vyhledání balíčku Newtonsoft. JSON](media/QS_Use-03-NewtonsoftJson.png)

1. Přijměte všechny výzvy k licenci.

1. (Visual Studio 2017) Pokud se zobrazí výzva k výběru formátu správy balíčků, vyberte **v souboru projektu možnost PackageReference**:

    ![Výběr formátu správy balíčků](media/QS_Use-03b-SelectFormat.png)

1. Pokud se zobrazí výzva ke kontrole změn, vyberte **OK**.

### <a name="package-manager-console"></a>Konzola Správce balíčků

1. Vyberte **nástroje > správce balíčků NuGet > nabídce konzoly Správce balíčků** .

1. Po otevření konzoly ověřte, zda je v rozevíracím seznamu **výchozí projekt** uveden projekt, do kterého chcete balíček nainstalovat. Pokud máte v řešení jeden projekt, je již vybrán.

    ![Vyhledání balíčku Newtonsoft. JSON](media/QS_Use-08-Console1.png)

1. Zadejte příkaz `Install-Package Newtonsoft.Json` (viz [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). V okně konzoly se zobrazí výstup příkazu. Chyby obvykle označují, že balíček není kompatibilní s cílovým rozhraním .NET Framework projektu.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití rozhraní API Newtonsoft. JSON v aplikaci

Pomocí balíčku Newtonsoft. JSON v projektu můžete zavolat jeho `JsonConvert.SerializeObject` metodu pro převod objektu na řetězec čitelný z lidského.

1. `MainPage.xaml` Existující`Grid` prvek otevřete a nahraďte následujícím:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otevřete soubor (umístěný v Průzkumník řešení `MainPage.xaml` pod uzlem) a do `MainPage` konstruktoru vložte následující kód: `MainPage.xaml.cs`

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. I když jste do projektu přidali balíček Newtonsoft. JSON, červené vlnovky se zobrazí v části `JsonConvert` , protože `using` potřebujete příkaz v horní části souboru kódu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem možnosti **ladění > spustit ladění**:

    ![Počáteční výstup aplikace UWP](media/QS_Use-06-AppStart.png)

1. Výběrem tlačítka na tomto tlačítku zobrazíte obsah TextBlock nahrazený nějakým textem JSON:

    ![Výstup aplikace UWP po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a>Další kroky

Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a Správa balíčků pomocí sady Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.

- [Přehled a pracovní postup pro spotřebu balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
