---
title: Cílení na více verzí pro balíčky NuGet
description: Popis různých metod k cílení na více verzí rozhraní .NET Framework z v rámci jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: 429b9743ea678cd500b6f51630d03aac7812441e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816953"
---
# <a name="supporting-multiple-net-framework-versions"></a>Podpora více verzí rozhraní .NET framework

*Projekty .NET Core pomocí nástroje NuGet 4.0 +, najdete v části [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md) podrobnosti o cílení na více verzí.*

Mnoho knihovny cílení na konkrétní verzi rozhraní .NET Framework. Například můžete mít jednu verzi knihovnu, která je specifická pro UPW a jinou verzi, která využívá funkce v rozhraní .NET Framework 4.6.

Pro přizpůsobení, podporuje NuGet uvedení více verzí stejnou knihovnu v jeden balíček, při použití založené na konvenci pracovní adresář metoda popsaná v [vytváření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).

## <a name="framework-version-folder-structure"></a>Struktura složek Framework verze

Při vytváření balíčku, který obsahuje pouze jednu verzi knihovny nebo cílové více rozhraní, je vytvořit podsložky `lib` pomocí různých malá a velká písmena framework názvy následující konvence:

    lib\{framework name}[{version}]

Úplný seznam podporovaných názvy, najdete v článku [odkazovat na cílové rozhraní](../reference/target-frameworks.md#supported-frameworks).

Nikdy byste měli mít verzi knihovny, které nejsou specifické pro rozhraní a umístěný přímo v kořenu `lib` složky. (Tato možnost se podporuje jenom s `packages.config`). To by upravit knihovny kompatibilní se žádné cílové rozhraní a povolit, aby byl nainstalován odkudkoli, pravděpodobně vést k chybám za běhu neočekávané. Přidání sestavení v kořenové složce (například `lib\abc.dll`) nebo v jejich podsložkách (například `lib\abc\abc.dll`) se už nepoužívá a je ignorována, pokud v PackagesReference formátu.

Například následující strukturu složek podporuje čtyři verze sestavení, které jsou specifické pro framework:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Při vytváření balíčku snadno zahrnout všechny tyto soubory, použijte rekurzivního `**` zástupný znak v `<files>` část vaší `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Architektura konkrétní složky

Pokud máte specifické pro architekturu sestavení, to znamená, samostatné sestavení, které cílí ARM, x 86 a x64, můžete je nutné umístit do složky s názvem `runtimes` v rámci dílčí složky s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native`. Například následující strukturu složek by zohlednit nativní a spravovaná knihovny DLL cílení na Windows 10 a `uap10.0` framework:

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

V tématu [vytvořit balíčky UWP](../guides/create-uwp-packages.md) příklad odkazující na tyto soubory v `.nuspec` manifest.

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Odpovídající verze sestavení a cílové rozhraní v projektu

Když NuGet nainstaluje balíček, který má více verzí sestavení, pokusí se shodovat s názvem framework sestavení s cílový framework projektu.

Pokud není nalezena shoda, zkopíruje NuGet sestavení pro nejvyšší verzi, která je menší než nebo rovno cílový framework projektu na, pokud je k dispozici. Pokud se nenajde žádné kompatibilní sestavení, vrátí NuGet příslušná chybová zpráva.

Zvažte například následující strukturu složek v balíčku:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Pokud při instalaci tohoto balíčku do projektu, jehož cílem rozhraní .NET Framework 4.6, NuGet nainstaluje sestavení v `net45` složky, protože se jedná o nejvyšší verzi k dispozici, která je menší než nebo rovna 4.6.

Pokud projekt cílem rozhraní .NET Framework 4.6.1, na druhé straně NuGet nainstaluje sestavení v `net461` složky.

Pokud projekt cílem rozhraní .NET framework 4.0 a starší, vyvolá NuGet příslušná chybová zpráva pro nemůžete najít kompatibilní sestavení.

## <a name="grouping-assemblies-by-framework-version"></a>Seskupování podle framework, verze sestavení

NuGet zkopíruje sestavení ze pouze jediná knihovna složky v balíčku. Předpokládejme například, že balíček má následující strukturu složek:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Při instalaci balíčku v projektu, jehož cílem rozhraní .NET Framework 4.5, `MyAssembly.dll` (v2.0) je nainstalována pouze sestavení. `MyAssembly.Core.dll` (verze 1.0) není nainstalována, protože není uveden ve `net45` složky. NuGet chová tímto způsobem, protože `MyAssembly.Core.dll` může mít sloučené do verze 2.0 `MyAssembly.dll`.

Chcete-li `MyAssembly.Core.dll` k instalaci pro rozhraní .NET Framework 4.5, umístěte kopii v `net45` složky.

## <a name="grouping-assemblies-by-framework-profile"></a>Seskupení sestavení profilem framework

Cílení na konkrétní framework profil připojením pomlčkou a název profilu na konec složce podporuje také NuGet.

    lib\{framework name}-{profile}

Podporované profily jsou následující:

- `client`: Profil klienta
- `full`: Full Profile
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>Určení, který NuGet cíle použít

Při vytváření balíčků knihovny cílení na přenosné knihovny tříd může být složité určit, který NuGet cílový ve složce názvy byste měli používat a `.nuspec` souboru, zvlášť pokud cílení jenom podmnožinu PCL. Následující externí prostředky vám pomůže s tímto:

- [Profily Framework v rozhraní .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [Přenosná knihovna tříd profily](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabulka výčtu PCL profily a jejich ekvivalent cíle NuGet
- [Přenosná knihovna tříd profily nástroj](https://github.com/StephenCleary/PortableLibraryProfiles) (webu github.com): nástroj příkazového řádku pro určení PCL profilů dostupných v systému

## <a name="content-files-and-powershell-scripts"></a>Soubory obsahu a skriptů prostředí PowerShell

> [!Warning]
> Měnitelný soubory obsahu a spouštění skriptů jsou k dispozici `packages.config` formát pouze; se nepoužívají v jiném formátu a by nemělo být použito pro všechny nové balíčky.

S `packages.config`, obsahu, soubory a skripty prostředí PowerShell lze seskupovat podle cílové rozhraní, pomocí stejné konvence složky uvnitř `content` a `tools` složek. Příklad:

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

Pokud složku rozhraní je prázdné, není NuGet přidejte odkazy na sestavení nebo soubory obsahu nebo spuštění skriptů prostředí PowerShell dané platformy.

> [!Note]
> Protože `init.ps1` se spustí v řešení úrovně a není závislá na projekt, je nutné ji umístit přímo pod `tools` složky. Pokud se umístit pod složku rozhraní je ignorován.
