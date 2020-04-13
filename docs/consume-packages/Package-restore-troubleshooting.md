---
title: Poradce při potížích s obnovením balíčků NuGet v sadě Visual Studio
description: Popis běžných chyb obnovení NuGet v sadě Visual Studio a jejich řešení.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860625"
---
# <a name="troubleshooting-package-restore-errors"></a>Poradce při potížích s chybami obnovení balíčku

Tento článek se zaměřuje na běžné chyby při obnovení balíčků a kroky k jejich vyřešení. 

Nástroj Restore package restore se pokusí nainstalovat všechny závislosti balíčků do správného stavu, který odpovídá odkazům na balíček v souboru projektu (*csproj*) nebo souboru *packages.config.* (V sadě Visual Studio se odkazy zobrazí v Průzkumníku řešení pod **závislostmi \ NuGet** nebo **uzel Reference.)** Chcete-li provést požadované kroky k obnovení balíčků, naleznete v [tématu Obnovení balíčků](../consume-packages/package-restore.md#restore-packages). Pokud jsou odkazy na balíček v souboru projektu (*.csproj*) nebo soubor *packages.config* nesprávné (neodpovídají požadovanému stavu po obnovení balíčku), musíte buď nainstalovat nebo aktualizovat balíčky namísto použití nástroje Obnovení balíčku.

Pokud pokyny zde nefungují pro vás, [prosím, soubor problém na GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) takže můžeme prozkoumat váš scénář pečlivěji. Nepoužívejte "Je tato stránka užitečná?" které se mohou na této stránce zobrazit, protože nám neumožňuje vás kontaktovat pro další informace.

## <a name="quick-solution-for-visual-studio-users"></a>Rychlé řešení pro uživatele sady Visual Studio

Pokud používáte Visual Studio, nejprve povolte obnovení balíčku následujícím způsobem. V opačném případě pokračujte do následujících oddílů.

1. Vyberte příkaz **příkaz U nástroje > Správce balíčků > nastavení Správce balíčků.**
1. Nastavte obě možnosti v části **Obnovení balíčku**.
1. Vyberte **OK**.
1. Sestavte svůj projekt znovu.

![Povolit obnovení balíčku NuGet v nástroji/možnostech](../consume-packages/media/restore-01-autorestoreoptions.png)

Tato nastavení lze také `NuGet.config` změnit v souboru; naleznete v sekci [souhlas.](#consent) Pokud váš projekt je starší projekt, který používá obnovení balíčku integrované MSBuild, budete muset [migrovat](package-restore.md#migrate-to-automatic-package-restore-visual-studio) na automatické obnovení balíčku.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí.

Úplná chybová zpráva:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

K této chybě dochází při pokusu o vytvoření projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou v současné době nainstalovány v počítači nebo v projektu.

- Při použití formátu správy [PackageReference](package-references-in-project-files.md) chyba znamená, že balíček není nainstalován ve složce *global-packages,* jak je popsáno v [části Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).
- Při použití [packages.config](../reference/packages-config.md), chyba znamená, že `packages` balíček není nainstalován ve složce v kořenovém adresáři řešení.

K této situaci obvykle dochází při získání zdrojového kódu projektu ze správy zdrojového kódu nebo jiného stažení. Balíčky jsou obvykle vynechány ze správy zdrojového kódu nebo stahování, protože je lze obnovit z kanálů balíčků, jako je nuget.org (viz [Balíčky a správa zdrojového kódu).](Packages-and-Source-Control.md) Jejich zahrnutí by jinak nafouklo úložiště nebo vytvořilo zbytečně velké .zip soubory.

K chybě může dojít také v případě, že soubor projektu obsahuje absolutní cesty do umístění balíčků a přesunutí projektu.

K obnovení balíčků použijte jednu z následujících metod:

- Pokud jste přesunuli soubor projektu, upravte soubor přímo a aktualizujte odkazy na balíček.
- [Visual Studio](package-restore.md#restore-using-visual-studio) [(automatické obnovení](package-restore.md#restore-packages-automatically-using-visual-studio) nebo ruční [obnovení)](package-restore.md#restore-packages-manually-using-visual-studio)
- [Rozhraní příkazového řádku dotnet](package-restore.md#restore-using-the-dotnet-cli)
- [Rozhraní příkazového řádku nuget.exe](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Po úspěšném obnovení by měl být balíček přítomen ve složce *globální balíčky.* U projektů používajících odkaz packagereference `obj/project.assets.json` by obnovení mělo znovu vytvořit soubor. pro projekty pomocí `packages.config`, balíček by `packages` měl být uveden ve složce projektu. Projekt by měl nyní úspěšně sestavit. Pokud ne, [posuňte na GitHubu problém,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abychom s vámi mohli navázat.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Soubor datových zdrojů project.assets.json nebyl nalezen.

Úplná chybová zpráva:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Soubor `project.assets.json` udržuje graf závislostí projektu při použití formátu správy PackageReference, který se používá k zajištění, že jsou v počítači nainstalovány všechny potřebné balíčky. Vzhledem k tomu, že tento soubor je generován dynamicky prostřednictvím obnovení balíčku, obvykle není přidán do správy zdrojového kódu. V důsledku toho k této chybě dochází při vytváření `msbuild` projektu s nástrojem, jako je například to není automaticky obnovit balíčky.

V tomto případě `msbuild -t:restore` spustit `msbuild`následuje `dotnet build` , nebo použít (který obnovuje balíčky automaticky). Můžete také použít některou z metod obnovení balíčku v [předchozí části](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Jeden nebo více balíčků NuGet je třeba obnovit, ale nemůže být, protože nebyl udělen souhlas

Úplná chybová zpráva:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Tato chyba označuje, že obnovení balíčku je zakázáno v konfiguraci NuGet.

Příslušná nastavení v sadě Visual Studio můžete změnit, jak je popsáno výše v části [Rychlé řešení pro uživatele sady Visual Studio](#quick-solution-for-visual-studio-users).

Tato nastavení můžete také upravit `nuget.config` přímo v `%AppData%\NuGet\NuGet.Config` příslušném `~/.nuget/NuGet/NuGet.Config` souboru (obvykle v systému Windows a na Počítači Mac/Linux). Ujistěte `enabled` se, že jsou klávesy a `automatic` v části `packageRestore` nastaveny na hodnotu True:

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
> Pokud upravujete `packageRestore` nastavení `nuget.config`přímo v aplikaci , restartujte visual studio tak, aby dialogové okno možností zobrazovaly aktuální hodnoty.

## <a name="other-potential-conditions"></a>Další potenciální podmínky

- Můžete se setkat s chybami sestavení kvůli chybějícím souborům se zprávou, která říká, že chcete použít obnovení NuGet k jejich stažení. Spuštění obnovení však může říkat: "Všechny balíčky jsou již nainstalovány a není nic k obnovení." V takovém případě `packages` odstraňte složku `packages.config`(při `obj/project.assets.json` použití) nebo soubor (při použití PackageReference) a znovu spusťte obnovení. Pokud chyba přetrvává, vymažte globální složky balíčků a mezipamětí, jak je popsáno v části [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md), použijte `nuget locals all -clear` nebo `dotnet locals all --clear` z příkazového řádku vymažte složky *globálních balíčků* a mezipaměti .

- Při získávání projektu ze správy zdrojového kódu mohou být složky projektu nastaveny na jen pro čtení. Změňte oprávnění ke složce a zkuste znovu obnovit balíčky.

- Pravděpodobně používáte starou verzi NuGet. [Zkontrolujte, nuget.org/downloads](https://www.nuget.org/downloads) najdete nejnovější doporučené verze. Pro Visual Studio 2015 doporučujeme 3.6.0.

Pokud narazíte na jiné problémy, [soubor problém na GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) takže můžeme získat další podrobnosti od vás.
