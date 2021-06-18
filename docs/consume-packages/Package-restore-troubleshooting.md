---
title: Řešení potíží s obnovením balíčků NuGet v Visual Studio
description: Popis běžných chyb obnovení NuGet v Visual Studio a jejich řešení.
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 0bd14104695a15d2e4c65a13b271143809c4ba8a
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323619"
---
# <a name="troubleshooting-package-restore-errors"></a>Řešení potíží s chybami obnovení balíčků

Tento článek se zaměřuje na běžné chyby při obnovování balíčků a postup jejich řešení. 

Obnovení balíčku se pokusí nainstalovat všechny závislosti balíčku do správného stavu, který odpovídá odkazům na balíček v souboru projektu (*.csproj*) *nebo* packages.configsouboru. (V Visual Studio se odkazy zobrazí v Průzkumník řešení pod **uzlem Závislosti \ NuGet** nebo **Odkazy.)** Pokud chcete obnovit balíčky podle požadovaných kroků, podívejte se na [obnovení balíčků](../consume-packages/package-restore.md#restore-packages). Pokud balíček odkazuje v souboru projektu (*.csproj)* nebo váš *souborpackages.config* je nesprávný (po obnovení balíčku se neshodují s požadovaným stavem), musíte místo použití obnovení balíčku buď nainstalovat, nebo aktualizovat balíčky.

Pokud zde uvedené pokyny pro vás nefungují, zakažte problém na [GitHubu,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abychom mohli váš scénář pečlivěji prozkoumat. Nepoužívejte "Je tato stránka užitečná?" ovládací prvek, který se může zobrazit na této stránce, protože nám nedává možnost vás kontaktovat a získat další informace.

## <a name="quick-solution-for-visual-studio-users"></a>Rychlé řešení pro Visual Studio uživatele

Pokud používáte následující Visual Studio, nejprve následujícím způsobem povolte obnovení balíčku. V opačném případě pokračujte k následujícím částem.

1. Vyberte příkaz **> NuGet Správce balíčků > Správce balíčků Nastavení.**
1. Obě možnosti nastavte v **části Obnovení balíčku.**
1. Vyberte **OK**.
1. Znovu sestavte projekt.

![Povolení obnovení balíčků NuGet v nástroji nebo možnostech](../consume-packages/media/restore-01-autorestoreoptions.png)

Tato nastavení můžete také změnit v `NuGet.Config` souboru. Viz část [o souhlasu.](#consent) Pokud je váš projekt starší projekt, který používá obnovení balíčku [](package-restore.md#migrate-to-automatic-package-restore-visual-studio) integrovaného do nástroje MSBuild, možná bude nutné provést migraci na automatické obnovení balíčku.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí.

Kompletní chybová zpráva:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

K této chybě dochází při pokusu o sestavení projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou v současnosti nainstalovány na počítači nebo v projektu.

- Při použití formátu [správy PackageReference](package-references-in-project-files.md) může být tato chyba ponechána na migraci z [](/nuget/resources/nuget-faq#working-with-packages) packages.config na PackageReference a je potřeba ji ručně odebrat ze souboru projektu.
- Při použití [packages.config](../reference/packages-config.md)znamená chyba, že balíček není nainstalovaný ve složce `packages` v kořenovém adresáři řešení.

K této situaci obvykle dochází, když zdrojový kód projektu získáte ze správy zdrojového kódu nebo jiného stahování. Balíčky jsou ze správy zdrojového kódu nebo stahování obvykle vynechány, protože je lze obnovit z informačních kanálů balíčků, jako je nuget.org (viz Balíčky a [správy zdrojového kódu).](Packages-and-Source-Control.md) Jejich zahrnutí by jinak nafoukalo úložiště nebo by zbytečně vytvářelo .zip soubory.

K této chybě může dojít také v případě, že soubor projektu obsahuje absolutní cesty k umístění balíčků a přesunete projekt.

K obnovení balíčků použijte jednu z následujících metod:

- Pokud jste přesunuli soubor projektu, upravte soubor přímo a aktualizujte odkazy na balíček.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([automatické obnovení](package-restore.md#restore-packages-automatically-using-visual-studio) nebo [ruční obnovení)](package-restore.md#restore-packages-manually-using-visual-studio)
- [dotnet CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Po úspěšném obnovení by měl být balíček ve složce *global-packages.* U projektů, které používají PackageReference, by se měl soubor obnovit znovu. U projektů pomocí by se měl balíček zobrazit `obj/project.assets.json` `packages.config` ve složce `packages` projektu. Projekt by se teď měl úspěšně sestavit. Pokud ne, [zařiďte problém na GitHubu,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abychom vás mohli sledovat.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Soubor assetů project.assets.jsse nenašel

Kompletní chybová zpráva:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Soubor udržuje graf závislostí projektu při použití formátu správy PackageReference, který se používá k zajištění, že jsou v počítači nainstalované `project.assets.json` všechny potřebné balíčky. Vzhledem k tomu, že se tento soubor generuje dynamicky prostřednictvím obnovení balíčku, obvykle se nepřidá do správy zdrojového kódu. V důsledku toho k této chybě dochází při sestavování projektu pomocí nástroje, jako je například , který `msbuild` automaticky obnovuje balíčky.

V takovém případě spusťte `msbuild -t:restore` příkaz následovaný příkazem `msbuild` nebo použijte příkaz `dotnet build` (který balíčky automaticky obnoví). Můžete také použít jakoukoli z metod obnovení balíčků v [předchozí části](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Jeden nebo více balíčků NuGet je potřeba obnovit, ale ne, protože nebyl udělen souhlas.

Kompletní chybová zpráva:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Tato chyba znamená, že obnovení balíčku je v konfiguraci NuGet zakázané.

Platná nastavení můžete změnit v části Visual Studio, jak je popsáno výše v části Rychlé řešení [pro Visual Studio uživatele](#quick-solution-for-visual-studio-users).

Tato nastavení můžete také upravit přímo v příslušném souboru (obvykle ve Windows a `nuget.config` `%AppData%\NuGet\NuGet.Config` v systému `~/.nuget/NuGet/NuGet.Config` Mac/Linux). Ujistěte se, `enabled` že jsou klíče a v části nastavené na Hodnotu `automatic` `packageRestore` True:

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
> Pokud upravíte nastavení `packageRestore` přímo v , restartujte Visual Studio, aby se v dialogovém okně možností zobrazují `nuget.config` aktuální hodnoty.

## <a name="other-potential-conditions"></a>Další potenciální podmínky

- Může dojít k chybám sestavení kvůli chybějícím souborům se zprávou o použití obnovení NuGet ke stažení. Při spuštění obnovení se ale může zobrazit tato informace: "Všechny balíčky jsou už nainstalované a není nic k obnovení". V takovém případě odstraňte složku (při použití ) nebo souboru (při použití `packages` `packages.config` PackageReference) a znovu spusťte `obj/project.assets.json` obnovení. Pokud chyba přetrvává, pomocí příkazu nebo z příkazového řádku vymažte globální balíčky a složky mezipaměti, jak je popsáno v tématu Správa globálních balíčků a složek `nuget locals all -clear` `dotnet nuget locals all --clear` [mezipaměti](managing-the-global-packages-and-cache-folders.md). 

- Při získávání projektu ze správy zdrojového kódu je možné nastavit složky projektu jen pro čtení. Změňte oprávnění ke složce a zkuste balíčky obnovit znovu.

- Možná používáte starou verzi NuGetu. [Zkontrolujte nuget.org/downloads](https://www.nuget.org/downloads) nejnovější doporučené verze. Pro Visual Studio 2015 doporučujeme 3.6.0.

Pokud narazíte na jiné problémy, [zakažte problém](https://github.com/NuGet/docs.microsoft.com-nuget/issues) na GitHubu, abychom od vás získali další podrobnosti.
