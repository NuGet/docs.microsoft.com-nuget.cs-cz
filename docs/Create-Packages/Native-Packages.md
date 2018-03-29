---
title: Vytváření balíčků NuGet nativní | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informace o vytváření nativní balíčky NuGet, které obsahuje C++ – kód místo spravovaného kódu pro použití v projektech C++.
keywords: Nativní balíčky NuGet, balíčky NuGet C++, balíčky nativního kódu, cílení projekty C++
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ed33f906f11a80c0d033292f7de151e93b8368fd
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="creating-native-packages"></a>Vytváření nativní balíčků

Nativní balíček obsahuje nativní kód C++ místo spravovaného kódu, díky kterému jej použít v projektech C++. (Viz [nativní balíčky C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) v části spotřebovat.)

Aby byl použití v projektu jazyka C++, musí být balíček `native` framework. V současné době nejsou k dispozici všechna čísla verze přidružené toto rozhraní jako NuGet zpracovává všechny projekty C++ stejné.

> [!Note]
> Nezapomeňte zahrnout *nativní* v `<tags>` část vaší `.nuspec` pomohou jinými vývojáři najít váš balíček tak, že na tuto značku.

Cílení na nativní balíčky NuGet `native` zadejte soubory v `\build`, `\content`, a `\tools` složek; `\lib` není použit v tomto případě (NuGet nelze přímo přidat odkazy na projektu jazyka C++). Balíček může zahrnovat také cíle a soubory props v `\build` , bude automaticky importovat do projektů, které využívají balíček NuGet. Tyto soubory musí být se stejným názvem jako ID balíčku se `.targets` nebo `.props` rozšíření. Například [cpprestsdk](https://nuget.org/packages/cpprestsdk/) balíček obsahuje `cpprestsdk.targets` souboru v jeho `\build` složky.

`\build` Složky lze použít pro všechny balíčky NuGet a právě nativní balíčky. `\build` Složky respektuje cílové rozhraní, podobně jako `\content`, `\lib`, a `\tools` složek. To znamená, že můžete vytvořit `\build\net40` složky a `\build\net45` složku a NuGet naimportuje příslušné soubory props a cíle do projektu. (Použití skriptů prostředí PowerShell k importu cíle MSBuild není nutné.)
