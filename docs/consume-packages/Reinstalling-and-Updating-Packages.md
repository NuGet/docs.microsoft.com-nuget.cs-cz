---
title: Opětovná instalace a aktualizace balíčků NuGet
description: Podrobnosti o Pokud je nutné znovu nainstalovat a aktualizovat balíčky, stejně jako u odkazy na balíček přerušeno v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: c58cf38bab45793bef820e2c52914a91d745ec77
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551780"
---
# <a name="how-to-reinstall-and-update-packages"></a>Jak znovu nainstalovat a aktualizovat balíčky

Existuje mnoho situací, popisujeme níže v části [kdy přeinstalovat balíček](#when-to-reinstall-a-package), kde může získat odkazy na balíček přerušeno v rámci projektu sady Visual Studio. V těchto případech se odinstalovat a znovu nainstalovat stejnou verzi balíčku obnovit tyto odkazy provozuschopný. Aktualizuje se balíček znamená jednoduše nainstalování aktualizované verze, které často obnoví balíček provozuschopný.

Aktualizace a přeinstalace balíčků se provádí následujícím způsobem:

| Metoda | Aktualizace | Znovu nainstalujte |
| --- | --- | --- |
| Konzola správce balíčků (popsané v [pomocí Update-Package](#using-update-package)) | `Update-Package` Příkaz | `Update-Package -reinstall` Příkaz |
| Uživatelské rozhraní Správce balíčků | Na **aktualizace** kartu, vyberte jeden nebo více balíčků a vyberte **aktualizace** | Na **nainstalováno** kartu, vyberte balíček, zaznamenejte její název a potom vyberte **odinstalovat**. Přepněte **Procházet** kartu, vyhledejte název balíčku, vyberte ji a potom vyberte **nainstalovat**). |
| rozhraní příkazového řádku nuget.exe | `nuget update` Příkaz | Pro všechny balíčky, odstraňte složku balíčku a potom spusťte `nuget install`. Pro jeden balíček, odstraňte složku s balíčkem a použít `nuget install <id>` stejný jako ten přeinstalovat. |

V tomto článku:

- [Kdy se má znovu nainstalovat balíček](#when-to-reinstall-a-package)
- [Omezení verze k upgradu](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Kdy se má znovu nainstalovat balíček

1. **Po obnovení balíčků nefunguje odkazy**: Pokud máte otevřen projekt a obnovit balíčky NuGet, ale stále viz nefunkční odkazy, zkuste přeinstalovat každý z těchto balíčků.
1. **Projekt je přerušeno z důvodu odstraněné soubory**: NuGet není vám zabrání odebrat položky přidané z balíčků, tak, aby byl snadno omylem změna nainstalované z balíčku obsahu a přerušení váš projekt. Chcete-li obnovit projekt, přeinstalujte ovlivněné balíčky.
1. **Balíček aktualizace se podařilo přerušit projektu**: Pokud aktualizace balíčku přeruší projektu, selhání je obecně způsobené závislost balíčku, který může mít také aktualizovat. Obnovit stav závislost, přeinstalujte na konkrétní balíček.
1. **Mění se cílení projektu nebo upgradovat**: to může být užitečné, když se změnilo nebo upgradovat projekt, a pokud balíček vyžaduje přeinstalace z důvodu změny v rozhraní .NET framework. NuGet zobrazuje chybu sestavení v takových případech ihned po mění se cílení projektu a upozornění na další sestavení vám oznamuje, že možná bude nutné přeinstalovat balíček. Pro upgrade projektu NuGet zobrazuje chybu do protokolu upgradu projektu.
1. **Opětovná instalace balíčku při jeho vývoji**: balíček Autoři často potřeba znovu nainstalovat stejnou verzi balíčku vyvíjejí otestovat chování. `Install-Package` Příkaz neposkytuje možnost vynutit přeinstalaci, proto `Update-Package -reinstall` místo.

## <a name="constraining-upgrade-versions"></a>Omezení verze k upgradu

Ve výchozím nastavení, opětovné instalace nebo aktualizace balíčku *vždy* nainstaluje nejnovější verzi k dispozici ze zdroje balíčku.

V projektech pomocí `packages.config` formátu správy však můžete konkrétně omezit rozsah verzí. Například pokud víte, že vaše aplikace funguje pouze s verzí 1.x balíčku ale není 2.0 a vyšší, pravděpodobně kvůli zásadní změny v balíčku rozhraní API a pak byste měli omezit inovace na verze 1.x. To zabrání náhodnému aktualizace, které by se narušil aplikace.

Pokud chcete nastavit omezení, otevřete `packages.config` v textovém editoru, najděte dotyčný závislostí a přidejte `allowedVersions` atribut s rozsah verzí. Například, chcete-li omezit aktualizace na verzi 1.x, nastavte `allowedVersions` k `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Ve všech případech použijte notaci podle [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Použití Update-Package

Probíhá s vědomím [aspekty](#considerations) je popsáno níže, můžete snadno přeinstalovat balíček pomocí [příkazu Update-Package](../Tools/ps-ref-update-package.md) v konzole Správce balíčků Visual Studio (**nástroje**  >  **Správce balíčků NuGet** > **Konzola správce balíčků**):

```ps
Update-Package -Id <package_name> –reinstall
```

Pomocí tohoto příkazu je mnohem jednodušší než odebírá se balíček a pak se pokusíte použít k vyhledání balíčku, stejné v galerii NuGet se stejnou verzí. Všimněte si, že `-Id` přepínač je volitelné.

Stejný příkaz bez `-reinstall` balíček aktualizace na novější verzi, pokud je k dispozici. Příkaz vrátí chybu, pokud ještě nemáte nainstalovaný balíček dotyčný v projektu. To znamená `Update-Package` není možné nainstalovat balíčky přímo.

```ps
Update-Package <package_name>
```

Ve výchozím nastavení `Update-Package` ovlivňuje všechny projekty v řešení. Chcete-li omezit akce k určitému projektu, použijte `-ProjectName` přepnout, pomocí názvu projektu, jak se zobrazí v Průzkumníku řešení:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

K *aktualizovat* všechny balíčky v projektu (nebo přeinstalovat pomocí `-reinstall`), použijte `-ProjectName` bez zadání jakékoli konkrétního balíčku:

```ps
Update-Package -ProjectName MyProject
```

Pokud chcete aktualizovat všechny balíčky v řešení, stačí použít `Update-Package` samostatně pomocí žádné argumenty ani přepínače. Tento formulář používejte opatrně, protože to může trvat docela dlouho, můžete provést všechny aktualizace:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Aktualizují se balíčky v projektu nebo řešení pomocí [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) vždy aktualizuje na nejnovější verzi balíčku (s výjimkou balíčky v předběžné verzi). Projekty, které používají `packages.config` , v případě potřeby omezit verze aktualizací jak je popsáno níže v [verze k upgradu Constraining](#constraining-upgrade-versions).

Všechny podrobnosti o příkazu najdete v článku [Update-Package](../Tools/ps-ref-update-package.md) odkaz.

### <a name="considerations"></a>Důležité informace

Následující mohou být ovlivněny při opětovné instalaci balíčku:

1. **Přeinstalace balíčků podle projektu cílové rozhraní framework mění se cílení**
    - V jednoduchém případě stačí přeinstalace balíčků pomocí `Update-Package –reinstall <package_name>` funguje. Odinstaluje balíček, který je nainstalován s původní cílovou architekturu a stejného balíčku se nainstaluje s aktuálním cílovém rozhraní projektu.
    - V některých případech může být balíček, který nepodporuje novou cílovou architekturou.
        - Pokud balíček podporuje přenosné knihovny tříd (PCLs) a cíl projektu změněn na kombinaci platformy již nejsou podporovány balíček, odkazy na balíček bude chybět po opětovné instalaci.
        - To může přinášet pro balíčky, které používáte přímo, nebo pro balíčky nainstalované jako závislosti. Je možné pro balíček, který používáte přímo pro podporu novou cílovou architekturou, ale nikoli jeho závislostí.
        - Pokud po mění se cílení aplikace vede k sestavení nebo modulu runtime chyby přeinstalace balíčků, budete muset vrátit cílové architektury nebo hledat alternativní balíčky, které podporují správně novému cílovému rozhraní.

1. **atribut requireReinstallation přidaní v souboru packages.config mění se cílení projektu nebo upgrade**
    - Pokud zjistí NuGet, balíčky byly ovlivněny Přeorientovat nebo upgrade projektu, přidá `requireReinstallation="true"` atribut `packages.config` na všechny ovlivněné odkazy na balíček. Z tohoto důvodu každé následující sestavení v sadě Visual Studio vyvolá upozornění sestavení pro tyto balíčky, které si zapamatujete, tak je znovu nainstaluje.

1. **Přeinstalace balíčků se závislostmi**
    - `Update-Package –reinstall` Configuration Manager přeinstaluje stejnou verzi původní balíček, ale nainstaluje nejnovější verzi závislosti, pokud jsou k dispozici omezení na konkrétní verzi. Umožňuje aktualizovat jenom závislosti podle potřeby problém opravit. Nicméně pokud závislost to vrátí zpátky na starší verzi, můžete použít `Update-Package <dependency_name>` přeinstalovat tuto jednu závislost, aniž by to ovlivnilo závislý balíček.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` Configuration Manager přeinstaluje stejnou verzi původní balíček, ale není znovu nainstalovat závislosti. Použijte ho, když je porušený aktualizace závislosti balíčků může způsobit

1. **Pokud jsou zahrnuty verze závislé přeinstalace balíčků**
    - Jak jsme vysvětlili výše, opětovné instalace balíčku nezmění verzích jiné nainstalované balíčky, které jsou na ní závislé. Je možné, a pak přeinstalovat závislost by mohlo narušit závislý balíček.
