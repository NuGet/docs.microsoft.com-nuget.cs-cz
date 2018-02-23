---
title: "Opětovné instalace a aktualizace balíčků NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2785879b-97f0-4a85-b3cc-bf4eaa5c39bf
description: "Údaje na to, kdy je potřeba znovu nainstalovat a aktualizovat balíčky, stejně jako u poškozený balíček odkazy v sadě Visual Studio."
keywords: "NuGet balíček instalace, přeinstalování balíčku NuGet, obnovení balíčků NuGet aktualizaci balíčku, Probíhá obnovení balíčků, opravě poškozenými odkazy"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2d62f34819138c51bd9ccc698a8a2495a45824d
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/20/2018
---
# <a name="how-to-reinstall-and-update-packages"></a>Jak znovu nainstalovat a aktualizovat balíčky

Existuje několik situací, popisujeme níže v části [při přeinstalaci balíček](#when-to-reinstall-a-package), kde může získat odkazy na balíček přerušeno v rámci projektu sady Visual Studio. V těchto případech obnoví odinstalovat a potom znovu nainstalovat stejnou verzi balíčku, tyto odkazy na fungují správně. Aktualizace balíčku jednoduše znamená nainstalování aktualizované verze, které často obnoví balíček fungují správně.

Aktualizace a opětovné instalace balíčků se provádí následujícím způsobem:

| Metoda | Aktualizace | Přeinstalujte |
| --- | --- | --- |
| Konzola správce balíčků (popsané v [použití aktualizace balíčku](#using-update-package)) | `Update-Package` příkaz | `Update-Package -reinstall` příkaz |
| Uživatelského rozhraní Správce balíčků | Na **aktualizace** kartě, vyberte jeden nebo více balíčků a vyberte **aktualizace** | Na **nainstalovaná** , vyberte balíček, zaznamenejte jeho název a potom vyberte **odinstalovat**. Přepnout **Procházet** kartě, vyhledejte název balíčku, vyberte ho a pak vyberte **nainstalovat**). |
| nuget.exe CLI | `nuget update` příkaz | Pro všechny balíčky, odstraňte složku balíček a potom spusťte `nuget install`. Pro jeden balíček, odstraňte složku balíčku a použít `nuget install <id>` stejný jako ten, přeinstalujte. |

V tomto článku:

- [Při přeinstalování balíčku](#when-to-reinstall-a-package)
- [Omezení upgradu verze](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Při přeinstalování balíčku

1. **Přerušený odkazy po obnovení balíčků**: Pokud jste otevřeli projekt a obnovení balíčků NuGet, ale stále poškozený najdete odkazy, zkuste znovu nainstalovat každou z těchto balíčků.
1. **Projekt je přerušený kvůli odstraněných souborů**: NuGet není vám zabrání odebrat položky přidané z balíčků, tak, aby byl snadno nechtěně změna nainstalované z balíčku obsahu a rozdělit projektu. Chcete-li obnovit projekt, přeinstalujte ovlivněných balíčků.
1. **Aktualizace balíčku překročila projektu**: Pokud aktualizace balíčku dělí na projekt, selhání je obvykle způsobeno závislost balíčku, který může mít také aktualizován. Chcete-li obnovit stav závislost, přeinstalujte tento konkrétní balíček.
1. **Změna orientace projektu nebo upgrade**: to může být užitečné, když projektu byla změnit cíl necílené nebo upgradovat, a pokud balíček vyžaduje přeinstalace z důvodu změny v cílové rozhraní. NuGet 2.7 a novější zobrazuje chybu sestavení v takových případech hned po Změna orientace projektu a následné sestavení upozornění vám oznamuje, že balíček pravděpodobně nutné přeinstalovat. Pro upgrade projektu NuGet ukazuje chybu v protokolu Upgrade projektu.
1. **Opětovné instalace balíčku při jeho vývoji**: balíček Autoři často nutné přeinstalovat stejnou verzi balíčku se vyvíjí k testování chování. `Install-Package` Příkaz nenabízí možnost vynutit přeinstalovat, takže použití `Update-Package -reinstall` místo.

## <a name="constraining-upgrade-versions"></a>Omezení upgradu verze

Ve výchozím nastavení, opětovné instalace nebo aktualizace balíčku *vždy* nainstaluje nejnovější verzi, která je k dispozici ve zdroji balíčků.

V projektech pomocí `packages.config` formát reference však můžete konkrétně omezit rozsah verze. Například pokud víte, že aplikace funguje pouze s verzí 1.x balíčku ale není 2.0 a vyšší, pravděpodobně kvůli změně hlavní v balíčku rozhraní API, pak by chcete omezit upgrade na 1.x verze. Tím se zabrání náhodnému aktualizace, které by rozdělit aplikace.

Pokud chcete nastavit omezení, otevřete `packages.config` v textovém editoru, vyhledejte dotyčném závislostí a přidat `allowedVersions` atribut s rozsahem verze. Například můžete omezit aktualizace na verzi 1.x, nastavte `allowedVersions` k `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Ve všech případech, použijte zápis popsané v [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Pomocí balíčku aktualizace

Probíhá s vědomím [aspekty](#considerations) popsané dál, můžete snadno přeinstalovat balíčku pomocí [příkaz balíček aktualizace](../Tools/ps-ref-update-package.md) v konzole Správce balíčků Visual Studio (**nástroje**  >  **Správce balíčků NuGet** > **Konzola správce balíčků**):

```ps
Update-Package -Id <package_name> –reinstall
```

Použití tohoto příkazu je mnohem jednodušší než odeberete balíček a potom pokusu o nalezení stejného balíčku v galerii NuGet se stejnou verzí. Všimněte si, že `-Id` přepínač je volitelné.

Stejný příkaz bez `-reinstall` aktualizuje balíček na novější verzi, pokud je k dispozici. Příkaz vrátí chybu, pokud ještě není nainstalovaný dotyčném balíček v projektu. To znamená `Update-Package` nenainstaluje balíčky přímo.

```ps
Update-Package <package_name>
```

Ve výchozím nastavení `Update-Package` ovlivňuje všechny balíčky v řešení. Chcete-li omezit akce na konkrétní projekt, použijte `-ProjectName` přepnout, pomocí názvu projektu, jak se objevuje v Průzkumníku řešení:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

K *aktualizace* všechny balíčky v projektu (nebo přeinstalovat pomocí `-reinstall`), použijte `-ProjectName` bez zadání žádné konkrétní balíček:

```ps
Update-Package -ProjectName MyProject
```

Pokud chcete aktualizovat všechny balíčky v řešení, použijte `Update-Package` samostatně bez argumentů nebo přepínače. Tento formulář použijte pečlivě, protože může trvat poměrně dlouho provádět všechny aktualizace:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Aktualizace balíčky v projektu nebo řešení pomocí [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) vždy aktualizuje na nejnovější verzi balíčku (s výjimkou předběžné verze balíčků). Projekty využívající `packages.config` můžete v případě potřeby omezit verze aktualizací jak je popsáno níže v [Constraining upgradu verze](#constraining-upgrade-versions).

Úplné podrobnosti o příkazu najdete v tématu [balíček aktualizace](../Tools/ps-ref-update-package.md) odkaz.

### <a name="considerations"></a>Důležité informace

Toto může být ovlivněn při přeinstalaci balíčku:

1. **Přeinstalování balíčky podle projektu Změna orientace cílový framework**
    - V případě jednoduchého právě přeinstalace balíčku pomocí `Update-Package –reinstall <package_name>` funguje. Získá Odinstaluje balíček, který je nainstalován na původní cílové rozhraní a stejného balíčku získá nainstaluje proti aktuální cílový framework projektu.
    - V některých případech může být balíček, který nepodporuje nové cílové rozhraní.
        - Pokud balíček podporuje knihovny přenosných tříd (PCLs) a projekt je změnit cíl na necílené kombinace platforem, které již nejsou podporovány balíček, odkazy na balíček chybět po opětovné instalaci.
        - To může surface pro balíčky, které používáte přímo, nebo pro balíčky nainstalované jako závislosti. Je možné, kterou používáte přímo pro podporu nové cílové rozhraní, ale nikoli jeho závislost balíčku.
        - Pokud přeinstalovat balíčky po Změna orientace aplikace vede k sestavení nebo modul runtime chyby, musíte vrátit cílové rozhraní nebo vyhledejte alternativní balíčky, které správně podporují vaší nové cílové rozhraní.

1. **atribut requireReinstallation přidat v souboru Packages.config je po Změna orientace projektu nebo upgradu**
    - Pokud NuGet zjistí, že balíčky situace měla vliv na Změna orientace nebo upgradu na projekt, přidá `requireReinstallation="true"` atribut `packages.config` ke všem vliv balíček odkazuje. Z toho důvodu každé následující sestavení v sadě Visual Studio vyvolá upozornění sestavení pro tyto balíčky, můžete nezapomeňte je přeinstalovat.

1. **Přeinstalování balíčky se závislostmi**
    - `Update-Package –reinstall` přeinstaluje stejnou verzi nástroje původní balíček, ale nainstaluje nejnovější verzi závislosti, pokud jsou k dispozici omezení na konkrétní verzi. To umožňuje aktualizovat jenom závislosti podle potřeby problém opravit. Ale pokud to závislost vrátí zpátky na starší verzi, můžete použít `Update-Package <dependency_name>` přeinstalovat tento závislostí bez ovlivnění závislý balíček.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` přeinstaluje stejnou verzi nástroje původní balíček, ale není znovu nainstalujte závislosti. Použít při aktualizaci závislosti balíčků může mít za následek narušeném stavu

1. **Opětovné instalace balíčků, pokud jsou zahrnuty závislé verze**
    - Jak je popsáno výše, opětovné instalace balíčku nezmění verzích všechny nainstalované balíčky, které na ní závisí. Je možné, a poté přeinstalovat závislost by mohlo způsobit narušení závislý balíček.
