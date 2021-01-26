---
title: Instalace a použití balíčku NuGet v aplikaci Visual Studio
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu sady Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775524"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Rychlý Start: instalace a použití balíčku v aplikaci Visual Studio (pouze Windows)

Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři. Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky se nainstalují do projektu sady Visual Studio pomocí Správce balíčků NuGet, [konzoly Správce balíčků](../consume-packages/install-use-packages-powershell.md)nebo příkazového [řádku dotnet](install-and-use-a-package-using-the-dotnet-cli.md). Tento článek popisuje proces použití oblíbených [Newtonsoft.Jsna](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku a projektu Windows Presentation Foundation (WPF). Stejný postup platí pro všechny ostatní projekty .NET nebo .NET Core.

Po instalaci se podívejte na balíček v kódu, `using <namespace>` kde \<namespace\> je specifický pro balíček, který používáte. Po provedení odkazu můžete balíček volat prostřednictvím jeho rozhraní API.

> [!Tip]
> **Začínáme s NuGet.org**: prohlížení *NuGet.org* je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích. Můžete vyhledat *NuGet.org* přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku. Obecné informace najdete v tématu [vyhledání a vyhodnocení balíčků NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Požadavky

- Visual Studio 2019 s úlohou vývoj desktopových aplikací .NET.

Edici 2019 Community Edition můžete zdarma nainstalovat z [VisualStudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.

Pokud používáte Visual Studio pro Mac, přečtěte si téma [instalace a použití balíčku v Visual Studio pro Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet se dají nainstalovat do libovolného projektu .NET, za předpokladu, že balíček podporuje stejnou cílovou architekturu jako projekt.

Pro tento návod použijte jednoduchou aplikaci WPF. V aplikaci Visual Studio vytvořte projekt pomocí **souboru**  >  **Nový projekt**, zadejte do vyhledávacího pole **.NET** a pak vyberte **aplikaci WPF (.NET Framework)**. Klikněte na **Next** (Další). Po zobrazení výzvy přijměte výchozí hodnoty pro **rozhraní** .

Visual Studio vytvoří projekt, který se otevře v Průzkumník řešení.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidání Newtonsoft.Jsdo balíčku NuGet

Chcete-li nainstalovat balíček, můžete použít buď správce balíčků NuGet, nebo konzolu Správce balíčků. Při instalaci balíčku zaznamená NuGet závislost v souboru projektu nebo v `packages.config` souboru (v závislosti na formátu projektu). Další informace najdete v tématu [Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Správce balíčků NuGet

1. V Průzkumník řešení klikněte pravým tlačítkem na **odkazy** a vyberte **Spravovat balíčky NuGet**.

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. Jako **zdroj balíčku** zvolte "NuGet.org", vyberte kartu **procházet** , vyhledejte **Newtonsoft.Jsna**, vyberte tento balíček v seznamu a vyberte **instalovat**:

    ![Hledání Newtonsoft.Jsv balíčku](media/QS_Use-03-NewtonsoftJson.png)

    Pokud chcete získat další informace o Správci balíčků NuGet, přečtěte si téma [instalace a Správa balíčků pomocí sady Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Přijměte všechny výzvy k licenci.

1. (Pouze Visual Studio 2017) Pokud se zobrazí výzva k výběru formátu správy balíčků, vyberte **v souboru projektu možnost PackageReference**:

    ![Výběr formátu správy balíčků](media/QS_Use-03b-SelectFormat.png)

1. Pokud se zobrazí výzva ke kontrole změn, vyberte **OK**.

### <a name="package-manager-console"></a>Konzola Správce balíčků

1. Vyberte **nástroje**  >  **Správce balíčků NuGet**  >  **Konzola** správce balíčků příkaz menu.

1. Po otevření konzoly ověřte, zda je v rozevíracím seznamu **výchozí projekt** uveden projekt, do kterého chcete balíček nainstalovat. Pokud máte v řešení jeden projekt, je již vybrán.

    ![Vyberte projekt pro balíček.](media/QS_Use-08-Console1.png)

1. Zadejte příkaz `Install-Package Newtonsoft.Json` (viz [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). V okně konzoly se zobrazí výstup příkazu. Chyby obvykle označují, že balíček není kompatibilní s cílovým rozhraním .NET Framework projektu.

   Pokud chcete získat další informace o konzole správce balíčků, přečtěte si téma [instalace a Správa balíčků pomocí konzoly Správce balíčků](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití Newtonsoft.Jsv rozhraní API v aplikaci

Pomocí Newtonsoft.Jsv balíčku v projektu můžete zavolat jeho `JsonConvert.SerializeObject` metodu pro převod objektu na řetězec čitelný z lidského.

1. `MainWindow.xaml`Existující prvek otevřete a nahraďte `Grid` následujícím:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otevřete `MainWindow.xaml.cs` soubor (umístěný v Průzkumník řešení pod `MainWindow.xaml` uzlem) a vložte následující kód do `MainWindow` třídy:

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

1. I když jste přidali Newtonsoft.Jsdo balíčku do projektu, zobrazí se červené vlnovky v části, `JsonConvert` protože potřebujete `using` příkaz v horní části souboru kódu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **ladění**  >  **Spustit ladění**:

    ![Počáteční výstup aplikace WPF](media/QS_Use-06-AppStart.png)

1. Výběrem tlačítka na tomto tlačítku zobrazíte obsah TextBlock nahrazený nějakým textem JSON:

    ![Výstup aplikace WPF po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Další videa k NuGetu najdete na webu [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Další kroky

Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a Správa balíčků pomocí sady Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Instalace a Správa balíčků pomocí konzoly Správce balíčků](../consume-packages/install-use-packages-powershell.md)

Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.

- [Přehled a pracovní postup pro spotřebu balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
