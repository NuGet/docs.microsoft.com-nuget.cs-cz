---
title: Vícenásobné cílení pro balíčky NuGet
description: Popis různých metod, které mají cílit na více verzí rozhraní .NET Framework z jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429008"
---
# <a name="support-multiple-net-versions"></a>Podpora více verzí rozhraní .NET

Mnoho knihoven cílí na konkrétní verzi rozhraní .NET Framework. Můžete mít například jednu verzi knihovny, která je specifická pro UPW, a jinou verzi, která využívá výhod funkcí v rozhraní .NET Framework 4.6. Chcete-li přizpůsobit toto, NuGet podporuje uvedení více verzí stejné knihovny v jednom balíčku.

Tento článek popisuje rozložení balíčku NuGet, bez ohledu na to, jak jsou vytvořeny balíček nebo sestavení (to znamená, že rozložení je stejné, ať už pomocí více souborů *csproj* ve stylu s dsad a vlastní soubor *.nuspec* nebo jeden víceúčelový *soubor SDK .csproj*). Pro projekt ve stylu Sady SDK cíle sady NuGet [pack](../reference/msbuild-targets.md) ví, jak musí být balíček rozložen a automatizuje umístění sestavení do správných složek lib a vytváření skupin závislostí pro každý cílový rámec (TFM). Podrobné pokyny naleznete v [tématu Podpora více verzí rozhraní .NET Framework v souboru projektu](multiple-target-frameworks-project-file.md).

Při použití metody pracovního adresáře založené na konvencích popsané v [článku Vytvoření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)je nutné ručně rozložit balíček. Pro projekt ve stylu sady SDK je doporučena automatizovaná metoda, ale můžete také ručně rozložit balíček, jak je popsáno v tomto článku.

## <a name="framework-version-folder-structure"></a>Struktura složek verzí architektury

Při vytváření balíčku, který obsahuje pouze jednu verzi knihovny nebo cíl `lib` více architektur, vždy vytvořit podsložky pod pomocí různých názvů rozhraní rozlišující malá a velká písmena s následující konvencí:

    lib\{framework name}[{version}]

Úplný seznam podporovaných názvů naleznete v [odkazu Cílové architektury](../reference/target-frameworks.md#supported-frameworks).

Nikdy byste neměli mít verzi knihovny, která není specifická `lib` pro rozhraní a umístěna přímo do kořenové složky. (Tato funkce byla `packages.config`podporována pouze s ). Pokud by bylo možné knihovnu kompatibilní s libovolným cílovým rozhraním a umožnit její instalaci kdekoli, což by pravděpodobně vedlo k neočekávaným chybám za běhu. Přidání sestavení do kořenové složky (například) `lib\abc.dll` `lib\abc\abc.dll`nebo podsložek (například ) bylo zastaralé a při použití formátu PackagesReference je ignorováno.

Například následující struktura složek podporuje čtyři verze sestavení, které jsou specifické pro architekturu:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Chcete-li při vytváření balíčku snadno zahrnout všechny tyto `**` soubory, `<files>` použijte v `.nuspec`části :

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Složky specifické pro architekturu

Pokud máte sestavení specifická pro architekturu, to znamená samostatná sestavení, která cílí na ARM, x86 a x64, musíte je umístit do složky s názvem `runtimes` v podsložkách s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native`. Například následující struktura složek by vyhovovala nativním i spravovaným knihovnám DLL zaměřeným na systém Windows 10 a `uap10.0` rámci:

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

Tato sestavení budou k dispozici pouze za běhu, takže pokud chcete poskytnout odpovídající `AnyCPU` sestavení `/ref/{tfm}` čas kompilace také pak mít sestavení ve složce. 

Upozorňujeme, nuget vždy vybere tyto kompilovat nebo runtime prostředky z `/ref` `/lib` jedné složky, takže pokud existují některé kompatibilní prostředky z té doby budou ignorovány přidat sestavení v době kompilace. Podobně, pokud existují některé kompatibilní `/runtimes` prostředky `/lib` z pak také budou ignorovány pro běh.

Viz [Vytvoření balíčků UPW](../guides/create-uwp-packages.md) pro příklad odkazování `.nuspec` na tyto soubory v manifestu.

Taky si přečtěte [část Balení součásti aplikace pro Windows Store pomocí NuGetu.](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Odpovídající verze sestavení a cílové rozhraní v projektu

Když NuGet nainstaluje balíček, který má více verzí sestavení, pokusí se shodovat název rámce sestavení s cílovým rámcem projektu.

Pokud není nalezena shoda, NuGet zkopíruje sestavení pro nejvyšší verzi, která je menší nebo rovna cílové rozhraní projektu, pokud je k dispozici. Pokud není nalezeno žádné kompatibilní sestavení, NuGet vrátí příslušnou chybovou zprávu.

Zvažte například následující strukturu složek v balíčku:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Při instalaci tohoto balíčku v projektu, který se zaměřuje na rozhraní .NET Framework 4.6, NuGet nainstaluje sestavení ve `net45` složce, protože to je nejvyšší dostupná verze, která je menší nebo rovna 4.6.

Pokud projekt cíle .NET Framework 4.6.1, na druhé straně NuGet `net461` nainstaluje sestavení ve složce.

Pokud se projekt zaměřuje na rozhraní .NET Framework 4.0 a starší, NuGet vyvolá příslušnou chybovou zprávu pro nenalezení kompatibilního sestavení.

## <a name="grouping-assemblies-by-framework-version"></a>Seskupení sestavení podle verze architektury

NuGet zkopíruje sestavení pouze z jedné složky knihovny v balíčku. Předpokládejme například, že balíček má následující strukturu složek:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Při instalaci balíčku v projektu, který se zaměřuje `MyAssembly.dll` na rozhraní .NET Framework 4.5 (v2.0) je pouze nainstalované sestavení. `MyAssembly.Core.dll`(v1.0) není nainstalován, protože není uveden `net45` ve složce. NuGet se chová tímto způsobem, protože `MyAssembly.Core.dll` pravděpodobně `MyAssembly.dll`byly sloučeny do verze 2.0 .

Pokud chcete `MyAssembly.Core.dll` být nainstalovánpro rozhraní .NET Framework 4.5, umístěte kopii do `net45` složky.

## <a name="grouping-assemblies-by-framework-profile"></a>Seskupení sestavení podle profilu rámce

NuGet také podporuje cílení na konkrétní profil architektury připojením pomlčka a název profilu na konec složky.

    lib\{framework name}-{profile}

Podporované profily jsou následující:

- `client`: Profil klienta
- `full`: Úplný profil
- `wp`: Windows Phone
- `cf`: Kompaktní rámec

## <a name="declaring-dependencies-advanced"></a>Deklarování závislostí (Upřesnit)

Při balení souboru projektu NuGet pokusí automaticky generovat závislosti z projektu. Informace v této části o použití souboru *.nuspec* k deklarování závislostí jsou obvykle nezbytné pouze pro pokročilé scénáře.

*(verze 2.0+)* Můžete deklarovat závislosti balíčku v *.nuspec* odpovídající cílovému `<group>` rámci `<dependencies>` cílového projektu pomocí prvků v rámci prvku. Další informace naleznete v tématu [element závislosti .](../reference/nuspec.md#dependencies-element)

Každá skupina má `targetFramework` atribut s názvem `<dependency>` a obsahuje nula nebo více prvků. Tyto závislosti jsou nainstalovány společně, když je cílový rámec kompatibilní s profilem architektury projektu. Viz [Cílové architektury](../reference/target-frameworks.md) pro přesné identifikátory rozhraní.

Doporučujeme použít jednu skupinu na cílový rámec zástupný název (TFM) pro soubory v *lib/* a *ref/* složky.

Následující příklad ukazuje různé varianty `<group>` prvku:

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

Při balení knihoven zaměřených na knihovnu přenosných tříd může být obtížné určit, který cíl NuGet byste měli použít v názvech a `.nuspec` souboru složek, zejména pokud cílíte pouze na podmnožinu pcl. S tím vám pomohou následující externí zdroje:

- [Profily architektury v rozhraní .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Profily knihovny přenosných tříd](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabulka s výčetem profilů PCL a jejich ekvivalentních cílů NuGet
- [Nástroj profily knihovny přenosných tříd](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): nástroj příkazového řádku pro určení profilů PCL dostupných ve vašem systému

## <a name="content-files-and-powershell-scripts"></a>Soubory obsahu a skripty prostředí PowerShell

> [!Warning]
> Mutable soubory obsahu a spuštění `packages.config` skriptu jsou k dispozici pouze ve formátu; jsou zastaralé se všemi ostatními formáty a neměly by být používány pro žádné nové balíčky.

Pomocí `packages.config`souborů obsahu a skriptů prostředí PowerShell lze seskupit `content` `tools` podle cílového rozhraní pomocí stejné konvence složek uvnitř složek a. Příklad:

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

Pokud je složka architektury ponechána prázdná, NuGet nepřidá odkazy na sestavení nebo soubory obsahu ani nespustí skripty prostředí PowerShell pro tento rámec.

> [!Note]
> Protože `init.ps1` je spuštěn na úrovni řešení a není závislá na projektu, musí být umístěnpřímo do `tools` složky. Je ignorována, pokud je umístěna pod rámcovou složkou.
