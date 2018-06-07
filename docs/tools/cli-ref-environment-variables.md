---
title: Proměnné prostředí NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro objekt environment variables nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 50bf8b469eda423db7665323823a2daf3f3aa41d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817070"
---
# <a name="nuget-cli-environment-variables"></a>Proměnné prostředí NuGet rozhraní příkazového řádku

Chování nuget.exe rozhraní příkazového řádku můžete nakonfigurovat přes počet proměnné prostředí, které ovlivňují nuget.exe na úrovni počítače, uživatele nebo zpracovat úrovně. Proměnné prostředí vždy přepisují nastavení v `NuGet.Config` soubory, umožňuje sestavit servery změňte příslušná nastavení beze změny žádné soubory.

Obecně platí, mají přednost před možností přímo na příkazovém řádku nebo v konfiguračních souborech NuGet, ale existuje pár výjimek, jako *FORCE_NUGET_EXE_INTERACTIVE*. Pokud zjistíte, že tento nuget.exe chová jinak mezi různými počítači, může být proměnné prostředí příčinu. Například Azure Web Apps Kudu (použitá při nasazení) má *NUGET_XMLDOC_MODE* nastavena na *přeskočit* zvýšit výkon obnovení balíčku a ušetřit místo na disku.

| Proměnná | Popis | Poznámky |
| --- | --- | --- |
| http_proxy | Server proxy protokolu HTTP, používat pro operace NuGet HTTP. | To by byl zadán jako `http://<username>:<password>@proxy.com`. |
| no_proxy | Nakonfiguruje domén obejít pomocí proxy serveru. | Zadaná jako domény oddělených čárkou (,). |
| EnableNuGetPackageRestore | Příznak pro Pokud NuGet by měl implicitně udělení souhlasu Pokud to vyžaduje balíček na obnovení. | Zadaný příznak je považován za *true* nebo *1*, žádné jiné hodnoty, které jsou považovány za příznak není nastavena. |
| NUGET_EXE_NO_PROMPT | Zabraňuje exe pro výzvu k zadání pověření. | Libovolná hodnota s výjimkou hodnotu null nebo prázdný řetězec, budou považovány za příznak sady nebo hodnotu true. |
| FORCE_NUGET_EXE_INTERACTIVE | Proměnné prostředí globální vynutit interaktivním režimu. | Libovolná hodnota s výjimkou hodnotu null nebo prázdný řetězec, budou považovány za příznak sady nebo hodnotu true. |
| NUGET_PACKAGES | Cestu pro použití u *globální balíčky* složky, jak je popsáno na [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Zadat jako absolutní cestu. |
| NUGET_FALLBACK_PACKAGES | Globální záložní balíčky složek. | Absolutní cesty ke složce zadat oddělených středníkem (;). |
| NUGET_HTTP_CACHE_PATH | Cestu pro použití u *http mezipaměti* složky, jak je popsáno na [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Zadat jako absolutní cestu. |
| NUGET_PERSIST_DG | Příznak, označuje, zda má nastavit jako trvalý, dg soubory (data shromážděná z nástroje MSBuild). | Zadaný jako *true* nebo *false* (výchozí), pokud není nastavena NUGET_PERSIST_DG_PATH se uloží do dočasného adresáře (NuGetScratch složka v aktuálním adresáři temp prostředí). |
| NUGET_PERSIST_DG_PATH | Cesta k zachování dg soubory. | Určený jako absolutní cesta, tato možnost je pouze použité případě *NUGET_PERSIST_DG* je nastaven na hodnotu true. |
| NUGET_RESTORE_MSBUILD_ARGS | Nastaví další argumenty MSBuild. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Nastaví MSBuild podrobností protokolu. | Výchozí hodnota je *quiet* ("nebo v: q"). Možné hodnoty *q [uiet]*, *m [den]*, *n [ormální]*, *d [podrobné]*, a *diag [nostic]*. |
| NUGET_SHOW_STACK | Určuje, zda má být zobrazena úplná výjimka (včetně trasování zásobníku) pro uživatele. | Zadaný jako *true* nebo *false* (výchozí). |
| NUGET_XMLDOC_MODE | Určuje způsob zpracování extrakce souborů dokumentace XML sestavení. | Jsou podporované režimy *přeskočit* (není extrahovat soubory dokumentace XML), *komprimovat* (ukládat soubory doc XML jako archivu zip) nebo *žádné* (výchozí, považovat za regular souborů dokumentace XML soubory). |
