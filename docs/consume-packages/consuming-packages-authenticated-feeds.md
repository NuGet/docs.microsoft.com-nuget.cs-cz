---
title: Spotřebovávající balíky z ověřených informačních kanálů
description: Spotřebovávající balíčky z ověřených informačních kanálů ve všech klientských scénářích NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231789"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Spotřebovávající balíky z ověřených informačních kanálů

Kromě nuget.org [veřejný zdroj](https://api.nuget.org/v3/index.json), NuGet klienti mají možnost pracovat s kanály souborů a soukromé http kanály.


Chcete-li ověřit pomocí soukromých http kanály, 2 přístupy jsou:

* Přidání pověření do [souboru NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Ověřte pomocí jednoho z mnoha modelů rozšiřitelnosti v závislosti na použitém klientovi.

## <a name="nuget-clients-authentication-extensibility"></a>Rozšiřitelnost ověřování klientů NuGet

Pro různé klienty NuGet soukromého poskytovatele informačního kanálu sám je zodpovědný za ověřování.
Všechny klienty NuGet mají metody rozšiřitelnosti pro podporu tohoto. Jedná se buď rozšíření sady Visual Studio nebo plugin, který může komunikovat s NuGet načíst pověření.

### <a name="visual-studio"></a>Visual Studio

V sadě Visual Studio NuGet zveřejňuje rozhraní, které zprostředkovatelé informačního kanálu můžete implementovat a poskytnout svým zákazníkům. Další podrobnosti naleznete v dokumentaci [k vytvoření zprostředkovatele pověření sady Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>K dispozici zprostředkovatelé pověření NuGet pro Visual Studio

V sadě Visual Studio je integrovaný poskytovatel přihlašovacích údajů, který podporuje Azure DevOps.


Mezi dostupné poskytovatele přihlašovacích údajů modulu plug-in patří:

* [MyGet zprostředkovatele pověření pro Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Když `nuget.exe` potřebuje pověření k ověření pomocí informačního kanálu, hledá je následujícím způsobem:

1. Vyhledejte pověření `NuGet.config` v souborech.
1. Použití zprostředkovatelů přihlašovacích údajů modulu plug-in V2
1. Použití zprostředkovatelů přihlašovacích údajů modulu plug-in V1
1. NuGet pak vyzve uživatele k zadání pověření na příkazovém řádku.

#### <a name="nugetexe-and-v2-credential-providers"></a>zprostředkovatelé pověření nuget.exe a V2

Ve `4.8` verzi NuGet definoval nový mechanismus modulu plug-in ověřování, dále jen zprostředkovatelé pověření V2.
Instalace a zjišťování těchto poskytovatelů naleznete [v nugetských zásuvných modulech pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>zprostředkovatelé pověření nuget.exe a V1

Ve `3.3` verzi NuGet představil první verzi ověřovacích pluginů.
Instalace a zjišťování těchto poskytovatelů naleznete na [nuget.exe zprostředkovatele pověření](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>K dispozici zprostředkovatelé pověření pro nuget.exe

* [Zprostředkovatelé přihlašovacích údajů Azure DevOps V2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) nebo [zprostředkovatel evitorů artefaktů Azure](https://github.com/microsoft/artifacts-credprovider)

S Visual Studio 2017 verze 15.9 a novější, Azure DevOps poskytovatel přihlašovacích údajů je součástí Sady Visual Studio.
Pokud `nuget.exe` používá MSBuild z této konkrétní sady nástrojů Sady visual studio, pak plugin bude zjištěna automaticky.

### <a name="dotnetexe"></a>dotnet.exe

Když `dotnet.exe` potřebuje pověření k ověření pomocí informačního kanálu, hledá je následujícím způsobem:

1. Vyhledejte pověření `NuGet.config` v souborech.
1. Použití zprostředkovatelů přihlašovacích údajů modulu plug-in V2

Ve `dotnet.exe` výchozím nastavení není interaktivní, takže `--interactive` možná budete muset předat příznak, aby se nástroj blokovat pro ověřování.

#### <a name="dotnetexe-and-v2-credential-providers"></a>Zprostředkovatelé pověření dotnet.exe a V2

Ve `2.2.100` verzi sady SDK definuje nuget mechanismus modulu plug-in ověřování, který funguje ve všech klientech.
Instalace a zjišťování těchto poskytovatelů naleznete [v nugetských zásuvných modulech pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Dostupní zprostředkovatelé pověření pro program dotnet.exe

* [Zprostředkovatel přihlašovacích údajů artefaktů Azure](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>Soubor MSBuild.exe

Když `MSBuild.exe` potřebuje pověření k ověření pomocí informačního kanálu, hledá je následujícím způsobem:

1. Hledání přihlašovacích `NuGet.config` údajů v souborech
1. Použití zprostředkovatelů přihlašovacích údajů modulu plug-in V2

Ve `MSBuild.exe` výchozím nastavení není interaktivní, takže `/p:NuGetInteractive=true` možná budete muset nastavit vlastnost, aby se nástroj blokovat pro ověřování.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Zprostředkovatelé pověření MSBuild.exe a V2

V aktualizaci Visual Studio 2019 Update 9, NuGet definován mechanismus modulu plug-in ověřování, který funguje ve všech klientech.
Instalace a zjišťování těchto poskytovatelů naleznete [v nugetských zásuvných modulech pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Dostupní zprostředkovatelé pověření pro soubor MSBuild.exe

* [Zprostředkovatel přihlašovacích údajů artefaktů Azure](https://github.com/microsoft/artifacts-credprovider)

S Visual Studio 2017 Update 9 a novější, Azure DevOps poskytovatel přihlašovacích údajů je součástí Sady Visual Studio. Nejsou vyžadovány žádné další kroky.
