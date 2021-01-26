---
title: Poznámky k verzi NuGet 2.7.2
description: Poznámky k verzi pro NuGet 2.7.2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776781"
---
# <a name="nuget-272-release-notes"></a>Poznámky k verzi NuGet 2.7.2

Poznámky k verzi [NuGet 2.7.1](../release-notes/nuget-2.7.1.md)  |  Zpráva k [vydání verze NuGet 2,8](../release-notes/nuget-2.8.md)

2.7.2 NuGet byl vydaný 11. listopadu 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Opravy a funkce chyb zajímavosti

### <a name="license-text"></a>Text licence
V některých případech společnost Microsoft zahrnula balíčky NuGet pro několik oblíbených open source knihoven jako součást výchozích šablon pro projekty webových aplikací v aplikaci Visual Studio. jQuery je pravděpodobně nejpravděpodobnějším známým příkladem tohoto typu knihovny. Vzhledem k tomu, že smlouva o podpoře je přidružená k součástem, které jsou dodávány společně s produktem, obsahuje soubor skriptu balíčku jiný text licence, než je soubor skriptu nalezený ve stejném balíčku ve veřejné galerii nuget.org. Tento rozdíl v textu může zabránit tomu, aby aktualizace balíčků mohly pokračovat v důsledku různých textových bloků s různými licencemi, které způsobí, že soubory skriptu mají různé hodnoty hash obsahu (a proto se mají v rámci projektu zpracovat jako upravené).

Pro zmírnění tohoto problému umožňuje 2.7.2 NuGet, aby autor skriptu zahrnoval textový blok s licenčními podmínkami v rámci speciálně označeného oddílu, který vypadá takto.

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

Při aktualizaci balíčků se soubory obsahu, které obsahují tento blok, NuGet nefaktoruje obsah bloku do porovnání s verzí v galerii NuGet a může proto odstranit a aktualizovat soubor obsahu, a to i tak, jak odpovídá původní kopii.

Tento blok je identifikovaný textem "NUGET: BEGIN LICENSE TEXT" a "NUGET: END LICENSE TEXT", který se vyskytuje kdekoli na začátku a na konci řádku.  Neexistují žádné další požadavky na formátování, což umožňuje použití této funkce v jakémkoli typu textového souboru bez ohledu na jazyk.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Přidání přesměrování vazby pro sestavení bez architektury
Pro sestavení, která jsou součástí .NET Framework, NuGet přeskočí Přidání přesměrování vazby do konfiguračního souboru aplikace při aktualizaci balíčku. Tato oprava řeší regresi v NuGet 2,7, kdy se pro některá sestavení nepřidaly přesměrování vazby, i když tato sestavení nejsou považována za součást .NET Framework. NuGet 2.7.2 obnoví předchozí chování NuGet 2,5 a 2,6 a přidá přesměrování vazby.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalace přenosných knihoven pomocí nainstalovaných nástrojů Xamarin
Když jsou vývojové nástroje Xamarin nainstalovány v počítači, upraví data konfigurace podporovaných rozhraní tak, aby určovala kompatibilitu mezi stávajícími kombinacemi cílového rozhraní a architekturou Xamarin. S verzí 2.7.2 nyní NuGet ví o těchto implicitních pravidlech kompatibility, a proto usnadňuje vývojářům cílené platformy Xamarin, aby nainstalovaly přenosné knihovny, které jsou kompatibilní s Xamarin, ale nejsou explicitně označené jako v metadatech balíčku.

### <a name="machine-wide-configuration-settings-honored"></a>Nastavení konfigurace na úrovni počítače bylo dodrženo.
Pokud používáte hierarchické Nuget.Config soubory, nedodržuje se klíč repositoryPath pro Nuget.Config soubory nejbližší kořenovému adresáři řešení. V Visual Studio 2013 NuGet nainstaluje vlastní soubor Nuget.Config v umístění% Složka ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config, aby se přidal zdroj balíčku Microsoft a .NET. Výsledkem je, že při práci s použitím vlastního repositoryPath v řešení bylo možné odstranit Nuget.Config na úrovni počítače – což také způsobilo odebrání zdroje balíčků "Microsoft a .NET". 2.7.2 NuGet teď při použití hierarchických Nuget.Configch souborů respektuje pravidla priority pro repositoryPath.

## <a name="all-changes"></a>Všechny změny
Úplný seznam pracovních položek opravených ve 2.7.2 NuGet najdete v [přehledu problémů NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
