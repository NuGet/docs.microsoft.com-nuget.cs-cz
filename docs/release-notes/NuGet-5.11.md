---
title: NuGet k vydání verze 5.11
description: Poznámky k verzi NuGet 5.11, včetně nových funkcí, oprav chyb a souborů DCRs.
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728433"
---
# <a name="nuget-511-release-notes"></a>NuGet k vydání verze 5.11

NuGet distribučních vozidel:

| NuGet verze | K dispozici ve Visual Studio verzi | K dispozici v sadě .NET SDK |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16.11](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Nainstalované s Visual Studio 2019 s úlohou .NET Core
  
> [!NOTE]
> Visual Studio 16.11, MSBuild 16.11 a .NET 5.0.400+ vyžaduje NuGet.exe 5.11 nebo novější.

## <a name="summary-whats-new-in-511"></a>Shrnutí: Co je nového ve windows 5.11

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chyby:**

* Nástroje –> Možnosti –> NuGet Správce balíčků řetězec je zkrácený – [#10779](https://github.com/NuGet/Home/issues/10779)

* Při spuštění události PackagesMissingStatusChanged přestane reagovat – [#10854](https://github.com/NuGet/Home/issues/10854)

* Klient NuGet ignoruje nastavení NO_PROXY – [#10902](https://github.com/NuGet/Home/issues/10902)

**[Seznam všech problémů opravených v této verzi – 5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[Seznam potvrzení v této verzi – 5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>Váš názor – vítejte

Vaše názory jsou pro nás důležité.  Pokud dojde k problémům s touto verzí, podívejte se na GitHub [problémy](https://github.com/NuGet/Home/issues) a [Visual Studio vývojářské Community](https://developercommunity.visualstudio.com/) problémy.  V případě nových problémů v NuGet nahlásit problém [GitHub problémy.](https://github.com/NuGet/Home/issues/new)
V případě obecných NuGet problémů s prostředím nám dejte vědět prostřednictvím možnosti Nahlásit problém, která se nachází ve vašem oblíbeném integrovaném vývojovém prostředí (IDE) **v části Nápověda > Nahlásit problém.** [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)
