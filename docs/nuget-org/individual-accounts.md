---
title: Jednotlivé účty
description: Pro publikování balíčků se vyžadují jednotlivé acccounts na NuGet.org.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c88b88015bd6d5bae4789765126c0a3dec527e24
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419848"
---
# <a name="individual-accounts"></a>Jednotlivé účty

Abyste mohli publikovat a spravovat balíčky na NuGet.org, musíte vytvořit jednotlivý účet.

## <a name="individual-accounts-vs-organization-accounts"></a>Jednotlivé účty vs. účty organizace

Váš jednotlivý uživatelský účet je vaší identitou v NuGet.org a může být členem libovolného počtu organizací. Balíček může patřit k účtu organizace, jako by mohl patřit k individuálnímu účtu. Uživatelé balíčku nevidí žádný rozdíl mezi jednotlivými účty nebo účtem organizace: obě se zobrazí jako balíčky `owners`.

Účet organizace má jako členy jeden nebo více jednotlivých účtů. Tito členové mohou spravovat sadu balíčků a přitom zachovat jedinou identitu pro vlastnictví.

## <a name="add-a-new-individual-account"></a>Přidat nový jednotlivý účet

Pokud chcete vytvořit účet NuGet.org, musíte mít osobní účet Microsoft (MSA) nebo účet Azure Active Directory (AAD). Pokud žádný nemáte, můžete si ho [vytvořit](https://signup.live.com) . Pokud máte účet MSA nebo AAD, postupujte podle následujících kroků.

1. Přejít na [přihlašovací stránku NuGet.org](https://www.nuget.org/users/account/LogOn)

1. Klikněte na tlačítko **Přihlásit se účtem Microsoft** .

1. Zadejte účet Microsoft nebo Azure Active Directory podrobnosti účtu.

1. Kliknutím na **Ano** přijměte oprávnění k aplikaci *NuGet.org* .

   ![Udělení oprávnění NuGet.org](media/nuget-org-permissions.png)

1. Budete přesměrováni na *NuGet.org*a požádáni, abyste zaregistrovali uživatelské jméno.

1. Do vstupního pole zadejte uživatelské jméno. Všimněte si, **že uživatelské jméno** rozlišuje velká a malá písmena a nelze je změnit nebo přejmenovat později.

   ![Zadat uživatelské jméno na NuGet.org](media/nuget-org-register.png) 

1. Klikněte na tlačítko **Registrovat** .

Teď máte účet NuGet.org. Správu účtů můžete provádět na stránce [Nastavení účtu](https://www.nuget.org/account) .

## <a name="enable-two-factor-authentication-2fa"></a>Povolit dvojúrovňové ověřování (2FA)

Chcete-li lépe chránit svůj účet, povolte dvojúrovňové ověřování (doporučeno).

1. Když se přihlásíte k účtu, otevřete svůj profil a v části **přihlašovací účet**vyberte **Povolit** .

   ![Povolit 2FA](media/nuget-org-register-2fa.png)

   Zobrazí se zpráva s informacemi o tom, že při příštím přihlášení k *NuGet.org*budete požádáni o další přihlašovací údaje.

2. Pokud chcete ověřování dokončit, odhlaste se a znovu se přihlaste.

3. Když se přihlásíte, vyberte jako druhou formu ověřování buď text, nebo e-mail.

   Ověřte telefonní číslo nebo e-mailovou adresu, která je už přidružená k vašemu účet Microsoft. Pro svůj účet možná budete muset zadat nové telefonní číslo nebo e-mailovou adresu. Pokud ano, zadejte požadované informace podle pokynů a klikněte na tlačítko **Další**.

   ![Povolit 2FA](media/nuget-org-sign-in-2fa.png)

4. Ověřte svoje zařízení nebo e-mailový účet a zadejte kód, který jste právě odeslali.

   ![Povolit 2FA](media/nuget-org-enter-code-2fa.png)

5. Dokončete dvojúrovňové ověřování podle všech dalších pokynů.
