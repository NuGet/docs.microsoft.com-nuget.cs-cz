---
title: Balíčky NuGet a směřované zdroje
description: Důležité informace o tom, jak zacházet s balíčky NuGet v rámci správy verzí a systémů správy zdrojového kódu a jak vynechat balíčky s git a TFVC.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69019983"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Vynechání balíčků NuGet v systémech správy zdrojového kódu

Vývojáři obvykle vynechat Balíčky NuGet z jejich úložiště správy zdrojového kódu a místo toho spoléhat na [obnovení balíčku](package-restore.md) přeinstalovat závislosti projektu před sestavením.

Důvody pro spoléhání se na obnovení balíčku patří následující:

1. Distribuované systémy správy verzí, jako je Git, obsahují úplné kopie všech verzí každého souboru v úložišti. Binární soubory, které jsou často aktualizovány vést k významné nafouknutí a prodlužuje čas potřebný ke klonování úložiště.
1. Pokud jsou balíčky zahrnuty v úložišti, vývojáři mohou přidat odkazy přímo na obsah balíčku na disku, nikoli odkazování na balíčky prostřednictvím NuGet, což může vést k pevně zakódované názvy cest v projektu.
1. Je stále těžší vyčistit vaše řešení všech nepoužívaných složek balíčků, protože je třeba zajistit, že neodstraníte žádné složky balíčků, které jsou stále používány.
1. Vynecháním balíčků udržujete čisté hranice vlastnictví mezi kódem a balíčky od ostatních, na kterých jste závislí. Mnoho balíčků NuGet jsou udržovány ve svých vlastních úložištích správy zdrojového kódu již.

Přestože obnovení balíčku je výchozí chování s NuGet, některé&mdash;ruční práce `packages` je nutné&mdash;vynechat balíčky konkrétně složku v projektu ze správy zdrojového kódu, jak je popsáno v tomto článku.

## <a name="omitting-packages-with-git"></a>Vynechání balíčků s Gitem

Pomocí [souboru .gitignore](https://git-scm.com/docs/gitignore) můžete mimo`.nupkg`jiné `packages` ignorovat `project.assets.json`balíčky NuGet ( ) a , mimo jiné. Další informace naleznete v [ukázce `.gitignore` pro projekty sady Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Důležité části souboru `.gitignore` jsou:

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Vynechání balíčků se spouštěním verzí Team Foundation

> [!Note]
> Před *přidáním* projektu do správy zdrojového kódu postupujte podle těchto pokynů, pokud je to možné. V opačném případě `packages` ručně odstraňte složku z úložiště a před pokračováním tuto změnu sezměna odevzdejte se změnami.

Zakázání integrace správy zdrojového kódu s TFVC pro vybrané soubory:

1. Vytvořte složku `.nuget` volanou ve `.sln` složce řešení (kde je soubor).
    - Tip: V systému Windows, chcete-li vytvořit `.nuget.` tuto složku v Průzkumníkovi Windows, použijte název *s* koncovou tečkou.

1. V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete jej pro úpravy.

1. Přidejte jako minimum následující text, kde nastavení [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) instruuje Visual Studio přeskočit vše ve `packages` složce:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Pokud používáte TFS 2010 nebo `packages` starší, maskovat složku v mapování pracovního prostoru.

1. Na TFS 2012 nebo novější nebo pomocí Visual `.tfignore` Studio Team Services vytvořte soubor, jak je popsáno v části [Přidat soubory na server](/vsts/tfvc/add-files-server?view=vsts#tfignore). Do tohoto souboru zahrňte níže uvedený `\packages` obsah, abyste explicitně ignorovali změny složky na úrovni úložiště a několik dalších zprostředkujících souborů. (Soubor můžete vytvořit v Průzkumníkovi Windows `.tfignore.` pomocí názvu a s koncovou tečkou, ale možná budete muset nejprve zakázat možnost Skrýt známé přípony souborů.):

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. `NuGet.Config` Přidejte `.tfignore` a do správy zdrojového kódu a vrácení změn se změnami.
