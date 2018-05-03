---
title: Vytváření balíčků nativní NuGet
description: Informace o vytváření nativní balíčky NuGet, které obsahuje C++ – kód místo spravovaného kódu pro použití v projektech C++.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 1fa8bf23a3fbed686b99f1c783b0ce55b373e548
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="creating-native-packages"></a><span data-ttu-id="689ac-103">Vytváření nativní balíčků</span><span class="sxs-lookup"><span data-stu-id="689ac-103">Creating native packages</span></span>

<span data-ttu-id="689ac-104">Nativní balíček obsahuje nativní kód C++ místo spravovaného kódu, díky kterému jej použít v projektech C++.</span><span class="sxs-lookup"><span data-stu-id="689ac-104">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="689ac-105">(Viz [nativní balíčky C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) v části spotřebovat.)</span><span class="sxs-lookup"><span data-stu-id="689ac-105">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="689ac-106">Aby byl použití v projektu jazyka C++, musí být balíček `native` framework.</span><span class="sxs-lookup"><span data-stu-id="689ac-106">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="689ac-107">V současné době nejsou k dispozici všechna čísla verze přidružené toto rozhraní jako NuGet zpracovává všechny projekty C++ stejné.</span><span class="sxs-lookup"><span data-stu-id="689ac-107">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="689ac-108">Nezapomeňte zahrnout *nativní* v `<tags>` část vaší `.nuspec` pomohou jinými vývojáři najít váš balíček tak, že na tuto značku.</span><span class="sxs-lookup"><span data-stu-id="689ac-108">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="689ac-109">Cílení na nativní balíčky NuGet `native` zadejte soubory v `\build`, `\content`, a `\tools` složek; `\lib` není použit v tomto případě (NuGet nelze přímo přidat odkazy na projektu jazyka C++).</span><span class="sxs-lookup"><span data-stu-id="689ac-109">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="689ac-110">Balíček může zahrnovat také cíle a soubory props v `\build` , bude automaticky importovat do projektů, které využívají balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="689ac-110">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="689ac-111">Tyto soubory musí být se stejným názvem jako ID balíčku se `.targets` nebo `.props` rozšíření.</span><span class="sxs-lookup"><span data-stu-id="689ac-111">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="689ac-112">Například [cpprestsdk](https://nuget.org/packages/cpprestsdk/) balíček obsahuje `cpprestsdk.targets` souboru v jeho `\build` složky.</span><span class="sxs-lookup"><span data-stu-id="689ac-112">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="689ac-113">`\build` Složky lze použít pro všechny balíčky NuGet a právě nativní balíčky.</span><span class="sxs-lookup"><span data-stu-id="689ac-113">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="689ac-114">`\build` Složky respektuje cílové rozhraní, podobně jako `\content`, `\lib`, a `\tools` složek.</span><span class="sxs-lookup"><span data-stu-id="689ac-114">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="689ac-115">To znamená, že můžete vytvořit `\build\net40` složky a `\build\net45` složku a NuGet naimportuje příslušné soubory props a cíle do projektu.</span><span class="sxs-lookup"><span data-stu-id="689ac-115">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="689ac-116">(Použití skriptů prostředí PowerShell k importu cíle MSBuild není nutné.)</span><span class="sxs-lookup"><span data-stu-id="689ac-116">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
