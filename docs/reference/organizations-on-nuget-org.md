---
title: Organizace v nuget.org
description: Organizace v nuget.org pomáhá spravovat balíčky publikovaná podle skupiny nebo v týmu, firemní prostředí.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449575"
---
# <a name="organization-on-nugetorg"></a>Organizace v nuget.org

Organizace povolit podnikům a open source projekty spolupracovat na balíčky pomocí jednoho nuget.org identity. Pro balíček příjemce zobrazí se stejné jako existující účet uživatele v nuget.org účet organizace.

## <a name="user-accounts-vs-organization-accounts"></a>Uživatelské účty a účty organizace

Váš uživatelský účet je své identity na nuget.org a může být členem skupiny libovolný počet organizace. Balíček může patřit k účtu organizace jako můžou patřit na uživatelský účet. Balíček příjemci nevidíte žádný rozdíl mezi uživatelský účet nebo účet organizace: obě zobrazí jako balíček `owners`.

Účet organizace obsahuje jeden nebo více uživatelské účty jako členy. Tito členové můžete spravovat sadu balíčky současně zachovat jedinou identitu pro vlastnictví.

## <a name="adding-a-new-organization"></a>Přidání nové organizace

Chcete-li přidat nové organizace, vyberte svůj účet na nuget.org a poté vyberte **Spravovat organizace...**  příkazu v nabídce:

![Možnost nabídky v nuget.org pro správce organizace](media/org-manage-option.png)

Na další stránce, vyberte **přidat nové organizace** tlačítko:

![Tlačítko vytvořte novou organizaci v nuget.org](media/org-add-new-option.png)

Na další stránce zadejte jméno a e-mailovou adresu organizace. Vzhledem k tomu, že účty organizace sdílet stejný obor názvů jako uživatelské účty, název organizace musí být odlišný od jiných stávající organizace nebo uživatelské účty. E-mailová adresa musí být také jedinečný mezi všechny účty.

![Přidat novou stránku organizace v nuget.org](media/org-add-new-page.png)

Po vytvoření účtu organizace se na správce a můžete odeslat balíčky pro organizaci a přidat členy organizace.

### <a name="transform-existing-account-to-an-organization"></a>Transformace existující účet organizace

> [!Warning]
> Převod účet je nevratné: nelze transformovat organizaci zpět na uživatelský účet.

Pokud jste spravovat balíčky jako tým pomocí jediného uživatelského účtu a chcete převést na organizaci, použijte tento účet **transformace váš účet organizace** možnost **Spravovat organizace** stránky:

![Možnost v nuget.org k transformaci existující účet organizace](media/org-transform-option.png)

Na další stránce zadejte jiného uživatelského účtu přiřadit jako správce organizace, a pak vyberte **transformace**.

![Zadávání informací pro transformaci účet uživatele organizaci](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Správa organizace členy

Jako správce organizace, můžete přidat členy tím, že poskytuje každý člen nuget.org *název uživatelského účtu*; e-mailové adresy nelze použít. Potom můžete označit každého člena jako spolupracovník nebo správce s následujícími oprávněními:

| Oprávnění | Spolupracovníka | Správce |
| --- | --- | --- |
| Správa balíčků organizace<br/>(odeslání nové balíčky, aktualizace nebo unlist existující balíčky) | Ano | Ano |
| Změna organizace metadat<br/>(e-mailovou adresu, nastavení oznámení) | Ne | Ano |
| Spravovat členy organizace | Ne | Ano |
| Žádosti o nebo provádět akce s co-ownership požadavky organizace balíčky | Ne | Ano |

## <a name="managing-packages"></a>Spravovat balíčky

Můžete zobrazit všechny balíčky přes svůj účet a všechny organizace, ve kterých jste členem na [spravovat balíčky](https://www.nuget.org/account/Packages) stránky. Pokud chcete zobrazit balíčky, které jsou specifické pro váš účet nebo žádné konkrétní organizace, použijte filtr účty v horní pravé části stránky.

![Spravovat balíčky s filtrem účtu](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Přenášení balíčky organizaci
Pokud chcete některé z vašich balíčků přenést do nově vytvořené organizace, můžete tak učinit vyžádáním účet organizace společně vlastní balíček a odebrání sami jako vlastník. Pokud jste správce organizace, není třeba tak, aby přijímal vlastnictví bez potvrzení. Ale pokud jste spolupracovníka, přidání organizace jako vlastníka vyžaduje jednu správců tak, aby přijímal vlastnictví.

## <a name="publishing-packages"></a>Publikování balíčků

Publikování balíčků organizaci jako publikovat balíčky na uživatelský účet: přímo nahrávat balíček k nuget.org nebo vynucením balíček `nuget push` nebo `dotnet nuget push` rozhraní příkazového řádku.

### <a name="uploading-packages"></a>Nahrává balíčky

Pokud jste přímo nahrát nový balíček na [nuget.org nahrávání](https://www.nuget.org/packages/manage/upload) stránky, můžete přiřadit vlastníka balíčku na účet uživatele nebo organizaci:

![Nahrání balíčku s možností účtu](media/org-upload-option.png)

### <a name="using-api-keys"></a>Použití klíče rozhraní API

Tak, aby nabízel balíček `nuget push` nebo `dotnet nuget push` příkazy rozhraní příkazového řádku, je nutné získat klíč rozhraní API vyžaduje těchto příkazů. Podrobnosti najdete v tématu [publikování balíčku](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Při vytváření nového klíče rozhraní API, vyberte v příslušné organizace **vlastníka balíčku** rozevírací nabídku. Všechny klíč rozhraní API, které vytvoříte, se vztahuje pouze na vybrané organizace:

![Klíč rozhraní API s možností účtu](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Odebrání organizace

Jako uživatel, můžete odebrat sami z organizace tak, že vyberete `X` tlačítko zobrazené ve vaší organizaci členství:

![Odebráním účet uživatele organizaci](media/org-remove-self-option.png)

Od organizace, včetně jiní správci mohou správci kteréhokoli člena odebrat. Pokud jste jediným správcem v organizaci, nelze sami odebrat, není-li přidat jiného člena jako správce.

### <a name="deleting-an-organization-account"></a>Odstranění účtu organizace

Tato funkce bude brzy k dispozici.
