---
title: Podpora nugetpro systém projektu sady Visual Studio
description: Integrace NuGet do systému projektu Visual Studio pro typy projektů třetích stran.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495921"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Podpora nuget pro systém projektu sady Visual Studio

Pro podporu typů projektů třetích stran v sadě Visual Studio podporuje NuGet 3.x+ [společný projektový systém (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)a NuGet 3.2+ podporuje také projektové systémy bez CPS.

Chcete-li integrovat s NuGet, projektový systém musí inzerovat vlastní podporu pro všechny možnosti projektu popsané v tomto tématu.

> [!Note]
> Nedeklarujte možnosti, které váš projekt ve skutečnosti nemá z důvodu povolení balíčků k instalaci v projektu. Mnoho funkcí sady Visual Studio a další rozšíření závisí na možnostech projektu kromě klienta NuGet. Nepravdivě reklamní schopnosti vašeho projektu může vést tyto součásti k poruše a zkušenosti uživatelů ke snížení.

## <a name="advertise-project-capabilities"></a>Inzerovat možnosti projektu

Klient NuGet určuje, které balíčky jsou kompatibilní s typem projektu na základě [možností projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), jak je popsáno v následující tabulce.

| Schopnost | Popis |
| --- | --- |
| Odkazy na sestavení | Označuje, že projekt podporuje odkazy na sestavení (odlišné od WinRTReferences). |
| Deklarované položky zdroje | Označuje, že projekt je typický msbuild projektu (ne DNX) v tom, že deklaruje zdrojové položky v samotném projektu. |
| Uživatelské položky|Označuje, že uživatel může do svého projektu přidávat libovolné soubory. |

Pro projektové systémy založené na CPS byly provedeny podrobnosti implementace pro možnosti projektu popsané ve zbývající části této části. Viz [deklarování možností projektu v projektech CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementace nástroje VsProjectCapabilitiesPresenceChecker

Třída `VsProjectCapabilitiesPresenceChecker` musí implementovat `IVsBooleanSymbolPresenceChecker` rozhraní, které je definováno takto:

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

Ukázková implementace tohoto rozhraní by pak byla:

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

Nezapomeňte přidat nebo odebrat `ActualProjectCapabilities` funkce ze sady na základě toho, co váš projektový systém skutečně podporuje. Úplné popisy naleznete v dokumentaci k [možnostem projektu.](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)

## <a name="responding-to-queries"></a>Odpovídání na dotazy

Projekt deklaruje tuto `VSHPROPID_ProjectCapabilitiesChecker` schopnost podporou `IVsHierarchy::GetProperty`vlastnostprostřednictvím . By měl vrátit `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`instanci , `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` která je definována v sestavení. Odkaz na toto sestavení instalací [jeho NuGet balíček](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Do `switch` příkazu `IVsHierarchy::GetProperty` metody můžete `case` například přidat následující příkaz:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Podpora DTE

NuGet řídí systém projektu přidat odkazy, položky obsahu a MSBuild importy voláním do [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), což je rozhraní automatizace visual studio nejvyšší úrovně. DTE je sada rozhraní COM, které již můžete implementovat.

Pokud je typ projektu založen na CPS, DTE je implementována za vás.
