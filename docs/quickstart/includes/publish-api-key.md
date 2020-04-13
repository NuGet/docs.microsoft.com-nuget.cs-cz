---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "68419915"
---
1. Pokud účet ještě nemáte, [přihlaste](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se ke svému nuget.org účtu nebo si vytvořte účet.

   Další informace o vytvoření účtu naleznete v [tématu Individuální účty](../../nuget-org/individual-accounts.md).

1. Vyberte své uživatelské jméno (vpravo nahoře) a pak vyberte **klávesy API**.

1. Vyberte **Vytvořit**, zadejte název klíče, vyberte **vybrat obory > push**. Zadejte * pro **vzorek Glob**a pak vyberte **Vytvořit**. (Další informace o oborech naleznete níže.)

1. Po vytvoření klíče vyberte **Kopírovat,** chcete-li načíst přístupový klíč, který potřebujete v příkazovém příkazu k příkazu k příkazu:

    ![Kopírování klíče rozhraní API do schránky](../media/QS_Create-02-APIKey.png)

1. **Důležité:** Uložte klíč na bezpečném místě, protože později jej nelze znovu zkopírovat. Pokud se vrátíte na stránku klíče rozhraní API, budete muset znovu vygenerovat klíč zkopírovat. Klíč rozhraní API můžete také odebrat, pokud již nechcete nabízeny balíčky prostřednictvím rozhraní se klis.

Obor umožňuje vytvořit samostatné klíče rozhraní API pro různé účely. Každý klíč má časový rámec vypršení platnosti a může být vymezen na konkrétní balíčky (nebo glob vzory). Každý klíč je také vymezen na konkrétní operace: nabízení nových balíčků a aktualizací, pouze nabízená aktualizace nebo vyřazení ze seznamu. Pomocí oborů můžete vytvořit klíče rozhraní API pro různé osoby, které spravují balíčky pro vaši organizaci tak, aby měli pouze oprávnění, která potřebují. Další informace naleznete v [tématu klíče rozhraní API s vymezenou sousto](../../nuget-org/scoped-api-keys.md).