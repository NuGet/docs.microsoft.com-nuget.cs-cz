---
title: Cílení na více platforem pro balíčky NuGet
description: Popis různých metod, které cílí na více .NET Framework verzí z jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 7c0da38ab4059b89c9693ecbece2bc8ed1a775ec
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237942"
---
# <a name="support-multiple-net-versions"></a>Podpora více verzí rozhraní .NET

Mnoho knihoven cílí na konkrétní verzi .NET Framework. Například můžete mít jednu verzi knihovny, která je specifická pro UWP, a další verzi, která využívá funkce v .NET Framework 4,6. Aby to bylo možné, NuGet podporuje vložení více verzí stejné knihovny do jednoho balíčku.

Tento článek popisuje rozložení balíčku NuGet bez ohledu na to, jak je sestaven balíček nebo sestavení (to znamená, že rozložení je stejné, ať už používáte více souborů *. csproj* , které NEPOUŽÍVAJÍ sadu SDK, a vlastní soubor *. nuspec* , nebo jeden pro více cílených sad SDK-Style *. csproj* ). Pro projekt ve stylu sady SDK zná [cíle sady](../reference/msbuild-targets.md) NuGet, jak musí být balíček layed a automatizuje vložení sestavení do správných složek lib a vytváření skupin závislostí pro každou cílovou architekturu (TFM). Podrobné pokyny najdete v tématu [Podpora více .NET Frameworkch verzí v souboru projektu](multiple-target-frameworks-project-file.md).

Pokud používáte metodu pracovního adresáře založenou na konvenci, která je popsaná v tématu [Vytvoření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory), musíte balíček ručně rozložit podle pokynů v tomto článku. Pro projekt ve stylu sady SDK se doporučuje automatizovaná metoda, ale můžete také zvolit ruční rozložení balíčku, jak je popsáno v tomto článku.

## <a name="framework-version-folder-structure"></a>Struktura složek verze rozhraní

Při sestavování balíčku, který obsahuje pouze jednu verzi knihovny nebo cílení na více platforem, je vždy nutné vytvořit podsložky v rámci `lib` používání různých názvů architektury s rozlišováním velkých a malých písmen s následující konvencí:

    lib\{framework name}[{version}]

Úplný seznam podporovaných názvů najdete v [referenčních informacích o cílových rozhraních](../reference/target-frameworks.md#supported-frameworks).

Nikdy byste neměli mít verzi knihovny, která není specifická pro rozhraní a umístěna přímo do kořenové `lib` složky. (Tato schopnost byla podporovaná jenom s `packages.config` .) Díky tomu by knihovna byla kompatibilní s libovolným cílovou architekturou a povolila se její instalace kdekoli, což pravděpodobně způsobí neočekávané chyby za běhu. Přidání sestavení do kořenové složky (například `lib\abc.dll` ) nebo podsložek (například) se už `lib\abc\abc.dll` nepoužívá a při použití formátu PackagesReference se ignoruje.

Například následující struktura složek podporuje čtyři verze sestavení, které jsou specifické pro rozhraní:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Pro snadné zahrnutí všech těchto souborů při sestavování balíčku použijte rekurzivní `**` zástupné znaky v `<files>` části svého `.nuspec` :

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Složky specifické pro architekturu

Pokud máte sestavení pro konkrétní architekturu, tj. samostatná sestavení, která cílí na ARM, x86 a x64, je nutné umístit je do složky s názvem `runtimes` v podsložkách s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native` . Například následující struktura složky by pokryla nativní i spravované knihovny DLL cílící na Windows 10 a `uap10.0` rozhraní:

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

Tato sestavení budou k dispozici pouze za běhu, takže pokud chcete zadat odpovídající sestavení pro čas kompilace a pak mít `AnyCPU` sestavení ve `/ref/{tfm}` složce. 

Počítejte s tím, že NuGet vždy vybere tyto kompilační nebo běhové prostředky z jedné složky, takže pokud existují některé kompatibilní prostředky, ze `/ref` `/lib` kterých bude možné přidat sestavení v době kompilace, bude ignorováno. Podobně platí, že pokud existují některé kompatibilní prostředky, `/runtimes` `/lib` budou také ignorovány pro modul runtime.

Příklady odkazů na tyto soubory v manifestu najdete v tématu věnovaném [Vytvoření balíčků UWP](../guides/create-uwp-packages.md) `.nuspec` .

Viz také [balení komponenty aplikace pro Windows Store pomocí nástroje NuGet](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Vyhovující verze sestavení a cílová architektura v projektu

Když NuGet nainstaluje balíček s více verzemi sestavení, pokusí se porovnat název rozhraní sestavení s cílovou architekturou projektu.

Pokud není nalezena shoda, NuGet zkopíruje sestavení pro nejvyšší verzi, která je menší než nebo rovna cílové verzi rozhraní .NET Framework projektu, je-li k dispozici. Pokud není nalezeno žádné kompatibilní sestavení, NuGet vrátí příslušnou chybovou zprávu.

Zvažte například následující strukturu složek v balíčku:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Při instalaci tohoto balíčku do projektu, který se zaměřuje na .NET Framework 4,6, NuGet nainstaluje sestavení do `net45` složky, protože to je nejvyšší dostupná verze, která je menší nebo rovna 4,6.

Pokud cílíte na projekt .NET Framework 4.6.1, nainstaluje NuGet do `net461` složky sestavení.

Pokud je projekt cílen na rozhraní .NET Framework 4,0 a starší, NuGet vyvolá příslušnou chybovou zprávu pro nalezení kompatibilního sestavení.

## <a name="grouping-assemblies-by-framework-version"></a>Seskupení sestavení podle verze architektury

NuGet kopíruje sestavení z jediné složky knihovny v balíčku. Předpokládejme například, že balíček má následující strukturu složek:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Když je balíček nainstalován v projektu, který cílí na .NET Framework 4,5, `MyAssembly.dll` (v 2.0) je jediné nainstalovaná sestavení. `MyAssembly.Core.dll` (v 1.0) není nainstalováno, protože není uvedeno ve `net45` složce. NuGet se chová tímto způsobem `MyAssembly.Core.dll` , protože se mohl sloučit do verze 2,0 systému `MyAssembly.dll` .

Pokud chcete `MyAssembly.Core.dll` nainstalovat .NET Framework 4,5, umístěte kopii do `net45` složky.

## <a name="grouping-assemblies-by-framework-profile"></a>Seskupení sestavení podle profilu architektury

NuGet také podporuje cílení na konkrétní profil architektury připojením pomlčky a názvu profilu na konec složky.

    lib\{framework name}-{profile}

Podporované profily jsou následující:

- `client`: Profil klienta
- `full`: Úplný profil
- `wp`: Windows Phone
- `cf`: Kompaktní rozhraní

## <a name="declaring-dependencies-advanced"></a>Deklarace závislostí (rozšířené)

Při balení souboru projektu se NuGet pokusí automaticky generovat závislosti z projektu. Informace v této části o použití souboru *. nuspec* k deklaraci závislostí jsou obvykle nezbytné jenom pro pokročilé scénáře.

*(Verze 2.0 +)* Můžete deklarovat závislosti balíčků v *. nuspec* odpovídající cílové architektuře cílového projektu pomocí `<group>` prvků v rámci `<dependencies>` elementu. Další informace naleznete v tématu [závislosti elementu](../reference/nuspec.md#dependencies-element).

Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<dependency>` prvků. Tyto závislosti jsou nainstalovány společně, pokud je cílový rámec kompatibilní s profilem rozhraní projektu. Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .

Pro soubory v *lib/* a *ref/* Folders doporučujeme použít jednu skupinu na moniker (TFM).

Následující příklad ukazuje různé varianty `<group>` elementu:

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a>Určení, který cíl NuGet použít

Při vytváření balíčků knihoven cílících na knihovnu přenosných tříd může být obtížné určit, který cíl NuGet byste měli použít ve svých názvech a `.nuspec` souborech složek, zejména pokud cílíte jenom na podmnožinu PCL. Následující externí prostředky vám pomůžou s tímto:

- [Profily architektury v rozhraní .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Přenositelné profily knihovny tříd](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): vytváření výčtu profilů PCL a jejich ekvivalentních cílů NuGet v tabulce
- [Nástroj pro profily přenosných knihoven tříd](https://github.com/StephenCleary/PortableLibraryProfiles) (GitHub.com): nástroj příkazového řádku pro určení profilů PCL dostupných ve vašem systému

## <a name="content-files-and-powershell-scripts"></a>Soubory obsahu a skripty PowerShellu

> [!Warning]
> Soubory s proměnlivým obsahem a provádění skriptu jsou k dispozici `packages.config` pouze ve formátu; jsou zastaralé pro všechny ostatní formáty a neměly by být použity pro žádné nové balíčky.

Se `packages.config` soubory obsahu a skripty PowerShellu se dají seskupovat podle cílové architektury pomocí stejné konvence složky ve `content` `tools` složkách a. Například:

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

Pokud je složka rozhraní ponechána prázdná, NuGet nepřidá odkazy na sestavení ani soubory obsahu nebo spustí skripty prostředí PowerShell pro tuto architekturu.

> [!Note]
> Vzhledem k tomu `init.ps1` , že je spuštěn na úrovni řešení a není závislý na projektu, je nutné jej umístit přímo do `tools` složky. Ignoruje se, pokud je umístěn do složky rozhraní.