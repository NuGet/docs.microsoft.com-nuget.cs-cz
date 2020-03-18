---
title: Přeinstalace a aktualizace balíčků NuGet
description: Podrobnosti o tom, kdy je nutné přeinstalovat a aktualizovat balíčky, stejně jako v případě nefunkčních odkazů na balíčky v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 101c6d6b9d93da912f60c40b27559e80327154b8
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428700"
---
# <a name="how-to-reinstall-and-update-packages"></a>Postup přeinstalace a aktualizace balíčků

Existuje několik situací, které jsou popsány níže v části [kdy se má přeinstalovat balíček](#when-to-reinstall-a-package), kde se odkazy na balíček mohou v projektu sady Visual Studio rozdělit. V těchto případech dojde k obnovení těchto odkazů na pracovní objednávku odinstalací a opětovnou instalací stejné verze balíčku. Aktualizace balíčku jednoduše znamená instalaci aktualizované verze, která často obnoví balíček do funkčního pořadí.

V aplikaci Visual Studio poskytuje konzola správce balíčků mnoho flexibilních možností pro aktualizaci a přeinstalaci balíčků.

Aktualizace a přeinstalace balíčků se provádí takto:

| Metoda | Aktualizace | Instaluje |
| --- | --- | --- |
| Konzola správce balíčků (popsaná v tématu [použití balíčku Update-Package](#using-update-package)) | `Update-Package` – příkaz | `Update-Package -reinstall` – příkaz |
| Uživatelské rozhraní Správce balíčků | Na kartě **aktualizace** vyberte jeden nebo více balíčků a vyberte **aktualizovat** . | Na kartě **nainstalované** vyberte balíček, zaznamenejte jeho název a pak vyberte **odinstalovat**. Přepněte na kartu **Procházet** , vyhledejte název balíčku, vyberte ho a pak vyberte **nainstalovat**). |
| rozhraní příkazového řádku NuGet. exe | `nuget update` – příkaz | Pro všechny balíčky odstraňte složku balíčku a pak spusťte `nuget install`. U jednoho balíčku odstraňte složku balíčku a použijte `nuget install <id>` k přeinstalování stejné. |

> [!NOTE]
> Pro rozhraní příkazového řádku dotnet není ekvivalentní postup povinný. V podobném scénáři můžete [balíčky obnovit pomocí rozhraní příkazového řádku dotnet](package-restore.md#restore-using-the-dotnet-cli).

V tomto článku:

- [Kdy přeinstalovat balíček](#when-to-reinstall-a-package)
- [Omezení verzí upgradu](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Kdy přeinstalovat balíček

1. **Poškozené odkazy po obnovení balíčku**: Pokud jste otevřeli projekt a obnovili balíčky NuGet, ale pořád vidíte poškozené odkazy, zkuste všechny tyto balíčky přeinstalovat.
1. **Projekt je přerušen z důvodu odstraněných souborů**: nástroj NuGet nebrání v odebírání položek přidaných z balíčků, takže je snadné nechtěně upravovat obsah nainstalovaný z balíčku a poškodit projekt. Chcete-li obnovit projekt, přeinstalujte příslušné balíčky.
1. **Aktualizace balíčku podařilo přerušit projekt**: Pokud aktualizace balíčku ukončí nějaký projekt, je selhání většinou způsobeno balíčkem závislostí, který se taky mohl aktualizovat. Chcete-li obnovit stav závislosti, přeinstalujte tento konkrétní balíček.
1. Změna **cílení nebo upgrade projektu**: to může být užitečné, pokud byl projekt změněn na cílený nebo upgradovaný a pokud balíček vyžaduje přeinstalaci z důvodu změny v cílové verzi rozhraní .NET Framework. NuGet zobrazuje chybu sestavení v takových případech ihned po provedení změny cíle projektu a následné výstrahy sestavení vám upozorní, že je možné balíček potřebovat přeinstalovat. V případě upgradu projektu NuGet zobrazuje chybu v protokolu upgradu projektu.
1. **Přeinstalace balíčku během vývoje**: autoři balíčku často potřebují přeinstalovat stejnou verzi balíčku, kterou vyvíjí, aby bylo možné chování otestovat. Příkaz `Install-Package` neposkytuje možnost vynutit přeinstalaci, takže místo toho použijte `Update-Package -reinstall`.

## <a name="constraining-upgrade-versions"></a>Omezení verzí upgradu

Při přeinstalaci nebo aktualizaci balíčku se ve výchozím nastavení *vždycky* nainstaluje nejnovější verze dostupná ze zdroje balíčku.

V projektech, které používají formát správy `packages.config`, však můžete rozsah verzí omezit. Pokud například víte, že vaše aplikace funguje jenom s verzí 1. x balíčku, ale ne 2,0 a vyšší, možná z důvodu významné změny v rozhraní API balíčku, pak byste chtěli omezit upgrady na 1. x verze. Tím zabráníte náhodným aktualizacím, které by aplikaci přerušily.

Chcete-li nastavit omezení, otevřete `packages.config` v textovém editoru, vyhledejte příslušnou závislost a přidejte atribut `allowedVersions` s rozsahem verzí. Chcete-li například omezit aktualizace na verzi 1. x, nastavte `allowedVersions` na `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Ve všech případech použijte zápis popsaný v tématu [Správa verzí balíčku](../concepts/package-versioning.md#version-ranges).

## <a name="using-update-package"></a>Použití Update-Package

Vědomi si níže uvedených [faktorů](#considerations) můžete snadno přeinstalovat všechny balíčky pomocí [příkazu Update-Package](../reference/ps-reference/ps-ref-update-package.md) v konzole správce balíčků sady Visual Studio (**nástroje** > **Správce balíčků NuGet** > **konzole správce balíčků**).

```ps
Update-Package -Id <package_name> –reinstall
```

Použití tohoto příkazu je mnohem jednodušší než odebrání balíčku a pak pokus o vyhledání stejného balíčku v galerii NuGet se stejnou verzí. Všimněte si, že přepínač `-Id` je nepovinný.

Stejný příkaz bez `-reinstall` aktualizuje balíček na novější verzi, pokud je k dispozici. Příkaz obsahuje chybu, pokud daný balíček ještě není v projektu nainstalován. To znamená, že `Update-Package` neinstaluje balíčky přímo.

```ps
Update-Package <package_name>
```

Ve výchozím nastavení `Update-Package` ovlivňuje všechny projekty v řešení. Chcete-li omezit akci na konkrétní projekt, použijte přepínač `-ProjectName` s použitím názvu projektu, jak je zobrazen v Průzkumník řešení:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Chcete-li *aktualizovat* všechny balíčky v projektu (nebo přeinstalovat pomocí `-reinstall`), použijte `-ProjectName` bez zadání konkrétního balíčku:

```ps
Update-Package -ProjectName MyProject
```

Chcete-li aktualizovat všechny balíčky v řešení, stačí použít `Update-Package` sám o sobě bez dalších argumentů nebo přepínačů. Tento formulář používejte opatrně, protože může trvat značnou dobu, než se provedou všechny aktualizace:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Aktualizace balíčků v projektu nebo řešení pomocí [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) vždy aktualizuje na nejnovější verzi balíčku (s výjimkou předběžných verzí balíčků). Projekty, které používají `packages.config` mohou v případě potřeby omezit verze aktualizací, jak je popsáno níže v tématu omezení [verzí upgradu](#constraining-upgrade-versions).

Úplné podrobnosti o příkazu naleznete v tématu [Update-Package](../reference/ps-reference/ps-ref-update-package.md) reference.

### <a name="considerations"></a>Požadavky

Při přeinstalaci balíčku se může týkat následující:

1. **Přeinstalace balíčků podle cílení cílového rozhraní .NET Framework**
    - V jednoduchém případě stačí znovu nainstalovat balíček pomocí `Update-Package –reinstall <package_name>` funguje. Balíček, který je nainstalovaný proti starému cílovému rozhraní, se odinstaluje a stejný balíček se nainstaluje na aktuální cílovou architekturu projektu.
    - V některých případech může existovat balíček, který nepodporuje novou cílovou architekturu.
        - Pokud balíček podporuje přenositelné knihovny tříd (PCLs) a projekt je zaměřen na kombinaci platforem, které již balíček nepodporuje, odkazy na balíček budou po přeinstalování chybět.
        - To může být plochy pro balíčky, které používáte přímo, nebo pro balíčky nainstalované jako závislosti. Je možné, že balíček, který používáte, přímo pro podporu nového cílového rozhraní, zatímco jeho závislost není.
        - Pokud přeinstalujete balíčky po provedení změny cíle aplikace v důsledku chyb sestavení nebo modulu runtime, možná budete muset vrátit cílové rozhraní nebo vyhledat alternativní balíčky, které správně podporují vaše nové cílové rozhraní.

1. **atribut requireReinstallation se přidal do souboru Packages. config po provedení změny cíle nebo upgradu projektu.**
    - Pokud NuGet detekuje, že balíčky byly ovlivněny změnou cílení nebo upgradem projektu, přidá do `packages.config` atribut `requireReinstallation="true"` do všech ovlivněných odkazů na balíčky. Z tohoto důvodu každé následné sestavení v aplikaci Visual Studio vyvolává pro tyto balíčky upozornění sestavení, abyste si je mohli znovu nainstalovat.

1. **Přeinstalace balíčků se závislostmi**
    - `Update-Package –reinstall` přeinstaluje stejnou verzi původního balíčku, ale nainstaluje nejnovější verzi závislostí, pokud nejsou k dispozici specifická omezení verze. To vám umožní aktualizovat pouze závislosti, jak je potřeba k vyřešení problému. Pokud se ale vrátí závislost zpátky na předchozí verzi, můžete použít `Update-Package <dependency_name>` k přeinstalování této závislosti, aniž by to ovlivnilo závislý balíček.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` přeinstaluje stejnou verzi původního balíčku, ale neinstaluje závislosti. Toto použijte v případě, že aktualizace závislostí balíčku může mít za následek poškozený stav.

1. **Přeinstalace balíčků, pokud jsou zapojené závislé verze**
    - Jak je vysvětleno výše, opětovná instalace balíčku nemění verze dalších nainstalovaných balíčků, které jsou na ní závislé. Je možné, že přeinstalování závislosti může poškodit závislý balíček.
