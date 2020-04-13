---
title: Instalace a použití balíčku NuGet pomocí rozhraní se konstatování dotnet
description: Návod k procesu instalace a používání balíčku NuGet v projektu .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231270"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Úvodní příručka: Instalace a použití balíčku pomocí rozhraní SE konstatování dotnet

Balíčky NuGet obsahují opakovaně použitelný kód, který vám ostatní vývojáři zpřístupní pro použití ve vašich projektech. Podívejte se [na co je NuGet?](../What-is-NuGet.md) pro pozadí. Balíčky jsou nainstalovány do projektu `dotnet add package` .NET Core pomocí příkazu, jak je popsáno v tomto článku pro populární [newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíček.

Po instalaci, odkazovat na `using <namespace>` balíček v kódu s kde \<obor názvů\> je specifické pro balíček, který používáte. Potom můžete použít rozhraní API balíčku.

> [!Tip]
> **Začněte s nuget.org**: Procházení nuget.org je způsob, jakým vývojáři rozhraní .NET obvykle vyhledávají součásti, které mohou znovu použít ve svých vlastních aplikacích. Můžete vyhledávat nuget.org přímo nebo najít a nainstalovat balíčky v rámci sady Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Požadavky

- Sada [.NET Core SDK](https://www.microsoft.com/net/download/) `dotnet` , která poskytuje nástroj příkazového řádku. Počínaje Visual Studio 2017, dotnet CLI se automaticky nainstaluje s všechny úlohy související s jádrem .NET.

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet lze nainstalovat do projektu .NET nějakého druhu. Pro tento návod vytvořte jednoduchý projekt konzoly .NET Core následujícím způsobem:

1. Vytvořte složku pro projekt.

1. Otevřete příkazový řádek a přepněte do nové složky.

1. Vytvořte projekt pomocí následujícího příkazu:

    ```dotnetcli
    dotnet new console
    ```

1. Slouží `dotnet run` k testování, že aplikace byla vytvořena správně.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidat balíček Newtonsoft.Json NuGet

1. K instalaci `Newtonsoft.json` balíčku použijte následující příkaz:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Po dokončení příkazu otevřete soubor a `.csproj` zotřite přidaný odkaz:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použití rozhraní Newtonsoft.Json API v aplikaci

1. Otevřete `Program.cs` soubor a v horní části souboru přidejte následující řádek:

    ```cs
    using Newtonsoft.Json;
    ```

1. K `class Program` řádku přidejte následující kód:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Nahraďte `Main` funkci následujícím:

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

1. Vytvořte a spusťte `dotnet run` aplikaci pomocí příkazu. Výstupem by měla být reprezentace `Account` JSON objektu v kódu:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Další kroky

Gratulujeme k instalaci a používání vašeho prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Instalace a použití balíčků pomocí rozhraní SE kontinu pro dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.

- [Přehled a pracovní postup spotřeby balíků](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Odkazy na balíčky v souborech projektů](../consume-packages/package-references-in-project-files.md)
