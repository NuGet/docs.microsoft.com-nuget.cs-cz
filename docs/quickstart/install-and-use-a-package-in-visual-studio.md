---
title: Úvodní příručka k pomocí balíčků NuGet v sadě Visual Studio
description: Kurz návod týkající se procesu instalace a použití balíčku NuGet v projektu sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 014b316ea03b45584406c313d46b96ad36340124
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426222"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Rychlý start: Nainstalovat a používat balíčky v sadě Visual Studio

Balíčky NuGet obsahují opakovaně použitelný kód, který jinými vývojáři zpřístupnit je pro použití ve vašich projektech. Zobrazit [co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky se nainstalují do projektu sady Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků. Tento článek popisuje proces pomocí Oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku a projekt univerzální platformy Windows (UPW). Stejný postup platí pro libovolný jiný projekt .NET nebo .NET Core.

Po instalaci se odkazovat na balíček v kódu s `using <namespace>` kde \<obor názvů\> je specifický pro balíček, který používáte. Jakmile se odkazuje, můžete volat balíček prostřednictvím jejího rozhraní API.

> [!Tip]
> **Začněte s nuget.org**: Procházení nuget.org je, jak vývojáři na platformě .NET obvykle najdete součásti můžete znovu použít ve svých vlastních aplikacích. Můžete vyhledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Požadavky

- Visual Studio 2017 s úlohou vývoj univerzální platformy Windows, nebo
- Visual Studio 2015 Update 3 s Tools for Universal Windows Apps.

Edice Community 2017 můžete nainstalovat zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použijte edice Professional nebo Enterprise.

Pokud používáte Visual Studio pro Mac, najdete v článku [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough).

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet můžete nainstalovat do jakéhokoli projektu .NET, za předpokladu, že balíček podporuje stejnou cílovou architekturu jako projekt.

V tomto návodu použijte jednoduché aplikace pro Universal Windows (UPW). Vytvoření projektu v sadě Visual Studio pomocí **soubor > Nový projekt...**  a vyberete **Windows Universal > prázdná aplikace (Universal Windows)** . Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček Newtonsoft.Json NuGet

Chcete-li nainstalovat balíček, můžete použít uživatelské rozhraní Správce balíčků nebo konzole Správce balíčků. Při instalaci balíčku NuGet zaznamenává závislost v jednom souboru projektu nebo `packages.config` souboru. Další informace najdete v tématu [balíček spotřeby přehled a pracovní postup](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Uživatelské rozhraní Správce balíčků

1. V Průzkumníku řešení klikněte pravým tlačítkem na **odkazy** a zvolte **spravovat balíčky NuGet**.

    ![Spravovat balíčky NuGet příkaz pro projektové odkazy](media/QS_Use-02-ManageNuGetPackages.png)

1. Zvolte možnost "nuget.org" jako **zdroj balíčku**, vyberte **Procházet** kartu, vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte  **Nainstalujte**:

    ![Vyhledání balíček Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Přijměte případné výzvy licence.

1. (Visual Studio 2017) Pokud se zobrazí výzva k výběru formát správy balíčků, vyberte **PackageReference v souboru projektu**:

    ![Vyberte formát správy balíčků](media/QS_Use-03b-SelectFormat.png)

1. Pokud budete vyzváni ke zkontrolování změn, vyberte **OK**.

### <a name="package-manager-console"></a>Konzola Správce balíčků

1. Vyberte **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu nabídky.

1. Jakmile se otevře se konzola, zkontrolujte, že **výchozí projekt** rozevíracím seznamu zobrazí projektu, do kterého chcete balíček nainstalovat. Pokud máte jeden projekt v řešení, je už vybraná.

    ![Vyhledání balíček Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Zadejte příkaz `Install-Package Newtonsoft.Json` (viz [Install-Package](../tools/ps-ref-install-package.md)). V okně konzoly se zobrazí výstup příkazu. Chyby obvykle signalizují, že balíček není kompatibilní s cílovou architekturu projektu.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použít Newtonsoft.Json rozhraní API v aplikaci

S balíčkem Newtonsoft.Json v projektu, můžete volat jeho `JsonConvert.SerializeObject` způsobů, jak převést objekt na řetězec čitelný.

1. Otevřít `MainPage.xaml` a nahraďte existující `Grid` element následujícím kódem:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otevřít `MainPage.xaml.cs` souboru (umístěné v Průzkumníkovi řešení pod `MainPage.xaml` uzlu) a vložte následující kód `MainPage` konstruktor:

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

1. I když jste přidali do projektu balíček Newtonsoft.Json, červenou vlnovkou se zobrazí v části `JsonConvert` vzhledem k tomu, že je nutné `using` příkazu v horní části souboru kódu:

    ```cs
    using Newtonsoft.Json;
    ```

1. Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **ladit > Spustit ladění**:

    ![Výstup počáteční aplikace pro UPW](media/QS_Use-06-AppStart.png)

1. Vyberte na tlačítko Zobrazit obsah TextBlock nahradit JSON text:

    ![Výstup aplikace UPW po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Související články

- [Přehled a pracovní postup využití balíčků](../consume-packages/overview-and-workflow.md)
- [Instalace a Správa balíčků s využitím sady Visual Studio](../tools/package-manager-ui.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Obvyklé konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md)
