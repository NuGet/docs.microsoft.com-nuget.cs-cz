---
title: Přehled a pracovní postup vytváření balíčků NuGet
description: Přehled procesu vytváření a publikování balíčku NuGet, s odkazy na další konkrétní části procesu.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 6b41b23df115c45e830404afcf9defa23615bd7c
ms.sourcegitcommit: ce97dded7715f217ec44f6c8368ab0df19c38342
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/29/2018
ms.locfileid: "52615753"
---
# <a name="package-creation-workflow"></a>Pracovní postup vytvoření balíčku

Vytvoření balíčku začíná zkompilovaný kód (obvykle sestavení .NET), které chcete balíček a sdílet s ostatními, buď prostřednictvím Galerie nuget.org veřejné nebo privátní Galerie ve vaší organizaci. Balíček může zahrnovat také další soubory, jako je například soubor readme, který se zobrazí, když je balíček nainstalován a může obsahovat transformací pro některé soubory projektu.

Balíček může také sloužit k pouze o přijetí změn v jakémkoli počtu Další závislosti, bez nadřazeného libovolný kód. Takový balíček je pohodlný způsob, jak poskytovat sady SDK, která se skládá z více nezávislých balíčků. V ostatních případech balíček smí obsahovat pouze znak (`.pdb`) soubory pro usnadnění ladění.

> [!Note]
> Při vytváření balíčku pro použití pro jiné vývojáře, je důležité pochopit, že se tak závislosti na svoji práci. V důsledku toho vytváření a publikování balíčku také znamená závazkem oprava chyb a provádění dalších aktualizací nebo na velmi nejméně provedete k dispozici jako balíček opensourcových ostatní mohli pomoct k její údržbě.

Bez ohledu případ, vytvoření balíčku začíná rozhodování o tom, která sestavení a další soubory balíčku. Vytvořte soubor manifestu, označuje jako `.nuspec` souboru k popisu obsah balíčku společně s jeho identifikátor, číslo verze, informace o autorských právech, vlastnosti nástroje MSBuild a cíle a spoustu dalších věcí.

Když jste připravili všechny potřebné soubory do příslušných složek a vytvořili odpovídající `.nuspec` soubor, pak použijete `nuget pack` příkazu (nebo [cíl nástroje MSBuild pack](../reference/msbuild-targets.md)) sestavit vše, co do `.nupkg` souboru. Pak jste připraveni nasadit balíček do libovolné hostitele zpřístupňuje je s ostatními vývojáři.

> [!Tip]
> Balíček NuGet s `.nupkg` rozšíření je soubor ZIP. Chcete-li snadněji zkontrolovat všechny balíčky obsahu, změňte příponu na `.zip` a rozbalte svůj obsah jako obvykle. Jenom nezapomeňte změnit rozšíření zpět `.nupkg` před pokusem o jeho nahrání do hostitele.

Další informace a pochopení proces vytváření, začněte s [vytvoření balíčku](../create-packages/creating-a-package.md) který vás provede klíčové procesy, které jsou společné pro všechny balíčky.

Odtud můžete zvážit řadu dalších možností pro svůj balíček:

- [Podpora více cílových platforem](../create-packages/supporting-multiple-target-frameworks.md) popisuje, jak vytvořit balíček s více variantami různá rozhraní .NET.
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md) popisuje strukturu balíček s více prostředků jazyka a použití samostatné lokalizované satelitní balíčků.
- [Předběžné verze balíčků](../create-packages/prerelease-packages.md) ukazuje, jak k uvolnění alpha, beta a rc balíčky pro zákazníky, kteří chtějí.
- [Zdroj a transformace souboru Config](../create-packages/source-and-config-file-transformations.md) popisuje, jak obě jednosměrné token nahrazení v souborech, které jsou přidány do projektu a upravte `web.config` a `app.config` s nastaveními, která se také vztahuje si při odinstalaci balíčku .
- [Symbol balíčky](../create-packages/symbol-packages-snupkg.md) nabízí pokyny k zadávání symboly pro knihovny, které umožňují uživatelům Krokovat s vnořením kód během ladění.
- [Balíček správy verzí](../reference/package-versioning.md) popisuje, jak určit přesné verze, které umožňují závislostí (další balíčky, které využívají ze svého balíčku).
- [Nativní balíčky](../create-packages/native-packages.md) popisuje proces pro vytvoření balíčku pro spotřebitele C++.
- [Podepisují se balíčky](../create-packages/sign-a-package.md) popisuje proces pro přidávání digitálního podpisu balíčku.

Pokud pak budete připraveni publikovat balíček na nuget.org, postupujte podle jednoduchých kroků v [publikování balíčku](../create-packages/publish-a-package.md).

Pokud chcete použít privátní kanál namísto nuget.org, přečtěte si článek [přehled hostování balíčků](../hosting-packages/overview.md)
