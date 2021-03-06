---
title: Návod k obnovení balíčku NuGet pomocí Team Foundation Build
description: Návod, jak obnovit balíček NuGet pomocí nástroje Team Foundation Build (TFS a Visual Studio Team Services).
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 8b993106d439dc137fbe040b51fda373539de81a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774992"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Nastavení obnovení balíčku pomocí Team Foundation Build

Tento článek poskytuje podrobný návod k tomu, jak obnovit balíčky v rámci [sestavení Team Services](/vsts/build-release/index) obou pro správu verzí Git i Team Services.

I když je tento návod specifický pro scénář použití Visual Studio Team Services, koncepce se vztahují také na jiné systémy správy verzí a sestavování.

Platí pro:

- Vlastní projekty MSBuild spuštěné v libovolné verzi TFS
- Team Foundation Server 2012 nebo starší
- Vlastní šablony procesu sestavení Team Foundation migrovány na TFS 2013 nebo novější
- Šablony procesu sestavení s odebranými funkcemi obnovení NuGet

Pokud používáte Visual Studio Team Services nebo Team Foundation Server 2013 se svými šablonami procesu sestavení, automatické obnovení balíčků probíhá jako součást procesu sestavení.

## <a name="the-general-approach"></a>Obecný přístup

Výhodou použití NuGet je, že ho můžete použít k tomu, abyste se vyhnuli vrácení binárních souborů do systému správy verzí.

To je užitečné hlavně v případě, že používáte [distribuovaný systém správy verzí](https://en.wikipedia.org/wiki/Distributed_revision_control) , jako je git, protože vývojáři potřebují klonovat celé úložiště, včetně úplné historie, aby mohli začít pracovat místně. Vracení souborů se změnami může způsobit významné dispozici determinističtější úložiště, protože binární soubory jsou obvykle uložené bez rozdílové komprese.

NuGet podporuje [obnovení balíčků](../consume-packages/package-restore.md) v rámci sestavení po dlouhou dobu. Předchozí implementace obsahovala nevaječný problém pro balíčky, které chtějí tento proces sestavení zvětšit, protože NuGet obnovil balíčky při sestavování projektu. Nástroj MSBuild ale neumožňuje rozšíření sestavení během sestavení; jedna z nich by mohla tvrdí tento problém v nástroji MSBuild, ale mám tvrdí, že se jedná o podstatný problém. V závislosti na tom, který aspekt potřebujete roztáhnout, může být příliš pozdě k registraci v době obnovení balíčku.

K tomuto problému se zajišťují, že se balíčky obnovují jako první krok procesu sestavení:

```cli
nuget restore path\to\solution.sln
```

Když proces sestavení obnoví balíčky před sestavením kódu, nemusíte soubory vracet se změnami `.targets`

> [!Note]
> Balíčky musí být vytvořeny tak, aby umožňovaly načítání v aplikaci Visual Studio. V opačném případě možná budete chtít soubory vrátit se změnami `.targets` , aby ostatní vývojáři mohli jednoduše otevřít řešení bez nutnosti obnovovat balíčky jako první.

Následující ukázkový projekt ukazuje, jak nastavit sestavení tak, aby `packages` složky a `.targets` soubory nemusely být vráceny se změnami. Také ukazuje, jak nastavit automatizované sestavení v Team Foundation Service pro tento vzorový projekt.

## <a name="repository-structure"></a>Struktura úložiště

Náš ukázkový projekt je jednoduchý nástroj příkazového řádku, který používá argument příkazového řádku pro dotazování Bingu. Cílí na .NET Framework 4 a používá mnoho [balíčků BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.NET. http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft. BCL](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft. BCL. Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)a [Microsoft. BCL. Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).

Struktura úložiště vypadá následovně:

```
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
```

Vidíte, že jsme nevrátili do `packages` složky ani do žádného `.targets` souboru.

V případě, že je `nuget.exe` to v průběhu sestavení potřeba, ale jsme vrátili se změnami. Tyto široce používané konvence jsme kontrolovali v rámci sdílené `tools` složky.

Zdrojový kód je pod `src` složkou. I když naše ukázka používá jenom jedno řešení, můžete si snadno představit, že tato složka obsahuje víc než jedno řešení.

### <a name="ignore-files"></a>Ignorování souborů

> [!Note]
> [V klientovi NuGet je aktuálně známá chyba](https://nuget.codeplex.com/workitem/4072) , která způsobuje, že klient bude stále přidávat `packages` složku do správy verzí. Alternativním řešením je zakázat integraci správy zdrojového kódu. Aby to bylo možné, budete potřebovat `Nuget.Config ` soubor ve  `.nuget` složce, která je pro vaše řešení paralelní. Pokud tato složka ještě neexistuje, je nutné ji vytvořit. Do [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) přidejte následující obsah:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Pro komunikaci se správou verzí, kterou nezáměrím vracet se změnami složky **balíčků** , jsme také přidali ignorovat soubory pro Git () i pro `.gitignore` správu verzí TF ( `.tfignore` ). Tyto soubory popisují vzory souborů, které nechcete vrátit se změnami.

`.gitignore`Soubor vypadá takto:

```
syntax: glob
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

`.gitignore`Soubor je [poměrně výkonný](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Například pokud chcete obecně nevracet obsah složky se změnami, `packages` ale chcete se podívat na předchozí pokyny k vrácení `.targets` souborů, které by mohly mít následující pravidlo:

```
packages
!packages/**/*.targets
```

Tím se vyloučí všechny `packages` složky, ale znovu se zahrnou všechny obsažené `.targets` soubory. Způsobem můžete najít šablonu pro `.gitignore` soubory, které jsou speciálně upraveny pro potřeby vývojářů sady Visual Studio. [](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)

Správa verzí TF podporuje velmi podobný mechanismus prostřednictvím souboru [. tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) . Syntaxe je prakticky stejná:

```
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

## <a name="buildproj"></a>sestavení. proj

V naší ukázce udržujeme proces sestavení poměrně jednoduchý. Vytvoříme projekt MSBuild, který sestaví všechna řešení a zajistěte, aby se balíčky obnovily ještě před sestavením řešení.

Tento projekt bude mít tři konvenční cíle `Clean` `Build` a `Rebuild` také nový cíl `RestorePackages` .

- `Build`Cíle a jsou `Rebuild` závislé na `RestorePackages` . Tím zajistíte, že můžete spouštět i `Build` `Rebuild` a spoléhat na obnovené balíčky.
- `Clean``Build`a `Rebuild` vyvolejte odpovídající cíl nástroje MSBuild pro všechny soubory řešení.
- `RestorePackages`Cíl vyvolá `nuget.exe` pro každý soubor řešení. K tomu je možné využít [funkci dávkování MSBuild](/visualstudio/msbuild/msbuild-batching).

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

## <a name="configuring-team-build"></a>Konfigurace týmového sestavení

Týmové sestavení nabízí různé šablony procesů. V této ukázce používáme Team Foundation Service. Místní instalace TFS budou velmi podobné, i když.

Správa verzí Gitu a TF mají jiné šablony sestavení týmu, takže následující kroky se budou lišit v závislosti na tom, který systém správy verzí používáte. V obou případech stačí pouze vybrat sestavit. proj jako projekt, který chcete sestavit.

Nejprve se podívejme na šablonu procesu pro Git. V šabloně založené na Gitu se sestavení vybere prostřednictvím vlastnosti `Solution to build` :

![Proces sestavení pro Git](media/PackageRestoreTeamBuildGit.png)

Všimněte si, že tato vlastnost je umístění v úložišti. Vzhledem k tomu `build.proj` , že se nachází v kořenovém adresáři, stačí použít `build.proj` . Pokud soubor sestavení umístíte do složky s názvem, bude `tools` hodnota `tools\build.proj` .

V šabloně správy verzí TF se projekt vybere prostřednictvím vlastnosti `Projects` :

![Proces sestavení pro TFVC](media/PackageRestoreTeamBuildTFVC.png)

Na rozdíl od šablony založené na Gitu podporuje Správa verzí TF (tlačítko na pravé straně se třemi tečkami). Takže pokud chcete zabránit jakýmkoli chybám při psaní, doporučujeme je použít k výběru projektu.
