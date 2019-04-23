---
title: Proměnné prostředí rozhraní příkazového řádku NuGet
description: Referenční informace pro objekt environment variables nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: ac1bf2b65ab6ec4e8cf864810181fc661236262a
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931979"
---
# <a name="nuget-cli-environment-variables"></a>Proměnné prostředí rozhraní příkazového řádku NuGet

Chování programu nuget.exe rozhraní příkazového řádku je možné nakonfigurovat procházet celou řadou proměnné prostředí, které ovlivňují nuget.exe pro celý počítač, uživatele nebo zpracovat úrovně. Proměnné prostředí vždy přepíší všechna nastavení v `NuGet.Config` soubory, což serverů sestavení ke změňte příslušná nastavení beze změny všech souborů.

Obecně platí, mají přednost před možností přímo na příkazovém řádku nebo v konfiguračních souborech na NuGet, ale existuje pár výjimek, jako *FORCE_NUGET_EXE_INTERACTIVE*. Pokud zjistíte, že tento nuget.exe chová odlišně mezi různými počítači, proměnné prostředí může být příčinou. Azure Web Apps Kudu (používá se během nasazení) má například *NUGET_XMLDOC_MODE* nastavena na *přeskočit* zrychlit výkonu obnovení balíčku a ušetřit místo na disku.

Rozhraní příkazového řádku NuGet používá ke čtení souborů projektu MSBuild. Všechny proměnné prostředí jsou k dispozici jako [vlastnosti](/visualstudio/msbuild/msbuild-command-line-reference) během vyhodnocování MSBuild.
Seznam vlastností, které jsou popsány v [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md#restore-properties) můžete také nastavit jako proměnné prostředí.

| Proměnná | Popis | Poznámky |
| --- | --- | --- |
| http_proxy | Proxy server HTTP pro operace NuGet HTTP. | To by se zadal jako `http://<username>:<password>@proxy.com`. |
| no_proxy | Nakonfiguruje domén obejít pomocí proxy serveru. | Zadaný jako domén oddělených čárkou (,). |
| EnableNuGetPackageRestore | Příznak pro Pokud NuGet by měl implicitně udělit souhlas Pokud, který vyžaduje balíček na obnovení. | Určený příznak je považován za *true* nebo *1*, jakákoli jiná hodnota, které jsou považovány za příznak není nastavený. |
| NUGET_EXE_NO_PROMPT | Zabraňuje exe pro vás vyzve k zadání přihlašovacích údajů. | Libovolná hodnota s výjimkou hodnotu null nebo prázdný řetězec bude zacházeno jako s tímto příznakem sadu nebo hodnotu true. |
| FORCE_NUGET_EXE_INTERACTIVE | Proměnná prostředí globální přinutit interaktivním režimu. | Libovolná hodnota s výjimkou hodnotu null nebo prázdný řetězec bude zacházeno jako s tímto příznakem sadu nebo hodnotu true. |
| NUGET_PACKAGES | Cesta pro *global-packages* složky, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Zadaný jako absolutní cestu. |
| NUGET_FALLBACK_PACKAGES | Složky globálních balíčků pro použití náhradní lokality. | Absolutní cesty ke složce zadat oddělených středníkem (;). |
| NUGET_HTTP_CACHE_PATH | Cesta pro *http-cache* složky, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Zadaný jako absolutní cestu. |
| NUGET_PERSIST_DG | Příznak označující, jestli by měl nastavit jako trvalý, distribuční skupině souborů (data shromážděná z MSBuild). | Zadaný jako *true* nebo *false* (výchozí), pokud není nastavený NUGET_PERSIST_DG_PATH se uloží do dočasného adresáře (NuGetScratch složka v aktuálním adresáři temp prostředí). |
| NUGET_PERSIST_DG_PATH | Cesta k trvalému ukládání souborů distribuční skupině. | Zadaný jako absolutní cestu, tato možnost je pouze použité při *NUGET_PERSIST_DG* je nastavena na hodnotu true. |
| NUGET_RESTORE_MSBUILD_ARGS | Nastaví další argumenty nástroje MSBuild. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Nastaví úroveň podrobností protokolu MSBuild. | Výchozí hodnota je *quiet* ("/ v: q"). Možné hodnoty *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etailed]*, a *diag [nostic]*. |
| NUGET_SHOW_STACK | Určuje, zda má být zobrazen úplných informacích o výjimce (včetně trasování zásobníku) pro uživatele. | Zadaný jako *true* nebo *false* (výchozí). |
| NUGET_XMLDOC_MODE | Určuje, jak by měl být zpracována extrakce souborů dokumentace XML sestavení. | Jsou podporované režimy *přeskočit* (ne extrahovat soubory dokumentace XML), *komprimovat* (Uložit soubory dokumentu XML jako archiv zip) nebo *žádný* (výchozí, považovat za standardní soubory XML doc soubory). |
| NUGET_CERT_REVOCATION_MODE | Určuje, jak zkontrolovat stav odvolání certifikátu použitého k podepsání balíčku, se provádí při instalaci nebo obnovit podepsaný balíček. Pokud není nastavený, výchozí hodnota je `online`.| Možné hodnoty *online* (výchozí), *offline*.  Související s [NU3028](../reference/errors-and-warnings/NU3028.md) |

