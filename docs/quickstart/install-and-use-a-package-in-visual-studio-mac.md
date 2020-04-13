---
title: Instalace a použití balíčku NuGet v Sadě Visual Studio pro Mac
description: Návod k procesu instalace a používání balíčku NuGet v projektu Visual Studio for Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238525"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Úvodní příručka: Instalace a použití balíčku v Visual Studiu pro Mac

Balíčky NuGet obsahují opakovaně použitelný kód, který vám ostatní vývojáři zpřístupní pro použití ve vašich projektech. Podívejte se [na co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky jsou nainstalovány do projektu Sady Visual Studio pro Mac pomocí Správce balíčků NuGet. Tento článek ukazuje proces pomocí populárního balíčku [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) a konzolového projektu .NET Core. Stejný proces platí pro všechny ostatní Xamarin nebo .NET Core projektu.

Po instalaci, odkazovat na `using <namespace>` balíček v kódu s kde \<obor názvů\> je specifické pro balíček, který používáte. Jakmile je odkaz, můžete volat balíček prostřednictvím jeho rozhraní API.

> [!Tip]
> **Začněte s nuget.org**: Procházení *nuget.org* je způsob, jakým vývojáři rozhraní .NET obvykle vyhledávají součásti, které mohou znovu použít ve svých vlastních aplikacích. Můžete hledat *nuget.org* přímo nebo najít a nainstalovat balíčky v rámci sady Visual Studio, jak je znázorněno v tomto článku. Obecné informace naleznete v [tématu Hledání a vyhodnocení balíčků NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Požadavky

- Visual Studio 2019 pro Mac.

Můžete nainstalovat edici Community 2019 zdarma z [visualstudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.

Pokud používáte Visual Studio ve Windows, přečtěte si informace [o instalaci a použití balíčku v sadě Visual Studio (jenom windows).](install-and-use-a-package-in-visual-studio.md)

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet lze nainstalovat do libovolného projektu .NET za předpokladu, že balíček podporuje stejný cílový rámec jako projekt.

Pro tento návod použijte jednoduchou aplikaci .NET Core Console. Vytvořte projekt ve Visual Studiu for Mac pomocí **souboru > novéřešení...**, vyberte šablonu **aplikace .NET Core > App > Console.** Klikněte na **Další**. Při přijetí výchozích hodnot pro **cílovou architekturu** po zobrazení výzvy.

Visual Studio vytvoří projekt, který se otevře v Průzkumníku řešení.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidat balíček Newtonsoft.Json NuGet

Chcete-li nainstalovat balíček, použijte Správce balíčků NuGet. Při instalaci balíčku NuGet zaznamenává závislost v souboru projektu `packages.config` nebo souboru (v závislosti na formátu projektu). Další informace naleznete v [tématu Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Správce balíčků NuGet

1. V Průzkumníku řešení klikněte pravým **tlačítkem** myši na závislosti a zvolte **Přidat balíčky...**.

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. V levém horním rohu dialogového okna zvolte "nuget.org" jako **zdroj balíčku** a vyhledejte **Newtonsoft.Json**, vyberte tento balíček v seznamu a vyberte **Přidat balíčky...**:

    ![Lokalizace newtonsoft.json balíčku](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Pokud chcete další informace o Správci balíčků NuGet, přečtěte si informace [o instalaci a správě balíčků pomocí Sady Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití rozhraní Newtonsoft.Json API v aplikaci

S newtonsoft.Json balíček v projektu, `JsonConvert.SerializeObject` můžete volat jeho metodu převést objekt na člověka čitelný řetězec.

1. Otevřete `Program.cs` soubor (umístěný v panelu řešení) a nahraďte obsah souboru následujícím kódem:

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. Vytvořte a spusťte aplikaci tak, že vyberete **Spustit > Spustit ladění**:

1. Po spuštění aplikace se v konzole zobrazí serializovaný výstup JSON:

  ![Výstup aplikace Konzola](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Další kroky
Gratulujeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a správa balíčků pomocí Visual Studia pro Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.

- [Přehled a pracovní postup spotřeby balíků](../consume-packages/overview-and-workflow.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
