---
title: "Poznámky k verzi služby WebMatrix NuGet 2.6.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Poznámky k verzi pro NuGet 2.6.1 pro službu WebMatrix, včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "Funkce, chcete přidat NuGet 2.6.1 pro poznámky k verzi služby WebMatrix, opravy chyb, známé problémy"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c37ddc998378b8aaa477dd5df814bab6f0b3c58
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 poznámky k verzi služby WebMatrix

[Poznámky k verzi NuGet 2.6](../release-notes/nuget-2.6.md) | [NuGet 2.7 poznámky k verzi](../release-notes/nuget-2.7.md)

Týmem NuGet vydala aktualizované rozšíření Správce balíčků NuGet pro službu WebMatrix 26 března 2014.  Tato aktualizace se dá nainstalovat z [Galerie rozšíření prostředí WebMatrix](http://extensions.webmatrix.com/packages/NuGetPackageManager/) pomocí následujících kroků:

1. Otevřete službu WebMatrix 3
2. Klikněte na ikonu rozšíření na pásu karet Domů
3. Vyberte kartu aktualizace
4. Klikněte na tlačítko Aktualizovat na verzi 2.6.1 Správce balíčků NuGet
6. Zavřete a znovu spusťte službu WebMatrix 3

## <a name="notable-changes"></a>Upozorňují na důležité změny

Tato rozšíření aktualizace řeší dva největších problémů uživatelů mají potýkají náročné balíčků NuGet v rámci služby WebMatrix.  První došlo k chybě verze schématu NuGet a druhý byl chyby vedoucí k knihovny DLL nula bajtů v `bin` složky.

### <a name="nuget-schema-version-error"></a>Chyba verze schématu NuGet

Vzhledem k tomu, že byl vydán služba WebMatrix 3, byly zavedeny nové funkce do NuGet, které vyžadují novou verzi schématu pro balíčky NuGet.  Při pokusu o spravovat vaše balíčky NuGet ve vašem webu, tyto nové balíčky může vést k chybám, které se zobrazí ve službě WebMatrix.

![Došlo k chybě. Verze schématu není kompatibilní. Prosím upgradujte rozšíření NuGet na nejnovější verzi.](./media/NuGet-2.8/webmatrix-schema-version.png)

Tato nejnovější verze poskytuje kompatibilitu s nejnovější balíčky NuGet, brání výskytu této chyby. Nové verze, včetně Microsoft.AspNet.WebPages balíčky můžete nyní nainstalovat ve službě WebMatrix.  Některé z těchto balíčků byly pomocí funkce NuGet, jako [XDT konfigurační transformaci](../release-notes/nuget-2.6.md#xdt), který dosud nebyl podporován ve službě WebMatrix.

### <a name="zero-byte-dlls-in-bin-folder"></a>Nula bajtů knihovny DLL ve složce Koš

Někteří uživatelé hlásili, která po instalaci NuGet zabalí ve službě WebMatrix, které zahrnují knihovny DLL, které jsou kopírovány do přihrádky, který zobrazení knihovny DLL v `bin` složky jako soubory 0 bajtů.  Tím se přeruší aplikace za běhu.

[Tento problém](https://nuget.codeplex.com/workitem/4060) nyní byl opraven.

## <a name="other-recent-improvements"></a>Další vylepšení poslední

Když 2.8 Správce balíčků NuGet byl vydán pro sadu Visual Studio, vydala společnost Microsoft také Správce balíčků NuGet 2.5.0 pro službu WebMatrix.  Pokud to bylo uvedeno v [poznámky k verzi 2.8 NuGet](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nebyla jsme zmínili, konkrétní nových funkcí tuto aktualizaci zavedená.

### <a name="update-all"></a>Aktualizuje všechny

Teď můžete aktualizovat všechny balíčky webové stránky v jednom kroku!  Když otevřete rozšíření NuGet ve službě WebMatrix, zobrazí seznam všech balíčků v galerii, nainstalované a ty aktualizace, které jsou k dispozici.  Dříve se jednotlivě aktualizovat všechny balíčky, ale nyní je užitečné tlačítko "Aktualizovat vše", které se zobrazí na kartě aktualizace.

![Klikněte na Aktualizovat vše aktualizovat všechny balíčky s aktualizacemi, k dispozici](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Přepsat existující soubory

Při instalaci balíčků, které obsahují soubory, které již existují na webovém serveru, NuGet ignorovala vždy bezobslužně tyto soubory (a nechat existující soubory samostatně).  To může vést k dojem, že byl nainstalován balíček, nebo správně aktualizován, když ve skutečnosti fungovat.  NuGet se nyní zobrazí výzvu k přepisovat soubory.

![Řešení konfliktů souborů](./media/NuGet-2.8/webmatrix-overwrite-file.png)
