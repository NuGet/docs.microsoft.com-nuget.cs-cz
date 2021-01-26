---
title: Přehled a pracovní postup vytváření balíčků NuGet
description: Přehled procesu vytvoření a publikování balíčku NuGet s odkazy na jiné konkrétní části procesu.
author: JonDouglas
ms.author: jodou
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: d34f8e73dce64a58393433637067651fced08173
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774679"
---
# <a name="package-creation-workflow"></a>Pracovní postup vytvoření balíčku

Vytvoření balíčku začíná zkompilovaným kódem (obvykle sestavení .NET), který chcete zabalit a sdílet s ostatními, a to prostřednictvím veřejné galerie nuget.org nebo privátní Galerie v rámci vaší organizace. Balíček může také obsahovat další soubory, například soubor Readme, který se zobrazí při instalaci balíčku, a může zahrnovat transformace na určité soubory projektu.

Balíček může také sloužit pouze k vyžádání jenom v jakémkoli počtu jiných závislostí, aniž by obsahoval vlastní kód. Takový balíček je pohodlný způsob, jak doručovat sadu SDK, která se skládá z několika nezávislých balíčků. V jiných případech může balíček obsahovat pouze soubory symbolů ( `.pdb` ) pro podporu ladění.

> [!Note]
> Když vytváříte balíček pro použití jinými vývojáři, je důležité pochopit, že se postará o práci. V takovém případě vytváření a publikování balíčku také implikuje závazek opravit chyby a provádět další aktualizace nebo při velmi minimálním zpřístupnění balíčku jako open source, aby ho ostatní mohli lépe udržovat.

Bez ohledu na to, že vytvoření balíčku začíná tím, že se rozhodnete jeho identifikátor, číslo verze, licenci, informace o autorských právech a veškerý další požadovaný obsah. Až budete hotovi, můžete použít příkaz Pack, který do souboru vloží všechno dohromady `.nupkg` . Tento soubor se dá publikovat do informačního kanálu NuGet, jako je nuget.org.

> [!Tip]
> Balíček NuGet s `.nupkg` příponou je prostě soubor zip. Chcete-li snadno kontrolovat obsah balíčku, změňte rozšíření na `.zip` a rozbalte jeho obsah obvyklým způsobem. Nezapomeňte změnit rozšíření zpátky na, `.nupkg` než se pokusíte o jeho nahrání na hostitele.

Pokud se chcete dozvědět a pochopit proces vytváření, začněte [vytvořením balíčku](../create-packages/creating-a-package.md) , který vás provede základními procesy společnými pro všechny balíčky.

Odtud můžete zvážit řadu dalších možností pro váš balíček:

- [Podpora více cílových rozhraní](../create-packages/supporting-multiple-target-frameworks.md) popisuje, jak vytvořit balíček s více variantami pro různá rozhraní .NET Framework.
- [Vytváření lokalizovaných balíčků](../create-packages/creating-localized-packages.md) popisuje, jak strukturovat balíček s více prostředky jazyka a jak používat samostatné lokalizované satelitní balíčky.
- [Balíčky předběžného vydání](../create-packages/prerelease-packages.md) ukazují, jak uvolnit balíčky Alpha, beta a RC na zákazníky, kteří mají zájem.
- [Transformace zdrojového a konfiguračního souboru](../create-packages/source-and-config-file-transformations.md) popisují, jak můžete provést jak jednosměrná nahrazení tokenů v souborech přidaných do projektu, tak upravit `web.config` a `app.config` s nastaveními, která jsou také zálohována při odinstalaci balíčku.
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md) nabízí pokyny pro poskytnutí symbolů pro vaši knihovnu, která umožňuje uživatelům krokovat kód při ladění.
- [Správa verzí balíčků](../concepts/package-versioning.md) popisuje, jak identifikovat přesné verze, které pro vaše závislosti povolíte (ostatní balíčky, které využíváte z balíčku).
- [Nativní balíčky](../guides/native-packages.md) popisují proces vytváření balíčku pro uživatele v jazyce C++.
- [Podpisové balíčky](../create-packages/sign-a-package.md) popisují proces přidání digitálního podpisu do balíčku.

Až budete připraveni publikovat balíček na nuget.org, postupujte podle jednoduchého procesu v části [publikování balíčku](../nuget-org/publish-a-package.md).

Pokud chcete použít privátní kanál místo nuget.org, přečtěte si téma [Přehled hostujících balíčků](../hosting-packages/overview.md) .
