---
title: Vytvoření a publikování balíčku .NET Framework pomocí sady Visual Studio na Windows
description: Kurz návod týkající se vytváření a publikování balíčku NuGet pro rozhraní .NET Framework pomocí sady Visual Studio 2017 na Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: c537ee97b79648428df2c1b52894f536f5626a9e
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508254"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Rychlý start: Vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Framework, Windows)

Vytvoření balíčku NuGet z knihovny tříd .NET Framework zahrnuje vytváření knihovny DLL v sadě Visual Studio ve Windows a pak pomocí nástroje příkazového řádku nuget.exe vytvoření a publikování balíčku.

> [!Note]
> V tomto rychlém startu platí pro Visual Studio 2017 pro Windows pouze. Visual Studio pro Mac nezahrnuje možnosti popsané tady. Použití [nástroje rozhraní příkazového řádku dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) místo.

## <a name="prerequisites"></a>Požadavky

1. Instalaci libovolné edice sady Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy. Visual Studio 2017 automaticky zahrnuje NuGet možnosti, když je nainstalovaná úloha .NET.

1. Nainstalujte `nuget.exe` rozhraní příkazového řádku, stáhněte si ji z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, který `.exe` soubor vhodný složky a přidání složky do proměnné prostředí PATH.

1. [Zaregistrujte si bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte. Vytvoření nového účtu se odešle e-mail s potvrzením. Účet musí ověřit dříve, než můžete nahrát balíček.

## <a name="create-a-class-library-project"></a>Vytvořte projekt knihovny tříd

Můžete použít existující projekt knihovny tříd .NET Framework pro kód, který chcete balíček nebo vytvořit jednoduchý následujícím způsobem:

1. V sadě Visual Studio, zvolte **soubor > Nový > projekt**, vyberte **Visual C#** uzlu, vyberte šablonu "Knihovna tříd (.NET Framework)", pojmenujte projekt AppLogger a klikněte na tlačítko **OK**.

1. Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** k Ujistěte se, že projekt je vytvořený řádně. Knihovny DLL se nachází složka pro ladění (nebo vydání, pokud vytváříte tuto konfiguraci místo).

V rámci skutečné balíčku NuGet samozřejmě, můžete implementovat mnoho užitečných funkcí, se kterými ostatní můžete vytvářet aplikace. Můžete také nastavit cílové rozhraní ale chcete. Příklad naleznete v tématu příručky k [UPW](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).

V tomto návodu ale nebude napíšete žádný další kód vzhledem k tomu, že knihovna tříd z této šablony je dostatečná pro vytvoření balíčku. Pokud chcete některé funkční kód pro balíček, stále, použijte následující:

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> Pokud nemáte důvod nerozhodnete jinak, .NET Standard je upřednostňovaným cílem, pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projektů. Zobrazit [vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Konfigurovat vlastnosti projektu pro balíček

Obsahuje manifest balíčku NuGet ( `.nuspec` souboru), který obsahuje metadata relevantní jako identifikátor balíčku, číslo verze, popis a další. Některé z nich může být odebírány z vlastnosti projektu přímo, díky tomu není nutné samostatně je aktualizovat v manifestu a projektu. Tato část popisuje, kde nastavit příslušné vlastnosti.

1. Vyberte **projektu > vlastnosti** nabídce příkaz a pak vyberte **aplikace** kartu.

1. V **název sestavení** pole, zadejte jedinečný identifikátor balíčku.

    > [!Important]
    > Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo cokoli, co můžete hostovat používáte. Pro Tento názorný postup doporučujeme, abyste pozdějším kroku publikování provádění balíček veřejně viditelné (i když nepravděpodobné, že kdo bude ve skutečnosti použít) včetně "Ukázkový" nebo "Test" v názvu.
    >
    > Při pokusu publikovat balíček s názvem, který již existuje, se zobrazí chyba.

1. Vyberte **informace o sestavení...**  tlačítko, kterým se zobrazí dialogové okno, ve kterém můžete zadat další vlastnosti, které přenášejí do manifestu (viz [odkaz na soubor souboru .nuspec – nahrazení tokeny](../reference/nuspec.md#replacement-tokens)). Nejčastěji používané pole jsou **Title**, **popis**, **společnosti**, **Copyright**, a **verze sestavení**. Tyto vlastnosti se zobrazí nakonec součástí vašeho balíčku na hostiteli, jako je nuget.org, proto se ujistěte, že jsou plně popisný.

    ![Informace o sestavení v rozhraní .NET Framework projektu v sadě Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Volitelné: Chcete-li zobrazit a upravit vlastnosti přímo, otevřete `Properties/AssemblyInfo.cs` soubor v projektu.

1. Když jsou nastaveny vlastnosti, nastavte konfiguraci projektu **vydání** a znovu sestavte projekt se vygenerovat aktualizované knihovny DLL.

## <a name="generate-the-initial-manifest"></a>Generovat manifest počáteční

S knihovnou DLL v sadě vlastností a projekt, můžete teď použít `nuget spec` příkazu vygenerujte počáteční `.nuspec` soubor z projektu. Tento krok zahrnuje relevantní nahrazení tokeny k vykreslení informace ze souboru projektu.

Spuštění `nuget spec` jen jednou pro generování počátečního manifestu. Při aktualizaci balíčku, můžete buď změnit hodnoty ve vašem projektu, nebo přímo upravit manifest.

1. Otevřete příkazový řádek a přejděte do složky projektu obsahujícího `AppLogger.csproj` souboru.

1. Spusťte následující příkaz: `nuget spec AppLogger.csproj`. Zadáním projektu NuGet vytvoří manifest, který odpovídá názvu projektu, v tomto případě `AppLogger.nuspec`. Také zahrnovat nahrazení tokeny v manifestu.

1. Otevřít `AppLogger.nuspec` v textovém editoru a zkontrolujte jeho obsah, který by měl vypadat následovně:

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Upravit manifest

1. NuGet dojde k chybě při pokusu vytvořit balíček s výchozími hodnotami v vaše `.nuspec` souboru, proto je nutné upravit následující pole, než budete pokračovat. V tématu [odkaz na soubor souboru .nuspec – elementy volitelná metadata](../reference/nuspec.md#optional-metadata-elements) popis jak používají.

    - LicenseUrl
    - ProjectUrl
    - IconUrl
    - ReleaseNotes
    - značky

1. Balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost **značky** vlastnost, protože značky pomoci ostatním najít váš balíček na zdroje, jako je nuget.org a pochopit jeho význam.

1. Můžete také přidat další prvky do manifestu v tuto chvíli, jak je popsáno v [odkaz na soubor souboru .nuspec](../reference/nuspec.md).

1. Uložte soubor předtím, než budete pokračovat.

## <a name="run-the-pack-command"></a>Spusťte příkaz pack

1. Na příkazovém řádku ve složce obsahující váš `.nuspec` souboru, spusťte příkaz `nuget pack`.

1. Generuje NuGet `.nupkg` souboru ve formě *identifikátor version.nupkg*, které zjistíte v aktuální složce.

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile budete mít `.nupkg` souboru, ji publikujete do nuget.org pomocí `nuget.exe` pomocí klíče rozhraní API získaných z nuget.org. Pro nuget.org je nutné použít `nuget.exe` 4.1.0 nebo vyšší.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získat klíč rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikování pomocí nuget nasdílení změn

1. Změnit na složku obsahující `.nupkg` souboru.

1. Spusťte následující příkaz, zadávání názvu balíčku a nahraďte hodnotu klíče svůj klíč rozhraní API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe zobrazuje výsledky procesu publikování:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Zobrazit [nuget nabízených](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Publikování chyby

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikované balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../create-packages/publish-a-package.md)
- [Balíčky v předběžné verzi](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových platforem](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
