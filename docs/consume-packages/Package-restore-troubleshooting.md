---
title: Řešení potíží s obnovením balíčku NuGet v aplikaci Visual Studio
description: Popis běžných chyb obnovení NuGet v aplikaci Visual Studio a jejich řešení.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860625"
---
# <a name="troubleshooting-package-restore-errors"></a>Řešení potíží s chybami při obnovení balíčku

Tento článek se zaměřuje na běžné chyby při obnovení balíčků a postupu jejich řešení. 

Obnovení balíčku se pokusí nainstalovat všechny závislosti balíčků do správného stavu, který odpovídá odkazům na balíček v souboru projektu ( *. csproj*) nebo souboru *Packages. config* . (V aplikaci Visual Studio se odkazy zobrazí v Průzkumník řešení pod uzlem **závislosti \ NuGet** nebo **odkazy** .) Postup obnovení balíčků pomocí požadovaných kroků najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md#restore-packages). Pokud balíček odkazuje v souboru projektu ( *. csproj*) nebo soubor Packages *. config* je nesprávný (neshoduje se s požadovaným stavem po obnovení balíčku), je třeba nainstalovat nebo aktualizovat balíčky namísto použití balíčku. Obnovil.

Pokud vám pokyny pro vás nefungují, zajistěte [prosím problém na GitHubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , abychom mohli podrobněji prošetřit svůj scénář. Nepoužívejte tuto stránku jako užitečnou? ovládací prvek, který se může zobrazit na této stránce, protože nám nedává možnost kontaktovat vám další informace

## <a name="quick-solution-for-visual-studio-users"></a>Rychlé řešení pro uživatele sady Visual Studio

Pokud používáte sadu Visual Studio, nejprve povolte obnovení balíčku následujícím způsobem. V opačném případě pokračujte v následujících oddílech.

1. Vyberte **nástroje > správce balíčků NuGet > nabídce Nastavení správce balíčků** .
1. V části **obnovení balíčku**nastavte obě možnosti.
1. Vyberte **OK**.
1. Sestavte projekt znovu.

![Povolit obnovení balíčků NuGet v nástrojích/možnostech](../consume-packages/media/restore-01-autorestoreoptions.png)

Tato nastavení lze také změnit v `NuGet.config` souboru. informace najdete v části věnované [souhlasu](#consent) . Pokud je váš projekt starší projekt, který používá obnovení balíčku integrovaného MSBuild, může být nutné [migrovat](package-restore.md#migrate-to-automatic-package-restore-visual-studio) na automatické obnovení balíčku.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Tento projekt odkazuje na balíčky NuGet, které na tomto počítači chybí.

Úplná chybová zpráva:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

K této chybě dochází, když se pokusíte sestavit projekt, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky se v počítači nebo v projektu aktuálně neinstalují.

- Při použití formátu správy [PackageReference](package-references-in-project-files.md) chyba znamená, že balíček není nainstalován ve složce *Global-Packages* , jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).
- Při použití [souboru Packages. config](../reference/packages-config.md)chyba znamená, že balíček není nainstalován ve `packages` složce v kořenu řešení.

K této situaci obvykle dochází, když získáte zdrojový kód projektu ze správy zdrojového kódu nebo z jiného stahování. Balíčky jsou obvykle vynechány ze správy zdrojového kódu nebo ze souborů ke stažení, protože je lze obnovit z kanálů balíčků jako nuget.org (viz [balíčky a Správa zdrojového kódu](Packages-and-Source-Control.md)). Zahrnutí by jinak dispozici determinističtější úložiště nebo vytvářet zbytečně velké soubory. zip.

K této chybě může dojít také v případě, že soubor projektu obsahuje absolutní cesty k umístěním balíčků a přesouváte projekt.

K obnovení balíčků použijte jednu z následujících metod:

- Pokud jste přesunuli soubor projektu, upravte soubor přímo a aktualizujte odkazy na balíčky.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([Automatické obnovení](package-restore.md#restore-packages-automatically-using-visual-studio) nebo [Ruční obnovení](package-restore.md#restore-packages-manually-using-visual-studio))
- [dotnet CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Po úspěšném obnovení by měl být balíček přítomen ve složce *Global-Packages* . Pro projekty, které používají PackageReference, by měl obnovení `obj/project.assets.json` soubor znovu vytvořit; pro projekty, které používají `packages.config`, by se měl balíček `packages` zobrazit ve složce projektu. Projekt by se teď měl úspěšně sestavit. Pokud ne, zapište [problém na GitHubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , abychom mohli pokračovat s vámi.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Soubor prostředků Project. assets. JSON se nenašel.

Úplná chybová zpráva:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` Soubor udržuje graf závislosti projektu při použití formátu správy PackageReference, který se používá k tomu, aby se zajistilo, že jsou v počítači nainstalovány všechny potřebné balíčky. Vzhledem k tomu, že tento soubor je generován dynamicky prostřednictvím obnovení balíčku, obvykle není přidán do správy zdrojového kódu. V důsledku toho k této chybě dochází při sestavování projektu s nástrojem `msbuild` , který neobnoví automaticky balíčky.

V takovém případě spusťte `msbuild -t:restore` `msbuild`nebo použijte `dotnet build` (který automaticky obnoví balíčky). Můžete také použít kteroukoli z metod obnovení balíčků v [předchozí části](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Nejméně jeden balíček NuGet je potřeba obnovit, ale nedala se k němu udělit souhlas.

Úplná chybová zpráva:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Tato chyba znamená, že obnovení balíčku je v konfiguraci NuGet zakázané.

V aplikaci Visual Studio můžete změnit příslušná nastavení, jak je popsáno výše v části [rychlé řešení pro uživatele sady Visual Studio](#quick-solution-for-visual-studio-users).

Tato nastavení můžete také upravit přímo v příslušném `nuget.config` souboru (obvykle `%AppData%\NuGet\NuGet.Config` ve Windows a `~/.nuget/NuGet/NuGet.Config` v systému Mac/Linux). Ujistěte se `enabled` , že `automatic` klíče a `packageRestore` v části jsou nastaveny na hodnotu true:

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
> Pokud upravíte `packageRestore` nastavení přímo v `nuget.config`, restartujte Visual Studio tak, aby se v dialogovém okně Možnosti zobrazily aktuální hodnoty.

## <a name="other-potential-conditions"></a>Další možné podmínky

- Může dojít k chybám sestavení z důvodu chybějících souborů. zpráva říká použití obnovení NuGet ke stažení. Při spuštění obnovení ale může znamenat, že všechny balíčky jsou už nainstalované a neexistuje žádná obnova. " V takovém případě odstraňte `packages` složku (při použití `packages.config`) nebo `obj/project.assets.json` soubor (při použití PackageReference) a znovu spusťte obnovení. Pokud chyba stále `nuget locals all -clear` přetrvává, pomocí příkazu nebo `dotnet locals all --clear` z příkazového řádku zrušte zaškrtnutí popsaných složek *Global-Packages* a cache, jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).

- Při získávání projektu ze správy zdrojového kódu mohou být složky projektu nastaveny jen pro čtení. Změňte oprávnění složky a zkuste znovu obnovit balíčky.

- Je možné, že používáte starou verzi NuGet. Vyhledejte nejnovější Doporučené verze v [NuGet.org/downloads](https://www.nuget.org/downloads) . Pro Visual Studio 2015 doporučujeme 3.6.0.

Pokud narazíte na jiné problémy, zapište [problém na GitHubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , abychom vám mohli získat další podrobnosti.
