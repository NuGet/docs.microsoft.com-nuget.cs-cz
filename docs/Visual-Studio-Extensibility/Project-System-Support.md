---
title: "Podpora NuGet pro projekt systému Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Integrace NuGet do projektu systému Visual Studio pro typy projektů třetích stran."
keywords: "NuGet v sadě Visual Studio, typy vlastních projektů, projektů sady Visual Studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e2f7c4a32f80b96360f08d04efb8af639af2ddd3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Podpora NuGet pro projekt systému Visual Studio

Pro podporu typy třetích stran projektů v sadě Visual Studio, podporuje NuGet 3.x+ [běžné projektu System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), a NuGet 3.2 + podporuje také systémy-prohlášení CPS projektu.

K integraci s NuGet, musí systému projektu inzerovat vlastní podporu pro všechny možnosti projektu popsaných v tomto tématu.

> [!Note]
> Nemáte deklarovat možnosti, které projektu nemá ve skutečnosti z důvodu povolení balíčků pro instalaci ve vašem projektu. Mnoho funkcí sady Visual Studio a další rozšíření závisí na možnostech projektu kromě klienta NuGet. Možnosti projektu nesprávně inzerování může způsobit, že tyto součásti fungovat správně a zkušenosti uživatelů snižovat.

## <a name="advertise-project-capabilities"></a>Inzerovat možnosti projektu

NuGet klienta Určuje, které balíčky jsou kompatibilní s typem vašeho projektu na základě [možnosti projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), jak je popsáno v následující tabulce.

| Funkce | Popis |
| --- | --- |
| AssemblyReferences | Označuje, že projekt podporuje odkazy na sestavení (liší od WinRTReferences). |
| DeclaredSourceItems | Označuje, že projekt je typické projektu nástroje MSBuild (ne DNX) v tom, že deklaruje položky zdroje v projektu. |
| UserSourceItems|Označuje, že uživatel může přidat libovolné soubory do svého projektu. |

U systémů, na základě CPS projektu jsou prováděny podrobnosti implementace pro možnosti projektu popsané ve zbývající části této části pro vás. V tématu [deklarace možnosti projektu v projektech CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementing VsProjectCapabilitiesPresenceChecker

`VsProjectCapabilitiesPresenceChecker` Musí implementovat třídu `IVsBooleanSymbolPresenceChecker` rozhraní, což je definován následujícím způsobem:

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

Ukázka implementace tohoto rozhraní by pak bylo:

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

Nezapomeňte přidat nebo odebrat možnosti z `ActualProjectCapabilities` založena na co se váš projekt systém skutečně podporuje. Najdete v článku [projektu možnosti dokumentaci](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) pro úplný popis.

## <a name="responding-to-queries"></a>Odpovídá na dotazy

Projekt deklaruje díky podpoře tato funkce `VSHPROPID_ProjectCapabilitiesChecker` vlastnosti prostřednictvím `IVsHierarchy::GetProperty`. Měla by vrátit instanci `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, která je definována v `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` sestavení. Toto sestavení odkazovat nainstalováním [jeho balíček NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Může například přidat následující `case` příkaz, který má vaše `IVsHierarchy::GetProperty` metody `switch` příkaz:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Podpora prostředí DTE

NuGet jednotky systému projektu přidáte odkazy, položky obsahu a MSBuild importuje voláním [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), což je nejvyšší úrovně rozhraní pro automatizaci sady Visual Studio. DTE je sada rozhraní modelu COM, které je může implementovat.

Pokud typ vašeho projektu je založená na CPS, DTE je implementována pro vás.
