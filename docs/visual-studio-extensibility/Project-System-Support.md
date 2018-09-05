---
title: Podpora NuGet pro projekt systému Visual Studio
description: Integrace NuGet do projektu systému Visual Studio pro typy projektů třetích stran.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551367"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="9841f-103">Podpora NuGet pro projekt systému Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9841f-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="9841f-104">Pro podporu typů projektů třetích stran v sadě Visual Studio, podporuje NuGet 3.x+ [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), a NuGet 3.2 + podporuje také systémů projektů prohlášení CPS.</span><span class="sxs-lookup"><span data-stu-id="9841f-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="9841f-105">K integraci s NuGet, musí systém projektu inzerovat vlastní podporu pro všechny možnosti projektu popsané v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="9841f-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="9841f-106">Nemusíte deklarovat funkce, které váš projekt nemá ve skutečnosti pro účely povolení balíčků pro instalaci ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="9841f-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="9841f-107">Mnoho funkcí sady Visual Studio a další rozšíření závisí na možnostech projektu kromě klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="9841f-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="9841f-108">Možnosti projektu falešně inzerování může způsobit, že tyto součásti selhání a zkušenosti vašich uživatelů dojít ke snížení.</span><span class="sxs-lookup"><span data-stu-id="9841f-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="9841f-109">Inzerování možností projektu</span><span class="sxs-lookup"><span data-stu-id="9841f-109">Advertise project capabilities</span></span>

<span data-ttu-id="9841f-110">NuGet klienta Určuje, které balíčky jsou kompatibilní s typem váš projekt na základě [možnosti projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), jak je popsáno v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="9841f-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="9841f-111">Funkce</span><span class="sxs-lookup"><span data-stu-id="9841f-111">Capability</span></span> | <span data-ttu-id="9841f-112">Popis</span><span class="sxs-lookup"><span data-stu-id="9841f-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9841f-113">Odkazy AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="9841f-113">AssemblyReferences</span></span> | <span data-ttu-id="9841f-114">Označuje, že projekt podporuje (liší od WinRTReferences) odkazy na sestavení.</span><span class="sxs-lookup"><span data-stu-id="9841f-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="9841f-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="9841f-115">DeclaredSourceItems</span></span> | <span data-ttu-id="9841f-116">Označuje, že projekt je obvyklou pro projekty MSBuild (ne DNX), deklaruje zdrojové položky v samotném projektu.</span><span class="sxs-lookup"><span data-stu-id="9841f-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="9841f-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="9841f-117">UserSourceItems</span></span>|<span data-ttu-id="9841f-118">Označuje, že uživatel může přidat různé soubory do svého projektu.</span><span class="sxs-lookup"><span data-stu-id="9841f-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="9841f-119">Pro systémy projektu založeného na CPS podrobnosti implementace pro možnosti projektu popsané ve zbytku této části jsme udělali za vás.</span><span class="sxs-lookup"><span data-stu-id="9841f-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="9841f-120">Zobrazit [deklarace schopnosti projektu v projektech CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="9841f-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="9841f-121">Implementing VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="9841f-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="9841f-122">`VsProjectCapabilitiesPresenceChecker` Třída musí implementovat `IVsBooleanSymbolPresenceChecker` rozhraní, která je definovaná následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="9841f-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="9841f-123">Ukázková implementace tohoto rozhraní by pak:</span><span class="sxs-lookup"><span data-stu-id="9841f-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="9841f-124">Nezapomeňte přidat nebo odebrat možnosti z `ActualProjectCapabilities` založena na co se projektový systém skutečně podporuje.</span><span class="sxs-lookup"><span data-stu-id="9841f-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="9841f-125">Najdete v článku [projektu dokumentaci funkce](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) úplný popis.</span><span class="sxs-lookup"><span data-stu-id="9841f-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="9841f-126">Reakce na dotazy</span><span class="sxs-lookup"><span data-stu-id="9841f-126">Responding to queries</span></span>

<span data-ttu-id="9841f-127">Projekt deklaruje díky podpoře tuto funkci `VSHPROPID_ProjectCapabilitiesChecker` vlastnosti prostřednictvím `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="9841f-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="9841f-128">Měla by vrátit instanci `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, který je definován v `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` sestavení.</span><span class="sxs-lookup"><span data-stu-id="9841f-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="9841f-129">Odkazují na toto sestavení nainstalováním [svůj balíček NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="9841f-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="9841f-130">Můžete například přidat následující `case` příkazu vaše `IVsHierarchy::GetProperty` metody `switch` – příkaz:</span><span class="sxs-lookup"><span data-stu-id="9841f-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="9841f-131">Podpora DTE</span><span class="sxs-lookup"><span data-stu-id="9841f-131">DTE Support</span></span>

<span data-ttu-id="9841f-132">NuGet jednotky systém projektu přidáte odkazy na položky obsahu a nástroje MSBuild importuje voláním [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), což je nejvyšší úrovně rozhraní automatizace sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9841f-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="9841f-133">DTE představuje sadu rozhraní modelu COM, které je mohou implementovat.</span><span class="sxs-lookup"><span data-stu-id="9841f-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="9841f-134">Pokud váš projekt je založena na CPS, DTE je implementovaná za vás.</span><span class="sxs-lookup"><span data-stu-id="9841f-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
