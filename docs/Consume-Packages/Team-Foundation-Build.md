---
title: Návod balíček NuGet obnovit pomocí aplikace Team Foundation Build | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Návod, jak balíček NuGet obnovení s Team Foundation Build (sady TFS a Visual Studio Team Services).
keywords: Obnovení balíčku NuGet, NuGet a sady TFS, NuGet a služby VSTS, systémy sestavení NuGet, team foundation build, vlastní projektů MSBuild cloudu, nepřetržité integrace sestavení
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f46a7402214bf965918a5195605027913a8c60c2
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Nastavení obnovení balíčků s Team Foundation Build

Tento článek obsahuje podrobný návod k obnovení balíčků jako součást [Team Services Build](/vsts/build-release/index) i pro Git a správě verzí Team Services.

I když Tento názorný postup je specifická pro scénář použití Visual Studio Team Services, koncepty také použít pro další ovládací prvek verze a sestavit systémy.

Platí pro:

- Vlastní projektů MSBuild spuštěna v libovolné verzi sady TFS
- Team Foundation Server 2012 nebo starším
- Vlastní Team Foundation sestavení šablony procesů migrovat do sady TFS 2013 nebo novější
- Šablony procesu sestavení odebrané funkce obnovení Nuget

Pokud používáte Visual Studio Team Services nebo Team Foundation Server 2013 s jeho šablony procesu sestavení, se stane balíček automatické obnovení jako součást procesu sestavení.

## <a name="the-general-approach"></a>Obecný přístup

Výhodou použití NuGet je, že jste ji používat předejdete kontrola v binární soubory do systému správy verzí.

To je zajímavé hlavně, pokud používáte [distribuované verzí](http://en.wikipedia.org/wiki/Distributed_revision_control) systému jako git, protože vývojáři muset klonovat celý úložiště, včetně úplnou historii, před spuštěním lokálně. Kontrola v binárních souborech může způsobit významné úložiště tomu, jak binární soubory se obvykle ukládají bez rozdílů komprese.

Obsahoval podporované NuGet [obnovují se balíčky](../consume-packages/package-restore.md) jako součást sestavení pro typ long čas nyní. Předchozí implementace došlo k potížím kuřecí a vaječných pro balíčky, které chcete rozšíření procesu sestavení, protože NuGet při sestavování projektu obnovení balíčků. Ale MSBuild neumožňuje rozšíření sestavení během vytváření sestavení; jeden může uvádějí, které tento problém v nástroji MSBuild, ale I by uvádějí, že se jedná o problém s vyplývajících. V závislosti na tom, které aspekt potřebujete rozšířit může být příliš pozdní registrovat, a v době obnovení vašeho balíčku.

Vytvrdit tento problém je ubezpečit, že jsou balíčky obnovit jako první krok v procesu sestavení:

```cli
nuget restore path\to\solution.sln
```

Když váš proces sestavení obnoví balíčky před vytvořením kód, nepotřebujete k vrácení se změnami `.targets` soubory

> [!Note]
> Balíčky musí být vytvořené umožňuje načítání v sadě Visual Studio. Jinak, může stále chcete vrátit se změnami `.targets` soubory, aby ostatní vývojáři mohli jednoduše otevřít řešení bez nutnosti nejprve obnovení balíčků.

Následující ukázkový projekt ukazuje, jak nastavit sestavení takovým způsobem, který `packages` složky a `.targets` soubory nemusí být vráceno se změnami. Také ukazuje, jak nastavit automatické sestavení na Team Foundation Service pro tento ukázkový projekt.

## <a name="repository-structure"></a>Struktura úložiště

Naše ukázkový projekt je nástroj jednoduché příkazového řádku, který používá argument příkazového řádku k dotazu služby Bing. Jeho cílem rozhraní .NET Framework 4 a používá řadu [BCL balíčky](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), a [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

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

Uvidíte, že jsme nebyly vráceno se změnami `packages` složku ani žádný `.targets` soubory.

Jsme k dispozici, ale vráceno se změnami `nuget.exe` potřeby během sestavení. Následující často používají konvence jsme jste změnami ji pod sdílenou `tools` složky.

Zdrojový kód je v části `src` složky. I když naše Ukázka používá jenom jedno řešení, můžete snadno představte, že tato složka obsahuje více než jedno řešení.

### <a name="ignore-files"></a>Ignorování souborů

> [!Note]
> V současné době není [známého problému v klientovi NuGet](https://nuget.codeplex.com/workitem/4072) který způsobuje, že klient stále přidat `packages` složky do správy verzí. Alternativní řešení je zakázat integrace ovládacích prvků zdrojového. Aby bylo možné provést, je nutné `Nuget.Config ` v soubor `.nuget` složky, která je paralelní k řešení. Pokud tato složka ještě neexistuje, musíte ji vytvořit. V [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), přidejte do něj následující obsah:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Pro komunikaci se správa verzí, že nepodporujeme záměr vrácení se změnami **balíčky** složek, jsme také doplnili ignorovat soubory pro oba git (`.gitignore`) a také TF správy verzí (`.tfignore`). Tyto soubory popisují vzorů souborů, které nechcete použít k vrácení se změnami.

`.gitignore` Souboru vypadá takto:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

`.gitignore` Soubor [velmi výkonné](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Například, pokud chcete obecně není vrácení se změnami obsah `packages` složka ale chcete přejít s předchozí pokyny k vrácení se změnami `.targets` soubory můžete mít následující pravidlo místo:

    packages
    !packages/**/*.targets

To vyloučí všechny `packages` složky ale bude znovu zahrnout všechny obsažené `.targets` soubory. Tím, můžete najít šablonu pro `.gitignore` soubory, které je specificky přizpůsobit pro potřeby vývojářů Visual Studio [zde](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Správa verzí TF podporuje velmi podobné mechanismus prostřednictvím [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) souboru. Syntaxe je v podstatě stejný:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

Pro naše ukázka jsme zjednodušení procesu sestavení poměrně. Vytvoříme projektu MSBuild, který sestavuje všechny řešení při a ujistěte se, že jsou balíčky obnovit před vytvořením řešení.

Tento projekt bude mít tři konvenční cíle `Clean`, `Build` a `Rebuild` i nový cíl `RestorePackages`.

- `Build` a `Rebuild` cíle obě závisí na `RestorePackages`. Tím je zajištěno, že oba spuštěním `Build` a `Rebuild` a spoléhá na balíčky obnovena.
- `Clean`, `Build` a `Rebuild` vyvolání odpovídající cíle MSBuild na všechny soubory řešení.
- `RestorePackages` Cíl vyvolá `nuget.exe` pro každý soubor řešení. To se dá udělat pomocí [je dávkování nástroje MSBuild funkce](/visualstudio/msbuild/msbuild-batching).

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

## <a name="configuring-team-build"></a>Konfigurace sestavení Team

Sestavení Team nabízí různé šablony procesů. Pro této ukázce používáme Team Foundation Service. Když bude velmi podobně jako na místní instalace sady TFS.

Git a správa verzí TF mít různé šablony Team Build, následující postup se bude lišit v závislosti na tom, které systém správy verzí, kterou používáte. V obou případech je třeba je výběr build.proj jako projekt, který chcete vytvořit.

První Podíváme se na šablony procesu pro git. V šabloně git na základě sestavení je vybrána přes vlastnost `Solution to build`:

![Proces sestavení pro git](media/PackageRestoreTeamBuildGit.png)

Upozorňujeme, že je tato vlastnost umístění v úložišti. Protože naše `build.proj` je v kořenovém adresáři, můžeme jednoduše použít `build.proj`. Pokud umístěte soubor sestavení do složky s názvem `tools`, bude hodnota `tools\build.proj`.

V šabloně TF verze ovládací prvek je vybrán projekt přes vlastnost `Projects`:

![Proces sestavení pro TFVC](media/PackageRestoreTeamBuildTFVC.png)

Na rozdíl od git na základě šablony TF podporuje Správa verzí ovládacích prvků výběr (tlačítko na pravé straně tři tečky). Takže aby se zabránilo chybám zadáním doporučujeme že použít vyberte projekt.
