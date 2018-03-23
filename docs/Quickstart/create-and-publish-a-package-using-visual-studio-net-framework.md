---
title: "Úvodní příručka k vytváření a publikování balíčku NuGet rozhraní .NET Framework pomocí sady Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Návod kurz týkající se vytváření a publikování Visual Studio 2017 pomocí balíčku NuGet pro rozhraní .NET Framework."
keywords: "Balíček NuGet vytvoření, publikování balíčku NuGet, kurzu NuGet sady Visual Studio vytvořit balíček NuGet, aktualizací Service pack nástroje msbuild"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 613cb6e8cf5762f354d69aa271c1e2f0d4851c97
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-framework"></a>Vytvoření a publikování balíčku pomocí sady Visual Studio (rozhraní .NET Framework)

Vytvoření balíčku NuGet z knihovny tříd rozhraní .NET Framework zahrnuje vytváření knihovny DLL v sadě Visual Studio a potom pomocí nástroje příkazového řádku nuget.exe vytvoření a publikování balíčku.

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte všechny edice Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) s žádným. NET související úlohy. Visual Studio 2017 automaticky zahrnuje NuGet možností při instalaci rozhraní .NET zatížení.

1. Nainstalujte `nuget.exe` CLI stažením z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, `.exe` souboru do složky vhodný, a přidáním této složce do vaší proměnné prostředí PATH.

1. [Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte. Vytvoření nového účtu odešle e-mail s potvrzením. Účet je potřeba zkontrolovat, než můžete nahrát balíček.

## <a name="create-a-class-library-project"></a>Vytvoření projektu knihovny tříd

Můžete použít existující projekt knihovna tříd rozhraní .NET Framework pro kód, který chcete balíček nebo vytvořit jednoduchý takto:

1. V sadě Visual Studio, vyberte **soubor > Nový > projekt**, vyberte **Visual C#** uzlu, vyberte šablonu, "Knihovny tříd (rozhraní .NET Framework)", název projektu AppLogger a klikněte na tlačítko **OK**.

1. Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** a ujistěte se, vytvoření projektu správně. Knihovny DLL nachází v rámci ladění složky (nebo verze, pokud vytváříte tuto konfiguraci místo).

V rámci skutečné balíčku NuGet samozřejmě můžete implementovat řadu užitečných funkcí, se kterými ostatní mohou vytvářet aplikace. Můžete také nastavit cílové rozhraní, ale chcete. Například v tématu příručky pro [UWP](../guides/create-uwp-packages.md) a [Xamarin](../guides/create-packages-for-xamarin.md).

V tomto návodu však nebude napsat další kód, protože knihovny tříd ze šablony, stačí vytvořit balíček. Pokud chcete některé funkční kód pro balíček, stále, použijte tento příkaz:

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
> Pokud nemáte důvod, proč zvolit jinak, .NET Standard je upřednostňovaný cíl pro balíčky NuGet, protože poskytuje kompatibilitu s širokou škálu využívání projekty. V tématu [vytvoření a publikování balíčku pomocí sady Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Konfigurovat vlastnosti projektu pro balíček

Balíček NuGet obsahuje manifest ( `.nuspec` soubor), který obsahuje relevantní metadata, jako je například identifikátor balíčku, číslo verze, popis a další. Některé z těchto lze rozlišovat z vlastností projektu přímo, což zabraňuje samostatně nutnost jejich následné aktualizace v projektu a manifest. Tato část popisuje, kde se má nastavit příslušné vlastnosti.

1. Vyberte **Projekt > vlastnosti** nabídky příkazu a pak vyberte **aplikace** kartě.

1. V **název sestavení** pole, zadejte svůj balíček jedinečný identifikátor.

    > [!Important]
    > Je třeba zadat balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte. Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).
    >
    > Pokud se pokusíte o publikování balíčku s názvem, který již existuje, zobrazí se chyba.

1. Vyberte **informací o sestavení...**  tlačítko, které vyvolá dialogové okno, ve kterém můžete zadat další vlastnosti, které přenášejí do manifestu (viz [odkaz na soubor příponou .nuspec - nahrazení tokeny](../reference/nuspec.md#replacement-tokens)). Nejčastěji používané pole jsou **název**, **popis**, **společnosti**, **Copyright**, a **verze sestavení**. Tyto vlastnosti se zobrazí nakonec součástí vašeho balíčku na hostitele, jako je nuget.org, proto se ujistěte, že jsou k plně popisný.

    ![Informace o sestavení v rozhraní .NET Framework projektu v sadě Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Volitelné: Chcete-li zobrazit a upravit vlastnosti přímo, otevřete `Properties/AssemblyInfo.cs` v projektu.

1. Pokud jsou nastaveny vlastnosti, nastavte konfiguraci projektu na **verze** a znovu sestavte projekt ke generování aktualizované knihovny DLL.

## <a name="generate-the-initial-manifest"></a>Vygenerujte manifest počáteční

S knihovny DLL v dolním a projekt sady vlastností, můžete teď používat `nuget spec` příkazu vygenerujte počáteční `.nuspec` souboru z projektu. Tento krok zahrnuje relevantní nahrazení tokeny k vykreslení informace ze souboru projektu.

Při spuštění `nuget spec` pouze jednou pro generování počátečního manifestu. Při aktualizaci balíčku, můžete buď změnit hodnoty v projektu, nebo přímo upravit v manifestu.

1. Otevřete příkazový řádek a přejděte do složky obsahující projekt `AppLogger.csproj` souboru.

1. Spusťte následující příkaz: `nuget spec AppLogger.csproj`. Zadáním projektu NuGet vytvoří manifestu, který odpovídá názvu projektu, v takovém případě `AppLogger.nuspec`. Zahrnují taky nahrazení tokenů v manifestu.

1. Otevřete `AppLogger.nuspec` v textovém editoru a pomocí něj prozkoumat její obsah, který by měl vypadat takto:

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

## <a name="edit-the-manifest"></a>Upravte manifest

1. NuGet vytvoří chybu, pokud se pokusíte vytvořit balíček s výchozími hodnotami ve vaší `.nuspec` souboru, proto je nutné upravit následující pole, než budete pokračovat. V tématu [odkaz na soubor příponou .nuspec - jednotlivé prvky](../reference/nuspec.md#single-elements) popis toho, jak se používají.

    - licenseUrl
    - projectUrl
    - IconUrl
    - ReleaseNotes
    - značky

1. Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **značky** vlastnosti, jako jsou značky ostatní najít váš balíček na zdroje, jako je nuget.org a co provádí.

1. Můžete také přidat další prvky k manifestu v tuto chvíli, jak je popsáno na [odkaz na soubor příponou .nuspec](../reference/nuspec.md).

1. Uložte soubor předtím, než budete pokračovat.

## <a name="run-the-pack-command"></a>Spusťte příkaz pack

1. Z příkazového řádku v složku, která obsahuje vaše `.nuspec` souboru, spusťte příkaz `nuget pack`.

1. Generuje NuGet `.nupkg` soubor ve formátu *identifikátor version.nupkg*, které zjistíte v aktuální složce.

## <a name="publish-the-package"></a>Umožňuje publikovat balíček

Jakmile máte `.nupkg` souboru ji publikujete pomocí nuget.org `nuget.exe` s klíčem rozhraní API získali z nuget.org. Pro nuget.org je nutné použít `nuget.exe` 4.1.0 nebo vyšší.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získat klíč rozhraní API

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publikování pomocí nabízených nuget

1. Změnit na složku, která obsahuje `.nupkg` souboru.

1. Spusťte následující příkaz, zadáte název balíčku a nahraďte hodnotu klíče klíč rozhraní API:

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

V tématu [nuget nabízené](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Publikování chyby

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Spravovat zveřejněný balíček

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../create-packages/publish-a-package.md)
- [Podpora více cílové rozhraní](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
