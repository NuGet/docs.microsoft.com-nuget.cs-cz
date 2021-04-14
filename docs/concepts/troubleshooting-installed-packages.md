---
title: Řešení potíží s nainstalovanými balíčky
description: Jak zjistit, který zdroj balíčku se použil pro jednotlivé balíčky
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387554"
---
# <a name="troubleshooting-installed-packages"></a>Řešení potíží s nainstalovanými balíčky

Někdy je možné, že budete chtít ověřit, ze kterého zdroje byl konkrétní balíček nainstalován. Tady je několik způsobů, jak můžete kontrolu provést.

> [!Note]
> Některé zdroje balíčků podporují koncept známý jako nadřazené zdroje. Například [Azure Artifacts nadřazené zdroje](/azure/devops/artifacts/concepts/upstream-sources). Klienti NuGet neznají, jestli balíček pochází z nadřazeného zdroje. Proto jakékoli protokolování zdroje balíčku zobrazí seznam nakonfigurovaného zdroje, nikoli nadřazeného zdroje.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>`.nupkg.metadata` soubor ve složce globálních balíčků

Při extrakci balíčku do složky *Global-Packages* `.nupkg.metadata` se zapíše soubor. Od 5.9.0 NuGet přidá NuGet zdroj balíčku. Níže najdete informace o mapování verzí NuGet na verze sady Visual Studio nebo .NET SDK. Například:

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> Pokud má složka *globálních balíčků* extrahovány balíčky před upgradováním na novější verzi nástrojů, které mají NuGet 5.9.0, bude `.nupkg.metadata` soubor verze 1 a nebude obsahovat zdroj balíčku. Můžete [Vymazat globální složku *balíčků*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) , abyste zajistili, že všechny balíčky budou obsahovat zdroj balíčku.

> [!Tip]
> NuGet zapisuje `.nupkg.metadata` soubor pouze do složky *Global-Packages* . Projekty používající `packages.config` použití složky balíčků řešení, která nevytváří `.nupkg.metadata` soubor.

## <a name="installed-package-log-message"></a>Nainstalovaná zpráva protokolu balíčku

Od 5.9.0 NuGet vyprodukuje výstup NuGet zdroj balíčku ve zprávě o obnovení, která informuje o instalaci balíčku. Například:

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Tato zpráva je ve výstupu normální/informativní podrobností. Visual Studio a `dotnet` CLI jsou ve výchozím nastavení na minimální úroveň podrobností, takže tato zpráva se ve výchozím nastavení nezobrazí. Nástroje rozhraní příkazového `msbuild` řádku a jsou `nuget` ve výchozím nastavení podrobností normální, takže se tato zpráva bude zobrazovat ve výchozím nastavení.

## <a name="http-log-message"></a>Zpráva protokolu HTTP

Pokud balíček není místně dostupný, buď ve složce *Global-Packages* , v záložní složce, nebo v místním zdroji souborů, NuGet ho stáhne z libovolného nakonfigurovaného zdroje balíčku přes HTTP. Požadavky HTTP a odpovědi jsou protokolovány v normální úrovni podrobností a měli byste vidět pouze jeden požadavek a odpověď na verzi balíčku. Například:

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Pokud byly soubory nedávno staženy, mohou být načteny z *mezipaměti protokolu HTTP* NuGet.

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

Formát adresy URL se může lišit pro různé implementace HTTP serveru NuGet a to, jestli implementuje protokol NuGet v2 nebo V3 HTTP.

Pokud `nuget.config` má definováno více zdrojů HTTP, zobrazí se pro každý soubor balíčku více požadavků `index.json` , jeden pro každý zdroj. Pro každou verzi balíčku bude ale k dispozici pouze jedno `nupkg` stažení.

## <a name="package-signature-log-message"></a>Zpráva protokolu podpisu balíčku

Pokud je stažený balíček podepsán, NuGet ověří podpis a zaprotokoluje následující zprávu podrobnou podrobnostem:

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Tato zpráva bude hlášena, zda byl balíček stažen ze zdroje balíčku HTTP nebo zkopírován z místního zdroje balíčku. Pokud je balíček už dostupný ve složce *Global-Packages* nebo v záložní složce, nebude se jednat o výstup.

> [!Important]
> Z důvodu [odebrání vztahu důvěryhodnosti NuGet CA pro certifikační autoritu](https://github.com/dotnet/announcements/issues/180) se u některých platforem v některých verzích NuGet a .NET SDK zakázalo podepsané ověření balíčku. Proto můžou mít stejné balíčky `PackageSignatureVerificationLog` protokoly, nebo můžou chybět protokoly v závislosti na tom, na které platformě se má obnovení spouštět a jakou verzi rozhraní .NET nebo NuGet používáte.

## <a name="nuget-version-map"></a>Mapa verze NuGet

Následující verze NuGet mají důležité změny týkající se protokolování zdroje balíčků:

|Verze NuGet|Verze sady Visual Studio|Verze sady .NET SDK|
|---|---|---|
|5.9.0 NuGet|Visual Studio 2019 16.9.0|5.0.200 SADY SDK PRO .NET 5|
