---
title: Moduly plug-in NuGet pro různé platformy
description: Moduly plug-in pro více platforem NuGet pro NuGet. exe, dotnet. exe, MSBuild. exe a Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380503"
---
# <a name="nuget-cross-platform-plugins"></a>Moduly plug-in NuGet pro různé platformy

V balíčku NuGet 4,8 + se přidala podpora pro moduly plug-in pro různé platformy.
To bylo dosaženo vytvořením nového modelu rozšiřitelnosti modulu plug-in, který musí odpovídat striktní sadě pravidel operace.
Moduly plug-in jsou samostatné spustitelné soubory (runnables na světě .NET Core), které klienti NuGet spouštějí v samostatném procesu.
Jedná se o skutečný zápis jednou a spustí se modul plug-in všude. Bude fungovat se všemi klientskými nástroji NuGet.
Moduly plug-in můžou být buď .NET Framework (NuGet. exe, MSBuild. exe a Visual Studio), nebo .NET Core (dotnet. exe).
Je definovaný protokol komunikace s verzemi mezi klientem NuGet a modulem plug-in. Během spuštění metody handshake 2 procesy vyjednají verzi protokolu.

Aby bylo možné pokrýt všechny scénáře klientských nástrojů NuGet, musí jedna z nich potřebovat .NET Framework i modul plug-in .NET Core.
Níže jsou popsány kombinace modulů plug-in a klientů/rozhraní.

| Nástroj klienta  | Rozhraní .NET Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet. exe | .NET Core |
| NuGet. exe | .NET Framework |
| MSBuild. exe | .NET Framework |
| NuGet. exe na mono | .NET Framework |

## <a name="how-does-it-work"></a>Jak to funguje

Pracovní postup vysoké úrovně lze popsat následujícím způsobem:

1. NuGet zjišťuje dostupné moduly plug-in.
1. V případě potřeby bude NuGet iterovat přes moduly plug-in v pořadí podle priority a spustí je jednou.
1. NuGet použije první modul plug-in, který může obsluhovat požadavek.
1. Moduly plug-in budou vypnuty, jakmile již nebudou potřeba.

## <a name="general-plugin-requirements"></a>Obecné požadavky na modul plug-in

Aktuální verze protokolu je *2.0.0*.
V rámci této verze jsou požadavky následující:

- Mít platná důvěryhodná sestavení podpisů Authenticode, která se budou spouštět v systému Windows a mono. Neexistují žádné speciální požadavky na vztah důvěryhodnosti pro sestavení spuštěná v systémech Linux a Mac. [Příslušný problém](https://github.com/NuGet/Home/issues/6702)
- Podpora bezstavového spouštění v rámci aktuálního kontextu zabezpečení klientských nástrojů NuGet Například klientské nástroje NuGet neuplatní zvýšení oprávnění ani další inicializaci mimo protokol plug-in, který je popsán později.
- Být neinteraktivní, pokud není výslovně zadáno.
- Dodržovat verzi protokolu vyjednané modulem plug-in.
- Reagovat na všechny žádosti v rozumném časovém období.
- Dodržet žádosti o zrušení pro jakékoli probíhající operace.

Technické specifikace jsou podrobněji popsány v následujících specifikacích:

- [Modul plug-in pro stažení balíčku NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Modul plug-in NuGet pro ověřování přes NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Interakce klienta s modulem plug-in

Klientské nástroje NuGet a moduly plug-in komunikují s JSON přes standardní streamy (stdin, stdout, stderr). Všechna data musí mít kódování UTF-8.
Moduly plug-in se spustí s argumentem "-plugin". V případě, že uživatel přímo spustí spustitelný soubor modulu plug-in bez tohoto argumentu, může modul plug-in poskytnout informativní zprávu místo čekání na protokol handshake.
Časový limit protokolu handshake je 5 sekund. Modul plug-in by měl dokončit instalaci v co nejkratší možné míře.
Klientské nástroje NuGet se dotazují na podporované operace modulu plug-in tak, že přejdou do indexu služby pro zdroj NuGet. Modul plug-in může použít index služby ke kontrole přítomnosti podporovaných typů služeb.

Komunikace mezi klientskými nástroji NuGet a modulem plug-in je obousměrná. Každý požadavek má časový limit 5 sekund. Pokud by operace měly trvat déle, než by měl příslušný proces zaslat zprávu o průběhu, aby se zabránilo vypršení časového limitu žádosti. Po 1 minutách nečinnosti se modul plug-in považuje za nečinný a vypne se.

## <a name="plugin-installation-and-discovery"></a>Instalace a zjišťování modulu plug-in

Moduly plug-in budou zjištěny prostřednictvím struktury adresáře založené na konvencích.
Scénáře CI/CD a skupiny Power Users můžou chování přepsat pomocí proměnných prostředí. Při použití proměnných prostředí jsou povoleny pouze absolutní cesty. Všimněte si, že `NUGET_NETFX_PLUGIN_PATHS` a `NUGET_NETCORE_PLUGIN_PATHS` jsou k dispozici pouze ve verzi 5.3 + verze nástrojů NuGet a novějších.

- `NUGET_NETFX_PLUGIN_PATHS` – definuje moduly plug-in, které budou používány nástroji založenými na .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio). Má přednost před `NUGET_PLUGIN_PATHS`. (Jenom NuGet verze 5.3 +)
- `NUGET_NETCORE_PLUGIN_PATHS` – definuje moduly plug-in, které budou použity nástroji založené na .NET Core (dotnet. exe). Má přednost před `NUGET_PLUGIN_PATHS`. (Jenom NuGet verze 5.3 +)
- `NUGET_PLUGIN_PATHS` – definuje moduly plug-in, které se budou používat pro tento proces NuGet, přičemž priorita zůstane zachovaná. Pokud je tato proměnná prostředí nastavena, přepíše zjišťování na základě konvence. Ignoruje se, pokud je zadána jedna z proměnných specifických pro rozhraní.
-  User-Location, domovské umístění NuGet v `%UserProfile%/.nuget/plugins`. Toto umístění nelze přepsat. Pro moduly plug-in a .NET Framework se bude používat jiný kořenový adresář.

| Rozhraní .NET Framework | Umístění kořenového zjišťování  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Každý modul plug-in musí být nainstalovaný ve vlastní složce.
Vstupním bodem modulu plug-in bude název nainstalované složky s příponami. dll pro .NET Core a příponou. exe pro .NET Framework.

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> Pro instalaci modulů plug-in není aktuálně k dispozici uživatelský scénář. Je to tak jednoduché jako přesunutí požadovaných souborů do předem definovaného umístění.

## <a name="supported-operations"></a>Podporované operace

V rámci nového protokolu plug-in jsou podporovány dvě operace.

| Název operace | Minimální verze protokolu | Minimální verze klienta NuGet |
| -------------- | ----------------------- | --------------------- |
| Stáhnout balíček | 1.0.0 | 4.3.0 |
| [Ověřování](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Spouštění modulů plug-in v rámci správného běhu

Pro NuGet ve scénářích dotnet. exe musí být moduly plug-in v rámci tohoto konkrétního modulu runtime nástroje dotnet. exe schopné spustit.
Je na poskytovateli modulů plug-in a příjemci, aby bylo zajištěno, že se používá kompatibilní kombinace dotnet. exe/plugin.
Může dojít k potenciálnímu problému s moduly plug-in umístění uživatele, pokud se například příkaz dotnet. exe v modulu runtime 2,0 pokusí použít modul plug-in napsaný pro modul runtime 2,1.

## <a name="capabilities-caching"></a>Ukládání schopností do mezipaměti

Ověření zabezpečení a vytváření instancí modulů plug-in je nákladné. Operace stahování se provádí častěji než operace ověřování, ale průměrný uživatel NuGet má pravděpodobně pouze modul plug-in ověřování.
Pro zlepšení prostředí NuGet uloží deklarace operací pro daný požadavek do mezipaměti. Tato mezipaměť je vázaná na jeden modul plug-in a klíč modulu plug-in je cestou k modulu plug-in a vypršení platnosti této mezipaměti schopností je 30 dní. 

Mezipaměť je umístěna v `%LocalAppData%/NuGet/plugins-cache` a bude přepsaná pomocí proměnné prostředí `NUGET_PLUGINS_CACHE_PATH`. Pokud chcete vymazat tuto [mezipaměť](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jedna může spustit příkaz místní hodnoty s možností `plugins-cache`.
Možnost lokálních hodnot `all` nyní také odstraní mezipaměť modulů plug-in. 

## <a name="protocol-messages-index"></a>Index zpráv protokolu

Zprávy verze *1.0.0* protokolu:

1.  Zavřít
    * Směr požadavku: NuGet-> modul plug-in
    * Požadavek nebude obsahovat žádnou datovou část.
    * Není očekávána žádná odpověď.  Správná odpověď je pro proces modulu plug-in k okamžitému ukončení.

2.  Kopírovat soubory v balíčku
    * Směr požadavku: NuGet-> modul plug-in
    * Požadavek bude obsahovat:
        * ID a verze balíčku
        * umístění zdrojového úložiště balíčku
        * Cesta k cílovému adresáři
        * výčty souborů v balíčku, které se mají zkopírovat do cesty k cílovému adresáři
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.
        * Vyčíslitelné úplných cest pro zkopírované soubory v cílovém adresáři, pokud byla operace úspěšná.

3.  Kopírovat soubor balíčku (. nupkg)
    * Směr požadavku: NuGet-> modul plug-in
    * Požadavek bude obsahovat:
        * ID a verze balíčku
        * umístění zdrojového úložiště balíčku
        * Cesta k cílovému souboru
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.

4.  Získat přihlašovací údaje
    * Směr požadavku: modul plug-in > NuGet
    * Požadavek bude obsahovat:
        * umístění zdrojového úložiště balíčku
        * Stavový kód protokolu HTTP získaný ze zdrojového úložiště balíčku pomocí aktuálních přihlašovacích údajů
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.
        * uživatelské jméno, pokud je k dispozici
        * heslo, pokud je k dispozici

5.  Získat soubory v balíčku
    * Směr požadavku: NuGet-> modul plug-in
    * Požadavek bude obsahovat:
        * ID a verze balíčku
        * umístění zdrojového úložiště balíčku
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.
        * výčty cest k souborům v balíčku, pokud byla operace úspěšná

6.  Získat deklarace operací 
    * Směr požadavku: NuGet-> modul plug-in
    * Požadavek bude obsahovat:
        * index služby. JSON pro zdroj balíčku
        * umístění zdrojového úložiště balíčku
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.
        * výčtem podporovaných operací (např.: stažení balíčku), pokud operace byla úspěšná.  Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.

> [!Note]
> Tato zpráva se aktualizovala ve verzi *2.0.0*. Je na klientovi, aby byla zachována zpětná kompatibilita.

7.  Získat hodnotu hash balíčku
    * Směr požadavku: NuGet-> modul plug-in
    * Požadavek bude obsahovat:
        * ID a verze balíčku
        * umístění zdrojového úložiště balíčku
        * algoritmus hash
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.
        * hodnota hash souboru balíčku pomocí požadovaného algoritmu hash, pokud byla operace úspěšná

8.  Získat verze balíčku
    * Směr požadavku: NuGet-> modul plug-in
    * Požadavek bude obsahovat:
        * ID balíčku
        * umístění zdrojového úložiště balíčku
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.
        * Vyčíslitelné verze balíčku, pokud byla operace úspěšná

9.  Získat index služby
    * Směr požadavku: modul plug-in > NuGet
    * Požadavek bude obsahovat:
        * umístění zdrojového úložiště balíčku
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.
        * index služby, pokud byla operace úspěšná

10.  Metody handshake
     * Směr požadavku: NuGet <-> modul plug-in
     * Požadavek bude obsahovat:
         * aktuální verze protokolu modulů plug-in
         * minimální podporovaná verze protokolu modulů plug-in
     * Odpověď bude obsahovat:
         * kód odpovědi, který indikuje výsledek operace.
         * dohodnutá verze protokolu, pokud byla operace úspěšná.  V důsledku selhání dojde k ukončení modulu plug-in.

11.  Initialize
     * Směr požadavku: NuGet-> modul plug-in
     * Požadavek bude obsahovat:
         * verze klientského nástroje NuGet
         * efektivní jazyk klientského nástroje NuGet.  Toto nastavení ForceEnglishOutput se bere v úvahu při použití.
         * výchozí časový limit požadavku, který nahrazuje výchozí protokol.
     * Odpověď bude obsahovat:
         * kód odpovědi, který indikuje výsledek operace.  V důsledku selhání dojde k ukončení modulu plug-in.

12.  protokolu
     * Směr požadavku: modul plug-in > NuGet
     * Požadavek bude obsahovat:
         * úroveň protokolu pro požadavek
         * zpráva, která se má protokolovat
     * Odpověď bude obsahovat:
         * kód odpovědi, který indikuje výsledek operace.

13.  Ukončení procesu NuGetu monitorování
     * Směr požadavku: NuGet-> modul plug-in
     * Požadavek bude obsahovat:
         * ID procesu NuGet
     * Odpověď bude obsahovat:
         * kód odpovědi, který indikuje výsledek operace.

14.  Předběžné načtení balíčku
     * Směr požadavku: NuGet-> modul plug-in
     * Požadavek bude obsahovat:
         * ID a verze balíčku
         * umístění zdrojového úložiště balíčku
     * Odpověď bude obsahovat:
         * kód odpovědi, který indikuje výsledek operace.

15.  Nastavit přihlašovací údaje
     * Směr požadavku: NuGet-> modul plug-in
     * Požadavek bude obsahovat:
         * umístění zdrojového úložiště balíčku
         * poslední známé zdrojové uživatelské jméno balíčku, pokud je k dispozici
         * poslední známé heslo zdroje balíčku, pokud je k dispozici
         * poslední známé uživatelské jméno proxy, pokud je k dispozici
         * poslední známé heslo proxy serveru, pokud je k dispozici
     * Odpověď bude obsahovat:
         * kód odpovědi, který indikuje výsledek operace.

16.  Nastavit úroveň protokolu
     * Směr požadavku: NuGet-> modul plug-in
     * Požadavek bude obsahovat:
         * Výchozí úroveň protokolování
     * Odpověď bude obsahovat:
         * kód odpovědi, který indikuje výsledek operace.

Zprávy verze protokolu *2.0.0*

17. Získat deklarace operací

* Směr požadavku: NuGet-> modul plug-in
    * Požadavek bude obsahovat:
        * index služby. JSON pro zdroj balíčku
        * umístění zdrojového úložiště balíčku
    * Odpověď bude obsahovat:
        * kód odpovědi, který indikuje výsledek operace.
        * výčtem podporovaných operací, pokud byla operace úspěšná.  Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.

    Pokud má index služby a zdroj balíčku hodnotu null, může modul plug-in odpovědět s ověřováním.

18. Získat přihlašovací údaje pro ověření

* Směr požadavku: NuGet-> modul plug-in
* Požadavek bude obsahovat:
    * identifikátor URI
    * Opakování
    * Neinteraktivní
    * CanShowDialog
* Odpověď bude obsahovat
    * jmen
    * Heslo
    * Zpráva
    * Seznam typů ověřování
    * MessageResponseCode
