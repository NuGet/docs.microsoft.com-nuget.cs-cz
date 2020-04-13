---
title: Vaše organizace na NuGet.org
description: Organizace na NuGet.org vám pomohou spravovat balíčky publikované podle skupiny nebo v týmovém prostředí společnosti.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427539"
---
# <a name="your-organization-on-nugetorg"></a>Vaše organizace na NuGet.org

Organizace umožňují firmám a projektům s otevřeným zdrojovým kódem spolupracovat na balíčcích pomocí jediné NuGet.org identity. Pro příjemce balíčku účet organizace se zobrazí stejně jako existující uživatelský účet na NuGet.org.

## <a name="organization-accounts-vs-individual-accounts"></a>Účty organizace vs. jednotlivé účty

Účet organizace má jeden nebo více individuálních (uživatelských) účtů jako svých členů. Tito členové mohou spravovat sadu balíčků při zachování jedné identity pro vlastnictví.

Váš individuální účet je vaší identitou na NuGet.org a může být členem libovolného počtu organizací. Balíček může patřit k účtu organizace, stejně jako může patřit k individuálnímu účtu. Spotřebitelé balíčků nevidí žádný rozdíl mezi individuálním účtem nebo účtem organizace: oba se zobrazují jako balíček `owners`.

## <a name="adding-a-new-organization"></a>Přidání nové organizace

Chcete-li přidat novou organizaci, vyberte svůj účet v NuGet.org a pak vyberte příkaz **nabídky Spravovat organizace...**

![Možnost nabídky v NuGet.org pro manažerské organizace](media/org-manage-option.png)

Na další stránce vyberte tlačítko **Přidat novou organizaci:**

![Tlačítko pro vytvoření nové organizace v NuGet.org](media/org-add-new-option.png)

Na další stránce zadejte název organizace a e-mailovou adresu. Vzhledem k tomu, že účty organizace sdílejí stejný obor názvů jako uživatelské účty, musí se název organizace lišit od všech ostatních existujících účtů organizace nebo uživatelů. E-mailová adresa musí být také jedinečná ve všech účtech.

![Přidání nové stránky organizace na NuGet.org](media/org-add-new-page.png)

Po vytvoření účtu organizace jste správcem a můžete odeslat balíčky pro organizaci a přidat členy organizace.

### <a name="transform-existing-account-to-an-organization"></a>Transformace existujícího účtu na organizaci

> [!Warning]
> Převod účtu je nevratný: nelze přeměnit organizaci zpět na uživatelský účet.

Pokud spravujete balíčky jako tým pomocí jednoho uživatelského účtu a chcete tento účet převést do organizace, použijte možnost **Transformovat svůj účet na organizaci** na stránce Spravovat **organizace:**

![Možnost NuGet.org transformovat existující účet na organizaci](media/org-transform-option.png)

Na další stránce zadejte jiný uživatelský účet, který chcete přiřadit jako správce organizace, a pak vyberte **Transformovat**.

![Zadávání informací o transformaci uživatelského účtu do organizace](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Správa členů organizace

Jako správce organizace můžete přidávat členy zadáním *NuGet.org uživatelského účtu*každého člena ; e-mailové adresy nelze použít. Potom označíte každého člena jako spolupracovníka nebo správce pomocí následujících oprávnění:

| Oprávnění | Spolupracovník | Správce |
| --- | --- | --- |
| Správa balíčků organizace<br/>(odeslat nové balíčky, aktualizovat nebo zrušit seznam existujících balíčků) | Ano | Ano |
| Změna metadat organizace<br/>(e-mailová adresa, nastavení oznámení) | Ne | Ano |
| Správa členů organizace | Ne | Ano |
| Žádost nebo jednat na základě žádostí o spoluvlastnictví pro organizační balíčky | Ne | Ano |

## <a name="managing-packages"></a>Správa balíčků

Můžete zobrazit všechny balíčky ve vašem účtu a všechny organizace, jejichž jste členem na stránce [Spravovat balíčky.](https://www.nuget.org/account/Packages) Chcete-li zobrazit balíčky specifické pro váš účet nebo konkrétní organizaci, použijte filtr účtů v pravém horním rohu stránky.

![Správa balíčků pomocí filtru účtu](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Přenos balíčků do organizace
Pokud chcete převést některé balíčky do nově vytvořené organizace, můžete tak učinit tak, že požádáte účet organizace, abyste spoluvlastnili balíček a poté se odebrali jako vlastník. Pokud jste správcem organizace, není nutné k přijetí vlastnictví žádné potvrzení. Pokud jste však spolupracovník, přidání organizace jako vlastníka vyžaduje, aby jeden ze správců převzal vlastnictví.

## <a name="publishing-packages"></a>Publikování balíčků

Publikujete balíčky do organizace, jako je publikování balíčků do uživatelského účtu: přímým `nuget push` nahráním balíčku do NuGet.org nebo odesláním balíčku prostřednictvím příkazů příkazu příkazu příkazu příkazu nebo `dotnet nuget push` CLI.

### <a name="uploading-packages"></a>Nahrávání balíčků

Když přímo nahrajete nový balíček na stránku [NuGet.org Upload,](https://www.nuget.org/packages/manage/upload) přiřadíte vlastníka balíčku k uživatelskému nebo organizačnímu účtu :

![Možnost Nahrát balíček s možností účtu](media/org-upload-option.png)

### <a name="using-api-keys"></a>Použití klíčů rozhraní API

Chcete-li protlačit `nuget push` `dotnet nuget push` balíček prostřednictvím příkazů příkazového příkazu nebo příkazového příkazu, musíte získat klíč rozhraní API, který tyto příkazy potřebují. Podrobnosti naleznete [v tématu Publikování balíčku](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Při vytváření nového klíče rozhraní API vyberte příslušnou organizaci v rozevíracím seznamu **Vlastník balíčku.** Jakýkoli klíč rozhraní API, který vytvoříte, se vztahuje pouze na vybranou organizaci:

![Klíč rozhraní API s možností účtu](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Odebrání organizace

Jako uživatel můžete odebrat sami sebe z organizace výběrem tlačítka **X** zobrazeného členstvím v organizaci:

![Odebrání uživatelského účtu z organizace](media/org-remove-self-option.png)

Správci mohou odebrat libovolného člena organizace, včetně jiných správců. Pokud jste jediným správcem organizace, nemůžete se odebrat sami, pokud jako správce nepřidáte jiného člena.

### <a name="deleting-an-organization-account"></a>Odstranění účtu organizace

Účet organizace můžete odstranit kliknutím na tlačítko **Odstranit** zobrazené na stránce organizace.

![Odstranění organizace](media/org-delete-option.png)

Chcete-li organizaci odstranit, musíte ji potvrdit kliknutím na tlačítko Odstranit potvrzení **organizace.**
