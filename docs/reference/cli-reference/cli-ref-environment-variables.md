---
title: Proměnné prostředí NuGet CLI
description: Reference pro proměnné prostředí nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a688382420633916e81a000ba6095ff83e036cf9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779382"
---
# <a name="nuget-cli-environment-variables"></a>Proměnné prostředí NuGet CLI

Chování rozhraní příkazového řádku nuget.exe lze nakonfigurovat prostřednictvím řady proměnných prostředí, které mají vliv na nuget.exe na úrovni počítače, uživatele nebo procesu. Proměnné prostředí vždy přepíší všechna nastavení v `NuGet.Config` souborech, což umožňuje serverům sestavení změnit odpovídající nastavení bez nutnosti měnit soubory.

Obecně platí, že možnosti zadané přímo na příkazovém řádku nebo v konfiguračních souborech NuGet mají přednost, ale existuje několik výjimek, například *FORCE_NUGET_EXE_INTERACTIVE*. Zjistíte-li, že nuget.exe se chová jinak než u různých počítačů, může to být způsobeno proměnnou prostředí. Například Azure Web Apps Kudu (použitý během nasazení) má *NUGET_XMLDOC_MODE* nastavené na *Přeskočit* , aby se urychlilo zrychlení obnovování balíčků a ušetřilo místo na disku.

NuGet CLI používá MSBuild ke čtení souborů projektu. Všechny proměnné prostředí jsou k dispozici jako [vlastnosti](/visualstudio/msbuild/msbuild-command-line-reference) během vyhodnocení nástroje MSBuild.
Seznam vlastností dokumentovaných v [sadě NuGet Pack a obnovení jako cíle nástroje MSBuild](../msbuild-targets.md#restore-properties) lze nastavit také jako proměnné prostředí.

| Proměnná | Popis | Poznámky |
| --- | --- | --- |
| http_proxy | Proxy server http, který se používá pro operace HTTP NuGet. | To bude určeno jako `http://<username>:<password>@proxy.com` . |
| no_proxy | Nakonfiguruje domény tak, aby se nepoužívaly při použití proxy serveru. | Zadáno jako domény oddělené čárkou (,). |
| EnableNuGetPackageRestore | Příznak, pokud má NuGet implicitně udělit souhlas, pokud to vyžaduje balíček při obnovení. | Zadaný příznak se považuje za *true* nebo *1*, ostatní hodnota se považuje za příznak, že není nastavená. |
| NUGET_EXE_NO_PROMPT | Zabraňuje souboru exe zobrazovat výzvy k zadání přihlašovacích údajů. | Jakákoli hodnota s výjimkou null nebo prázdného řetězce bude považována za nastavenou příznakem/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Globální proměnná prostředí pro vynucení interaktivního režimu. | Jakákoli hodnota s výjimkou null nebo prázdného řetězce bude považována za nastavenou příznakem/true. |
| NUGET_PACKAGES | Cesta, která se má použít pro složku *Global-Packages* , jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Zadáno jako absolutní cesta. |
| NUGET_FALLBACK_PACKAGES | Složky globálních záložních balíčků. | Absolutní cesty ke složkám oddělené středníkem (;). |
| NUGET_HTTP_CACHE_PATH | Cesta, která se má použít pro složku *mezipaměti HTTP* , jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Zadáno jako absolutní cesta. |
| NUGET_PERSIST_DG | Příznak označující, zda se mají zachovat soubory DG (data shromážděná z MSBuildu). | Zadáno jako *true* nebo *false* (výchozí), pokud NUGET_PERSIST_DG_PATH nenastavena, budou uloženy do dočasného adresáře (složka NuGetScratch v aktuálním dočasném adresáři prostředí). |
| NUGET_PERSIST_DG_PATH | Cesta k trvalému distribučnímu souboru. | Zadáno jako absolutní cesta, tato možnost se používá pouze v případě, *NUGET_PERSIST_DG* je nastavena na hodnotu true. |
| NUGET_RESTORE_MSBUILD_ARGS | Nastaví další argumenty MSBuild. | Předejte argumenty stejné jako způsob, jak byste je předávali msbuild.exe. Příkladem nastavení vlastnosti projektu foo z příkazového řádku na řádek hodnoty by byl/p: foo = bar. |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Nastaví podrobnost protokolu MSBuild. | Výchozí hodnota je *tichá* ("/v: q"). Možné hodnoty *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etailed]* a *diag [nostic]*. |
| NUGET_SHOW_STACK | Určuje, zda má uživatel zobrazit úplnou výjimku (včetně trasování zásobníku). | Zadáno jako *true* nebo *false* (výchozí). |
| NUGET_XMLDOC_MODE | Určuje, jak by měla být zpracována extrakce souborů dokumentace XML pro sestavení. | Podporované režimy jsou *přeskočeny* (soubory dokumentace XML nejsou extrahovány), *komprimují* (ukládají soubory dokumentů XML jako archiv zip) nebo *žádné* (výchozí, považujte soubory doc XML za běžné soubory). |
| NUGET_CERT_REVOCATION_MODE | Určuje, jakým způsobem má být při instalaci nebo obnovení podepsaného balíčku proveden pokus o kontrolu stavu odvolání certifikátu použitého k podepsání balíčku. Pokud není nastaveno, výchozí hodnota je `online` .| Možné hodnoty jsou *online* (výchozí), *offline*.  Související s [NU3028](../errors-and-warnings/NU3028.md) |

