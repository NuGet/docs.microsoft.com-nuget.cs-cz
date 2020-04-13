---
title: Jednotlivé účty - NuGet.org
description: Jednotlivé počty na NuGet.org jsou povinny publikovat balíky
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429015"
---
# <a name="individual-accounts-on-nugetorg"></a>Jednotlivé účty na NuGet.org

Chcete-li publikovat a spravovat balíčky v NuGet.org, musíte vytvořit individuální účet.

## <a name="individual-accounts-vs-organization-accounts"></a>Jednotlivé účty a účty organizace

Váš individuální (uživatelský) účet je vaše identita na NuGet.org a může být členem libovolného počtu organizací. Balíček může patřit k účtu organizace, stejně jako může patřit k individuálnímu účtu. Spotřebitelé balíčků nevidí žádný rozdíl mezi individuálním účtem nebo účtem organizace: oba se zobrazují jako balíček `owners`.

Účet organizace má jeden nebo více individuálních účtů jako své členy. Tito členové mohou spravovat sadu balíčků při zachování jedné identity pro vlastnictví.

## <a name="add-a-new-individual-account"></a>Přidání nového individuálního účtu

Chcete-li vytvořit účet NuGet.org, musíte mít osobní účet Microsoft (MSA) nebo účet Azure Active Directory (AAD). Pokud ho nemáte, můžete ho [vytvořit.](https://signup.live.com) Pokud máte účet MSA nebo AAD, postupujte podle následujících kroků.

1. Přejděte na [přihlašovací stránku NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Klikněte na **Tlačítko Přihlásit se pomocí Microsoftu.**

1. Zadejte podrobnosti o účtu Microsoft nebo Azure Active Directory.

1. Chcete-li přijmout oprávnění k NuGet.org *aplikaci,* klepněte na tlačítko **Ano.**

   ![Udělení oprávnění k NuGet.org](media/nuget-org-permissions.png)

1. Budete přesměrováni na *nuget.org*a budete požádáni o registraci uživatelského jména.

1. Zadejte uživatelské jméno do vstupního pole. Upozorňujeme, že uživatelské jméno **rozlišuje** malá a velká písmena a nelze jej později změnit ani přejmenovat.

   ![Zadání uživatelského jména v NuGet.org](media/nuget-org-register.png) 

1. Klepněte na tlačítko **Registrovat.**

Nyní máte účet NuGet.org. Správu účtu můžete provádět na stránce [nastavení účtu.](https://www.nuget.org/account)

## <a name="enable-two-factor-authentication-2fa"></a>Povolit dvoufaktorové ověřování (2FA)

Dvoufaktorové ověřování neboli 2FA je další vrstva zabezpečení používaná při přihlašování k webům nebo aplikacím. S 2FA se musíte přihlásit pomocí svého účtu Microsoft (MSA) a poskytnout jinou formu ověřování, kterou znáte nebo k němu máte přístup pouze vy. Chcete-li lépe chránit svůj účet, povolte dvoufaktorové ověřování (doporučeno).

1. Když se přihlásíte ke svému účtu, otevřete si profil a v části **Přihlašovací účet**zvolte **Povolit** .

   ![Povolit 2FA](media/nuget-org-register-2fa.png)

   Zobrazí se zpráva s oznámením, že při příštím přihlášení k *nuget.org*budete požádáni o další pověření.

2. Chcete-li ověření dokončit, odhlaste se a znovu se přihlaste.

3. Při přihlášení zvolte jako druhou formu ověřování text nebo e-mail.

   Ověřte telefonní číslo nebo e-mail, který je již přidružen k vašemu účtu Microsoft. Možná budete muset zadat nové telefonní číslo nebo e-mail pro svůj účet. Pokud ano, zadejte požadované informace podle pokynů a klepněte na tlačítko **Další**.

   ![Povolit 2FA](media/nuget-org-sign-in-2fa.png)

4. Zkontrolujte zařízení nebo e-mailový účet a zadejte kód, který vám byl právě odeslán.

   ![Povolit 2FA](media/nuget-org-enter-code-2fa.png)

5. Dokončete dvoufaktorové ověřování podle pokynů.

> [!Tip]
> Povolení 2FA pro váš účet NuGet.org nemá vliv na nastavení ověřování pro jiné účty nebo služby, které mohou být propojeny s účtem Microsoft, který používáte k přihlášení k NuGet.org.

## <a name="delete-a-nugetorg-account"></a>Odstranění NuGet.org účtu

Nápovědu k dalším úkolům souvisejícím s účtem, jako je například odstranění NuGet.org účtu, naleznete [v tématu správa účtu NuGet.org](nuget-org-faq.md#nugetorg-account-management).
