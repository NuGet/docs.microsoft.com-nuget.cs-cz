---
title: "Vytváření balíčků NuGet nativní | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 7a70d748-efe2-4f8f-a3fd-67ddb0f6214e
description: "Informace o vytváření nativní balíčky NuGet, které obsahuje C++ – kód místo spravovaného kódu pro použití v projektech C++."
keywords: "Nativní balíčky NuGet, balíčky NuGet C++, balíčky nativního kódu, cílení projekty C++"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa5baaa6ecbad0f5f6dd85d657679ffbbbc8a47a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="creating-native-packages"></a>Vytváření nativní balíčků

Nativní balíček obsahuje nativní kód C++ místo spravovaného kódu, díky kterému jej použít v projektech C++. (Viz [nativní balíčky C++](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) v části spotřebovat.)

Aby byl použití v projektu jazyka C++, musí být balíček `native` framework. V současné době nejsou k dispozici všechna čísla verze přidružené toto rozhraní jako NuGet zpracovává všechny projekty C++ stejné.

> [!Note]
> Nezapomeňte zahrnout *nativní* v `<tags>` část vaší `.nuspec` pomohou jinými vývojáři najít váš balíček tak, že na tuto značku.

Cílení na nativní balíčky NuGet `native` zadejte soubory v `\build`, `\content`, a `\tools` složek; `\lib` není použit v tomto případě (NuGet nelze přímo přidat odkazy na projektu jazyka C++). Balíček může zahrnovat také cíle a soubory props v `\build` , bude automaticky importovat do projektů, které využívají balíček NuGet. Tyto soubory musí být se stejným názvem jako ID balíčku se `.targets` nebo `.props` rozšíření. Například [cpprestsdk](https://nuget.org/packages/cpprestsdk/) balíček obsahuje `cpprestsdk.targets` souboru v jeho `\build` složky.

`\build` Složky lze použít pro všechny balíčky NuGet a právě nativní balíčky. `\build` Složky respektuje cílové rozhraní, podobně jako `\content`, `\lib`, a `\tools` složek. To znamená, že můžete vytvořit `\build\net40` složky a `\build\net45` složku a NuGet naimportuje příslušné soubory props a cíle do projektu. (Použití skriptů prostředí PowerShell k importu cíle MSBuild není nutné.)
