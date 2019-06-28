---
title: Samostatné účty
description: Jednotlivé acccounts na NuGet.org je potřeba publikovat balíčky
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427557"
---
# <a name="individual-accounts"></a>Samostatné účty

Musíte vytvořit samostatný účet pro publikování a správě balíčků na NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Samostatné účty a účty organizace

Váš účet osoba (uživatel) je svoji identitu na NuGet.org a může mít libovolný počet organizace. Balíček může patřit k účtu organizace jako můžou patřit do individuálního účtu. Balíček příjemci nezobrazuje žádný rozdíl mezi samostatný účet nebo účet organizace: oba se objeví jako balíček `owners`.

Účet organizace má jeden nebo více samostatné účty jako členy. Tyto členy můžete spravovat sadu balíčků při zachování jedinou identitu pro vlastnictví.

## <a name="add-a-new-individual-account"></a>Přidat nový individuálního účtu

Pokud chcete vytvořit účet NuGet.org, potřebujete osobní účet Microsoft (MSA) nebo účet Azure Active Directory (AAD). Pokud nemáte, můžete si [vytvořit](https://signup.live.com) jeden. Pokud již máte účet MSA nebo AAD, postupujte podle následujících kroků.

1. Přejděte [NuGet.org přihlašovací stránku](https://www.nuget.org/users/account/LogOn).

1. Klikněte na **přihlásit se účtem Microsoft** tlačítko.

1. Zadejte svůj účet Microsoft nebo podrobnosti o účtu služby Azure Active Directory.

1. Po klepnutí na **Ano** tak, aby přijímal oprávnění k *NuGet.org* aplikace.

   ![Udělení oprávnění ke NuGet.org](media/nuget-org-permissions.png)

1. Budete přesměrováni na *nuget.org*a zobrazí se výzva k registraci uživatelské jméno.

1. Zadejte uživatelské jméno do vstupního pole. Pamatujte, že uživatelské jméno **je** malá a velká citlivé a nelze změnit ani přejmenovat později.

   ![Zadejte uživatelské jméno na NuGet.org](media/nuget-org-register.png) 

1. Klikněte na tlačítko **zaregistrovat** tlačítko.

Teď máte účet NuGet.org. Správa účtů můžete provádět na [nastavení účtu](https://www.nuget.org/account) stránky.
