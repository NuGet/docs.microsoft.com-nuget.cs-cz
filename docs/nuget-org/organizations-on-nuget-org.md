---
title: Vaše organizace na NuGet.org
description: Organizace na NuGet.org vám umožní spravovat balíčky publikovaná podle skupiny nebo týmu, firemní prostředí.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427539"
---
# <a name="your-organization-on-nugetorg"></a>Vaše organizace na NuGet.org

Organizacím umožňují podnikům a open source projekty, spolupracovat na balíčky pomocí jediné identity NuGet.org. Pro spotřebitele balíčku zobrazí se stejná jako existující uživatelský účet na NuGet.org účet organizace.

## <a name="organization-accounts-vs-individual-accounts"></a>Účty organizace a samostatné účty

Účet organizace má jeden nebo více účtů osoba (uživatel) jako členy. Tyto členy můžete spravovat sadu balíčků při zachování jedinou identitu pro vlastnictví.

Svého individuálního účtu je svoji identitu na NuGet.org a může mít libovolný počet organizace. Balíček může patřit k účtu organizace jako můžou patřit do individuálního účtu. Balíček příjemci nezobrazuje žádný rozdíl mezi samostatný účet nebo účet organizace: oba se objeví jako balíček `owners`.

## <a name="adding-a-new-organization"></a>Přidává se nová organizace

Pokud chcete přidat novou organizaci, vyberte svůj účet na NuGet.org a pak vyberte **Správa organizace...**  příkazu nabídky:

![Možnost nabídky na NuGet.org pro správce organizace](media/org-manage-option.png)

Na další stránce vyberte **přidat novou organizaci** tlačítka:

![Pro vytvoření nové organizace na NuGet.org](media/org-add-new-option.png)

Na další stránce zadejte jméno a e-mailovou adresu organizace. Protože účty organizace sdílejí stejný obor názvů jako uživatelské účty, název organizace musí být odlišné od všech existující organizace nebo uživatelské účty. E-mailová adresa musí být také jedinečný ve všech účtech.

![Přidejte novou stránku organizace na NuGet.org](media/org-add-new-page.png)

Po vytvoření účtu organizace, se na správce a můžete odesílat balíčky pro organizaci a přidat členy organizace.

### <a name="transform-existing-account-to-an-organization"></a>Transformace existující účet organizace

> [!Warning]
> Převod účtu je nevratná operace: nelze transformovat organizace zpět na uživatelský účet.

Pokud už správu balíčků v týmu pomocí jediného uživatelského účtu a chcete převést na tento účet organizace, použijte **transformovat váš účet organizace** možnost **Správa organizace** stránky:

![Možnost převést existující účet organizace na NuGet.org](media/org-transform-option.png)

Na další stránce zadejte jiného uživatelského účtu přiřadit jako správce organizace, a pak vyberte **transformace**.

![Zadání informací pro transformaci uživatelský účet organizace](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Správa organizace členy

Jako správce organizace, můžete přidat členy tím, že poskytuje každý člen NuGet.org *název uživatelského účtu*; e-mailové adresy nelze použít. Pak označit každý člen jako spolupracovník nebo správce s následujícími oprávněními:

| Oprávnění | Spolupracovníka | Správce |
| --- | --- | --- |
| Správa balíčků pro organizaci<br/>(odeslání nové balíčky, aktualizace nebo vyjmutí ze seznamu existujících balíčků) | Ano | Ano |
| Změna organizace metadat<br/>(e-mailovou adresu, nastavení oznámení) | Ne | Ano |
| Spravovat členy organizace | Ne | Ano |
| Požádat o nebo reagovat na požadavky co-ownership pro organizaci balíčky | Ne | Ano |

## <a name="managing-packages"></a>Správa balíčků

Můžete zobrazit všechny balíčky přes svůj účet a všechny organizace, kterých jste členem na [spravovat balíčky](https://www.nuget.org/account/Packages) stránky. Chcete-li zobrazit balíčky, které jsou specifické pro váš účet nebo libovolné konkrétní organizaci, použijte filtr účty v horní části stránky.

![Správa balíčků s filtrem účtu](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Přenos balíčků do organizace
Pokud chcete převést některé své balíčky do nově vytvořeného organizace, můžete k tomu vyžádání účet organizace, který chcete spoluvlastní balíček a odebrat sami sebe jako vlastníka. Pokud jste správcem organizace, neexistuje žádná potvrzení vyžadovat, abyste přijali vlastnictví. Ale pokud spolupracovníka, přidání organizace jako vlastníka vyžaduje jednu z Správci tak, aby přijímal vlastnictví.

## <a name="publishing-packages"></a>Publikování balíčků

Publikovat balíčky organizace jako publikovat balíčky uživatelský účet: přímo nahráním balíček do NuGet.org nebo vynucením balíček `nuget push` nebo `dotnet nuget push` příkazy rozhraní příkazového řádku.

### <a name="uploading-packages"></a>Nahrání balíčků

Když můžete přímo nahrát nový balíček na [nahrát NuGet.org](https://www.nuget.org/packages/manage/upload) stránce přiřadit vlastníka balíčku k účtu uživatele nebo organizaci:

![Nahrání balíčku s možností účtu](media/org-upload-option.png)

### <a name="using-api-keys"></a>Pomocí klíče rozhraní API

Vložit balíčku `nuget push` nebo `dotnet nuget push` příkazy rozhraní příkazového řádku, je nutné získat klíč rozhraní API vyžaduje těchto příkazů. Podrobnosti najdete v tématu [publikování balíčku](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Při vytváření nového klíče rozhraní API, vyberte příslušné organizaci **vlastníka balíčku** rozevírací seznam. Žádné klíče rozhraní API, které vytvoříte se vztahuje pouze na zvoleném organizace:

![Klíč rozhraní API s možností účtu](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Odebrání organizace

Jako uživatel, můžete odebrat sami sebe z organizace tak, že vyberete **X** tlačítko zobrazí vaše členství v organizaci:

![Odebrání uživatelského účtu z organizace](media/org-remove-self-option.png)

Správci můžou odeberte všechny členy z organizace, včetně jiných správců. Pokud jste jediným správcem organizace, nemůžete se sami odebrat není-li přidat jiného člena jako správce.

### <a name="deleting-an-organization-account"></a>Odstraňuje se účet organizace

Účet organizace můžete odstranit kliknutím **odstranit** tlačítko zobrazené na stránce vaší organizace.

![Odstranit organizaci](media/org-delete-option.png)

Odstranit organizace, musíte potvrdit ho kliknutím **odstranit organizaci** tlačítko potvrzení.
