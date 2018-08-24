---
title: NuGet pro různé platformy ověřování modulu plug-in
description: NuGet pro různé platformy ověřování moduly plug-in pro NuGet.exe, dotnet.exe, msbuild.exe a sady Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 02db20e72f67463fffc45f3cba891ae670d67067
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794201"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet pro různé platformy ověřování modulu plug-in

Ve verzi 4.8 +, všechny klienty (NuGet.exe, Visual Studio, dotnet.exe a MSBuild.exe) můžete použít ověřování modul plug-in postavený na NuGet [NuGet pro různé platformy moduly plug-in](NuGet-Cross-Platform-Plugins.md) modelu.

## <a name="authentication-in-dotnetexe"></a>Ověřování v dotnet.exe

Visual Studio a NuGet.exe jsou ve výchozím nastavení interaktivní. NuGet.exe obsahuje přepínač k němu [neinteraktivního](../../tools/nuget-exe-CLI-Reference.md).
Kromě modulů plug-in NuGet.exe a sady Visual Studio vyzve uživatele k zadání.
V dotnet.exe není nebude tato výzva a výchozí hodnota je není interaktivní.

Mechanismus ověřování ve dotnet.exe je tok zařízení. Při obnovení nebo přidat operaci balíčku je spustit interaktivně, operace bloky a pokyny pro uživatele, jak k dokončení ověřování, poskytneme vám na příkazovém řádku.
Když je ověřování dokončeno uživatel operace bude pokračovat.

Operace interaktivní, jeden by měl předáním `--interactive`.
Aktuálně pouze explicitní `dotnet restore` a `dotnet add package` příkazy podpory interaktivní přepínače.
Neexistuje žádný interaktivní přepínač na `dotnet build` a `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Ověřování v nástroji MSBuild

Podobně jako dotnet.exe MSBuild.exe je ve výchozím nastavení není že interaktivní je ověřovací mechanismus MSBuild.exe tok zařízení.
Pokud chcete povolit obnovení pozastavení a počkejte, ověřování, volání obnovení s `msbuild /t:restore /p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Vytvoření modulu plug-in pro ověřování různé platformy

Ukázková implementace lze nalézt v [modulu plug-in MSCredProvider](https://github.com/Microsoft/mscredprovider).

Je velmi důležité, moduly plug-in odpovídá na požadavky na zabezpečení stanoví pomocí klientských nástrojů Nugetu.
Minimální verze požadovaná pro modul plug-in bude ověřování modul plug-in je *2.0.0*.
NuGet provede ověření typu handshake modulu plug-in a dotazů pro deklarace identity podporovaná operace.
NuGet pro různé platformy modul plug-in najdete [zprávy protokolu](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) další podrobnosti o konkrétní zprávy.

NuGet nastavit úroveň protokolu, který se poskytují informace o proxy serveru pro modul plug-in v případě potřeby.
Protokolování NuGet konzoly je přijatelné až NuGet nastavil úroveň protokolování pro modul plug-in.

- Chování ověřování modulu plug-in rozhraní .NET framework

V rozhraní .NET Framework na moduly plug-in můžou vyzvat uživatele k zadání vstupu v podobě dialogové okno.

- Chování ověřování modulu plug-in .NET core

V .NET Core nelze zobrazit dialogové okno. Moduly plug-in k ověření používala zařízení toku.
Modul plug-in můžete odesílat zprávy protokolu NuGet s pokyny pro uživatele.
Všimněte si, že je protokolování je k dispozici po úroveň protokolu je nastavená na modul plug-in.
NuGet nepořizuje žádné interaktivní vstup z příkazového řádku.

Když klient volá modul plug-in se získat přihlašovací údaje pro ověření, třeba moduly plug-in v souladu s přepínačem interaktivitu a respektovat přepínač dialogové okno. 

Následující tabulka shrnuje chování modulu plug-in pro všechny kombinace.

| IsNonInteractive | CanShowDialog | Chování modulu plug-in |
| ---------------- | ------------- | --------------- |
| true | true | Přepínač IsNonInteractive má přednost před přepínačem dialogového okna. Modul plug-in není povoleno vyvolat přes pop dialogové okno. Tato kombinace platí pouze pro moduly plug-in rozhraní .NET Framework |
| true | false | Přepínač IsNonInteractive má přednost před přepínačem dialogového okna. Modul plug-in není povolené blokování. Tato kombinace platí pouze pro moduly plug-in .NET Core |
| false | true | Modul plug-in by se zobrazit dialogové okno. Tato kombinace platí pouze pro moduly plug-in rozhraní .NET Framework |
| false | false | Modul plug-in byste/může nezobrazovat dialogové okno. Modul plug-in byste tok zařízení používají k ověření protokolováním zprávu instrukce prostřednictvím protokolovacího nástroje. Tato kombinace platí pouze pro moduly plug-in .NET Core |

Před zápisem modul plug-in najdete následující specifika plánu.

- [Modul plug-in stahování balíčku NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet pro různé platformy ověřování modulu plug-in](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
