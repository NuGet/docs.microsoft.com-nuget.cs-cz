---
title: Cílení na více platforem pro balíčky NuGet
description: Popis různých metod cílit na více verzí rozhraní .NET Framework z v rámci jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: c59839240935e2a6c590dea3adf623313f79f02f
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981142"
---
# <a name="supporting-multiple-net-framework-versions"></a>Podpora více verzí rozhraní .NET framework

*Pro projekty .NET Core pomocí nástroje NuGet 4.0 +, naleznete v tématu [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md) podrobnosti o cílení na různé.*

Mnoho knihoven mířila na konkrétní verzi rozhraní .NET Framework. Například může mít jednu verzi knihovny, která je specifická pro UPW a jinou verzi, která využívá funkce sady rozhraní .NET Framework 4.6.

Aby se tomuto, podporuje NuGet uvedení více verzí stejného knihovny v jediném balíčku, při použití založené na konvenci pracovní adresář metody popsané v [vytvoření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).

## <a name="framework-version-folder-structure"></a>Struktura složek verzi rozhraní Framework

Při vytváření balíčku, který obsahuje pouze jednu verzi knihovny nebo cílové více rozhraní, byste vždy měli vytvořit podsložky `lib` názvy jiné rozhraní malá a velká písmena pomocí následující konvence:

    lib\{framework name}[{version}]

Úplný seznam podporovaných názvy, najdete v článku [odkazovat na cílové rozhraní](../reference/target-frameworks.md#supported-frameworks).

Nikdy byste měli mít verzi knihovny, které nejsou specifické pro architekturu a umístěný přímo v kořenovém adresáři `lib` složky. (Tato možnost je podporován pouze s `packages.config`). Mohlo by nastavit knihovnu jako kompatibilní s žádné cílové rozhraní framework a umožňují, aby byl nainstalován kdekoli, pravděpodobně výsledkem neočekávané běhové chyby. Přidávání sestavení do kořenové složky (například `lib\abc.dll`) nebo v jejích podsložkách (například `lib\abc\abc.dll`) je zastaralá a je ignorován při použití formátu PackagesReference.

Například následující strukturu složek podporuje čtyři verze sestavení, které jsou specifické pro architekturu:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Snadno zahrnout všechny tyto soubory při sestavování balíčku, použít k rekurzivnímu `**` zástupných znaků v `<files>` část vaší `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Složky specifické pro architekturu

Pokud máte specifické pro architekturu sestavení, to znamená, samostatné sestavení, které se zaměřují ARM, x 86 a x64, je nutné je umístit do složky s názvem `runtimes` do podsložky s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native`. Například následující strukturu složek by odpovídala knihovny DLL nativního a spravovaného cílení na Windows 10 a `uap10.0` framework:

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

Tato sestavení budou k dispozici pouze v době běhu, takže pokud byste chtěli poskytnout odpovídající kompilace čas sestavení a potom mít `AnyCPU` sestavení v `/ref{tfm}` složky. 

Všimněte si, že NuGet vždy vybere těmito kompilace nebo runtime prostředky z jedné složky, pokud existují nějaké kompatibilní assety z `/ref` pak `/lib` ignorují se přidání sestavení v době kompilace. Podobně pokud existují nějaké assety kompatibilní z `/runtime` pak také `/lib` pro modul runtime bude ignorován.

Naleznete v tématu [vytvoření balíčků UPW](../guides/create-uwp-packages.md) příklad odkazování na tyto soubory `.nuspec` manifestu.

Viz také [balení komponent aplikace Windows store pomocí NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Odpovídající verze sestavení a Cílová architektura, která v projektu

NuGet nainstaluje balíček, který má více verzí sestavení, pokusí se vyhledat název rozhraní sestavení s cílovou architekturu projektu.

Pokud není nalezena shoda, zkopíruje NuGet sestavení nejvyšší verze, která je menší než nebo rovna cílové rozhraní projektu, pokud je k dispozici. Pokud se nenajde žádné kompatibilní sestavení, NuGet vrátí příslušnou chybovou zprávu.

Zvažte například následující strukturu složky v balíčku:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Při instalaci tohoto balíčku v projektu, který cílí na rozhraní .NET Framework 4.6, NuGet nainstaluje sestavení v `net45` složky, protože to je nejvyšší dostupná verze, která je menší než nebo rovna 4.6.

Pokud projekt cílí na rozhraní .NET Framework 4.6.1, na druhé straně NuGet nainstaluje sestavení v `net461` složky.

Pokud projekt cílí na rozhraní .NET framework 4.0 a starší, vyvolá NuGet příslušnou chybovou zprávu pro nenašli kompatibilní sestavení.

## <a name="grouping-assemblies-by-framework-version"></a>Seskupení sestavení ve verzi rozhraní framework

NuGet zkopíruje sestavení ze složky v balíčku pouze jediná knihovna. Předpokládejme například, že balíček má následující strukturu složek:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Při instalaci balíčku v projektu, který cílí na rozhraní .NET Framework 4.5, `MyAssembly.dll` (v2.0) je pouze sestavení nainstalována. `MyAssembly.Core.dll` (verze 1.0) není nainstalována, protože není uveden v `net45` složky. NuGet chová tímto způsobem, protože `MyAssembly.Core.dll` může mít sloučené do verze 2.0 `MyAssembly.dll`.

Chcete-li `MyAssembly.Core.dll` potřeba instalovat rozhraní .NET Framework 4.5, umístěte kopii `net45` složky.

## <a name="grouping-assemblies-by-framework-profile"></a>Seskupení sestavení v rámci profilu

NuGet také podporuje cílení na konkrétní verzi rozhraní framework profil přidáním spojovníkem a název profilu na konec složce.

    lib\{framework name}-{profile}

Podporované profily jsou následující:

- `client`: Profil klienta
- `full`: Full Profile
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>Určení cíl NuGet

Při balení knihovny, které cílí přenosné knihovny tříd může být složité určit, které se zaměřují NuGet, abyste používali v názvech složek a `.nuspec` souborů, zejména v případě cílení na pouze podmnožinu PCL. Tyto externí prostředky vám pomůžou s tímto:

- [Profily rozhraní v rozhraní .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [Přenosné knihovny tříd profily](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabulka výčet PCL profily a jejich odpovídající cíle NuGet
- [Přenosné knihovny tříd profily nástroj](https://github.com/StephenCleary/PortableLibraryProfiles) (webu github.com): nástroj příkazového řádku pro určení PCL profily k dispozici v systému

## <a name="content-files-and-powershell-scripts"></a>Soubory obsahu a skripty prostředí PowerShell

> [!Warning]
> Jsou k dispozici s měnitelnou soubory obsahu a spuštění skriptu `packages.config` formát pouze; se považují za zastaralé v jiném formátu by se neměl používat pro všechny nové balíčky.

S `packages.config`, obsahu, soubory a skripty prostředí PowerShell můžete seskupit podle cílové rozhraní framework pomocí stejné konvence složky uvnitř `content` a `tools` složek. Příklad:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

Pokud je prázdné složky framework, nebude NuGet přidat odkazy na sestavení nebo soubory obsahu nebo spouštění skriptů prostředí PowerShell pro dané rozhraní.

> [!Note]
> Protože `init.ps1` provádí řešení úrovně a není závislá na projekt, musí být umístěné přímo pod `tools` složky. Pokud je umístěn v rámci složky framework je ignorován.
