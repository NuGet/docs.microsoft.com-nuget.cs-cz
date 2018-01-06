---
title: "Podpora NuGet pro projekt systému Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 9d7fa7f6-82ed-4df6-9734-f43a3d8e3b98
description: "Integrace NuGet do projektu systému Visual Studio pro typy projektů třetích stran."
keywords: "NuGet v sadě Visual Studio, typy vlastních projektů, projektů sady Visual Studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c8cad46f18578bec41bd9280985e42972a9b3c1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="596e1-104">Podpora NuGet pro projekt systému Visual Studio</span><span class="sxs-lookup"><span data-stu-id="596e1-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="596e1-105">Pro podporu typy třetích stran projektů v sadě Visual Studio, podporuje NuGet 3.x+ [běžné projektu System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), a NuGet 3.2 + podporuje také systémy-prohlášení CPS projektu.</span><span class="sxs-lookup"><span data-stu-id="596e1-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="596e1-106">K integraci s NuGet, musí systému projektu inzerovat vlastní podporu pro všechny možnosti projektu popsaných v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="596e1-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>


> [!NOTE]
> <span data-ttu-id="596e1-107">Nedeklarujte možnosti, které projektu nemá ve skutečnosti z důvodu povolení balíčků pro instalaci ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="596e1-107">Do not declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="596e1-108">Mnoho funkcí sady Visual Studio a další rozšíření závisí na možnostech projektu kromě klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="596e1-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="596e1-109">Možnosti projektu nesprávně inzerování může způsobit, že tyto součásti fungovat správně a zkušenosti uživatelů snižovat.</span><span class="sxs-lookup"><span data-stu-id="596e1-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="596e1-110">Inzerovat možnosti projektu</span><span class="sxs-lookup"><span data-stu-id="596e1-110">Advertise project capabilities</span></span>

<span data-ttu-id="596e1-111">NuGet klienta Určuje, které balíčky jsou kompatibilní s typem vašeho projektu na základě [možnosti projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), jak je popsáno v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="596e1-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>


|<span data-ttu-id="596e1-112">Funkce</span><span class="sxs-lookup"><span data-stu-id="596e1-112">Capability</span></span>|<span data-ttu-id="596e1-113">Popis</span><span class="sxs-lookup"><span data-stu-id="596e1-113">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="596e1-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="596e1-114">AssemblyReferences</span></span>|<span data-ttu-id="596e1-115">Označuje, že projekt podporuje odkazy na sestavení (liší od WinRTReferences)</span><span class="sxs-lookup"><span data-stu-id="596e1-115">Indicates that the project supports assembly references (distinct from WinRTReferences)</span></span>|
|<span data-ttu-id="596e1-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="596e1-116">DeclaredSourceItems</span></span>|<span data-ttu-id="596e1-117">Označuje, že projekt je typické projektu nástroje MSBuild (ne DNX) v tom, že deklaruje položky zdroje v projektu (ne `project.json` soubor, který se předpokládá, všechny soubory ve složce jsou součástí kompilace).</span><span class="sxs-lookup"><span data-stu-id="596e1-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself (rather than a `project.json` file that assumes all files in the folder are part of a compilation).</span></span>|
|<span data-ttu-id="596e1-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="596e1-118">UserSourceItems</span></span>|<span data-ttu-id="596e1-119">Označuje, že uživatel může přidat libovolné soubory do svého projektu.</span><span class="sxs-lookup"><span data-stu-id="596e1-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span>|

<span data-ttu-id="596e1-120">U systémů, na základě CPS projektu jsou prováděny podrobnosti implementace pro možnosti projektu popsané ve zbývající části této části pro vás.</span><span class="sxs-lookup"><span data-stu-id="596e1-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="596e1-121">V tématu [deklarace možnosti projektu v projektech CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="596e1-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="596e1-122">Implementace VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="596e1-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="596e1-123">`VsProjectCapabilitiesPresenceChecker` Musí implementovat třídu `IVsBooleanSymbolPresenceChecker` rozhraní, což je definován následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="596e1-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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


<span data-ttu-id="596e1-124">Ukázka implementace tohoto rozhraní by pak bylo:</span><span class="sxs-lookup"><span data-stu-id="596e1-124">A sample implementation of this interface would then be:</span></span>
    
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

<span data-ttu-id="596e1-125">Nezapomeňte přidat nebo odebrat možnosti z `ActualProjectCapabilities` založena na co se váš projekt systém skutečně podporuje.</span><span class="sxs-lookup"><span data-stu-id="596e1-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="596e1-126">Najdete v článku [projektu možnosti dokumentaci](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) pro úplný popis.</span><span class="sxs-lookup"><span data-stu-id="596e1-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="596e1-127">Odpovídá na dotazy</span><span class="sxs-lookup"><span data-stu-id="596e1-127">Responding to queries</span></span>

<span data-ttu-id="596e1-128">Projekt deklaruje díky podpoře tato funkce `VSHPROPID_ProjectCapabilitiesChecker` vlastnosti prostřednictvím `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="596e1-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="596e1-129">Měla by vrátit instanci `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, která je definována v `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` sestavení.</span><span class="sxs-lookup"><span data-stu-id="596e1-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="596e1-130">Toto sestavení odkazovat nainstalováním [jeho balíček NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="596e1-130">Reference this assembly by installing the [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="596e1-131">Může například přidat následující `case` příkaz, který má vaše `IVsHierarchy::GetProperty` metody `switch` příkaz:</span><span class="sxs-lookup"><span data-stu-id="596e1-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="596e1-132">Podpora prostředí DTE</span><span class="sxs-lookup"><span data-stu-id="596e1-132">DTE Support</span></span>

<span data-ttu-id="596e1-133">NuGet jednotky systému projektu přidáte odkazy, položky obsahu a MSBuild importuje voláním [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), což je nejvyšší úrovně rozhraní pro automatizaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="596e1-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="596e1-134">DTE je sada rozhraní modelu COM, které je může implementovat.</span><span class="sxs-lookup"><span data-stu-id="596e1-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="596e1-135">Pokud typ vašeho projektu je založená na CPS, DTE je implementována pro vás.</span><span class="sxs-lookup"><span data-stu-id="596e1-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
