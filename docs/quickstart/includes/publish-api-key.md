---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419915"
---
1. [Přihlaste se k účtu NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) nebo vytvořte účet, pokud ho ještě nemáte.

   Další informace o vytvoření účtu najdete v tématu [jednotlivé účty](../../nuget-org/individual-accounts.md).

1. Vyberte své uživatelské jméno (v pravém horním rohu) a pak vyberte **klíče rozhraní API**.

1. Vyberte **vytvořit**, zadejte název pro svůj klíč, vyberte **vybrat obory > Push**. Zadejte * pro **vzor glob**a pak vyberte **vytvořit**. (Další informace o oborech najdete níže.)

1. Po vytvoření klíče vyberte **Kopírovat** a v rozhraní PŘÍKAZového řádku načtěte přístupový klíč, který potřebujete:

    ![Zkopírování klíče rozhraní API do schránky](../media/QS_Create-02-APIKey.png)

1. **Důležité**informace: Klíč uložte na bezpečném místě, protože ho později nemůžete zkopírovat. Pokud se vrátíte na stránku klíče rozhraní API, budete muset klíč znovu vygenerovat, abyste ho mohli zkopírovat. Klíč rozhraní API můžete odebrat i v případě, že už nechcete nabízet balíčky přes rozhraní příkazového řádku.

Rozsah umožňuje vytvořit samostatné klíče rozhraní API pro různé účely. Každý klíč má svůj časový rámec vypršení platnosti a může být vymezen na konkrétní balíčky (nebo vzory glob). Každý klíč je také vymezen pro konkrétní operace: vložení nových balíčků a aktualizací, pouze nabízených aktualizací nebo oddálení v seznamu. Pomocí oboru můžete vytvořit klíče rozhraní API pro různé lidi, kteří spravují balíčky pro vaši organizaci tak, aby měli jenom potřebná oprávnění. Další informace najdete v tématu [vymezené klíče rozhraní API](../../nuget-org/scoped-api-keys.md).