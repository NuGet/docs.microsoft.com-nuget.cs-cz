---
title: Úvodní příručka k použití NuGet balíčky prostřednictvím rozhraní příkazového řádku dotnet.
description: Návod kurz týkající se procesu instalace a použití balíčku NuGet v projektu .NET Core.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 41a249394a8a0504cc8841d3bdb67ad29ec2dc26
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Rychlý úvod: Instalace a použití balíčku pomocí rozhraní příkazového řádku dotnet.

Balíčky NuGet obsahovat opakovaně použitelný kód, který jinými vývojáři zpřístupnění pro použití ve vašich projektů. V tématu [co je NuGet?](../What-is-NuGet.md) pozadí. Balíčky jsou nainstalovány do projektu .NET Core pomocí `dotnet add package` příkaz, jak je popsáno v tomto článku Oblíbené [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) balíčku.

Po instalaci odkazovat na balíček v kódu pomocí `using <namespace>` kde \<obor názvů\> je specifická pro balíček, který používáte. Pak můžete použít rozhraní API balíčku.

> [!Tip]
> **Začněte s nuget.org**: procházení nuget.org je, jak .NET vývojáři obvykle najít součásti můžete opakovaně použít ve svých vlastních aplikacích. Můžete hledat nuget.org přímo nebo najít a nainstalovat balíčky v sadě Visual Studio, jak je znázorněno v tomto článku.

## <a name="prerequisites"></a>Požadavky

- [.NET Core SDK](https://www.microsoft.com/net/download/), který poskytuje `dotnet` nástroj příkazového řádku.

## <a name="create-a-project"></a>Vytvoření projektu

Balíčky NuGet lze nainstalovat do projektu .NET určitého druhu. Pro účely tohoto postupu vytvoření jednoduché projektu konzoly .NET Core následujícím způsobem:

1. Vytvořte složku pro projekt.

1. Vytvoření projektu pomocí následujícího příkazu:

    ```cli
    dotnet new console
    ```

1. Použití `dotnet run` k testování, aby byla správně vytvořená aplikace.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Přidejte balíček Newtonsoft.Json NuGet

1. Použijte následující příkaz k instalaci `Newtonsoft.json` balíčku:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. Po dokončení příkazu, otevřete `.csproj` soubor přidaný odkaz:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Použít Newtonsoft.Json rozhraní API v aplikaci

1. Otevřete `Program.cs` souborů a v horní části souboru přidejte následující řádek:

    ```cs
    using Newtonsoft.Json;
    ```

1. Přidejte následující kód, než `class Program` řádku:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Nahraďte `Main` funkce následujícím kódem:

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

1. Sestavení a spuštění aplikace pomocí `dotnet run` příkaz. Výstup by měl být reprezentaci JSON `Account` objektu v kódu:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a>Související články

- [Přehled a pracovní postup spotřeby balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Způsoby, jak nainstalovat balíček](../consume-packages/ways-to-install-a-package.md)
- [Konfigurace chování NuGetu](../consume-packages/configuring-nuget-behavior.md)
