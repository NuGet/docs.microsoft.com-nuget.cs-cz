---
title: Řešení potíží s obnovení balíčků NuGet v sadě Visual Studio
description: Popis běžné NuGet restore chyby v sadě Visual Studio a postupy jejich řešení.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: b85b586e76e424442dc0ba3acfecbee1e8755345
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453465"
---
# <a name="troubleshooting-package-restore-errors"></a>Řešení potíží s chybami obnovení balíčku

Tento článek se zaměřuje na běžných chyb při obnovování balíčků a kroky k jejich řešení. Kompletní informace o obnovování balíčků, najdete v části [obnovení balíčku](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Pokud zde uvedených pokynů, nebudou fungovat, [založte prosím problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby nám více pečlivě prozkoumat váš scénář. Nepoužívejte "je tato stránka užitečná?" ovládací prvek, který může zobrazit na této stránce, protože se nám nedává možnost kontaktovat v souvislosti s další informace.

## <a name="quick-solution-for-visual-studio-users"></a>Rychlé řešení pro uživatele sady Visual Studio

Pokud používáte Visual Studio, nejprve následujícím způsobem povolte obnovení balíčků. V opačném případě pokračujte následující části.

1. Vyberte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkazu nabídky.
1. Obě možnosti v části Nastavení **obnovení balíčků**.
1. Vyberte **OK**.
1. Znovu sestavte projekt.

![Povolit obnovení balíčků NuGet v dialogovém okně nástroje/Možnosti](../consume-packages/media/restore-01-autorestoreoptions.png)

Tato nastavení lze také změnit v vaše `NuGet.config` souboru; najdete v článku [souhlas](#consent) oddílu.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Tento projekt odkazuje na balíčky NuGet, které jsou na tomto počítači chybí

Kompletní chybová zpráva:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

K této chybě dochází při pokusu o vytvoření projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou v současné době nainstalované v počítači nebo v projektu.

- Při použití formátu správy PackageReference chyba znamená, že balíček není nainstalována v *global-packages* složky, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).
- Při použití `packages.config`, chyba znamená, že balíček není nainstalována v `packages` složku v kořenovém adresáři řešení.

Této situaci dochází běžně, když získal zdrojový kód projektu ze správy zdrojového kódu nebo jiného stahování. Balíčky jsou obvykle vynechány ze správy zdrojového kódu nebo soubory ke stažení, protože je možné obnovit z informační kanály balíčků, jako je nuget.org (viz [balíčky a Správa zdrojového kódu](Packages-and-Source-Control.md)). Jejich zahrnování by jinak nafouknutí úložiště nebo vytvořit soubory .zip zbytečně velký.

Chyba může dojít, pokud váš soubor projektu obsahuje absolutní cesty k umístění balíčku, a přesunout projektu.

Obnovení balíčků, použijte jednu z následujících metod:

- Pokud po přesunutí souboru projektu, upravte soubor přímo aktualizovat odkazy na balíček.
- V sadě Visual Studio povolit obnovení balíčků tak, že vyberete **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkazu nabídky nastavení obě možnosti v části **obnovení balíčků**a výběrem  **OK**. Poté znovu sestavte řešení.
- Pro projekty .NET Core, spusťte `dotnet restore` nebo `dotnet build` (který automaticky spustí obnovení).
- Na příkazovém řádku spusťte `nuget restore` (s výjimkou projekty vytvořené pomocí `dotnet`, v takovém případě použijte `dotnet restore`).
- V příkazovém řádku s projekty pomocí formátu PackageReference spustit `msbuild -t:restore`.

Po úspěšné obnovení by měla být k dispozici v balíčku *global-packages* složky. Pro projekty pomocí PackageReference obnovení musí znovu vytvořit `obj/project.assets.json` soubor; pro projekty používající `packages.config`, balíček by se měla objevit v projektu `packages` složky. Projekt by měl nyní úspěšně sestavit. V opačném případě [založte problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak jsme poradí s vámi.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Nebyl nalezen project.assets.json souboru prostředků

Kompletní chybová zpráva:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` Souboru udržuje graf závislosti projektu při použití formátu správy PackageReference, který se používá k zajištění toho, že jsou v počítači nainstalovány všechny potřebné balíčky. Protože tento soubor se generuje dynamicky pomocí obnovení balíčků, není obvykle přidat do správy zdrojového kódu. V důsledku toho k této chybě dochází při sestavování projektu pomocí nástroje, jako `msbuild` , neobnoví automaticky balíčky.

V takovém případě spusťte `msbuild -t:restore` následovaný `msbuild`, nebo použijte `dotnet build` (což obnoví balíčky automaticky). Můžete také použít některou z metod obnovení balíčku v [předchozí části](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Jeden nebo více balíčků NuGet je nutné obnovit, ale nepodařilo, protože nebyl udělen souhlas

Kompletní chybová zpráva:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Tato chyba označuje, že obnovení balíčků je zakázáno v konfiguraci Nugetu.

Použít nastavení v sadě Visual Studio můžete změnit, jak je popsáno výše v části [rychlé řešení pro uživatele sady Visual Studio](#quick-solution-for-visual-studio-users).

Můžete také upravit tato nastavení přímo v příslušné `nuget.config` soubor (obvykle `%AppData%\NuGet\NuGet.Config` na Windows a `~/.nuget/NuGet/NuGet.Config` na Mac/Linux). Ujistěte se, že `enabled` a `automatic` klíče v části `packageRestore` jsou nastaveny na hodnotu True:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> Pokud upravíte `packageRestore` přímo v nastavení `nuget.config`, restartujte aplikaci Visual Studio tak, aby se dialogové okno Možnosti zobrazuje aktuální hodnoty.

## <a name="other-potential-conditions"></a>Další potenciální podmínky

- Chyby sestavení z důvodu chybějících souborů, kterým může dojít u zpráva, že si je stáhnout pomocí obnovení NuGet. Ale spuštění obnovení může být například "všechny balíčky jsou už nainstalované a neexistuje žádné položky k obnovení." V takovém případě odstranit `packages` složky (při použití `packages.config`) nebo `obj/project.assets.json` souboru (při použití PackageReference) a spusťte obnovení znovu. Pokud chyba stále přetrvává, použijte `nuget locals all -clear` nebo `dotnet locals all --clear` z příkazového řádku pro vymazání *global-packages* a jak je popsáno v mezipaměti složky [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).

- Při získávání projekt ze správy zdrojových kódů, složky projektu může být nastavená na jen pro čtení. Změňte oprávnění pro složky a zkuste to znovu obnovují se balíčky.

- Může používat stará verze balíčku nuget. Zkontrolujte [nuget.org/downloads](https://www.nuget.org/downloads) nejnovější doporučených verzí. Pro Visual Studio 2015 doporučujeme 3.6.0.

Pokud narazíte na jiné problémy [založte problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) proto jsme od vás získali více podrobností.
