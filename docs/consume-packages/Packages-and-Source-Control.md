---
title: Balíčky NuGet a Správa zdrojového kódu
description: Informace o tom, jak zacházet s balíčky NuGet v rámci správy verzí a systémy správy zdrojového kódu a jak vynechat balíčky pomocí Gitu a TFVC.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: fa3ec6992002224c9fb56a53aee9096e6d2c6fbb
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901665"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Vynechávání balíčků NuGet v systémech správy zdrojového kódu

Vývojáři obvykle vynechává balíčky NuGet ze svých úložišť správy zdrojového kódu a využívají se místo toho, aby [obnovily](package-restore.md) závislosti projektu před sestavením.

Důvody pro spoléhání na obnovení balíčku zahrnují následující:

1. Distribuované systémy správy verzí, jako je git, obsahují úplné kopie každé verze každého souboru v úložišti. Binární soubory, které se často aktualizují, vedou k významným dispozici determinističtějšíům a prodlouží dobu potřebnou k naklonování úložiště.
1. Když jsou balíčky zahrnuté do úložiště, můžou vývojáři přidat odkazy přímo na obsah balíčku na disku místo na odkazování na balíčky přes NuGet, což může vést k pevně zakódovaným názvům cest v projektu.
1. Je obtížnější vyčistit řešení všech nepoužívaných složek balíčku, protože je potřeba zajistit, aby se neodstranily žádné složky balíčku, které se pořád používají.
1. Vynecháním balíčků zachováte čisté hranice vlastnictví mezi kódem a balíčky od ostatních, na kterých jste závislí. Mnoho balíčků NuGet se už ve vlastních úložištích správy zdrojových kódů udržuje.

I když je obnovení balíčku výchozím chováním nástroje NuGet, některé ruční práce jsou nezbytné k vynechání balíčků &mdash; konkrétně, `packages` ze složky v projektu &mdash; ze správy zdrojového kódu, jak je popsáno v tomto článku.

## <a name="omitting-packages-with-git"></a>Vynechávání balíčků v Gitu

Pomocí [souboru. gitignore](https://git-scm.com/docs/gitignore) můžete ignorovat balíčky NuGet ( `.nupkg` ) `packages` složku, a `project.assets.json` mimo jiné. Referenční informace naleznete v [ukázce `.gitignore` pro projekty sady Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Vynechávání balíčků s Správa verzí Team Foundation

> [!Note]
> Pokud je to možné, postupujte podle těchto pokynů, *než* přidáte projekt do správy zdrojových kódů. V opačném případě ručně odstraňte `packages` složku z úložiště a vraťte se změnami, než budete pokračovat.

Chcete-li zakázat integraci správy zdrojového kódu s TFVC pro vybrané soubory:

1. Ve složce řešení vytvořte složku s názvem `.nuget` (kde `.sln` je soubor).
    - Tip: v systému Windows Chcete-li vytvořit tuto složku v Průzkumníku Windows, použijte název `.nuget.` *s* koncovou tečkou.

1. V této složce vytvořte soubor s názvem `NuGet.Config` a otevřete ho pro úpravy.

1. Přidejte následující text jako minimální, kde nastavení [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) vydá aplikaci Visual Studio, aby přeskočila vše ve `packages` složce:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Pokud používáte TFS 2010 nebo starší, skryté `packages` složky v mapování pracovních prostorů.

1. Na serveru TFS 2012 nebo novějším nebo pomocí Visual Studio Team Services vytvořte `.tfignore` soubor, jak je popsáno v tématu [Přidání souborů na server](/vsts/tfvc/add-files-server?view=vsts#tfignore&preserve-view=true). V tomto souboru zahrňte níže uvedený obsah, který explicitně ignoruje změny `\packages` složky na úrovni úložiště a několik dalších zprostředkujících souborů. (Soubor můžete vytvořit v Průzkumníkovi Windows pomocí názvu a `.tfignore.` s koncovou tečkou, ale možná budete muset nejdřív zakázat možnost "Skrýt známé přípony souborů".):

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

1. Přidejte `NuGet.Config` a `.tfignore` do správy zdrojových kódů a vraťte se změnami.
