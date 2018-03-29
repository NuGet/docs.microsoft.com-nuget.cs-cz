---
title: Přehled a pracovní postup vytváření balíčků NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Přehled procesu vytváření a publikování balíčku NuGet, s odkazy na další konkrétní části procesu.
keywords: Vytvoření balíčku NuGet, Přehled vytváření NuGet, pracovní postup vytvoření NuGet, pracovní postup vytvoření balíčku, Přehled vytváření balíčku.
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: df08e15c2632a88ea7cc3333d64f4844c78c278d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="package-creation-workflow"></a>Pracovní postup vytvoření balíčku

Vytváření balíčku začíná zkompilovaný kód (obvykle sestavení .NET), které chcete balíček a sdílet s ostatními, buď prostřednictvím Galerie nuget.org veřejné nebo soukromé Galerie v rámci vaší organizace. Balíček může zahrnovat také další soubory, jako je například soubor readme, který se zobrazí, když je balíček nainstalován a může obsahovat transformací pro určité soubory projektu.

Balíček může taky sloužit pouze stáhnout libovolný počet dalších závislosti bez obsahující všechny vlastní kód. Takový balíček je pohodlný způsob, jak dodat sadu SDK, které se skládá z více nezávislých balíčků. V ostatních případech balíček může obsahovat pouze symbol (`.pdb`) souborů a usnadňuje ladění.

> [!Note]
> Když vytvoříte balíček pro použití jinými vývojáři, je důležité si uvědomit, že jejich trvá závislost na vaši práci. Jako takový vytváření a publikování balíčku také znamená závazek oprava chyby a provedení jiné aktualizace, nebo na velmi alespoň využívajícího otevřít balíčku k dispozici jako zdroj, ostatní může pomoci k její údržbě.

Ať tak, vytváření balíčku začíná při rozhodování o tom, které sestavení a dalších souborů do balíčku. Pak vytvořte soubor manifestu, označuje jako `.nuspec` souboru k popisu obsah balíčku společně s jeho identifikátoru, číslo verze, informace o autorských právech, MSBuild props a cílů a mnoho dalšího.

Když jste připravili všechny potřebné soubory v příslušné složky a vytvořili odpovídající `.nuspec` soubor, pak použijete `nuget pack` příkaz (nebo [MSBuild pack cíl](../reference/msbuild-targets.md)) všechno dávat dohromady do `.nupkg` souboru. Pak budete připraveni k nasazení balíčku na jakémkoli hostitele je k dispozici jinými vývojáři.

> [!Tip]
> Balíček NuGet se `.nupkg` rozšíření je jednoduše soubor ZIP. Snadno zjistit jakékoli balíčku obsahu, změňte příponu na `.zip` a rozbalte obsah jako obvykle. Jenom nezapomeňte změnit rozšíření zpět na `.nupkg` před pokusem o nahrajte ho do hostitele.

Další informace a pochopit procesu vytváření, začínat [vytváření balíčku](../create-packages/creating-a-package.md) který vás provede klíčové procesy, které jsou společné pro všechny balíčky.

Odtud můžete zvážit několik dalších možností pro svůj balíček:

- [Podpora více cílové rozhraní](../create-packages/supporting-multiple-target-frameworks.md) popisuje, jak vytvořit balíček s více variant pro různé rozhraní .NET Framework.
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md) popisuje postup struktury balíček s více prostředky jazyk a jak používat samostatné lokalizované satelitní balíčky.
- [Předběžné verze balíčků](../create-packages/prerelease-packages.md) ukazuje, jak k uvolnění alpha, beta a rc balíčky pro zákazníky, kteří se chtějí.
- [Zdroj a konfiguračním souboru transformace](../create-packages/source-and-config-file-transformations.md) popisuje, jak můžete provést i jednosměrný tokenu nahrazení v souborech, které jsou přidány do projektu a upravit `web.config` a `app.config` s nastavením, které jsou také vyřadit při odinstalaci balíčku .
- [Symbolů balíčky](../create-packages/symbol-packages.md) nabízí pokyny k zadávání symboly pro své knihovny, které umožňují příjemcům kroku do kódu při ladění.
- [Správa verzí balíčku](../reference/package-versioning.md) popisuje, jak určit přesné verze, které umožňují pro svoje závislosti (další balíčky, které spotřebujete ze svého balíčku).
- [Nativní balíčky](../create-packages/native-packages.md) popisuje proces vytváření balíčku pro spotřebitele C++.
- [Podepisování balíčků](../create-packages/sign-a-package.md) popisuje postup pro přidání digitální podpis balíčku.

Pokud pak budete připraveni k publikování balíčku do nuget.org, postupujte podle jednoduchý proces v [publikování balíčku](../create-packages/publish-a-package.md).

Pokud chcete používat privátní informačního kanálu místo nuget.org, najdete v článku [hostování Přehled balíčků](../hosting-packages/overview.md)
