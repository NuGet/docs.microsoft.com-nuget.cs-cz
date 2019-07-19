---
title: Víceplatformní ověřovací moduly plug-in NuGet
description: Moduly plug-in pro ověřování na různých platformách NuGet pro NuGet. exe, dotnet. exe, MSBuild. exe a Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317281"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>Víceplatformní ověřovací moduly plug-in NuGet

Ve verzi 4.8 + můžou všichni klienti NuGet (NuGet. exe, Visual Studio, dotnet. exe a MSBuild. exe) používat modul plug-in pro ověřování sestavený nad modelem [modulů plug-in NuGet pro různé platformy](NuGet-Cross-Platform-Plugins.md) .

## <a name="authentication-in-dotnetexe"></a>Ověřování v příkazu dotnet. exe

Visual Studio a NuGet. exe jsou ve výchozím nastavení interaktivní. NuGet. exe obsahuje přepínač, který ho [neinteraktivní](../nuget-exe-CLI-Reference.md).
Navíc nástroje NuGet. exe a moduly plug-in sady Visual Studio vyzvat uživatele ke vstupu.
V příkazu dotnet. exe není žádné výzvy a výchozí hodnota není interaktivní.

Mechanismus ověřování v příkazu dotnet. exe je tok zařízení. Pokud se operace obnovení nebo přidání balíčku spustí interaktivně, zablokují se operace a pokyny pro uživatele, jak dokončit ověřování, k dispozici na příkazovém řádku.
Když uživatel dokončí ověřování, operace bude pokračovat.

Aby byla operace interaktivní, jedna by se měla `--interactive`předat.
V současné době pouze `dotnet restore` explicitní `dotnet add package` příkazy a podporují interaktivní přepínač.
V `dotnet build` a`dotnet publish`není k dispozici žádný interaktivní přepínač.

## <a name="authentication-in-msbuild"></a>Ověřování v nástroji MSBuild

Podobně jako dotnet. exe, MSBuild. exe je ve výchozím nastavení neinteraktivním mechanismem ověřování MSBuild. exe je tok zařízení.
Chcete-li obnovit pozastavení a čekání na ověření, zavolejte příkaz Restore `msbuild -t:restore -p:NuGetInteractive="true"`with.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Vytvoření modulu plug-in pro ověřování pro různé platformy

Ukázkovou implementaci najdete v [modulu plug-in zprostředkovatele přihlašovacích údajů Microsoftu](https://github.com/Microsoft/artifacts-credprovider).

Je velmi důležité, aby moduly plug-in splňovaly požadavky na zabezpečení stanovené klientskými nástroji NuGet.
Minimální požadovaná verze modulu plug-in pro ověřování je *2.0.0*.
NuGet provede metodu handshake s modulem plug-in a dotazem na podporované deklarace operací.
Další podrobnosti o konkrétních zprávách najdete v [zprávách protokolu](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) plug-in pro různé platformy NuGet.

NuGet nastaví úroveň protokolu a v případě potřeby poskytne informace o proxy na modul plug-in.
Protokolování do konzoly NuGet je přijatelné až poté, co NuGet nastaví úroveň protokolu na modul plug-in.

- Chování ověřování modulu plug-in .NET Framework

V .NET Framework můžou moduly plug-in zobrazit uživateli výzvu k zadání vstupu ve formě dialogového okna.

- Chování ověřování modulem plug-in .NET Core

V rozhraní .NET Core nelze zobrazit dialog. Moduly plug-in by měly používat tok zařízení k ověření.
Modul plug-in může do nástroje NuGet odeslat zprávy protokolu s pokyny pro uživatele.
Všimněte si, že protokolování je dostupné po nastavení úrovně protokolu na modul plug-in.
NuGet nebude mít žádný interaktivní vstup z příkazového řádku.

Když klient zavolá modul plug-in s přihlašovacími údaji pro ověření, moduly plug-in musí splňovat přepínač interaktivity a respektovat přepínač pro dialog. 

Následující tabulka shrnuje, jak se má modul plug-in chovat pro všechny kombinace.

| IsNonInteractive | CanShowDialog | Chování modulu plug-in |
| ---------------- | ------------- | --------------- |
| true | true | Přepínač IsNonInteractive má přednost před přepínačem dialogu. Modul plug-in nemůže automaticky otevřít dialog. Tato kombinace je platná jenom pro .NET Framework moduly plug-in. |
| true | false | Přepínač IsNonInteractive má přednost před přepínačem dialogu. Modul plug-in není povolený blokování. Tato kombinace je platná jenom pro moduly plug-in .NET Core. |
| false | true | Modul plug-in by měl zobrazovat dialogové okno. Tato kombinace je platná jenom pro .NET Framework moduly plug-in. |
| false | false | Modul plug-in nemůže zobrazit dialog. Modul plug-in by měl použít tok zařízení k ověření protokolováním zprávy instrukcí prostřednictvím protokolovacího nástroje. Tato kombinace je platná jenom pro moduly plug-in .NET Core. |

Než začnete psát modul plug-in, přečtěte si následující specifikace.

- [Modul plug-in pro stažení balíčku NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Modul plug-in NuGet pro ověřování přes NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
