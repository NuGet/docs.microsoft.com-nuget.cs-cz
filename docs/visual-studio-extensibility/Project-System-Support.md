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
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Podpora NuGet pro projekt systému Visual Studio

Pro podporu typů projektů třetích stran v sadě Visual Studio, podporuje NuGet 3.x+ [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), a NuGet 3.2 + podporuje také systémů projektů prohlášení CPS.

K integraci s NuGet, musí systém projektu inzerovat vlastní podporu pro všechny možnosti projektu popsané v tomto tématu.

> [!Note]
> Nemusíte deklarovat funkce, které váš projekt nemá ve skutečnosti pro účely povolení balíčků pro instalaci ve vašem projektu. Mnoho funkcí sady Visual Studio a další rozšíření závisí na možnostech projektu kromě klienta NuGet. Možnosti projektu falešně inzerování může způsobit, že tyto součásti selhání a zkušenosti vašich uživatelů dojít ke snížení.

## <a name="advertise-project-capabilities"></a>Inzerování možností projektu

NuGet klienta Určuje, které balíčky jsou kompatibilní s typem váš projekt na základě [možnosti projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), jak je popsáno v následující tabulce.

| Funkce | Popis |
| --- | --- |
| Odkazy AssemblyReferences | Označuje, že projekt podporuje (liší od WinRTReferences) odkazy na sestavení. |
| DeclaredSourceItems | Označuje, že projekt je obvyklou pro projekty MSBuild (ne DNX), deklaruje zdrojové položky v samotném projektu. |
| UserSourceItems|Označuje, že uživatel může přidat různé soubory do svého projektu. |

Pro systémy projektu založeného na CPS podrobnosti implementace pro možnosti projektu popsané ve zbytku této části jsme udělali za vás. Zobrazit [deklarace schopnosti projektu v projektech CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementing VsProjectCapabilitiesPresenceChecker

`VsProjectCapabilitiesPresenceChecker` Třída musí implementovat `IVsBooleanSymbolPresenceChecker` rozhraní, která je definovaná následujícím způsobem:

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

Ukázková implementace tohoto rozhraní by pak:

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

Nezapomeňte přidat nebo odebrat možnosti z `ActualProjectCapabilities` založena na co se projektový systém skutečně podporuje. Najdete v článku [projektu dokumentaci funkce](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) úplný popis.

## <a name="responding-to-queries"></a>Reakce na dotazy

Projekt deklaruje díky podpoře tuto funkci `VSHPROPID_ProjectCapabilitiesChecker` vlastnosti prostřednictvím `IVsHierarchy::GetProperty`. Měla by vrátit instanci `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, který je definován v `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` sestavení. Odkazují na toto sestavení nainstalováním [svůj balíček NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Můžete například přidat následující `case` příkazu vaše `IVsHierarchy::GetProperty` metody `switch` – příkaz:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Podpora DTE

NuGet jednotky systém projektu přidáte odkazy na položky obsahu a nástroje MSBuild importuje voláním [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), což je nejvyšší úrovně rozhraní automatizace sady Visual Studio. DTE představuje sadu rozhraní modelu COM, které je mohou implementovat.

Pokud váš projekt je založena na CPS, DTE je implementovaná za vás.
