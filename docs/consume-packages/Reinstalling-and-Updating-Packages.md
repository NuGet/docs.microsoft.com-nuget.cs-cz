---
title: Přeinstalace a aktualizace balíčků NuGet
description: Podrobnosti o tom, kdy je nutné přeinstalovat a aktualizovat balíčky, jako u nefunkčních odkazů na balíčky v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 101c6d6b9d93da912f60c40b27559e80327154b8
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428700"
---
# <a name="how-to-reinstall-and-update-packages"></a>Jak přeinstalovat a aktualizovat balíčky

Existuje řada situací popsaných níže v části [Při přeinstalaci balíčku](#when-to-reinstall-a-package), kde odkazy na balíček může dojít k porušení v rámci projektu sady Visual Studio. V těchto případech odinstalování a přeinstalování stejné verze balíčku obnoví tyto odkazy na funkční pořádek. Aktualizace balíčku jednoduše znamená instalaci aktualizované verze, která často obnoví balíček do funkčního stavu.

V sadě Visual Studio nabízí konzola Správce balíčků mnoho flexibilních možností aktualizace a přeinstalace balíčků.

Aktualizace a přeinstalace balíčků se provádí následujícím způsobem:

| Metoda | Aktualizace | Přeinstalovat |
| --- | --- | --- |
| Konzola Správce balíčků (popsaná v [pořce Pomocí balíčku aktualizací)](#using-update-package) | Příkaz `Update-Package` | Příkaz `Update-Package -reinstall` |
| Uživatelské rozhraní Správce balíčků | Na kartě **Aktualizace** vyberte jeden nebo více balíčků a vyberte **Aktualizovat** | Na kartě **Nainstalováno** vyberte balíček, zaznamenejte jeho název a pak vyberte **Odinstalovat**. Přepněte na kartu **Procházet,** vyhledejte název balíčku, vyberte jej a pak vyberte **Instalovat**). |
| Rozhraní příkazového řádku nuget.exe | Příkaz `nuget update` | U všech balíčků odstraňte složku `nuget install`balíčku a spusťte . U jednoho balíčku odstraňte složku `nuget install <id>` balíčku a použijte k přeinstalaci stejné. |

> [!NOTE]
> Pro dotnet CLI ekvivalentní postup není vyžadován. V podobném scénáři můžete [obnovit balíčky s dotnet CLI](package-restore.md#restore-using-the-dotnet-cli).

V tomto článku:

- [Kdy přeinstalovat balíček](#when-to-reinstall-a-package)
- [Omezení verzí upgradu](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Kdy přeinstalovat balíček

1. **Přerušené odkazy po obnovení balíčku**: Pokud jste otevřeli projekt a obnovili balíčky NuGet, ale stále se zobrazují poškozené odkazy, zkuste každý z těchto balíčků přeinstalovat.
1. **Projekt je přerušeno z důvodu odstraněných souborů**: NuGet nezabrání odebrání položek přidaných z balíčků, takže je snadné neúmyslně upravit obsah nainstalovaný z balíčku a přerušit projekt. Chcete-li projekt obnovit, přeinstalujte ohrožené balíčky.
1. **Aktualizace balíčku přerušila projekt**: Pokud aktualizace balíčku rozdělí projekt, selhání je obecně způsobeno balíčkem závislostí, který mohl být také aktualizován. Chcete-li obnovit stav závislosti, přeinstalujte tento konkrétní balíček.
1. **Opětovné zacílení nebo upgrade projektu**: To může být užitečné, když byl projekt přecílen nebo upgradován a pokud balíček vyžaduje přeinstalaci z důvodu změny v cílovém rámci. NuGet zobrazí chybu sestavení v takových případech ihned po opětovném zacílení projektu a následné sestavení upozornění, že balíček může být nutné přeinstalovat. Pro upgrade projektu NuGet zobrazí chybu v protokolu upgradu projektu.
1. **Přeinstalace balíčku během jeho vývoje**: Autoři balíčku často potřebují přeinstalovat stejnou verzi balíčku, kterou vyvíjejí, aby otestovali chování. Příkaz `Install-Package` neposkytuje možnost vynutit přeinstalaci, `Update-Package -reinstall` proto použijte místo.

## <a name="constraining-upgrade-versions"></a>Omezení verzí upgradu

Ve výchozím nastavení přeinstalace nebo aktualizace balíčku *vždy* nainstaluje nejnovější verzi dostupnou ze zdroje balíčku.

V projektech `packages.config` používajích formát správy však můžete konkrétně omezit rozsah verzí. Například pokud víte, že vaše aplikace funguje pouze s verzí 1.x balíčku, ale ne 2.0 a vyšší, možná z důvodu významné změny v rozhraní API balíčku, pak byste chtěli omezit upgrady na verze 1.x. Tím se zabrání náhodné aktualizace, které by přerušit aplikaci.

Chcete-li nastavit `packages.config` omezení, otevřete v textovém editoru, `allowedVersions` vyhledejte dotyčnou závislost a přidejte atribut s rozsahem verzí. Chcete-li například omezit aktualizace verze 1.x, nastavte `allowedVersions` na `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Ve všech případech použijte zápis popsaný v [package versioning](../concepts/package-versioning.md#version-ranges).

## <a name="using-update-package"></a>Použití balíčku aktualizace

S ohledem na [důležité informace](#considerations) popsané níže, můžete snadno přeinstalovat libovolný balíček pomocí [příkazu Update-Package](../reference/ps-reference/ps-ref-update-package.md) v konzole Správce balíčků sady Visual Studio **(Nástroje** > **NuGet Package Manager** > **Console**).

```ps
Update-Package -Id <package_name> –reinstall
```

Použití tohoto příkazu je mnohem jednodušší než odebrání balíčku a pokusu o vyhledání stejného balíčku v galerii NuGet se stejnou verzí. Všimněte `-Id` si, že přepínač je volitelný.

Stejný příkaz `-reinstall` bez aktualizace balíčku na novější verzi, pokud je k dispozici. Příkaz poskytuje chybu, pokud daný balíček již není nainstalován v projektu; to znamená, `Update-Package` že nenainstaluje balíčky přímo.

```ps
Update-Package <package_name>
```

Ve výchozím `Update-Package` nastavení ovlivňuje všechny projekty v řešení. Chcete-li akci omezit na konkrétní `-ProjectName` projekt, použijte přepínač pomocí názvu projektu tak, jak je uveden v Průzkumníku řešení:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Chcete-li *aktualizovat* všechny balíčky v `-reinstall`projektu `-ProjectName` (nebo přeinstalovat pomocí ), použijte bez zadání konkrétní balíček:

```ps
Update-Package -ProjectName MyProject
```

Chcete-li aktualizovat všechny balíčky `Update-Package` v řešení, stačí použít samostatně bez jiných argumentů nebo přepínačů. Tento formulář používejte opatrně, protože provedení všech aktualizací může trvat značnou dobu:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Aktualizace balíčků v projektu nebo řešení pomocí [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) vždy aktualizuje nejnovější verzi balíčku (s výjimkou předběžných verzí balíčků). Projekty, `packages.config` které používají, mohou v případě potřeby omezit verze aktualizací, jak je popsáno níže v [oznámení Omezující verze upgradu](#constraining-upgrade-versions).

Podrobné informace o příkazu naleznete v odkazu [update-package.](../reference/ps-reference/ps-ref-update-package.md)

### <a name="considerations"></a>Požadavky

Při přeinstalaci balíčku mohou být ovlivněny následující skutečnosti:

1. **Přeinstalace balíčků podle retargetingu cílového rámce projektu**
    - V jednoduchém případě, stačí přeinstalovat balíček pomocí `Update-Package –reinstall <package_name>` funguje. Balíček, který je nainstalován proti staré cílové rozhraní získá odinstalován a stejný balíček získá nainstalován proti aktuální cílové rozhraní projektu.
    - V některých případech může existovat balíček, který nepodporuje nový cílový rámec.
        - Pokud balíček podporuje knihovny přenosných tříd (PCL) a projekt je přecílen na kombinaci platforem, které již balíček nepodporuje, odkazy na balíček budou po přeinstalaci chybět.
        - To může povrch pro balíčky, které používáte přímo nebo pro balíčky nainstalované jako závislosti. Je možné pro balíček, který používáte přímo pro podporu nové cílové rozhraní, zatímco jeho závislost není.
        - Pokud přeinstalace balíčků po retargeting u vaší aplikace vede k chybám sestavení nebo běhu, budete muset vrátit cílové rozhraní nebo vyhledat alternativní balíčky, které správně podporují váš nový cílový rámec.

1. **requireReinstallation attribute added in packages.config after project retargeting or upgrade requireReinstallation attribute added in packages.config after project retargeting or upgrade requireReinstallation attribute added in packages.config after project retargeting or upgrade requireRe**
    - Pokud NuGet zjistí, že balíčky byly ovlivněny retargeting nebo `requireReinstallation="true"` upgrade `packages.config` projektu, přidá atribut do všech odkazů na balíček ovlivněné. Z tohoto důvodu každé následné sestavení v sadě Visual Studio vyvolává upozornění sestavení pro tyto balíčky, takže si můžete pamatovat přeinstalovat.

1. **Přeinstalace balíčků se závislostmi**
    - `Update-Package –reinstall`Přeinstaluje stejnou verzi původního balíčku, ale nainstaluje nejnovější verzi závislostí, pokud nejsou k dispozici omezení konkrétní verze. To umožňuje aktualizovat pouze závislosti podle potřeby opravit problém. Pokud se však toto svalí závislost zpět `Update-Package <dependency_name>` do starší verze, můžete přeinstalovat tuto jednu závislost bez ovlivnění závislého balíčku.
    - `Update-Package –reinstall <packageName> -ignoreDependencies`Přeinstaluje stejnou verzi původního balíčku, ale nepřeinstaluje závislosti. Tuto možnost použijte při aktualizaci závislostí balíčků, které mohou mít za následek přerušený stav.

1. **Přeinstalace balíčků v případě, že se jedná o závislé verze**
    - Jak je vysvětleno výše, přeinstalování balíčku nezmění verze jiných nainstalovaných balíčků, které jsou na něm závislé. Je tedy možné, že přeinstalování závislosti může přerušit závislý balíček.
