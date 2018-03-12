---
title: "Úvodní příručka k používání balíčků NuGet z Visual Studia | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Návod kurz týkající se procesu instalace a použití balíčku NuGet v sadě Visual Studio projektu."
keywords: "Nainstalujte NuGet, využívání balíčku NuGet, instalace balíčků NuGet, odkazů na balíček NuGet, pomocí balíčků NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2cfe2d9b929d43f733fd28ba7336c0b04f718e6
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/08/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a>Instalace a použití balíčku v sadě Visual Studio

Balíčky NuGet obsahovat opakovaně použitelný kód, který jinými vývojáři zpřístupnění pro použití ve vašich projektů. V tématu [co je NuGet?](../What-is-NuGet.md) pozadí. Balíčky jsou nainstalovány do projektu Visual Studia pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků, jak je popsáno v tomto článku Oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíček a projekt univerzální platformu Windows (UWP).

Po instalaci odkazovat na balíček v kódu pomocí `using <namespace>` kde \<obor názvů\> je specifická pro balíček, který používáte. Jakmile se odkazuje, můžete volat balíček prostřednictvím jejího rozhraní API.

> [!Tip]
> **Začněte s nuget.org**: procházení nuget.org je, jak .NET vývojáři obvykle najít součásti můžete opakovaně použít ve svých vlastních aplikacích. Můžete hledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Požadavky

- Visual Studio 2017 se zatížením, vývoj pro univerzální platformu Windows, nebo
- Visual Studio 2015 Update 3 pomocí nástrojů pro univerzální aplikace pro Windows.

Edice Community 2017 můžete nainstalovat zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použijte edice Professional nebo Enterprise.

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet lze nainstalovat do projektu .NET určitého druhu. V tomto návodu použijete jednoduchou aplikaci Universal Windows (UWP). Vytvoření projektu v sadě Visual Studio pomocí **soubor > Nový projekt...**  a výběrem **univerzální pro Windows > prázdná aplikace (univerzální pro Windows)**. Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček Newtonsoft.Json NuGet

Chcete-li nainstalovat balíček, můžete použít uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.

### <a name="package-manager-ui"></a>Uživatelského rozhraní Správce balíčků

1. V Průzkumníku řešení klikněte pravým tlačítkem na **odkazy** a zvolte **spravovat balíčky NuGet**.

    ![Správa balíčků NuGet příkaz pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. Vyberte "nuget.org" jako **zdroj balíčku**, vyberte **Procházet** kartě, vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte  **Nainstalujte**:

    ![Vyhledání Newtonsoft.Json balíčku](media/QS_Use-03-NewtonsoftJson.png)

1. Přijměte zobrazování výzev licence.

1. (Visual Studio 2017) Po zobrazení výzvy vyberte formát balíček správy, vyberte **PackageReference v souboru projektu**:

    ![Výběr formátu odkaz na balíček](media/QS_Use-03b-SelectFormat.png)

1. Pokud budete vyzváni ke zkontrolování změn, vyberte **OK**.

### <a name="package-manager-console"></a>Konzola správce balíčků

1. Vyberte **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu nabídky.

1. Jakmile se otevře se konzola, zkontrolujte, zda **výchozí projekt** rozevíracího seznamu zobrazuje projekt, do kterého chcete nainstalovat balíček. Pokud máte jeden projekt v řešení, je již vybrána.

    ![Vyhledání Newtonsoft.Json balíčku](media/QS_Use-08-Console1.png)

1. Zadejte příkaz `Install-Package Newtonsoft.json` (viz [Install-Package](../tools/ps-ref-install-package.md)). V okně konzoly zobrazí výstup příkazu. Chyby obvykle naznačují, že balíček není kompatibilní s cílový framework projektu na.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použít Newtonsoft.Json rozhraní API v aplikaci

S balíčkem Newtonsoft.Json v projektu, můžete volat jeho `JsonConvert.SerializeObject` způsobů, jak převést objekt na řetězec čitelná pro člověka.

1. Otevřete `MainPage.xaml` a nahradit existující `Grid` element s následující:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otevřete `MainPage.xaml.cs` souboru (umístěné v Průzkumníku řešení v části `MainPage.xaml` uzlu) a vložte následující kód do `MainPage` konstruktor:

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

1. I když jste přidali Newtonsoft.Json balíčku do projektu, se zobrazí červený podtržení vlnovkou pod `JsonConvert` vzhledem k tomu, že budete potřebovat `using` příkaz v horní části souboru kódu:

    ```cs
    using Newtonsoft.json;
    ```

1. Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **ladění > Spustit ladění**:

    ![Počáteční výstup aplikace UWP](media/QS_Use-06-AppStart.png)

1. Vyberte na tlačítko Zobrazit obsah TextBlock nahradí JSON text:

    ![Výstup aplikace UWP po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Související články

- [Přehled a pracovní postup spotřeby balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Způsoby, jak nainstalovat balíček](../consume-packages/ways-to-install-a-package.md)
- [Konfigurace chování NuGetu](../consume-packages/configuring-nuget-behavior.md)
