---
title: "Způsoby instalace balíčků NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Popisuje postup instalace balíčků NuGet do projektu, včetně toho, co se stane, na disku a pro soubory použít projektu."
keywords: "Nainstalujte NuGet, využívání balíčku NuGet, instalace balíčků NuGet, odkazy na balíček NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Různé způsoby, jak nainstalovat balíček NuGet

Balíčky NuGet jsou stáhli a nainstalovali pomocí kteréhokoli z následujících metod (najdete v části [nástrojích klienta nainstalovat NuGet](../install-nuget-client-tools.md) Pokud nemáte tyto již nainstalována):

| Metoda | Popis |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet install <package_name>` | (Všechny platformy) Stáhne balíček identifikovaný \<název_balíčku\>, představuje obsah ve složce v aktuálním adresáři a přidá odkaz na soubor projektu. Také se stáhne a nainstaluje závislosti.<ul><li>[Instalace a použití balíčku (rozhraní příkazového řádku dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Příkazy dotnet](../tools/dotnet-commands.md)</li></ul> |
| Uživatelského rozhraní Správce balíčků (Visual Studio) | (Windows a Mac) Poskytuje uživatelské rozhraní, pomocí kterého můžete procházet, vyberte a nainstalujte balíčky a jejich závislosti do projektu. Přidá odkazy na balíčky nainstalované do souboru projektu.<ul><li>[Instalace a použití balíčku (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Odkaz uživatelského rozhraní Správce balíčků (Windows)](../tools/package-manager-ui.md)</li><li>[Včetně balíček NuGet do projektu (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Konzola správce balíčků (Visual Studio)<br/>`Install-Package <package_name>` | (Jenom Windows) Stáhne a nainstaluje balíček identifikovaný \<název_balíčku\> do zadaného projektu v řešení, pak přidá odkaz na soubor projektu. Také se stáhne a nainstaluje závislosti.<ul><li>[Instalace a použití balíčku (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Konzola správce balíčků Průvodce](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (Všechny platformy) Stáhne balíček identifikovaný \<název_balíčku\> a rozšíří jeho obsah do složky v aktuálním adresáři, můžete si taky stáhnout všechny balíčky uvedené v `packages.config` souboru. Také stáhne a nainstaluje závislosti, ale neprovede žádné změny souborů projektu.<ul><li>[příkaz instalovat](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Proces instalace obecné

Obecně platí NuGet provede následující pak zobrazí výzva k instalaci balíčku:

1. Získání balíčku:
    - Zkontrolujte, zda požadovaný balíček již existuje v mezipaměti (viz [Správa mezipaměti NuGet](managing-the-nuget-cache.md)).
    - Pokud balíček není v mezipaměti, pokusí se stáhnout balíček z zdrojích uvedených v [konfigurační soubory](Configuring-NuGet-Behavior.md).
      - U projektů pomocí `packages.config` formát reference, NuGet používá pořadí zdrojů v konfiguraci.
      - Pro projekty formátu PackageReference NuGet kontroluje zdroje, které jsou místní složky nejprve pak zkontroluje zdrojů na sdílené síťové složky, pak zkontroluje zdrojů HTTP (Internet).
      - Obecně platí není zvlášť důležité, pořadí, ve kterém NuGet kontroluje zdroje, protože libovolný daný balíček s číslem konkrétní identifikátor a verzi se přesně shodují na jakémkoli zdroji zjistí.
    - Pokud balíček je úspěšně získali z jednoho zdroje, NuGet přidán do mezipaměti. Jinak instalace se nezdaří.

1. Rozbalte balíček do projektu.
    - Rozšiřování znamená rozbalení obsah balíčku do příslušné složky. Kopii `.nupkg` samotné je také umístěna v podsložce.
    - Pokud balíček se instaluje do projektu sady Visual Studio nebo .NET Core, jsou pouze soubory, které se týkají cílový framework projektu na rozšířit. Při instalaci pomocí příkazového řádku nuget.exe jsou rozšířit ve všech sestaveních.

1. Pokud je balíček nainstalován v sadě Visual Studio nebo dotnet rozhraní příkazového řádku, odkaz se přidá k souboru příslušná projektu (nebo `packages.config` pro některé typy projektů v sadě Visual Studio).

## <a name="related-topics"></a>Související témata

- [Přehled a pracovní postup spotřeby balíčku](../consume-packages/overview-and-workflow.md)
- [Vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md)
- [Konfigurace chování NuGetu](../consume-packages/configuring-nuget-behavior.md)
- [Správa mezipaměti NuGetu](managing-the-nuget-cache.md)
