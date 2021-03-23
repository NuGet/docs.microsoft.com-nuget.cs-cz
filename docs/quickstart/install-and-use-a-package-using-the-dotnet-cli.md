---
title: Instalace a použití balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Návodný postup pro instalaci a používání balíčku NuGet v projektu .NET Core.
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: dbe1d3ee8e50a90803140bc2c5cb5821b485a2fd
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859431"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Rychlý Start: instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet

Balíčky NuGet obsahují opakovaně použitelný kód, který vám pro použití v projektech zpřístupní jiní vývojáři. Podívejte [se, co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky jsou nainstalovány do projektu .NET Core pomocí `dotnet add package` příkazu, jak je popsáno v tomto článku pro oblíbené [Newtonsoft.Jsv](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku.

Po instalaci se podívejte na balíček v kódu, `using <namespace>` kde \<namespace\> je specifický pro balíček, který používáte. Pak můžete použít rozhraní API balíčku.

> [!Tip]
> **Začínáme s NuGet.org**: prohlížení NuGet.org je způsob, jakým vývojáři rozhraní .NET obvykle hledají komponenty, které mohou znovu použít ve svých vlastních aplikacích. Můžete vyhledat nuget.org přímo nebo vyhledat a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Předpoklady

- [.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` Nástroj příkazového řádku. Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet se dají nainstalovat do projektu .NET nějakého druhu. Pro tento návod vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:

1. Vytvořte složku pro projekt.

1. Otevřete příkazový řádek a přepněte do nové složky.

1. Vytvořte projekt pomocí následujícího příkazu:

    ```dotnetcli
    dotnet new console
    ```

1. Použijte `dotnet run` k otestování, jestli se aplikace správně vytvořila.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidání Newtonsoft.Jsdo balíčku NuGet

1. K instalaci balíčku použijte následující příkaz `Newtonsoft.json` :

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Po dokončení příkazu otevřete `.csproj` soubor, abyste viděli přidaný odkaz:

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití Newtonsoft.Jsv rozhraní API v aplikaci

1. Otevřete `Program.cs` soubor a na začátek souboru přidejte následující řádek:

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

1. Nahraďte tuto `Main` funkci následujícím způsobem:

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

1. Sestavte a spusťte aplikaci pomocí `dotnet run` příkazu. Výstup by měl být reprezentace objektu ve formátu JSON `Account` v kódu:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

Další videa k NuGetu najdete na webu [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Další kroky

Blahopřejeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a použití balíčků pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.

- [Přehled a pracovní postup pro spotřebu balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
