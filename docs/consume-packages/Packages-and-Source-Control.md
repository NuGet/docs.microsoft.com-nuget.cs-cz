---
title: Balíčky NuGet a Správa zdrojového kódu
description: Důležité informace týkající se má stát s balíčků NuGet v rámci správy verzí a zdroj řízení systémů a jak vynechejte balíčky s git a TFVC.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: bc2c6d5e9933f2f6103363a2e69fbb9b47f80ecf
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Vynechání balíčky NuGet ve zdrojových systémech ovládací prvek

Vývojáři obvykle vynechejte balíčky NuGet z jejich zdrojová ovládací prvek úložiště a místo toho spoléhají na [obnovení balíčků](package-restore.md) přeinstalovat projektu závislosti před sestavení.

Důvody pro spoléhat na obnovení balíčků zahrnují následující:

1. Distribuované verze řízení systémů, jako je například Git, zahrnují úplnou kopií každé verzi každého souboru v úložišti. Binární soubory, které jsou často aktualizované vést k výrazné tomu a prodlouží dobu potřebnou k klonovat úložiště.
1. Když balíčky jsou zahrnuty v úložišti, podléhají vývojáři přidáte odkazy na obsah balíčku přímo na disku než odkazující balíčky prostřednictvím balíčku NuGet, což může vést k názvy pevně cest v projektu.
1. Bude těžší Vyčistit řešení nepoužívá balíček složek, jako je třeba zajistit, že nemáte odstranit všechny složky balíčku stále používáno.
1. Díky vynechání balíčky, Udržovat čistou hranice vlastnictví až balíčky od ostatních, které závisí na kódu. Mnoho balíčky NuGet jsou zachována ve své vlastní zdrojová úložiště ovládací prvek již.

I když se obnovení balíčku je výchozí chování u balíčku NuGet, některé ručního nastavení je potřeba vynechejte balíčky&mdash;konkrétně, `packages` složku ve vašem projektu&mdash;od správy zdrojového kódu, jak je popsáno v tomto článku.

## <a name="omitting-packages-with-git"></a>Vynechání balíčky s Gitem

Použití [soubor .gitignore](https://git-scm.com/docs/gitignore) ignorovat balíčky NuGet (`.nupkg`) `packages` složku, a `project.assets.json`, mimo jiné. Odkaz, najdete v článku [ukázka `.gitignore` pro projekty v sadě Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Důležitou součástí `.gitignore` souboru jsou:

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Vynechání balíčky s verzí Team Foundation

> [!Note]
> Pokud je to možné postupovat podle těchto pokynů *před* přidání projektu do správy zdrojového kódu. Jinak, odstraňte ručně `packages` složky z úložiště a tato změna před pokračováním se změnami.

Postup při zakázání integrace ovládacích prvků zdrojového s TFVC pro vybrané soubory:

1. Vytvořte složku s názvem `.nuget` ve složce řešení (kde `.sln` soubor).
    - Tip: v systému Windows, k vytvoření této složky v Průzkumníku Windows, použijte název `.nuget.` *s* koncovou tečku.

1. V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete pro úpravy.

1. Přidejte následující text jako minimální, kde [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) nastavení dá pokyn chcete přeskočit všechno ve Visual Studio `packages` složky:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Pokud používáte sady TFS 2010 nebo starší, cloak `packages` složky mapování pracovního prostoru.

1. V sadě TFS 2012 nebo novější, nebo s Visual Studio Team Services, vytvořit `.tfignore` souboru, jak je popsáno na [AddFiles k serveru](/vsts/tfvc/add-files-server.md?view=vsts#tfignore). V tomto souboru zahrnout obsah níže explicitně Ignorovat změny `\packages` složky na úrovni úložiště a několik dalších zprostředkující soubory. (Soubor můžete vytvořit v Průzkumníku Windows pomocí názvu `.tfignore.` s koncovou tečku, ale může být nutné zakázat "Skrýt známému souboru rozšíření" možnost nejprve.):

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Přidat `NuGet.Config` a `.tfignore` ovládací prvek zdroje a změny se změnami.
