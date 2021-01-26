---
title: Vytváření nativních balíčků NuGet
description: Podrobnosti o vytváření nativních balíčků NuGet, které obsahují kód jazyka C++ namísto spravovaného kódu, pro použití v projektech jazyka C++.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 2a95fca2ce5496512627e913273e5b66128e34c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774209"
---
# <a name="creating-native-packages"></a>Vytváření nativních balíčků

Nativní balíček obsahuje nativní binární soubory namísto spravovaných sestavení, což umožňuje použití v rámci projektů C++ (nebo podobných). (Viz téma věnované [nativním balíčkům C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) v části spotřebovat.)

Aby bylo možné v projektu C++ být spotřební, balíček musí cílit na `native` rámec. V současné době nejsou k dispozici žádná čísla verzí přidružená k tomuto rozhraní, protože NuGet zpracovává všechny projekty C++ stejné.

> [!Note]
> Ujistěte se, že  do `<tags>` části vaší aplikace zadáte nativní `.nuspec` , abyste ostatním vývojářům pomohli najít balíček pomocí hledání této značky.

Nativní cílení balíčků NuGet `native` , které pak poskytují soubory v `\build` , `\content` a `\tools` složky; `\lib` se v tomto případě nepoužijí (NuGet nemůže přidat odkazy na projekt C++). Balíček může také zahrnovat cíle a soubory props v `\build` této NuGet se automaticky naimportují do projektů, které daný balíček využívají. Tyto soubory musí být pojmenovány stejně jako ID balíčku s `.targets` příponami a/nebo `.props` . Například balíček [cpprestsdk](https://nuget.org/packages/cpprestsdk/) zahrnuje `cpprestsdk.targets` soubor do své `\build` složky.

`\build`Složku lze použít pro všechny balíčky NuGet, nikoli jenom pro nativní balíčky. `\build`Složka respektuje cílová rozhraní, stejně jako `\content` složky, `\lib` a `\tools` . To znamená, že můžete vytvořit `\build\net40` složku a `\build\net45` složku a NuGet bude importovat příslušné soubory props a targets do projektu. (Pro import cílů MSBuild není potřeba používat skripty PowerShellu.)
