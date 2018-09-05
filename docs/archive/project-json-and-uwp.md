---
title: Soubor project.json NuGet s projekty UPW
description: Popis, jak soubor project.json slouží ke sledování závislostí NuGet v projektech univerzální platformy Windows (UPW).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548661"
---
# <a name="projectjson-and-uwp"></a>Project.JSON a UPW

> [!Important]
> Tento obsah je zastaralý. Projekty by měl použít buď `packages.config` nebo PackageReference formátů.

Tento dokument popisuje strukturu balíček, který využívá funkce ve Správci NuGet 3 + (Visual Studio 2015 a novější). `minClientVersion` Vlastnictví vaší `.nuspec` je možné stanovit, zda vyžadujete funkce popsané tady nastavením na 3.1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Přidání podpory pro UPW do existujícího balíčku

Pokud máte existující balíček a chcete přidat podporu pro aplikace UPW, pak není nutné přijmout balení formátu popsaném tady. Stačí přijmout tento formát, pokud vyžadujete funkce popisuje a jste ochotni pracovat pouze s klienty, kteří mají aktualizována na verzi 3 + klienta NuGet.

## <a name="i-already-target-netcore45"></a>Už mám cílit netcore45

Pokud je cílem `netcore45` již a nemusíte využít výhod funkce tady, není vyžadována žádná akce. `netcore45` balíčky mohou být spotřebovány aplikacemi UWP.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Budu chtít využívat výhod určitých rozhraní API Windows 10

V tomto případě budete muset přidat `uap10.0` cílit na moniker rozhraní (TFM nebo TxM) do balíčku. Vytvoření nové složky v balíčku a přidejte sestavení, která byla zkompilována pro práci s Windows 10 do této složky.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Nepotřebuji konkrétní rozhraní API Windows 10, ale má nové funkce rozhraní .NET nebo již nemáte netcore45

V tomto případě přidáte `dotnet` TxM do vašeho balíčku. Na rozdíl od jiných TxMs `dotnet` není určeno styčné plochy nebo platformu. Je s informacemi o tom, které váš balíček funguje na libovolné platformě, která závislostí pracovat. Při vytváření balíčku s `dotnet` TxM, budete pravděpodobně mají mnoho další TxM specifické závislosti vašich `.nuspec`, jako je třeba definovat závisí na tyto balíčky BCL `System.Text`, `System.Xml`atd. Umístění, které tyto závislosti fungují na definovat, pracuje, jak váš balíček.

### <a name="how-do-i-find-out-my-dependencies"></a>Jak zjistím volání závislostí

Existují dva způsoby, jak zjistit, jaké závislosti na seznamu:

1. Použití [generátor závislostí souboru NuSpec](https://github.com/onovotny/ReferenceGenerator) **3. stran** nástroj. Nástroj automatizuje proces a aktualizace vašich `.nuspec` soubor se závislé balíčky v sestavení. Je k dispozici prostřednictvím balíčku NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Přiznejme) Použití `ILDasm` podívat se na vaše `.dll` zobrazíte, jaké sestavení jsou skutečně potřeba za běhu. Pak zjistěte balíčky NuGet, které každá pocházejí.

Zobrazit [ `project.json` ](project-json.md) tématu informace o funkcích, které pomáhají při vytváření balíčku, který podporuje `dotnet` TxM.

> [!Important]
> Pokud váš balíček je určená pro práci s projekty PCL, důrazně doporučujeme vytvořit `dotnet` složky, aby se zabránilo upozornění a potenciální problémy s kompatibilitou.

## <a name="directory-structure"></a>Adresářová struktura

Balíčky NuGet pomocí tohoto formátu mají následující dobře známou složku a chování:

| Folder | Chování |
| --- | --- |
| Sestavení | Obsahuje nástroje MSBuild cíle a soubory vlastností v této složce jsou jinak integrované do projektu, ale jinak není žádná změna. |
| Nástroje | `install.ps1` a `uninstall.ps1` se nespustí. `init.ps1` funguje jako má vždy. |
| Obsah | Obsah není automaticky zkopíruje do projektu uživatele. Podpora pro zařazení obsahu v projektu je naplánovaná pro novější verzi. |
| lib | Pro mnoho balíčků `lib` funguje stejně v NuGet 2.x, ale rozšířené možnosti, které názvů může být použit uvnitř ho a lépe logiku pro výběr správné dílčí složky při využívání balíčků. Ale při použití ve spojení s `ref`, `lib` složka obsahuje sestavení, které implementují styčné plochy definované v sestavení `ref` složky. |
| REF | `ref` je volitelný složku, která obsahuje sestavení .NET definování veřejného surface (veřejné typy a metody) pro aplikaci kompilovat proti. Sestavení v této složce mohou nemají implementaci, čistě se používají k definování povrchu pro kompilátor. Pokud balíček nemá žádné `ref` složku, pak bude `lib` se referenční sestavení a sestavení implementace. |
| Moduly runtime | `runtimes` je volitelný složku, která obsahuje určitý kód operačního systému, jako je architektura procesoru a konkrétního nebo jinak závislého na platformě binární soubory. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>Nástroj MSBuild cíle a soubory vlastností v balíčcích

Může obsahovat balíčky NuGet `.targets` a `.props` soubory, které jsou importovány do jakékoli projektu nástroje MSBuild, který je nainstalován balíček do. Ve Správci NuGet 2.x, to se provádí vkládání `<Import>` příkazy do `.csproj` souboru, ale NuGet 3.0 není nic konkrétní "instalace do projektu". Místo toho proces obnovení balíčku zapíše dva soubory `[projectname].nuget.props` a `[projectname].NuGet.targets`.

Nástroj MSBuild ví těchto dvou souborů a automaticky importuje poblíž začátku a na konci procesu sestavení projektu. To poskytuje velmi podobné chování NuGet 2.x, ale s jedním z hlavních rozdílů: *není zaručeno pořadí cíle/props soubory v tomto případě*. Nástroj MSBuild poskytuje však způsoby, jak pořadí cíle prostřednictvím `BeforeTargets` a `AfterTargets` atributy `<Target>` definice (naleznete v tématu [Target – Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>LIB a Ref

Chování `lib` složky významně nezměnila ve verzi 3 NuGet. Však musí spadat do podsložky s názvem po TxM všechna sestavení a můžete už umístit přímo pod `lib` složky. TxM je název platformy, která daný prostředek v balíčku by měla fungovat. Logicky Toto jsou rozšíření cílové rozhraní Framework Monikery (TFM), třeba `net45`, `net46`, `netcore50`, a `dnxcore50` jsou všechny příklady TxMs (naleznete v tématu [cílové architektury](../reference/target-frameworks.md). TxM mohou odkazovat na rozhraní (TFM) a také další specifické pro platformu plochy. Například TxM UPW (`uap10.0`) představuje útoku na rozhraní .NET, jakož i plochy Windows pro aplikace UPW.

Příklad lib struktury:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` Složka obsahuje sestavení, které se používají v době běhu. Pro většinu balíčků složku ve složce `lib` pro každý cíl TxMs je vše, co je povinný.

## <a name="ref"></a>REF

Někdy existují případy, kdy jiné sestavení by měla sloužit během kompilace (odkaz na sestavení .NET do této dnes). Pro tyto případy použijte složku nejvyšší úrovně s názvem `ref` (zkratka "odkaz na sestavení").

Většina autory balíčku nevyžadují `ref` složky. To je užitečné pro balíčky, které je potřeba poskytnout konzistentní styčné plochy pro kompilaci a technologie IntelliSense, ale pak je mít jinou implementaci pro různé TxMs. Největší případ použití jsou `System.*` balíčky, které jsou vytvořených jako součást přenosů .NET Core na webu NuGet. Tyto balíčky obsahují různé implementace, které jsou právě sjednocené konzistentní sada referenční sestavení.

Mechanicky, sestavení součástí `ref` složky jsou referenční sestavení, jsou předány kompilátoru. Pro ty z vás, kteří použili csc.exe jde o sestavení jsme jsou předány [možnosti/reference jazyka C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) přepnout.

Struktura `ref` složka je stejná jako `lib`, například:

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

V tomto příkladu sestavení v `ref` adresáře by být identické.

## <a name="runtimes"></a>Moduly runtime

Složka moduly runtime obsahuje sestavení a nativních knihoven, které jsou potřeba ke spouštění na konkrétní "moduly runtime", které jsou obvykle definovány pomocí Architektura operačního systému a procesoru. Tyto moduly runtime jsou označeny pomocí [Runtime identifikátorů (RID)](/dotnet/core/rid-catalog) například `win`, `win-x86`, `win7-x86`, `win8-64`atd.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Nativní Pomocné rutiny používat rozhraní API pro konkrétní platformu

Následující příklad ukazuje balíček, který má plně spravovanou implementaci pro několik platforem, ale používá nativní Pomocné rutiny ve Windows 8, ve kterém může volat do systému Windows 8 specifických nativních rozhraní API.

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

Zadaný balíček výše následující situace:

- Pokud není v systému Windows 8 `lib/net40/MyLibrary.dll` sestavení používá.

- Pokud je na Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` se používá a `native/MyNativeHelper.dll` je zkopírován do výstupního sestavení.

Ve výše uvedeném příkladu `lib/net40` sestavení je čistě spravovaném kódu, zatímco sestavení ve složce modulů runtime bude nespravovaného kódu do nativních pomocné rutiny sestavení pro volání rozhraní API specifická pro systém Windows 8.

Pouze jeden `lib` složky je někdy má vybrat, takže pokud je konkrétní složka modulu runtime je vybrán přes konkrétní – modul runtime `lib`. Nativní složka je additive, pokud existuje, je zkopírován do výstupního sestavení.

## <a name="managed-wrapper"></a>Spravovaná obálka

Dalším způsobem, jak používat moduly runtime je k odeslání balíčku, který je čistě spravovaná obálka nad nativní sestavení. V tomto scénáři vytvoříte balíček vypadat asi takto:

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

V tomto případě není již nejvyšší úrovně `lib` implementaci tohoto balíčku, který se nemusí spoléhat na odpovídající nativní sestavení je složka jako této složky, protože došlo. Pokud spravované sestavení `MyLibrary.dll`, byla přesně stejné v obou těchto případech potom jsme mohli uvolnit ji v nejvyšší úrovni `lib` složky, ale protože chybějící nativní sestavení nezpůsobí balíček k selhání instalace, pokud byla nainstalovaná na platformě, která nebyl win-x86 nebo win-x64 pak by se použily lib nejvyšší úrovně, ale má být zkopírováno žádné nativní sestavení.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Vytváření balíčků pro NuGet 2 a NuGet 3

Pokud chcete vytvořit balíček, který mohou být spotřebovány projektů s použitím `packages.config` stejně jako balíčky pomocí `project.json` následujících podmínek:

- REF a moduly runtime funguje jenom u NuGet 3. Obě jsou ignorovány NuGet 2.

- Nelze spoléhat na `install.ps1` nebo `uninstall.ps1` funkce. Tyto soubory provést při použití `packages.config`, ale jsou ignorovány s `project.json`. Aby váš balíček musí být možné bez jejich spuštění. `init.ps1` sice dál běží na NuGet 3.

- Cíle a vlastnosti instalace se liší, proto se ujistěte, že váš balíček funguje podle očekávání na obou klientských počítačích.

- Podadresáře lib musí být TxM NuGet 3. Knihovny nelze umístit v kořenovém adresáři `lib` složky.

- Obsah není zkopírován automaticky s NuGet 3. Příjemci balíčku může kopírovat soubory sami nebo použít nástroje, jako je Spouštěč úloh k automatizaci kopírování souborů.

- Transformace zdrojových a konfiguračních souborů nejsou spustit NuGet 3.

Pokud podporujete NuGet 2 a 3 vaše `minClientVersion` by měla mít nejnižší verzi klienta NuGet 2, který váš balíček funguje na. V případě existující balíček ho nebylo potřeba měnit.
