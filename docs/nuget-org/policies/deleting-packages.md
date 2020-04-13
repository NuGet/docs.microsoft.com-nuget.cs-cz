---
title: Odstranění balíčků NuGet z nuget.org
description: Zásady pro vyřazení balíků z nuget.org; trvalé odstranění není podporováno s výjimkou případů, kdy balíčky porušují jiné zásady.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581268"
---
# <a name="deleting-packages"></a>Odstranění balíčků

nuget.org nepodporuje trvalé odstranění balíčků. Tím by se rozbít každý projekt v závislosti na dostupnosti balíčku, zejména s pracovní postupy sestavení, které zahrnují obnovení balíčku.

nuget.org podporuje [zrušení výpisu balíčku](#unlisting-a-package), což lze provést na stránce správy balíčků na webu. Neuvedené balíčky se nezobrazují v nuget.org nebo v uzlech sady Visual Studio a nezobrazují se ve výsledcích hledání. Neuvedené balíčky však lze stále stáhnout a nainstalovat pomocí přesného čísla verze, které podporuje obnovení balíčku. Kromě toho mohou být neuvedené balíčky stále zjištěny v následujících konkrétních scénářích:

- Obnovení balíčku pomocí plovoucích verzí `1.0.0-*`(například ), pokud je nejnovější dostupný balíček odpovídající omezením verze nebo závislostí neuvedený balíček.
- Replikace balíčků prostřednictvím katalogu (protože katalog také obsahuje neuvedené balíčky).

## <a name="exceptions"></a>Výjimky

Ve výjimečných situacích, jako je porušení autorských práv a potenciálně škodlivý obsah, mohou být balíčky ručně odstraněny týmem NuGet. Balíček můžete nahlásit pomocí tlačítka "Nahlásit zneužití" na stránce s podrobnostmi o NuGet.org balíčku. Pokud jste vlastníkem balíčku, přihlaste se ke svému účtu NuGet.org k dosažení podpory NuGet pomocí tlačítka "Kontaktovat podporu" na stránce podrobností NuGet.org balíčku.

## <a name="prohibited-use"></a>Zakázané použití

Balíčky, které splňují některé z následujících kritérií nejsou povoleny na veřejné NuGet galerie a budou okamžitě odebrány bez diskuse. Vlastníci balíčků však budou o odstranění informováni.

- Obsahuje malware, adware nebo jakýkoli druh spywaru.
- Jsou navrženy tak, aby poškodit pracovní stanici vývojáře nebo jejich organizace.
- Porušuje autorská práva nebo porušuje licence.
- Obsahuje neplatný obsah.
- Jsou používány squat na identifikátory balíčků, včetně balíčků, které mají nulový produktivní obsah. Balíky musí obsahovat kód nebo majitelé musí připustit identifikátor někomu, kdo má skutečně produkt k odeslání.
- Pokuste se, aby galerie udělat něco, co není výslovně určen k tomu.

Pokud najdete balíček, který porušuje některou z těchto položek, klikněte na stránce s podrobnostmi o balíčku na odkaz **Nahlásit zneužití** a odešlete zprávu.

Všimněte si, že tým NuGet a .NET Foundation si vyhrazuje právo tato kritéria kdykoli změnit.

## <a name="unlisting-a-package"></a>Zrušení výpisu balíčku
Zrušení seznamu verzí balíčku ji skryje z vyhledávání a ze nuget.org stránce podrobností o balíčku. To umožňuje stávajícím uživatelům balíčku pokračovat v jeho používání, ale snižuje nové přijetí, protože balíček není viditelný ve vyhledávání.

Postup zrušení seznamu balíčku:

1. Vyberte `Your account name` (v pravém horním rohu) >`Manage packages` > `Published packages`
1. Vyberte ikonu "Spravovat balíček"
1. Rozbalte oddíl "Výpis" a vyberte verzi balíčku
1. Zrušte zaškrtnutí políčka "Seznam ve výsledcích hledání" a vyberte možnost Uložit.

Konkrétní verze balíčku byla nyní neuvedena. Chcete-li to ověřit, odhlaste se od svého účtu a přejděte na https://www.nuget.org/packages/YOUR-PACKAGE-NAME/stránku balíčku (bez části verze), např.: . Zobrazí se všechny verze tohoto balíčku, které **nebyly** neuvedeny. Vlastník balíčku však při přihlášení může zobrazit všechny verze a jejich stav výpisu.

Je také možné zamezit verzi balíčku (v případě, že nelze odstranit verzi balíčku). Další informace o zastaralá verze balíčků naleznete [v tématu Zastaralé balíčky](../deprecate-packages.md).
