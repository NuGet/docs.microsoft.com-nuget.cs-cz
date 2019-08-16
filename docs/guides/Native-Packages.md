---
title: Vytváření nativních balíčků NuGet
description: Podrobnosti o vytváření nativních balíčků NuGet, C++ které obsahují kód namísto spravovaného kódu, pro C++ použití v projektech.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520597"
---
# <a name="creating-native-packages"></a>Vytváření nativních balíčků

Nativní balíček obsahuje nativní binární soubory namísto spravovaných sestavení, což umožňuje použití v rámci C++ (nebo podobných) projektech. (Podívejte se na téma [nativní C++ balíčky](../consume-packages/finding-and-choosing-packages.md#native-c-packages) v části spotřebovat.)

Aby bylo možné v C++ projektu být spotřební, balíček musí cílit na `native` rozhraní. V současné době nejsou k dispozici žádná čísla verzí přidružená k tomuto rozhraní, protože C++ NuGet považuje všechny projekty za stejné.

> [!Note]
> Ujistěte se, že do `<tags>` části vaší aplikace `.nuspec` zadáte nativní, abyste ostatním vývojářům pomohli najít balíček pomocí hledání této značky.

Nativní balíčky NuGet zaměřené `native` na potom poskytují soubory `\build`ve `\content`složkách, `\tools` a. se v tomto případě nepoužívá (NuGet nemůže přímo přidat odkazy na C++ projekt). `\lib` Balíček může také zahrnovat cíle a soubory props v `\build` této NuGet se automaticky naimportují do projektů, které daný balíček využívají. Tyto soubory musí být pojmenovány stejně jako ID balíčku s `.targets` příponami a/nebo. `.props` Například balíček [cpprestsdk](https://nuget.org/packages/cpprestsdk/) zahrnuje `cpprestsdk.targets` soubor do své `\build` složky.

`\build` Složku lze použít pro všechny balíčky NuGet, nikoli jenom pro nativní balíčky. Složka respektuje cílová rozhraní `\content`, stejně jako složky, `\lib`a `\tools`. `\build` To znamená, že můžete vytvořit `\build\net40` složku `\build\net45` a složku a NuGet bude importovat příslušné soubory props a targets do projektu. (Pro import cílů MSBuild není potřeba používat skripty PowerShellu.)
