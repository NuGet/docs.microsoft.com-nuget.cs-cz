---
title: Instalace a použití balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: ee456fd49675db37fee78dc14502a897d84a2b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342468"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Rychlý start: Instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet

Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři. Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky jsou nainstalovány do projektu .NET Core pomocí `dotnet add package` příkazu, jak je popsáno v tomto článku pro oblíbený balíček [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) .

Po instalaci se podívejte na balíček v kódu `using <namespace>` , kde \<obor názvů\> je specifický pro balíček, který používáte. Pak můžete použít rozhraní API balíčku.

> [!Tip]
> **Začínáme s NuGet.org**: Procházení nuget.org je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích. Můžete vyhledat nuget.org přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Požadavky

- [.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` nástroj příkazového řádku. Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet se dají nainstalovat do projektu .NET nějakého druhu. Pro tento návod vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:

1. Vytvořte složku pro projekt.

1. Vytvořte projekt pomocí následujícího příkazu:

    ```cli
    dotnet new console
    ```

1. Použijte `dotnet run` k otestování, jestli se aplikace správně vytvořila.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček NuGet Newtonsoft. JSON.

1. K instalaci `Newtonsoft.json` balíčku použijte následující příkaz:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. Po dokončení příkazu otevřete `.csproj` soubor, abyste viděli přidaný odkaz:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití rozhraní API Newtonsoft. JSON v aplikaci

1. `Program.cs` Otevřete soubor a na začátek souboru přidejte následující řádek:

    ```cs
    using Newtonsoft.Json;
    ```

1. Přidejte následující kód před `class Program` řádek:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Nahraďte `Main` tuto funkci následujícím způsobem:

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

1. Sestavte a spusťte aplikaci pomocí `dotnet run` příkazu. Výstup by měl být reprezentace `Account` objektu ve formátu JSON v kódu:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a>Další postup

Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a použití balíčků pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.

- [Přehled a pracovní postup pro spotřebu balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
