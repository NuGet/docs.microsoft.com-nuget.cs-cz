---
title: Vytváření nativních nugetových balíčků
description: Podrobnosti o vytváření nativní chodište balíčky NuGet, který obsahuje kód C++ namísto spravovaného kódu, pro použití v projektech jazyka C++.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69520597"
---
# <a name="creating-native-packages"></a>Vytváření nativních balíčků

Nativní balíček obsahuje nativní binární soubory namísto spravovaných sestavení, což umožňuje jeho použití v rámci projektů jazyka C++ (nebo podobných). (Viz [nativní balíčky jazyka C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) v části Spotřebovávat.)

Chcete-li být spotřební v projektu Jazyka C++, balíček musí cílit na `native` rozhraní. V současné době neexistují žádná čísla verzí přidružené k této rámci jako NuGet zachází všechny projekty Jazyka C++ stejné.

> [!Note]
> Nezapomeňte zahrnout *nativní* `<tags>` v části `.nuspec` vašeho pomoci ostatním vývojářům najít balíček vyhledáváním na této značce.

Nativní `native` cílení balíčků NuGet `\build` `\content`pak `\tools` poskytuje soubory v , a složky; `\lib` se v tomto případě nepoužívá (NuGet nemůže přímo přidat odkazy na projekt jazyka C++). Balíček může také obsahovat cíle `\build` a rekvizity soubory v tomto NuGet bude automaticky importovat do projektů, které spotřebovávají balíček. Tyto soubory musí být pojmenovány stejně `.targets` jako ID balíčku s a/nebo `.props` rozšíření. Například balíček [cpprestsdk](https://nuget.org/packages/cpprestsdk/) `cpprestsdk.targets` obsahuje soubor `\build` ve své složce.

Složku `\build` lze použít pro všechny balíčky NuGet a nikoli pouze nativní balíčky. Složka `\build` respektuje cílové architektury stejně `\content` `\lib`jako `\tools` , a složky. To znamená, že `\build\net40` můžete `\build\net45` vytvořit složku a složku a NuGet importuje příslušné rekvizity a cíle soubory do projektu. (K importu cílů MSBuild není potřeba používat skripty prostředí PowerShell.)
