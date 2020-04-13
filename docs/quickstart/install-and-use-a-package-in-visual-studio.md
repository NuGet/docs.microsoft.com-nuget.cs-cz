---
title: Instalace a použití balíčku NuGet v sadě Visual Studio
description: Návod k procesu instalace a používání balíčku NuGet v projektu sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147484"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Úvodní příručka: Instalace a použití balíčku v sadě Visual Studio (jenom pro Windows)

Balíčky NuGet obsahují opakovaně použitelný kód, který vám ostatní vývojáři zpřístupní pro použití ve vašich projektech. Podívejte se [na co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky jsou nainstalovány do projektu sady Visual Studio pomocí Správce balíčků NuGet, [Konzola správce balíčků](../consume-packages/install-use-packages-powershell)nebo [rozhraní SE kontinuu dotnet .](install-and-use-a-package-using-the-dotnet-cli.md) Tento článek ukazuje proces pomocí populární [newtonsoft.json](https://www.nuget.org/packages/Newtonsoft.Json/) balíček a Windows Presentation Foundation (WPF) projekt. Stejný proces platí pro všechny ostatní projekty .NET nebo .NET Core.

Po instalaci, odkazovat na `using <namespace>` balíček v kódu s kde \<obor názvů\> je specifické pro balíček, který používáte. Jakmile je odkaz, můžete volat balíček prostřednictvím jeho rozhraní API.

> [!Tip]
> **Začněte s nuget.org**: Procházení *nuget.org* je způsob, jakým vývojáři rozhraní .NET obvykle vyhledávají součásti, které mohou znovu použít ve svých vlastních aplikacích. Můžete hledat *nuget.org* přímo nebo najít a nainstalovat balíčky v rámci sady Visual Studio, jak je znázorněno v tomto článku. Obecné informace naleznete v [tématu Hledání a vyhodnocení balíčků NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Požadavky

- Visual Studio 2019 s úlohou vývoje plochy .NET.

Můžete nainstalovat edici Community 2019 zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.

Pokud používáte Visual Studio pro Mac, přečtěte si informace [o instalaci a použití balíčku ve Visual Studiu for Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet lze nainstalovat do libovolného projektu .NET za předpokladu, že balíček podporuje stejný cílový rámec jako projekt.

Pro tento návod použijte jednoduchou aplikaci WPF. Vytvořte projekt v sadě Visual Studio pomocí**nového projektu** **souboru** > , zadejte **rozhraní .NET** do vyhledávacího pole a pak vyberte **aplikaci WPF (.NET Framework).** Klikněte na **Další**. Přijímejte výchozí hodnoty pro **rozhraní Framework** po zobrazení výzvy.

Visual Studio vytvoří projekt, který se otevře v Průzkumníku řešení.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidat balíček Newtonsoft.Json NuGet

Chcete-li nainstalovat balíček, můžete použít buď Správce balíčků NuGet nebo konzolu Správce balíčků. Při instalaci balíčku NuGet zaznamenává závislost v souboru projektu `packages.config` nebo souboru (v závislosti na formátu projektu). Další informace naleznete v [tématu Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Správce balíčků NuGet

1. V Průzkumníku řešení klepněte pravým **tlačítkem** myši na reference a zvolte **Spravovat balíčky NuGet**.

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. Jako **zdroj balíčku**zvolte "nuget.org", vyberte kartu **Procházet,** vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte **Instalovat**:

    ![Lokalizace newtonsoft.json balíčku](media/QS_Use-03-NewtonsoftJson.png)

    Pokud chcete další informace o Správci balíčků NuGet, přečtěte si informace [o instalaci a správě balíčků pomocí sady Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Přijměte všechny výzvy k licenci.

1. (Pouze Visual Studio 2017) Pokud se zobrazí výzva k výběru formátu správy balíčků, vyberte **v souboru projektu položku PackageReference**:

    ![Výběr formátu správy balíčků](media/QS_Use-03b-SelectFormat.png)

1. Pokud se zobrazí výzva ke kontrole změn, vyberte **OK**.

### <a name="package-manager-console"></a>Konzola Správce balíčků

1. Vyberte příkaz příkaz **konzoly** > Správce > **balíčků** Správce balíčků Nástroje**NuGet.**

1. Po otevření konzoly zkontrolujte, zda se v rozevíracím seznamu **Výchozí projekt** zobrazuje projekt, do kterého chcete balíček nainstalovat. Pokud máte v řešení jeden projekt, je již vybrán.

    ![Lokalizace newtonsoft.json balíčku](media/QS_Use-08-Console1.png)

1. Zadejte `Install-Package Newtonsoft.Json` příkaz (viz [Instalační balíček](../reference/ps-reference/ps-ref-install-package.md)). Okno konzoly zobrazuje výstup příkazu. Chyby obvykle označují, že balíček není kompatibilní s cílovým rámcem projektu.

   Chcete-li získat další informace o konzoli Správce balíčků, přečtěte si informace [o instalaci a správě balíčků pomocí konzoly Správce balíčků](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití rozhraní Newtonsoft.Json API v aplikaci

S newtonsoft.Json balíček v projektu, `JsonConvert.SerializeObject` můžete volat jeho metodu převést objekt na člověka čitelný řetězec.

1. Otevřete `MainWindow.xaml` a `Grid` nahraďte existující prvek následujícím:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otevřete `MainWindow.xaml.cs` soubor (umístěný v `MainWindow.xaml` Průzkumníku řešení pod uzlovým) a do `MainWindow` třídy vložte následující kód:

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

1. I když jste do projektu přidali balíček Newtonsoft.Json, `JsonConvert` zobrazí se `using` pod ním červené vlnovky, protože potřebujete prohlášení v horní části souboru kódu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **možnosti Ladění** > **ladění startování**:

    ![Počáteční výstup aplikace WPF](media/QS_Use-06-AppStart.png)

1. Výběrem na tlačítku zobrazíte obsah textového bloku nahrazený nějakým textem JSON:

    ![Výstup aplikace WPF po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Další kroky

Gratulujeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a správa balíčků pomocí sady Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Instalace a správa balíčků pomocí konzoly Správce balíčků](../consume-packages/install-use-packages-powershell.md)

Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.

- [Přehled a pracovní postup spotřeby balíků](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
