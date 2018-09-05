---
title: Návod k obnovení balíčků NuGet s aplikací Team Foundation Build
description: Návod, jak se balíček NuGet restore s pomocí procesu Team Foundation Build (TFS a Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0e69491525fce03e504d9d455bee2718510c83c2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549882"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Nastavení obnovení balíčku s Team Foundation Build

Tento článek poskytuje podrobný návod k obnovení balíčků v rámci [sestavení Team Services](/vsts/build-release/index) i pro Git a správy verzí produktu Team Services.

I když Tento názorný postup je specifické pro scénář, jak pomocí služby Visual Studio Team Services, koncepty také použít další správu verzí a sestavení systémy.

Platí pro:

- Vlastní projekty MSBuild běží na libovolné verzi sady TFS
- Team Foundation Server 2012 nebo starší
- Migrovat vlastní Team Foundation sestavení šablony procesu TFS 2013 nebo novější
- Šablony procesu sestavení odebrat funkce obnovení Nuget

Pokud používáte Visual Studio Team Services nebo Team Foundation Server 2013 s jeho šablony procesu sestavení, balíček automatické obnovení se stane jako součást procesu sestavení.

## <a name="the-general-approach"></a>Je obecný přístup

Výhodou použití NuGet je, že vám pomůže se vyhněte se vracení binárních souborů do systému správy verzí.

To je obzvláště zajímavé, pokud používáte [distribuovanou správu verzí](http://en.wikipedia.org/wiki/Distributed_revision_control) systému, jako je git vzhledem k tomu, že vývojáři potřebují klonovat celé úložiště, včetně úplné historie, než mohou začít pracovat místně. Vracení binárních souborů může způsobit významné úložiště determinističtější jako binární soubory jsou obvykle uložená bez komprese delta.

NuGet má podporované [obnovují se balíčky](../consume-packages/package-restore.md) jako součást sestavení pro dlouho dobou. Předchozí provádění došlo k potížím kuřecí egg pro balíčky, které chcete rozšíření procesu sestavení, protože NuGet obnovit balíčky při vytváření projektu. Však MSBuild neumožňuje rozšíření sestavení během sestavování; jeden může tvrdí, že tento problém v nástroji MSBuild, ale I by tvrdí, že se jedná o problém s vlastní. V závislosti na tom, se kterými aspekty, které potřebujete k rozšiřování může být příliš pozdě pro registraci v době, kdy váš balíček se obnoví.

Léčba tohoto problému je zajistit, že prvním krokem v procesu sestavení obnovení balíčků:

```cli
nuget restore path\to\solution.sln
```

Pokud váš proces sestavení obnoví balíčky před vytvořením kódu, není nutné k vrácení se změnami `.targets` soubory

> [!Note]
> Balíčky musí být vytvořen umožňuje načítání v aplikaci Visual Studio. V opačném případě může stále chcete vrátit se změnami `.targets` soubory tak, aby ostatní vývojáři mohou jednoduše otevřete řešení aniž byste museli nejdřív obnovit balíčky.

Následující ukázkový projekt ukazuje, jak nastavit sestavení takovým způsobem, který `packages` složky a `.targets` soubory nemusí být vrácené se změnami. Také ukazuje, jak nastavit automatické sestavení ve službě Team Foundation Service pro tento ukázkový projekt.

## <a name="repository-structure"></a>Struktura úložiště

Náš ukázkový projekt je jednoduchý příkazového řádku nástroj, který používá argument příkazového řádku pro dotaz Bingu. Cílí na rozhraní .NET Framework 4 a používá mnoho [BCL balíčky](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), a [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

Struktury úložiště by měl vypadat takto:

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

Uvidíte, že jsme nejsou vrácené se změnami `packages` složky ani žádné `.targets` soubory.

Budeme mít, ale vrácené se změnami `nuget.exe` potřeby během sestavení. Následující často používá konvence jsme jsme vrátili ho se změnami v rámci sdílené `tools` složky.

Zdrojový kód je v části `src` složky. I když naše Ukázka používá pouze jedno řešení, snadno dokážete představit, že tato složka obsahuje více než jednoho řešení.

### <a name="ignore-files"></a>Ignorování souborů

> [!Note]
> Aktuálně nejsou k dispozici [známého problému nástroje klienta NuGet](https://nuget.codeplex.com/workitem/4072) , který způsobí, že klient přesto přidat `packages` složky do správy verzí. Alternativní řešení je zakázat integraci správy zdrojového kódu. Chcete-li to mohli udělat, musíte `Nuget.Config ` soubor `.nuget` složku, která je paralelní do vašeho řešení. Pokud tato složka ještě neexistuje, musíte ji vytvořit. V [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), přidejte následující obsah:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Ke komunikaci do správy verzí, že není cílem je vrácení se změnami **balíčky** složek, přidali jsme také ignorovat soubory pro obě git (`.gitignore`) i správa verzí TF (`.tfignore`). Tyto soubory popisují vzory souborů, které nechcete, aby k vrácení se změnami.

`.gitignore` Soubor bude vypadat takto:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

`.gitignore` Soubor [poměrně efektivní](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Například, pokud chcete obecně není vrácení se změnami obsah `packages` složka ale chcete přejít s předchozím pokyny k vrácení se změnami `.targets` souborů může mít následující pravidlo místo:

    packages
    !packages/**/*.targets

To se vyřadit všechny `packages` složky bude znovu zahrnout všechny `.targets` soubory. Tím, jak můžete najít šablonu pro `.gitignore` soubory, které specificky přizpůsobit pro potřeby Visual Studio získávají vývojáři [tady](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Správa verzí TF podporuje plní podobné funkce jako mechanismus prostřednictvím [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) souboru. Syntaxe je v podstatě stejný:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

Pro naši ukázku uchováváme proces sestavení poměrně jednoduché. Vytvoříme projektu MSBuild, který vytváří všechna řešení, přičemž zajistěte, že se balíčky neobnoví před sestavením řešení.

Tento projekt bude mít tři konvenční cíle `Clean`, `Build` a `Rebuild` i nový cíl `RestorePackages`.

- `Build` a `Rebuild` cíle i závisí na `RestorePackages`. Tím je zajištěno, že oba spustíte `Build` a `Rebuild` a Spolehněte se na balíčky, který se má obnovit.
- `Clean`, `Build` a `Rebuild` vyvolání odpovídající cíle MSBuild na všechny soubory řešení.
- `RestorePackages` Vyvolá cíl `nuget.exe` pro každý soubor řešení. To lze provést pomocí [funkce v dávkování nástroje MSBuild](/visualstudio/msbuild/msbuild-batching).

Výsledek by měl vypadat takto:

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

Týmový Build nabízí různé šablony procesu. Pro tuto ukázku jsme používáte Team Foundation Service. I když bude velmi podobně jako na místní instalace TFS.

Git a správa verzí TF mají různé šablony služby Team Build, takže takto se budou lišit v závislosti na tom, který systém správy verzí, kterou používáte. V obou případech se vše, co potřebujete je výběr build.proj jako projekt, který má být sestaveno.

Nejprve Podívejme se na šablonu procesu pro git. V šabloně git na základě výběru sestavení prostřednictvím vlastnosti `Solution to build`:

![Proces sestavení pro git](media/PackageRestoreTeamBuildGit.png)

Všimněte si, že je tato vlastnost umístění v úložišti. Protože naše `build.proj` je v kořenovém adresáři, můžeme jednoduše použít `build.proj`. Pokud byste umístit soubor sestavení v rámci složky s názvem `tools`, bude hodnota `tools\build.proj`.

V šabloně ovládacího prvku verze TF je projekt určen prostřednictvím vlastnosti `Projects`:

![Proces sestavení pro TFVC](media/PackageRestoreTeamBuildTFVC.png)

Na rozdíl od TF git na základě šablony Správa verzí podporuje výběrech (tlačítko na pravé straně se třemi tečkami). Proto pokud se chcete vyhnout chybám psaní doporučujeme, že pomocí kterých lze vyberte projekt.
