---
title: Instalace a použití balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 9b6eb012b4bc8135b1648fa9f5e84d7d1c9d6b16
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825346"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Rychlý Start: instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet

Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři. Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky jsou nainstalovány do projektu .NET Core pomocí příkazu `dotnet add package`, jak je popsáno v tomto článku pro oblíbený balíček [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) .

Po instalaci se podívejte na balíček v kódu s `using <namespace>`, kde \<oboru názvů\> je specifické pro balíček, který používáte. Pak můžete použít rozhraní API balíčku.

> [!Tip]
> **Začínáme s NuGet.org**: prohlížení NuGet.org je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích. Můžete vyhledat nuget.org přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Požadavky

- [.NET Core SDK](https://www.microsoft.com/net/download/), který poskytuje nástroj příkazového řádku `dotnet`. Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet se dají nainstalovat do projektu .NET nějakého druhu. Pro tento návod vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:

1. Vytvořte složku pro projekt.

1. Otevřete příkazový řádek a přepněte do nové složky.

1. Vytvořte projekt pomocí následujícího příkazu:

    ```dotnetcli
    dotnet new console
    ```

1. Použijte `dotnet run` k otestování, jestli se aplikace správně vytvořila.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček NuGet Newtonsoft. JSON.

1. K instalaci balíčku `Newtonsoft.json` použijte následující příkaz:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Po dokončení příkazu otevřete soubor `.csproj`, abyste viděli přidaný odkaz:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití rozhraní API Newtonsoft. JSON v aplikaci

1. Otevřete soubor `Program.cs` a do horní části souboru přidejte následující řádek:

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

1. Nahraďte funkci `Main` následujícím způsobem:

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

1. Sestavte a spusťte aplikaci pomocí příkazu `dotnet run`. Výstupem by měl být reprezentace JSON objektu `Account` v kódu:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a>Další kroky

Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a použití balíčků pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.

- [Přehled a pracovní postup pro spotřebu balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
