---
title: Podpora NuGet pro systém projektů Visual studia
description: Integrace NuGet do systému projektu sady Visual Studio pro typy projektů třetích stran.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 7af330f88b47352666933598719d9c8f8cb66a78
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779402"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="c7c49-103">Podpora NuGet pro systém projektů Visual studia</span><span class="sxs-lookup"><span data-stu-id="c7c49-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="c7c49-104">Pro podporu typů projektů třetích stran v aplikaci Visual Studio NuGet 3. x + podporuje [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)a NuGet 3.2 + podporuje také systémy jiných projektů než CPS.</span><span class="sxs-lookup"><span data-stu-id="c7c49-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="c7c49-105">Pro integraci s NuGet musí projektový systém inzerovat svou vlastní podporu pro všechny možnosti projektu popsané v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="c7c49-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="c7c49-106">Nedeklarujte možnosti, které váš projekt ve skutečnosti nepotřebuje k tomu, aby bylo možné balíčky nainstalovat do projektu.</span><span class="sxs-lookup"><span data-stu-id="c7c49-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="c7c49-107">Mnoho funkcí sady Visual Studio a dalších rozšíření závisí na možnostech projektu kromě klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="c7c49-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="c7c49-108">Nepravdivé reklamní schopnosti vašeho projektu můžou těmto komponentám způsobit nefunkčnost a možnosti vašich uživatelů ke zhoršení.</span><span class="sxs-lookup"><span data-stu-id="c7c49-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="c7c49-109">Inzerovat možnosti projektu</span><span class="sxs-lookup"><span data-stu-id="c7c49-109">Advertise project capabilities</span></span>

<span data-ttu-id="c7c49-110">Klient NuGet určuje, které balíčky jsou kompatibilní s typem projektu na základě [schopností projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), jak je popsáno v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="c7c49-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="c7c49-111">Schopnost</span><span class="sxs-lookup"><span data-stu-id="c7c49-111">Capability</span></span> | <span data-ttu-id="c7c49-112">Description</span><span class="sxs-lookup"><span data-stu-id="c7c49-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7c49-113">Odkazy AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="c7c49-113">AssemblyReferences</span></span> | <span data-ttu-id="c7c49-114">Označuje, že projekt podporuje odkazy na sestavení (DISTINCT z WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="c7c49-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="c7c49-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="c7c49-115">DeclaredSourceItems</span></span> | <span data-ttu-id="c7c49-116">Označuje, že projekt je typický projekt MSBuild (ne DNX) v tom, že deklaruje zdrojové položky v samotném projektu.</span><span class="sxs-lookup"><span data-stu-id="c7c49-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="c7c49-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="c7c49-117">UserSourceItems</span></span>|<span data-ttu-id="c7c49-118">Indikuje, že uživatel smí do svého projektu přidat libovolné soubory.</span><span class="sxs-lookup"><span data-stu-id="c7c49-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="c7c49-119">V případě systémů projektů založených na CPS jsme pro vás provedli podrobnosti o implementaci funkcí projektu popsaných ve zbývající části tohoto oddílu.</span><span class="sxs-lookup"><span data-stu-id="c7c49-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="c7c49-120">Viz téma [deklarace možností projektu v projektech CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="c7c49-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="c7c49-121">Implementace VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="c7c49-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="c7c49-122">`VsProjectCapabilitiesPresenceChecker`Třída musí implementovat `IVsBooleanSymbolPresenceChecker` rozhraní, které je definováno následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="c7c49-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="c7c49-123">Ukázková implementace tohoto rozhraní by pak byla:</span><span class="sxs-lookup"><span data-stu-id="c7c49-123">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="c7c49-124">Nezapomeňte přidat nebo odebrat funkce ze `ActualProjectCapabilities` sady na základě toho, co váš projektový systém skutečně podporuje.</span><span class="sxs-lookup"><span data-stu-id="c7c49-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="c7c49-125">Úplný popis najdete v [dokumentaci k funkcím projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) .</span><span class="sxs-lookup"><span data-stu-id="c7c49-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="c7c49-126">Reakce na dotazy</span><span class="sxs-lookup"><span data-stu-id="c7c49-126">Responding to queries</span></span>

<span data-ttu-id="c7c49-127">Projekt deklaruje tuto schopnost tím, že podporuje  `VSHPROPID_ProjectCapabilitiesChecker` vlastnost prostřednictvím `IVsHierarchy::GetProperty` .</span><span class="sxs-lookup"><span data-stu-id="c7c49-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="c7c49-128">Měla by vracet instanci `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` , která je definována v `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` sestavení.</span><span class="sxs-lookup"><span data-stu-id="c7c49-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="c7c49-129">Odkázat na toto sestavení instalací [balíčku NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="c7c49-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="c7c49-130">Do příkazu vaší metody můžete například přidat následující `case` příkaz `IVsHierarchy::GetProperty` `switch` :</span><span class="sxs-lookup"><span data-stu-id="c7c49-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="c7c49-131">Podpora DTE</span><span class="sxs-lookup"><span data-stu-id="c7c49-131">DTE Support</span></span>

<span data-ttu-id="c7c49-132">NuGet řídí projektový systém k přidávání odkazů, položek obsahu a importů MSBuild voláním do [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), což je rozhraní automatizace sady Visual Studio nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="c7c49-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="c7c49-133">DTE je sada rozhraní COM, která může být již implementována.</span><span class="sxs-lookup"><span data-stu-id="c7c49-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="c7c49-134">Pokud je váš typ projektu založený na CPS, implementuje se zařízení DTE za vás.</span><span class="sxs-lookup"><span data-stu-id="c7c49-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
