---
title: NuGet 2.6.1 pro WebMatrix poznámky
description: Zpráva k vydání verze pro NuGet 2.6.1 pro WebMatrix, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550314"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 pro WebMatrix poznámky

[Zpráva k vydání verze NuGet 2.6](../release-notes/nuget-2.6.md) | [zpráva k vydání verze NuGet 2.7](../release-notes/nuget-2.7.md)

Tým NuGet vydána aktualizace rozšíření Správce balíčků NuGet pro službu WebMatrix 26. března 2014.  Tato aktualizace se dá nainstalovat z [Galerie rozšíření nástroje WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) pomocí následujících kroků:

1. Otevřete nástroj WebMatrix 3
1. Klepněte na ikonu rozšíření na pásu karet Domů
1. Vyberte kartu aktualizace
1. Klikněte na tlačítko Aktualizovat správce balíčků NuGet 2.6.1
1. Zavřete a znovu spusťte službu WebMatrix 3

## <a name="notable-changes"></a>Upozorňují na důležité změny

Tato rozšíření aktualizace řeší dvou největších problémů uživatelů mají ve využívání balíčků NuGet v rámci služby WebMatrix.  První: došlo k chybě schématu verze NuGet a druhým byla chyba vede na nula bajtů knihovny DLL v `bin` složky.

### <a name="nuget-schema-version-error"></a>Chyba verze schématu NuGet

Od vydání služby WebMatrix 3 byly zavedeny nové funkce do NuGet, které vyžadují nové schéma verze pro balíčky NuGet.  Při pokusu o správu vašich balíčků NuGet na vašem webu, tyto nové balíčky může vést k chybám, které se zobrazí ve službě WebMatrix.

![Došlo k chybě. Verze schématu není kompatibilní. Upgradujte prosím NuGet na nejnovější verzi.](./media/NuGet-2.8/webmatrix-schema-version.png)

Tato nejnovější vydaná verze poskytuje kompatibilitu s nejnovějšími balíčky NuGet, brání výskytu této chyby. Nové verze balíčků, včetně Microsoft.AspNet.WebPages lze nyní nainstalovat ve Webmatrixu.  Některé z těchto balíčků byly jako například používání funkcí NuGet [XDT konfigurační transformaci](../release-notes/nuget-2.6.md#xdt), který nebyl podporován ve službě WebMatrix až doteď.

### <a name="zero-byte-dlls-in-bin-folder"></a>Nula bajtů knihovny DLL ve složce bin

Někteří uživatelé nahlásili, která po instalaci NuGet zabalí ve službě WebMatrix, které obsahují knihovny DLL, které se zkopíruje do adresáře bin, který zobrazit knihovny DLL v `bin` složky jako soubory 0 bajtů.  Tím je prolomen aplikace za běhu.

[Tento problém](https://nuget.codeplex.com/workitem/4060) nyní byla opravena.

## <a name="other-recent-improvements"></a>Další nedávné vylepšení

Pokud pro sadu Visual Studio byla vydána 2.8 Správce balíčků NuGet, jsme také vydali Správce balíčků NuGet 2.5.0 pro službu WebMatrix.  Když to jsem už zmínili v [zpráva k vydání verze NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), jsme neměli uvést konkrétní novým funkcím tuto aktualizaci zavedena.

### <a name="update-all"></a>Aktualizovat vše

Teď můžete aktualizovat všechny balíčky webové stránky v jednom kroku.  Při otevření rozšíření NuGet v nástroji WebMatrix zobrazí seznam všech balíčků ve galerii, které máte nainstalované a ty s aktualizacemi, které jsou k dispozici.  Dříve všech balíčků byste museli možné aktualizovat jednotlivě, ale teď je užitečné tlačítko "Aktualizovat vše", který se zobrazuje na kartě aktualizace.

![Klikněte na tlačítko Aktualizovat vše aktualizovat všechny balíčky dostupnými aktualizacemi](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Přepsat existující soubory

Při instalaci balíčků, které obsahují soubory, které již existují na vašem webu, NuGet má vždy jen tiše ignorováno těchto souborů (existující soubory opuštění samostatně).  To může vést k dojem, že balíček byl nainstalovány nebo aktualizovány správně, když ve skutečnosti nebylo.  NuGet teď vyzve pro soubory přepsání.

![Řešení konfliktů souborů](./media/NuGet-2.8/webmatrix-overwrite-file.png)
