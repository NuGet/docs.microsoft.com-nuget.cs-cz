---
title: Balíčky NuGet a Správa zdrojového kódu
description: Důležité informace o tom, jak nakládat s balíčky NuGet v rámci systémy správy verzí ovládacího prvku a zdroje a jak chcete vynechat, nechte balíčky s git a TFVC.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: ef4c45451cc52eb08dc627f8442c48e853d8ceaf
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324731"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Vynechání balíčky NuGet v systémy správy zdrojového kódu

Vývojáři obvykle vynechat balíčků NuGet z jejich úložiště správy zdrojového kódu a místo toho spoléhají na [obnovení balíčků](package-restore.md) přeinstalovat závislosti projektu před během sestavení.

Důvody pro spoléhání se na obnovení balíčků, patří:

1. Systémy správy distribuovaných verzí, jako je Git, zahrnout úplné kopie každé verze každého souboru v rámci tohoto úložiště. Binární soubory, které se často aktualizují vést k výrazné determinističtější a prodlouží čas potřebný ke klonování úložiště.
1. Při balíčky jsou zahrnuty v úložišti, mohou vývojáři přidat odkazy přímo na obsah balíčku na disku než odkazující balíčků prostřednictvím balíčku NuGet, což může vést k názvům pevně zakódované cesty v projektu.
1. Bude obtížnější Vyčistit řešení složek nepoužívaných balíčků, jako je nutné se ujistit, že nechcete odstranit všechny složky balíčku stále používán.
1. Vynecháním balíčky udržovat čisté hranice vlastnictví mezi kódu a balíčků od ostatních, které závisí na aplikaci. Mnoho balíčky NuGet jsou zachována ve své vlastní úložiště správy zdrojového kódu už.

Výchozí chování nuget sice obnovit balíček úkony ruční je nezbytné vynechejte balíčky&mdash;totiž, `packages` složku ve vašem projektu&mdash;ze správy zdrojového kódu, jak je popsáno v tomto článku.

## <a name="omitting-packages-with-git"></a>Vynechání balíčky s Gitem

Použití [soubor .gitignore](https://git-scm.com/docs/gitignore) ignorovat balíčky NuGet (`.nupkg`) `packages` složky, a `project.assets.json`, mimo jiné. Odkaz, najdete v článku [ukázka `.gitignore` pro projekty aplikace Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Důležité části `.gitignore` souboru jsou:

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Vynechání balíčky s Team Foundation – správa verzí

> [!Note]
> Pokud je to možné postupujte podle těchto pokynů *před* přidání projektu do správy zdrojového kódu. V opačném případě odstraňte ručně `packages` složku z vašeho úložiště a vrácení se změnami tuto změnu, než budete pokračovat.

Chcete-li zakázat integrace správy zdrojového kódu s TFVC pro vybrané soubory:

1. Vytvořte složku s názvem `.nuget` ve složce řešení (kde `.sln` soubor).
    - Tip: na Windows, k vytvoření této složky v Průzkumníku Windows, použijte název `.nuget.` *s* koncovou tečku.

1. V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete pro úpravy.

1. Přidejte následující text jako minimum, kde [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) nastavení dá pokyn Přeskočit vše v sadě Visual Studio `packages` složky:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Pokud používáte TFS 2010 nebo starší, skrytí `packages` složky v mapování pracovního prostoru.

1. Na serveru TFS 2012 nebo novější, nebo službou Visual Studio Team Services, vytvořit `.tfignore` sdílené, jak je popsáno na [přidat soubory serveru](/vsts/tfvc/add-files-server?view=vsts#tfignore). V tomto souboru zahrnují následující explicitně Ignorovat změny obsah `\packages` složky na úrovni úložiště a několik dalších zprostředkujících souborů. (Tento soubor můžete vytvořit v Průzkumníku Windows pomocí názvu `.tfignore.` s koncovou tečku, ale může být nutné zakázat "Skrýt příponu souborů známých" možnost nejprve.):

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

1. Přidat `NuGet.Config` a `.tfignore` do správy zdrojového kódu a vrácení zpět se změnami.
