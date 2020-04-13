---
title: Návod obnovení balíčku NuGet s sestavením team foundation
description: Návod, jak NuGet balíček obnovit s Team Foundation Build (TFS a Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73611006"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Nastavení obnovení balíčku pomocí team foundation buildu

Tento článek obsahuje podrobný návod, jak obnovit balíčky jako součást [team services sestavení](/vsts/build-release/index) obou, pro Git a Team Services version control.

Přestože tento návod je specifický pro scénář použití Visual Studio Team Services, koncepty platí také pro jiné verze správy a sestavení systémů.

Platí pro:

- Vlastní projekty MSBuild spuštěné v libovolné verzi tfs
- Team Foundation Server 2012 nebo starší
- Šablony procesů sestavení vlastní hospo- základy Team Foundation migrované na TFS 2013 nebo novější
- Vytváření šablon procesů s odebranou funkcí obnovení nugetu

Pokud používáte Visual Studio Team Services nebo Team Foundation Server 2013 s jeho šablony procesu sestavení, automatické obnovení balíčků se stane jako součást procesu sestavení.

## <a name="the-general-approach"></a>Obecný přístup

Výhodou použití NuGet je, že můžete použít, aby se zabránilo vrácení binárních souborů v systému správy verzí.

To je obzvláště zajímavé, pokud používáte [distribuovaný](https://en.wikipedia.org/wiki/Distributed_revision_control) systém správy verzí, jako je git, protože vývojáři potřebují klonovat celé úložiště, včetně úplné historie, než mohou začít pracovat místně. Vrácení binárních souborů se změnami může způsobit významné nafouknutí úložiště, protože binární soubory jsou obvykle uloženy bez rozdílové komprese.

NuGet podporuje [obnovení balíčků](../consume-packages/package-restore.md) jako součást sestavení po dlouhou dobu. Předchozí implementace měla problém kuře a vejce pro balíčky, které chcete rozšířit proces sestavení, protože NuGet obnovené balíčky při vytváření projektu. MSBuild však neumožňuje rozšíření sestavení během sestavení; dalo by se tvrdit, že tento problém v MSBuild, ale já bych tvrdit, že se jedná o vlastní problém. V závislosti na tom, který aspekt je třeba prodloužit, může být příliš pozdě na registraci v době, kdy je balíček obnoven.

Lékna tento problém je ujistit se, že balíčky jsou obnoveny jako první krok v procesu sestavení:

```cli
nuget restore path\to\solution.sln
```

Když proces sestavení obnoví balíčky před vytvořením kódu, nemusíte `.targets` soubory vrácení se změnami

> [!Note]
> Balíčky musí být vytvořen, aby bylo možné načítat v sadě Visual Studio. V opačném případě můžete stále `.targets` chtít vrátit soubory se změnami, aby ostatní vývojáři mohli jednoduše otevřít řešení bez nutnosti nejprve obnovit balíčky.

Následující ukázkový projekt ukazuje, jak nastavit sestavení tak, aby `packages` složky a `.targets` soubory není nutné se změnami. Také ukazuje, jak nastavit automatické sestavení služby Team Foundation pro tento ukázkový projekt.

## <a name="repository-structure"></a>Struktura úložiště

Náš demo projekt je jednoduchý nástroj příkazového řádku, který používá argument příkazového řádku k dotazování Bingu. Zaměřuje se na rozhraní .NET Framework 4 a používá mnoho [balíčků BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)a [Microsoft.Bcl.Build).](https://www.nuget.org/packages/Microsoft.Bcl.Build)

Struktura úložiště vypadá takto:

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

Můžete vidět, že jsme nezkontrolovali `packages` složku ani `.targets` žádné soubory.

Máme však zkontrolovat- jak `nuget.exe` je potřeba během sestavení. Po široce používaných konvencích jsme je `tools` zkontrolovali ve sdílené složce.

Zdrojový kód je `src` ve složce. Ačkoli naše demo používá pouze jediné řešení, můžete si snadno představit, že tato složka obsahuje více než jedno řešení.

### <a name="ignore-files"></a>Ignorování souborů

> [!Note]
> V klientovi NuGet je aktuálně [známá chyba,](https://nuget.codeplex.com/workitem/4072) která `packages` způsobí, že klient stále přidá složku do správy verzí. Řešení je zakázat integraci správy zdrojového kódu. Chcete-li to provést, `Nuget.Config ` potřebujete soubor `.nuget` ve složce, která je rovnoběžná s vaším řešením. Pokud tato složka ještě neexistuje, musíte ji vytvořit. V [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), přidejte následující obsah:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Chcete-li sdělit správu verzí, že nemáme v úmyslu zařazovat složky balíčků se **změnami,** přidali jsme také soubory ignorování pro git (`.gitignore`) i pro správu verzí TF (`.tfignore`). Tyto soubory popisují vzory souborů, které nechcete se změnami.

Soubor `.gitignore` vypadá takto:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

Soubor `.gitignore` je [poměrně silný](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Chcete-li například obecně nevrátit obsah `packages` složky se změnami, ale chcete použít `.targets` předchozí pokyny pro vrácení souborů se změnami, můžete mít místo toho následující pravidlo:

    packages
    !packages/**/*.targets

Tím se `packages` vyloučí všechny složky, ale znovu zahrnete všechny obsažené `.targets` soubory. Mimochodem, můžete najít šablonu `.gitignore` pro soubory, která je speciálně přizpůsobena potřebám vývojářů sady Visual Studio [zde](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Tf verze řízení podporuje velmi podobný mechanismus prostřednictvím souboru [.tfignore.](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) Syntaxe je prakticky stejná:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

Pro naše demo, udržujeme proces sestavení poměrně jednoduché. Vytvoříme projekt MSBuild, který vytvoří všechna řešení a zároveň zajistí, že balíčky jsou obnoveny před sestavením řešení.

Tento projekt bude mít `Clean`tři `Build` `Rebuild` konvenční cíle a `RestorePackages`také nový cíl .

- A `Build` `Rebuild` cíle jsou `RestorePackages`závislé na . Tím zajistíte, že `Build` můžete `Rebuild` spustit a spoléhat na balíčky, které jsou obnoveny.
- `Clean`a `Build` `Rebuild` vyvolat odpovídající cíl MSBuild ve všech souborech řešení.
- Cíl `RestorePackages` vyvolá `nuget.exe` pro každý soubor řešení. Toho lze dosáhnout pomocí [funkce dávkování msbuild](/visualstudio/msbuild/msbuild-batching).

Výsledek vypadá takto:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>Konfigurace sestavení týmu

Team Build nabízí různé šablony procesů. Pro tuto demonstraci používáme službu Team Foundation Service. Místní instalace TFS bude velmi podobné ačkoli.

Git a TF Version Control mají různé šablony team buildu, takže následující kroky se budou lišit v závislosti na tom, který systém správy verzí používáte. V obou případech vše, co potřebujete, je vybrat build.proj jako projekt, který chcete sestavit.

Nejprve se podívejme na šablonu procesu pro git. V šabloně založené na gitu `Solution to build`je sestavení vybráno pomocí vlastnosti :

![Proces sestavení pro git](media/PackageRestoreTeamBuildGit.png)

Vezměte prosím na vědomí, že toto zařízení je místem ve vašem úložišti. Vzhledem `build.proj` k tomu, naše `build.proj`je v kořeni, jsme prostě použili . Pokud umístíte soubor sestavení pod `tools`složku s `tools\build.proj`názvem , bude hodnota .

V šabloně správy verzí TF je `Projects`projekt vybrán prostřednictvím vlastnosti :

![Proces sestavení pro TFVC](media/PackageRestoreTeamBuildTFVC.png)

Na rozdíl od git založené šablony podporuje ovládací prvek verze TF výběr (tlačítko na pravé straně se třemi tečkami). Aby chomáč chyb y jejich zadání doporučujeme použít k výběru projektu.
