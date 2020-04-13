---
title: Přehled a pracovní postup vytváření balíčků NuGet
description: Přehled procesu vytváření a publikování balíčku NuGet s odkazy na jiné konkrétní části procesu.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: e4b9f6dae3a4be69e523888cc9bd2f212b45829c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488848"
---
# <a name="package-creation-workflow"></a>Pracovní postup vytvoření balíčku

Vytvoření balíčku začíná zkompilovaným kódem (obvykle sestaveními .NET), které chcete zabalit a sdílet s ostatními, a to buď prostřednictvím veřejné nuget.org galerie nebo soukromé galerie v rámci vaší organizace. Balíček může také obsahovat další soubory, jako je například readme, který se zobrazí při instalaci balíčku a může zahrnovat transformace na určité soubory projektu.

Balíček může také sloužit pouze vyžádat libovolný počet jiných závislostí, aniž by obsahoval jakýkoli vlastní kód. Takový balíček je pohodlný způsob, jak doručit sdk, který se skládá z více nezávislých balíčků. V ostatních případech může balíček`.pdb`obsahovat pouze soubory symbol ( ) pro podporu ladění.

> [!Note]
> Při vytváření balíčku pro použití jinými vývojáři, je důležité si uvědomit, že jsou s závislostí na vaší práci. Jako takový, vytváření a publikování balíčku také znamená závazek k opravě chyb a provádění dalších aktualizací, nebo přinejmenším zpřístupnění balíčku jako open source, takže ostatní mohou pomoci udržovat.

V každém případě začíná vytvoření balíčku rozhodnutím o jeho identifikátoru, čísle verze, licenci, informacích o autorských právech a dalším nezbytném obsahu. Po dokončení můžete použít příkaz "pack" a dát `.nupkg` vše dohromady do souboru. Tento soubor lze publikovat do informačního kanálu NuGet, jako je nuget.org.

> [!Tip]
> Balíček NuGet `.nupkg` s příponou je jednoduše soubor ZIP. Chcete-li snadno prozkoumat obsah libovolného `.zip` balíčku, změňte rozšíření a rozbalte jeho obsah obvyklým způsobem. Jen nezapomeňte změnit rozšíření zpět `.nupkg` na před pokusem o jeho nahrání do hostitele.

Chcete-li se naučit a pochopit proces vytváření, [začněte vytvořením balíčku,](../create-packages/creating-a-package.md) který vás provede základními procesy společnými pro všechny balíčky.

Odtud můžete zvážit řadu dalších možností pro váš balíček:

- [Podpora více cílových rámců](../create-packages/supporting-multiple-target-frameworks.md) popisuje, jak vytvořit balíček s více variantami pro různé rozhraní .NET Frameworks.
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md) popisuje, jak strukturovat balíček s více jazykovými prostředky a jak používat samostatné lokalizované satelitní balíčky.
- [Předběžné verze balíčků](../create-packages/prerelease-packages.md) ukazuje, jak uvolnit alfa, beta a rc balíčky pro ty zákazníky, kteří mají zájem.
- [Transformace zdrojového a konfigurovaného souboru](../create-packages/source-and-config-file-transformations.md) popisuje, jak můžete provést jak jednosměrné nahrazení `web.config` `app.config` tokenů v souborech, které jsou přidány do projektu, tak upravit a s nastaveními, která jsou také zálohována při odinstalaci balíčku.
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md) nabízí pokyny pro poskytování symbolů pro vaši knihovnu, které umožňují spotřebitelům krok ovat do kódu při ladění.
- [Správa verzí balíčků](../concepts/package-versioning.md) popisuje, jak identifikovat přesné verze, které povolíte pro vaše závislosti (jiné balíčky, které spotřebováváte z balíčku).
- [Nativní balíčky](../guides/native-packages.md) popisuje proces pro vytvoření balíčku pro spotřebitele Jazyka C++.
- [Podepisování balíčků](../create-packages/sign-a-package.md) popisuje proces přidání digitálního podpisu do balíčku.

Až budete připraveni publikovat balíček pro nuget.org, postupujte podle [jednoduchého procesu](../nuget-org/publish-a-package.md)v části Publikovat balíček .

Pokud chcete místo nuget.org používat soukromý zdroj, přečtěte si část [Přehled hostování balíčků](../hosting-packages/overview.md)
