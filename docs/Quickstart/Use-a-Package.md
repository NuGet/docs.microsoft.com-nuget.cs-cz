---
title: "Úvodní příručka k používání balíčků NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "Návod kurz týkající se procesu instalace a použití balíčku NuGet v projektu."
keywords: "Nainstalujte NuGet, využívání balíčku NuGet, instalace balíčků NuGet, odkazů na balíček NuGet, pomocí balíčků NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a>Instalace a použití balíčku

Balíčky NuGet jsou jednotky opakovaně použitelný kód, který jinými vývojáři zpřístupnění pro použití ve vašich projektů. V tématu [co je NuGet?](../What-is-NuGet.md) pozadí.

[!INCLUDE [install-methods](../includes/install-methods.md)]

Po instalaci odkazovat na balíček v kódu pomocí `using <namespace>` kde \<obor názvů\> je specifická pro balíček, který používáte. Jakmile se odkazuje, můžete volat balíček prostřednictvím jejího rozhraní API.

Zbývající část tohoto tématu provede procesem instalace oblíbených pomocí uživatelského rozhraní Správce balíčků [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíček v projektu univerzální platformu Windows (UWP). Poté zobrazí příklad použití balíčku. Podobně jako stejný pracovní postup se používá pro opravdu každého balíčku NuGet, které můžete použít v projektu.

- [Nainstalujte požadavky](#install-pre-requisites)
- [Vytvoření projektu](#create-a-project)
- [Přidejte balíček Newtonsoft.Json NuGet](#add-the-newtonsoftjson-nuget-package)
- [Použít Newtonsoft.Json rozhraní API v aplikaci](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Začněte s nuget.org**: instalace balíčků z nuget.org je běžné pracovní postup, který .NET vývojáři použít k vyhledání součásti můžete opakovaně použít ve svých vlastních aplikacích. Můžete vždy hledání nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto tématu.

## <a name="install-pre-requisites"></a>Nainstalujte požadavky

Tento kurz vyžaduje Visual Studio 2015 Update 3 pomocí nástrojů pro univerzální aplikace pro Windows nebo Visual Studio 2017 se zatížením, vývoj pro univerzální platformu Windows. Pokud již máte nainstalovanou sadu Visual Studio, můžete spustit instalační program znovu a přidat UWP nástroje.

Edice Community můžete nainstalovat zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použijte edice Professional nebo Enterprise. 

## <a name="create-a-project"></a>Vytvoření projektu

Pokud chcete nainstalovat balíček NuGet, je nutné některé druh. Na základě NET projektu v sadě Visual Studio. V tomto návodu můžete použít jednoduchou aplikaci Windows Presentation Foundation (WPF) nebo Universal Windows (UWP):

- WPF (Windows 7 +), zvolte **soubor > Nový > projekt**, rozbalte položku **Visual C#**, vyberte **klasický desktopový Windows > aplikace WPF (rozhraní .NET Framework)**a vyberte **OK**.
- Pro UPW (Windows 10), použijte **univerzální pro Windows > prázdná aplikace (univerzální pro Windows)** místo. Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček Newtonsoft.Json NuGet

1. V Průzkumníku řešení klikněte pravým tlačítkem na **odkazy** a zvolte **spravovat balíčky NuGet**.

    ![Správa balíčků NuGet příkaz pro odkazy na projekt](media/QS_Use-02-ManageNuGetPackages.png)

1. Vyberte "nuget.org" jako **zdroj balíčku**, vyberte **Procházet** kartě, vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte  **Nainstalujte**:

    ![Vyhledání Newtonsoft.Json balíčku](media/QS_Use-03-NewtonsoftJson.png)

1. Po zobrazení výzvy vyberte formát balíček správy zvolit PackageReference (doporučeno) a `packages.config`:

    ![Výběr formátu odkaz na balíček](media/QS_Use-03b-SelectFormat.png)

1. Pokud budete vyzváni ke zkontrolování změn, vyberte **OK**.

1. V Průzkumníku řešení klikněte pravým tlačítkem a vyberte **sestavit řešení**. Tím se obnoví všechny balíčky NuGet uvedených v části **odkazy**. Další podrobnosti najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použít Newtonsoft.Json rozhraní API v aplikaci

S balíčkem Newtonsoft.Json v projektu, můžete volat jeho `JsonConvert.SerializeObject` způsobů, jak převést objekt na řetězec čitelná pro člověka.

1. Otevřete `MainWindow.xaml` (WPF) nebo `MainPage.xaml` (UWP) a nahradit existující `Grid` element s následující:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Rozbalte `MainWindow.xaml` (WPF) nebo `MainPage.xaml` uzlu (UPW) v Průzkumníku řešení otevřete `.cs` soubor a vložte následující kód do `MainWindow` nebo `MainPage` po konstruktor – třída:

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

1. I když jste přidali Newtonsoft.Json balíčku do projektu, se zobrazí červený podtržení vlnovkou pod `JsonConvert` vzhledem k tomu, že budete potřebovat `using` příkaz. Najeďte myší podtrženou `JsonConvert` a uvidíte žárovek a možnost **zobrazit potenciální opravy**:

    ![Žárovek s zobrazit potenciální opravy příkazu](media/QS_Use-04-ShowPotentialFixes.png)


1. Klikněte na **zobrazit potenciální opravy** (nebo žárovek) a vyberte první navrhované opravu `using Newtonsoft.Json;`. Tento postup přidá nezbytné řádku do horní části souboru.

    ![Poskytnutí možnosti přidat pomocí žárovek – příkaz](media/QS_Use-05-AddUsing.png)

1. Sestavte a spusťte aplikaci stisknutím klávesy F5 nebo výběrem **ladění > Spustit ladění** (UPW zobrazeny zde; WPF je podobný):

    ![Počáteční výstup aplikace UWP](media/QS_Use-06-AppStart.png)

1. Vyberte na tlačítko Zobrazit obsah TextBlock nahradí JSON text:

    ![Výstup aplikace UWP po výběru tlačítka](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>Související témata

- [Přehled a pracovní postup spotřeby balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Konfigurace chování NuGetu](../consume-packages/configuring-nuget-behavior.md)
