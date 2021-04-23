---
title: Využívání balíčků ze ověřených informačních kanálů
description: Využívání balíčků ze ověřených informačních kanálů ve všech scénářích klientů NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901509"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Využívání balíčků ze ověřených informačních kanálů

Kromě [veřejného informačního kanálu](https://api.nuget.org/v3/index.json)NuGet.org mají klienti NuGet možnost pracovat s kanály souborů a soukromými kanály http.


K ověřování pomocí privátních informačních kanálů http jsou k diskaždé dva přístupy:

* Přidat pověření v [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Proveďte ověření pomocí jednoho z mnoha modelů rozšiřitelnosti v závislosti na použitém klientovi.

## <a name="nuget-clients-authentication-extensibility"></a>Rozšiřitelnost ověřování klientů NuGet

U různých klientů NuGet zodpovídá poskytovatel privátního informačního kanálu za ověřování.
Všichni klienti NuGet mají metody rozšíření, které to podporují. Jsou to buď rozšíření sady Visual Studio, nebo modul plug-in, který může komunikovat s NuGet za účelem načtení přihlašovacích údajů.

### <a name="visual-studio"></a>Visual Studio

V aplikaci Visual Studio NuGet zveřejňuje rozhraní, které poskytovatelé kanálu můžou implementovat a poskytnout svým zákazníkům. Další podrobnosti najdete v dokumentaci o [tom, jak vytvořit poskytovatele pověření sady Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>K dispozici poskytovatelé pověření NuGet pro Visual Studio

Do sady Visual Studio je integrovaný poskytovatel přihlašovacích údajů, který podporuje Azure DevOps.


K dispozici jsou poskytovatelé přihlašovacích údajů pro modul plug-in:

* [Poskytovatel pověření MyGet pro Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Když `nuget.exe` potřebují přihlašovací údaje k ověřování pomocí informačního kanálu, vyhledají je následující:

1. Vyhledejte přihlašovací údaje v `NuGet.config` souborech.
1. Použít poskytovatele pověření modulu plug-in v2
1. Použít poskytovatele přihlašovacích údajů modulu plug-in v1
1. NuGet pak vyzve uživatele k zadání přihlašovacích údajů na příkazovém řádku.

#### <a name="nugetexe-and-v2-credential-providers"></a>Poskytovatelé přihlašovacích údajů nuget.exe a v2

Ve verzi `4.8` NuGet definoval nový mechanismus ověřovacího modulu plug-in (dále jen jako poskytovatelé přihlašovacích údajů v2).
Pro instalaci a zjišťování těchto zprostředkovatelů se podívejte na [moduly plug-in NuGet pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>Poskytovatelé přihlašovacích údajů pro nuget.exe a v1

Ve verzi `3.3` NuGet představil první verzi modulů plug-in pro ověřování.
Pro instalaci a zjišťování těchto zprostředkovatelů se odkazují na [nuget.exe poskytovatelé přihlašovacích údajů](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery) .

#### <a name="available-credential-providers-for-nugetexe"></a>K dispozici poskytovatelé přihlašovacích údajů pro nuget.exe

* Poskytovatelé [přihlašovacích údajů služby Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) nebo [Poskytovatel pověření Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

V sadě Visual Studio 2017 verze 15,9 a novější je poskytovatel přihlašovacích údajů Azure DevOps zahrnutý v sadě Visual Studio.
Při `nuget.exe` použití nástroje MSBuild z konkrétní sady nástrojů sady Visual Studio bude modul plug-in zjištěn automaticky.

### <a name="dotnetexe"></a>dotnet.exe

Když `dotnet.exe` potřebují přihlašovací údaje k ověřování pomocí informačního kanálu, vyhledají je následující:

1. Vyhledejte přihlašovací údaje v `NuGet.config` souborech.
1. Použít poskytovatele pověření modulu plug-in v2

Ve výchozím nastavení není `dotnet.exe` interaktivní, takže možná budete muset předat příznak pro `--interactive` získání nástroje k blokování ověřování.

#### <a name="dotnetexe-and-v2-credential-providers"></a>Poskytovatelé přihlašovacích údajů dotnet.exe a v2

Ve verzi `2.2.100` sady SDK sada NuGet definovala mechanismus ověřovacího modulu plug-in, který funguje ve všech klientech.
Pro instalaci a zjišťování těchto zprostředkovatelů se podívejte na [moduly plug-in NuGet pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>K dispozici poskytovatelé přihlašovacích údajů pro dotnet.exe

* [Poskytovatel pověření Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

Když `MSBuild.exe` potřebují přihlašovací údaje k ověřování pomocí informačního kanálu, vyhledají je následující:

1. Hledat přihlašovací údaje v `NuGet.config` souborech
1. Použít poskytovatele pověření modulu plug-in v2

Ve výchozím nastavení není `MSBuild.exe` interaktivní, takže možná budete muset nastavit `/p:NuGetInteractive=true` vlastnost tak, aby byl nástroj blokovaný pro ověřování.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Poskytovatelé přihlašovacích údajů MSBuild.exe a v2

V sadě Visual Studio 2019 Update 9, NuGet definoval mechanismus ověřovacího modulu plug-in, který funguje ve všech klientech.
Pro instalaci a zjišťování těchto zprostředkovatelů se podívejte na [moduly plug-in NuGet pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>K dispozici poskytovatelé přihlašovacích údajů pro MSBuild.exe

* [Poskytovatel pověření Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

V sadě Visual Studio 2017 Update 9 a novějších je poskytovatel přihlašovacích údajů Azure DevOps zahrnutý v sadě Visual Studio. Nejsou nutné žádné další kroky.
