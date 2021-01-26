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
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Podpora NuGet pro systém projektů Visual studia

Pro podporu typů projektů třetích stran v aplikaci Visual Studio NuGet 3. x + podporuje [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)a NuGet 3.2 + podporuje také systémy jiných projektů než CPS.

Pro integraci s NuGet musí projektový systém inzerovat svou vlastní podporu pro všechny možnosti projektu popsané v tomto tématu.

> [!Note]
> Nedeklarujte možnosti, které váš projekt ve skutečnosti nepotřebuje k tomu, aby bylo možné balíčky nainstalovat do projektu. Mnoho funkcí sady Visual Studio a dalších rozšíření závisí na možnostech projektu kromě klienta NuGet. Nepravdivé reklamní schopnosti vašeho projektu můžou těmto komponentám způsobit nefunkčnost a možnosti vašich uživatelů ke zhoršení.

## <a name="advertise-project-capabilities"></a>Inzerovat možnosti projektu

Klient NuGet určuje, které balíčky jsou kompatibilní s typem projektu na základě [schopností projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), jak je popsáno v následující tabulce.

| Schopnost | Description |
| --- | --- |
| Odkazy AssemblyReferences | Označuje, že projekt podporuje odkazy na sestavení (DISTINCT z WinRTReferences). |
| DeclaredSourceItems | Označuje, že projekt je typický projekt MSBuild (ne DNX) v tom, že deklaruje zdrojové položky v samotném projektu. |
| UserSourceItems|Indikuje, že uživatel smí do svého projektu přidat libovolné soubory. |

V případě systémů projektů založených na CPS jsme pro vás provedli podrobnosti o implementaci funkcí projektu popsaných ve zbývající části tohoto oddílu. Viz téma [deklarace možností projektu v projektech CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementace VsProjectCapabilitiesPresenceChecker

`VsProjectCapabilitiesPresenceChecker`Třída musí implementovat `IVsBooleanSymbolPresenceChecker` rozhraní, které je definováno následujícím způsobem:

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

Nezapomeňte přidat nebo odebrat funkce ze `ActualProjectCapabilities` sady na základě toho, co váš projektový systém skutečně podporuje. Úplný popis najdete v [dokumentaci k funkcím projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) .

## <a name="responding-to-queries"></a>Reakce na dotazy

Projekt deklaruje tuto schopnost tím, že podporuje  `VSHPROPID_ProjectCapabilitiesChecker` vlastnost prostřednictvím `IVsHierarchy::GetProperty` . Měla by vracet instanci `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` , která je definována v `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` sestavení. Odkázat na toto sestavení instalací [balíčku NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Do příkazu vaší metody můžete například přidat následující `case` příkaz `IVsHierarchy::GetProperty` `switch` :

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Podpora DTE

NuGet řídí projektový systém k přidávání odkazů, položek obsahu a importů MSBuild voláním do [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), což je rozhraní automatizace sady Visual Studio nejvyšší úrovně. DTE je sada rozhraní COM, která může být již implementována.

Pokud je váš typ projektu založený na CPS, implementuje se zařízení DTE za vás.
