---
title: Instalace a použití balíčku NuGet v Visual Studio pro Mac
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu Visual Studio pro Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238525"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Rychlý start: Instalace a použití balíčku v Visual Studio pro Mac

Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři. Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky se nainstalují do Visual Studio pro Mac projektu pomocí Správce balíčků NuGet. Tento článek popisuje proces použití oblíbeného balíčku [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) a projektu konzoly .NET Core. Stejný postup platí pro všechny ostatní projekty Xamarin nebo .NET Core.

Po instalaci se podívejte na balíček v kódu `using <namespace>` , kde \<obor názvů\> je specifický pro balíček, který používáte. Po provedení odkazu můžete balíček volat prostřednictvím jeho rozhraní API.

> [!Tip]
> **Začínáme s NuGet.org**: Procházení *NuGet.org* je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích. Můžete vyhledat *NuGet.org* přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku. Obecné informace najdete v tématu [vyhledání a vyhodnocení balíčků NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Požadavky

- Visual Studio 2019 pro Mac.

Edici 2019 Community Edition můžete zdarma nainstalovat z [VisualStudio.com](https://www.visualstudio.com/) nebo použít edice Professional nebo Enterprise.

Pokud používáte sadu Visual Studio ve Windows, přečtěte si téma [instalace a použití balíčku v aplikaci Visual Studio (pouze Windows)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet se dají nainstalovat do libovolného projektu .NET, za předpokladu, že balíček podporuje stejnou cílovou architekturu jako projekt.

Pro tento návod použijte jednoduchou konzolovou aplikaci .NET Core. Vytvořit projekt v Visual Studio pro Mac pomocí **souborového > nové řešení...** vyberte šablonu **konzolové aplikace > aplikace .NET Core >** . Klikněte na **Další**. Po zobrazení výzvy přijměte výchozí hodnoty pro **cílovou architekturu** .

Visual Studio vytvoří projekt, který se otevře v Průzkumník řešení.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček NuGet Newtonsoft. JSON.

K instalaci balíčku použijte Správce balíčků NuGet. Při instalaci balíčku zaznamená NuGet závislost v souboru projektu nebo `packages.config` v souboru (v závislosti na formátu projektu). Další informace najdete v tématu [Přehled spotřeby balíčků a pracovní postup](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Správce balíčků NuGet

1. V Průzkumník řešení klikněte pravým tlačítkem na **závislosti** a vyberte **Přidat balíčky...** .

    ![Příkaz Spravovat balíčky NuGet pro odkazy na projekt](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. V levém horním rohu dialogového okna vyberte "nuget.org" jako **zdroj balíčku** a vyhledejte **Newtonsoft. JSON**, vyberte tento balíček v seznamu a vyberte **Přidat balíčky...** :

    ![Vyhledání balíčku Newtonsoft. JSON](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Pokud chcete získat další informace o Správci balíčků NuGet, přečtěte si téma [instalace a Správa balíčků pomocí Visual Studio pro Mac](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití rozhraní API Newtonsoft. JSON v aplikaci

Pomocí balíčku Newtonsoft. JSON v projektu můžete zavolat jeho `JsonConvert.SerializeObject` metodu pro převod objektu na řetězec čitelný z lidského.

1. `Program.cs` Otevřete soubor (umístěný v oblast řešení) a nahraďte jeho obsah následujícím kódem:

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

1. Sestavte a spusťte aplikaci výběrem možnosti **spustit > spustit ladění**:

1. Po spuštění aplikace se v konzole zobrazí serializovaný výstup JSON:

  ![Výstup aplikace konzoly](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Další postup
Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a Správa balíčků pomocí Visual Studio pro Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.

- [Přehled a pracovní postup pro spotřebu balíčku](../consume-packages/overview-and-workflow.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
