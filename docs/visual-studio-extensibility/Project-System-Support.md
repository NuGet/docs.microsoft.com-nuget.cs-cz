---
title: Podpora NuGet pro projekt systému Visual Studio
description: Integrace NuGet do projektu systému Visual Studio pro typy projektů třetích stran.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: b0937d5c149d79f25a776efac1946c9f42c161e8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816901"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="af4a5-103">Podpora NuGet pro projekt systému Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af4a5-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="af4a5-104">Pro podporu typy třetích stran projektů v sadě Visual Studio, podporuje NuGet 3.x+ [běžné projektu System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), a NuGet 3.2 + podporuje také systémy-prohlášení CPS projektu.</span><span class="sxs-lookup"><span data-stu-id="af4a5-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="af4a5-105">K integraci s NuGet, musí systému projektu inzerovat vlastní podporu pro všechny možnosti projektu popsaných v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="af4a5-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="af4a5-106">Nemáte deklarovat možnosti, které projektu nemá ve skutečnosti z důvodu povolení balíčků pro instalaci ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="af4a5-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="af4a5-107">Mnoho funkcí sady Visual Studio a další rozšíření závisí na možnostech projektu kromě klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="af4a5-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="af4a5-108">Možnosti projektu nesprávně inzerování může způsobit, že tyto součásti fungovat správně a zkušenosti uživatelů snižovat.</span><span class="sxs-lookup"><span data-stu-id="af4a5-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="af4a5-109">Inzerovat možnosti projektu</span><span class="sxs-lookup"><span data-stu-id="af4a5-109">Advertise project capabilities</span></span>

<span data-ttu-id="af4a5-110">NuGet klienta Určuje, které balíčky jsou kompatibilní s typem vašeho projektu na základě [možnosti projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), jak je popsáno v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="af4a5-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="af4a5-111">Funkce</span><span class="sxs-lookup"><span data-stu-id="af4a5-111">Capability</span></span> | <span data-ttu-id="af4a5-112">Popis</span><span class="sxs-lookup"><span data-stu-id="af4a5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="af4a5-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="af4a5-113">AssemblyReferences</span></span> | <span data-ttu-id="af4a5-114">Označuje, že projekt podporuje odkazy na sestavení (liší od WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="af4a5-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="af4a5-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="af4a5-115">DeclaredSourceItems</span></span> | <span data-ttu-id="af4a5-116">Označuje, že projekt je typické projektu nástroje MSBuild (ne DNX) v tom, že deklaruje položky zdroje v projektu.</span><span class="sxs-lookup"><span data-stu-id="af4a5-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="af4a5-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="af4a5-117">UserSourceItems</span></span>|<span data-ttu-id="af4a5-118">Označuje, že uživatel může přidat libovolné soubory do svého projektu.</span><span class="sxs-lookup"><span data-stu-id="af4a5-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="af4a5-119">U systémů, na základě CPS projektu jsou prováděny podrobnosti implementace pro možnosti projektu popsané ve zbývající části této části pro vás.</span><span class="sxs-lookup"><span data-stu-id="af4a5-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="af4a5-120">V tématu [deklarace možnosti projektu v projektech CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="af4a5-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="af4a5-121">Implementing VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="af4a5-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="af4a5-122">`VsProjectCapabilitiesPresenceChecker` Musí implementovat třídu `IVsBooleanSymbolPresenceChecker` rozhraní, což je definován následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="af4a5-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="af4a5-123">Ukázka implementace tohoto rozhraní by pak bylo:</span><span class="sxs-lookup"><span data-stu-id="af4a5-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="af4a5-124">Nezapomeňte přidat nebo odebrat možnosti z `ActualProjectCapabilities` založena na co se váš projekt systém skutečně podporuje.</span><span class="sxs-lookup"><span data-stu-id="af4a5-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="af4a5-125">Najdete v článku [projektu možnosti dokumentaci](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) pro úplný popis.</span><span class="sxs-lookup"><span data-stu-id="af4a5-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="af4a5-126">Odpovídá na dotazy</span><span class="sxs-lookup"><span data-stu-id="af4a5-126">Responding to queries</span></span>

<span data-ttu-id="af4a5-127">Projekt deklaruje díky podpoře tato funkce `VSHPROPID_ProjectCapabilitiesChecker` vlastnosti prostřednictvím `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="af4a5-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="af4a5-128">Měla by vrátit instanci `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, která je definována v `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` sestavení.</span><span class="sxs-lookup"><span data-stu-id="af4a5-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="af4a5-129">Toto sestavení odkazovat nainstalováním [jeho balíček NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="af4a5-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="af4a5-130">Může například přidat následující `case` příkaz, který má vaše `IVsHierarchy::GetProperty` metody `switch` příkaz:</span><span class="sxs-lookup"><span data-stu-id="af4a5-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="af4a5-131">Podpora prostředí DTE</span><span class="sxs-lookup"><span data-stu-id="af4a5-131">DTE Support</span></span>

<span data-ttu-id="af4a5-132">NuGet jednotky systému projektu přidáte odkazy, položky obsahu a MSBuild importuje voláním [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), což je nejvyšší úrovně rozhraní pro automatizaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af4a5-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="af4a5-133">DTE je sada rozhraní modelu COM, které je může implementovat.</span><span class="sxs-lookup"><span data-stu-id="af4a5-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="af4a5-134">Pokud typ vašeho projektu je založená na CPS, DTE je implementována pro vás.</span><span class="sxs-lookup"><span data-stu-id="af4a5-134">If your project type is based on CPS, DTE is implemented for you.</span></span>