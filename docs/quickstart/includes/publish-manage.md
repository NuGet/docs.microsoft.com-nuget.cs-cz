---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495975"
---
Ve svém profilu na nuget.org vyberte **Spravovat balíčky,** abyste viděli ten, který jste právě publikovali. Obdržíte také potvrzovací e-mail. Všimněte si, že může chvíli trvat, než bude váš balíček indexován a zobrazí se ve výsledcích hledání tam, kde ho mohou najít ostatní. Během této doby se na stránce balíčku zobrazí níže uvedená zpráva:

![Tento balíček ještě nebyl indexován. Zobrazí se ve výsledcích vyhledávání a bude k dispozici pro instalaci nebo obnovení po dokončení indexování.](../media/QS_Create-03-NotIndexed.png)

A to je vše! Právě jste publikovali první balíček NuGet k nuget.org, které ostatní vývojáři můžete použít ve svých vlastních projektech.

Pokud jste v tomto návodu vytvořili balíček, který není ve skutečnosti užitečný (například balíček vytvořený s prázdnou knihovnou tříd), měli byste zrušit *seznam* balíčku, abyste ho skryli z výsledků hledání:

1. V nuget.org vyberte své uživatelské jméno (vpravo nahoře na stránce) a pak vyberte **Spravovat balíčky**.

1. Vyhledejte balíček, který chcete zrušit v části **Publikováno,** a vyberte ikonu koše vpravo:

    ![Ikona koše zobrazená pro výpis balíčku na nuget.org](../media/qs_create-vs-03-trash-can.png)

1. Na následující stránce zrušte zaškrtnutí políčka **Seznam (název balíčku) ve výsledcích hledání** a vyberte **Uložit**:

    ![Zrušení zaškrtnutí políčka Seznam pro balíček v nuget.org](../media/qs_create-vs-04-unlist.png)