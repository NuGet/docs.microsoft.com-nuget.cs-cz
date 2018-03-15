---
title: "Řešení potíží s balíček NuGet obnovit v sadě Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Popis běžné NuGet obnovit chyby v sadě Visual Studio a řešení potíží s nimi."
keywords: "Řešení potíží s obnovení balíčku NuGet, obnovení balíčků, řešení potíží"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>Řešení potíží s chybami obnovení balíčku

Tento článek se zaměřuje na běžné chyby při obnovování balíčků a kroky k jejich řešení. Úplné podrobnosti o obnovení balíčků naleznete v tématu [obnovení balíčků](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Pokud pokynů tady nefungují, [prosím soubor problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby jsme více pečlivě zkontrolujte váš scénář. Nepoužívejte "je tato stránka užitečné?" ovládací prvek, který může vypadat na této stránce, protože se nám nedává možnost kontaktovat v souvislosti s další informace.

## <a name="quick-solution-for-visual-studio-users"></a>Rychlé řešení pro uživatele v sadě Visual Studio

Pokud používáte Visual Studio, nejdřív takto povolte obnovení balíčků. V opačném případě pokračujte v následujících částech.

1. Vyberte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkazu nabídky.
1. Nastavit obě možnosti v části **obnovení balíčků**.
1. Vyberte **OK**.
1. Znovu sestavte projekt.

![Povolit obnovení balíčků NuGet v Nástroje/možnosti](../consume-packages/media/restore-01-autorestoreoptions.png)

Tato nastavení lze změnit také v vaše `NuGet.config` soubor; najdete v článku [souhlas](#consent) části.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Tento projekt odkazuje na balíčky NuGet, které nejsou v tomto počítači

Dokončení chybová zpráva:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

K této chybě dojde, pokusíte sestavení projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou uložené v mezipaměti v současné době v projektu. (Balíčky jsou uložené v `packages` složku v kořenovém adresáři řešení, pokud projekt používá `packages.config`, nebo v `obj/project.assets.json` souboru Pokud projekt používá formát PackageReference.)

K této situaci dochází běžně při získání zdrojového kódu projektu ze správy zdrojového kódu nebo jiného stahování. Balíčky jsou obvykle ze zdrojového kódu nebo stahování vynechána, protože bylo možné obnovit z balíčku kanály jako nuget.org (viz [balíčky a Správa zdrojového kódu](Packages-and-Source-Control.md)). Včetně jejich by jinak nafouknutí úložiště nebo vytvořte .zip zbytečně velké soubory.

Aby se obnovily balíčky, použijte jednu z následujících metod:

- V sadě Visual Studio, povolit obnovení balíčků výběrem **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkaz nabídky, obě možnosti v části Nastavení **obnovení balíčků**a výběr  **OK**. Pak znovu sestavte řešení.
- .NET Core projekty, spusťte `dotnet restore` nebo `dotnet build` (který automaticky spustí obnovení).
- Na příkazovém řádku spusťte `nuget restore` (s výjimkou projektů vytvořených s `dotnet`, v takovém případě použijte `dotnet restore`).
- Na příkazovém řádku s projekty formátu PackageReference, spusťte `msbuild /t:restore`.

Po úspěšné obnovení, měli byste vidět buď `packages` složky (při použití `packages.config`) nebo `obj/project.assets.json` souboru (při použití PackageReference). Projekt má nyní sestavit úspěšně. Pokud ne, [souboru problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak nám s vámi následnou akci.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Prostředky souboru project.assets.json nebyl nalezen

Dokončení chybová zpráva:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Tato chyba nastane ze stejných důvodů, jak je popsáno v [předchozí části](#missing), a má stejné náhrad. Například běžet `msbuild` na .NET Core projektu, který byl získán od správy zdrojového kódu nebude automaticky obnovení balíčků. V takovém případě spusťte `msbuild /t:restore` následuje `msbuild`, nebo použijte `dotnet build` (což obnoví balíčky automaticky).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Jeden nebo více balíčků NuGet je potřeba, ale nebylo možné, protože nebyl udělen souhlas

Dokončení chybová zpráva:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Tato chyba znamená, že obnovení balíčku je zakázáno v konfiguraci NuGet.

Použít nastavení v sadě Visual Studio můžete změnit, jak je popsáno výše v části [rychlé řešení pro Visual Studio uživatele](#quick-solution-for-visual-studio-users).

Můžete také upravit tato nastavení přímo v příslušné `nuget.config` souboru (obvykle `%AppData%\NuGet\NuGet.Config` v systému Windows a `~/.nuget/NuGet/NuGet.Config` na Mac/Linux). Zajistěte, aby `enabled` a `automatic` klíče v části `packageRestore` jsou nastaveny na hodnotu True:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

Všimněte si, že pokud chcete upravit `packageRestore` nastavení přímo v `nuget.config`, restartujte Visual Studio, aby se dialogové okno Možnosti zobrazuje aktuální hodnoty.

## <a name="other-potential-conditions"></a>Další potenciální podmínky

- Chyby sestavení z důvodu chybějících souborů, může dojít u zpráva, že je stáhnout pomocí obnovení NuGet. Však spuštění obnovení říci, "všechny balíčky jsou už nainstalované a neexistuje žádné položky k obnovení." V takovém případě odstraňte `packages` složky (při použití `packages.config`) nebo `obj/project.assets.json` souboru (při použití PackageReference) a spusťte obnovení znovu.

- Při získávání projektu od správy zdrojového kódu, může být vaše složky projektu nastaven jen pro čtení. Změňte oprávnění složky a znovu Probíhá obnovení balíčků.

- Možná používáte starší verzi NuGet. Zkontrolujte [nuget.org/downloads](https://www.nuget.org/downloads) nejnovější doporučená verze. Pro Visual Studio 2015 doporučujeme 3.6.0.

Pokud narazíte na jiné problémy [souboru problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak jsme od vás získali další podrobnosti.