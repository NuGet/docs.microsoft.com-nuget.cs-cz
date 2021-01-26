---
title: Odstraňují se balíčky NuGet z nuget.org.
description: Zásady pro odseznamování balíčků z nuget.org; trvalé odstranění se nepodporuje s výjimkou případů, kdy balíčky narušují jiné zásady.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: e5c62177b40162cb8b6b37b0d272fb7a945156c1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775704"
---
# <a name="deleting-packages"></a>Odstranění balíčků

nuget.org nepodporuje trvalé odstranění balíčků. Tím by se všechny projekty přerušily v závislosti na dostupnosti balíčku, zejména při vytváření pracovních postupů, které zahrnují obnovení balíčku.

nuget.org podporuje [odbalení balíčku](#unlisting-a-package), který se dá provést na stránce Správa balíčků na webu. Neuvedené balíčky se nezobrazí v nuget.org nebo v uživatelském rozhraní sady Visual Studio a ve výsledcích hledání se nezobrazí. Neuvedené balíčky se ale pořád dají stáhnout a nainstalovat přes přesné číslo verze, které podporuje obnovení balíčku. Kromě toho mohou být neuvedené balíčky stále zjištěny v následujících konkrétních scénářích:

- Obnovení balíčků pomocí plovoucích verzí (například `1.0.0-*` ), pokud nejnovější dostupný balíček, který odpovídá omezením verze nebo závislosti, je neuvedené balíčky.
- Replikace balíčků prostřednictvím katalogu (jako katalog obsahuje také neuvedené balíčky).

## <a name="exceptions"></a>Výjimky

Ve výjimečných situacích, jako je porušení autorského práva a potenciálně škodlivý obsah, je možné balíčky odstranit ručně týmem NuGet. Balíček můžete ohlásit pomocí tlačítka pro zneužití sestav na stránce s podrobnostmi balíčku NuGet.org. Pokud jste vlastníkem balíčku, přihlaste se k účtu NuGet.org, abyste mohli získat podporu NuGet pomocí tlačítka "kontaktujte podporu" na stránce s podrobnostmi balíčku NuGet.org.

## <a name="prohibited-use"></a>Zakázané použití

Balíčky, které splňují některá z následujících kritérií, nejsou ve veřejné galerii NuGet povolené a budou se okamžitě odebírat bez diskuze. Vlastníci balíčku budou ale upozorněni na odebrání.

- Obsahuje malware, adware nebo jakýkoliv druh spywaru.
- Jsou navržené tak, aby poškodily pracovní stanici nebo jejich organizaci vývojářů.
- Odrušuje autorská práva nebo porušuje licence.
- Obsahuje neplatný obsah.
- Slouží k squatí identifikátorů balíčků, včetně balíčků, které nemají žádný produktivní obsah. Balíčky musí obsahovat kód nebo vlastníci musí povolit identifikátor někomu, kdo má produkt k odeslání.
- Pokusí se Galerie udělat něco, co není výslovně navržené.

Pokud zjistíte balíček, který je v rozporu s některou z těchto položek, klikněte na odkaz **Oznámit zneužití** na stránce s podrobnostmi balíčku a odešlete zprávu.

Všimněte si, že tým NuGet a .NET Foundation si vyhrazuje právo Tato kritéria kdykoli změnit.

## <a name="unlisting-a-package"></a>Odbalení balíčku
Po odbalení verze balíčku se na stránce s podrobnostmi balíčku nuget.org skryje. To umožňuje stávajícím uživatelům balíčku pokračovat v používání, ale zkracuje nové přijetí, protože balíček není při hledání viditelný.

Postup pro odbalení balíčku:

1. Vyberte `Your account name` (v pravém horním rohu) >`Manage packages` > `Published packages`
1. Vyberte ikonu spravovat balíček.
1. Rozbalte část "výpis" a vyberte verzi balíčku.
1. Zrušte zaškrtnutí seznamu ve výsledcích hledání a vyberte Uložit.

Konkrétní verze balíčku teď není v seznamu. Pokud to chcete ověřit, odhlaste si účet a přejděte na stránku balíčku (bez části verze), například: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ . Zobrazí se všechny verze balíčku, u kterých **nedošlo k jejich** nezobrazení. Vlastník balíčku, pokud je přihlášen, ale může zobrazit všechny verze a jejich stav výpisu.

Je také možné vyřadit verzi balíčku jako nejenom v případě, že nemůžete odstranit verzi balíčku. Další informace o vyřazení verzí balíčku najdete v tématu [zastaralé balíčky](../deprecate-packages.md).
