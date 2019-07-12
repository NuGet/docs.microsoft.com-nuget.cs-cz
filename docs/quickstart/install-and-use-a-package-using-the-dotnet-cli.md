---
title: Úvodní příručka k pomocí NuGet balíčky pomocí rozhraní příkazového řádku dotnet
description: Kurz návod týkající se procesu instalace a použití balíčku NuGet v projektu .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 0d637c441cf9f36e8e3e04e47b524b2defecae52
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67841670"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Rychlý start: Instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet

Balíčky NuGet obsahují opakovaně použitelný kód, který jinými vývojáři zpřístupnit je pro použití ve vašich projektech. Zobrazit [co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky se nainstalují do projektu .NET Core s použitím `dotnet add package` příkaz, jak je popsáno v tomto článku pro oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku.

Po instalaci se odkazovat na balíček v kódu s `using <namespace>` kde \<obor názvů\> je specifický pro balíček, který používáte. Pak můžete použít rozhraní API balíčku.

> [!Tip]
> **Začněte s nuget.org**: Procházení nuget.org je, jak vývojáři na platformě .NET obvykle najdete součásti můžete znovu použít ve svých vlastních aplikacích. Můžete vyhledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Požadavky

- [.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` nástroj příkazového řádku. Spouští se v sadě Visual Studio 2017, které pomocí libovolné platformy .NET Core se automaticky nainstaluje rozhraní příkazového řádku dotnet související úlohy.

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet můžete nainstalovat do projektu .NET určitého druhu. V tomto návodu vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:

1. Vytvořte složku pro projekt.

1. Vytvořte projekt pomocí následujícího příkazu:

    ```cli
    dotnet new console
    ```

1. Použití `dotnet run` k otestování, zda aplikace byl vytvořen správně.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček Newtonsoft.Json NuGet

1. Použijte následující příkaz k instalaci `Newtonsoft.json` balíčku:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. Po dokončení příkazu Otevřít `.csproj` soubor přidaný odkaz:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použít Newtonsoft.Json rozhraní API v aplikaci

1. Otevřít `Program.cs` a přidejte následující řádek na začátek souboru:

    ```cs
    using Newtonsoft.Json;
    ```

1. Přidejte následující kód před `class Program` řádku:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Nahradit `Main` funkce následujícím kódem:

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. Sestavte a spusťte aplikaci pomocí `dotnet run` příkazu. Výstup by měl být reprezentaci JSON `Account` objekt v kódu:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a>Související články

- [Nainstalovat a používat balíčky pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md)
- [Přehled a pracovní postup využití balíčků](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Běžné konfigurace NuGetu](../consume-packages/configuring-nuget-behavior.md)
