---
title: 2.6.1 NuGet pro poznámky k verzi WebMatrixu
description: Poznámky k verzi NuGet 2.6.1 pro WebMatrix, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780422"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>2.6.1 NuGet pro poznámky k verzi WebMatrixu

Zpráva k [vydání verze](../release-notes/nuget-2.6.md)  |  NuGet 2,6 Zpráva k [vydání verze NuGet 2,7](../release-notes/nuget-2.7.md)

Tým NuGet uvolnil aktualizované rozšíření Správce balíčků NuGet pro WebMatrix na 26. března 2014.  Tuto aktualizaci můžete nainstalovat z [Galerie rozšíření WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) pomocí následujících kroků:

1. Otevřít WebMatrix 3
1. Klikněte na ikonu rozšíření na pásu karet domů.
1. Vyberte kartu aktualizace.
1. Kliknutím můžete aktualizovat Správce balíčků NuGet na 2.6.1
1. Zavřít a restartovat WebMatrix 3

## <a name="notable-changes"></a>Významné změny

Tato aktualizace rozšíření řeší dva z největších problémů, které uživatelé čelí využívání balíčků NuGet v rámci WebMatrixu.  První byla chyba verze schématu NuGet a druhá byla chyba vedoucí do složky DLL s nulovým počtem bajtů `bin` .

### <a name="nuget-schema-version-error"></a>Chyba verze schématu NuGet

Vzhledem k tomu, že byla vydána WebMatrix 3, byly do sady NuGet zavedeny nové funkce, které vyžadují novou verzi schématu pro balíčky NuGet.  Při pokusu o správu balíčků NuGet na webu můžou tyto nové balíčky vést k chybám, které vidíte ve WebMatrixu.

![Došlo k chybě. Verze schématu je nekompatibilní. Upgradujte prosím NuGet na nejnovější verzi.](./media/NuGet-2.8/webmatrix-schema-version.png)

Tato nejnovější vydaná verze poskytuje kompatibilitu s nejnovějšími balíčky NuGet, což brání v výskytu této chyby. Nové verze balíčků, včetně Microsoft. AspNet. webpages, se teď dají nainstalovat do WebMatrixu.  Některé z těchto balíčků používaly funkce NuGet, jako jsou [transformace XDT config](../release-notes/nuget-2.6.md#xdt), které se ještě nepodporovaly ve WebMatrixu.

### <a name="zero-byte-dlls-in-bin-folder"></a>Zero-Byte knihovny DLL ve složce bin

Někteří uživatelé oznámili, že po instalaci balíčků NuGet ve WebMatrixu, které obsahují knihovny DLL, které kopírují do bin, se knihovny DLL zobrazují ve `bin` složce jako soubory o velikosti 0 bajtů.  Tím dojde k přerušení aplikace za běhu.

[Tento problém](https://nuget.codeplex.com/workitem/4060) byl nyní opraven.

## <a name="other-recent-improvements"></a>Další nejnovější vylepšení

Po vydání Správce balíčků NuGet 2,8 pro Visual Studio jsme vydali také správce balíčků NuGet 2.5.0 pro WebMatrix.  I když se to zmiňuje v [poznámkách k verzi NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nezmiňujeme vám konkrétní nové funkce, které aktualizace zavádí.

### <a name="update-all"></a>Aktualizovat vše

Nyní můžete aktualizovat všechny balíčky webu v jednom kroku!  Když otevřete rozšíření NuGet v WebMatrixu, zobrazí se seznam všech balíčků v galerii, nainstalované a ty, které mají dostupné aktualizace.  Dřív se musí každý balíček aktualizovat jednotlivě, ale teď je užitečné tlačítko Aktualizovat vše, které se zobrazí na kartě aktualizace.

![Kliknutím na Aktualizovat vše aktualizujte všechny balíčky s dostupnými aktualizacemi.](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Přepsat existující soubory

Při instalaci balíčků, které obsahují soubory, které už na vašem webu existují, má NuGet vždycky jenom tiché ignorování těchto souborů (vaše stávající soubory zůstanou beze všech).  To může vést ke dojmu o tom, že byl balíček nainstalovaný nebo aktualizovaný správně, ale ve skutečnosti to nebylo.  NuGet se teď zobrazí výzva, aby se soubory přepsaly.

![Řešení konfliktů souborů](./media/NuGet-2.8/webmatrix-overwrite-file.png)
