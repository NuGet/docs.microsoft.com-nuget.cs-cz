---
title: NuGet pro různé platformy modulů plug-in
description: NuGet pro různé platformy moduly plug-in pro NuGet.exe, dotnet.exe, msbuild.exe a sady Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794203"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet pro různé platformy modulů plug-in

Ve Správci NuGet 4.8 + byla přidána podpora pro různé platformy moduly plug-in.
Bylo dosaženo pomocí vytvořením nový model rozšiřitelnosti modulu plug-in, obsahující tak, aby odpovídal striktní sadu pravidel operace.
Moduly plug-in jsou samostatné spustitelné soubory (runnables ve světě .NET Core), který klienti NuGet spustit v samostatném procesu.
To je PRAVDA zápis jednou spustit všude, kde modul plug-in. Bude fungovat s všechny klientské nástroje Nugetu.
Moduly plug-in může být rozhraní .NET Framework (NuGet.exe, MSBuild.exe a sady Visual Studio) nebo .NET Core (dotnet.exe).
Je definovaný verzí komunikační protokol mezi klientem NuGet a modulu plug-in. Během handshake spuštění 2 procesy vyjednávat verze protokolu.

Aby bylo možné měli pokryté všechny scénáře nástroje klienta NuGet, jedna bude nutné rozhraní .NET Framework a .NET Core modul plug-in.
Níže jsou popsány kombinace klienta a rozhraní moduly plug-in.

| Klienta nástroje  | Rozhraní .NET Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| DotNet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| NuGet.exe v Mono | .NET Framework |

## <a name="how-does-it-work"></a>Jak to funguje

Základní pracovní postup lze popsat následujícím způsobem:

1. NuGet zjistí dostupné moduly plug-in.
1. V případě potřeby NuGet provádí iterace nad moduly plug-in v pořadí podle priority a začne je jeden po druhém.
1. NuGet použije první modul plug-in, která může obsluhovat žádosti.
1. Moduly plug-in se ukončí, pokud už nepotřebujete.

## <a name="general-plugin-requirements"></a>Modul plug-in obecné požadavky

Je aktuální verze protokolu *2.0.0*.
V této verzi jsou následující požadavky:

- Máte platný a důvěryhodné Authenticode podpis sestavení, které poběží na Windows a Mono. Neexistuje žádný požadavek speciální vztahu důvěryhodnosti pro sestavení ještě spuštěna na Linuxu a Macu. [Relevantní problém](https://github.com/NuGet/Home/issues/6702)
- Podpora bezstavové, spouští se v aktuálním kontextu zabezpečení klientských nástrojů Nugetu. Klientské nástroje Nugetu nebude provádět například zvýšení úrovně oprávnění nebo další inicializace mimo protokolu modulu plug-in je popsáno dále.
- Pokud není výslovně být není interaktivní.
- Proto zavázala dodržovat verze protokolu vyjednávaný modulu plug-in.
- Reagovat na všechny požadavky v příslušném časovém období.
- Případném dalším sdílení dodržovat požadavky zrušení pro všechny probíhající operace.

Technické specifikace je popsána podrobněji následující specifikace:

- [Modul plug-in stahování balíčku NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet pro různé platformy ověřování modulu plug-in](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Klient – modul plug-in interakce

Klientské nástroje Nugetu a moduly plug-in komunikaci s JSON přes standardní datové proudy (stdin, stdout a stderr). Všechna data musí být UTF-8.
Moduly plug-in jsou spouštěny v argumentu "-modul plug-in". V případě, že uživatel přímo spustí spustitelný soubor bez tohoto argumentu modulu plug-in, modul plug-in vám může poskytnout informativní zprávy místo abyste čekali, protokol metody handshake.
Časový limit metody handshake protokolu je 5 sekund. Modul plug-in by se měl dokončit v nastavení jako nemá množství co nejvíc.
Klientské nástroje Nugetu bude dotaz podporované operace modulu plug-in předáním index služby pro zdroj NuGet. Modul plug-in může index služby použijte ke kontrole přítomnosti podporovaných typů služeb.

Komunikace mezi klientské nástroje Nugetu a modulu plug-in je obousměrný. Každá žádost má časový limit 5 sekund. Pokud máte operace trvá déle by měl odpovídající proces odeslání zprávu o průběhu chcete zabránit vypršení časového limitu žádosti. Modul plug-in po jedné minutě nečinnosti považuje za nečinné a je vypnutý.

## <a name="plugin-installation-and-discovery"></a>Instalace modulu plug-in a zjišťování

Moduly plug-in, bude zjištěno prostřednictvím založené na konvenci adresářovou strukturu.
CI/CD scénáře IT a zkušené uživatele můžete použít proměnnou prostředí k potlačení chování.

- `NUGET_PLUGIN_PATHS` -Definuje moduly plug-in, který se použije pro tento proces NuGet, priority, které jsou vyhrazené. Pokud tato proměnná prostředí je nastavena, přepíše zjišťování na základě konvence.
-  Umístění uživatele, NuGet domovskou místo v `%UserProfile%/.nuget/plugins`. Toto umístění nelze přepsat. Různé kořenový adresář se použije pro moduly plug-in pro .NET Core a .NET Framework.

| Rozhraní .NET Framework | Kořenový adresář zjišťování  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Každý modul plug-in musí být nainstalován ve vlastní složce.
Vstupní bod modulu plug-in bude název nainstalovaných složku s příponou DLL pro .NET Core a příponou .exe pro rozhraní .NET Framework.

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
> Aktuálně neexistuje žádný uživatelský scénář pro instalaci na moduly plug-in. Je snadné – stačí přesunu požadované soubory do předem umístění.

## <a name="supported-operations"></a>Podporované operace

Dvě operace jsou podporovány v rámci nového modulu plug-in protokolu.

| Název operace | Protokol minimální verze | Minimální verzi klienta NuGet |
| -------------- | ----------------------- | --------------------- |
| Stáhněte si balíček | 1.0.0 | 4.3.0 |
| [Ověřování](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>S moduly plug-in v rámci správné modulu runtime

Moduly plug-in pro NuGet ve scénářích dotnet.exe, musí být moci být prováděny v rámci tohoto konkrétního modulu runtime dotnet.exe.
Je na modul plug-in zprostředkovatele a spotřebitele Ujistěte se, že se používá dotnet.exe/plugin kompatibilní kombinace.
Potenciální problém může vzniknout s moduly plug-in umístění uživatele, když například, dotnet.exe v rámci 2.0 modulu runtime se pokusí použít modul plug-in napsané pro modul runtime 2.1.

## <a name="capabilities-caching"></a>Možnosti ukládání do mezipaměti

Ověření zabezpečení a vytvoření instance na moduly plug-in je nákladné. Operace stahování se stane způsobem častěji než operaci ověřování, ale Průměrný uživatel NuGet je pouze nejspíš ověřování modul plug-in.
Vylepšit celkovou funkčnost, bude mezipaměti NuGet deklarace operací pro danou žádost. Tato mezipaměť je každý modul plug-in s klíčem modul plug-in se cesta modulu plug-in a vypršení platnosti pro mezipaměť této možnosti je 30 dní. 

Mezipaměť se nachází v `%LocalAppData%/NuGet/plugins-cache` a být monitorconfigurationoverride proměnnou prostředí `NUGET_PLUGINS_CACHE_PATH`. Vymazat tím [mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jedno spuštění lokální příkaz `plugins-cache` možnost.
`all` Možnost místní hodnoty nyní také odstraní mezipaměti moduly plug-in. 

## <a name="protocol-messages-index"></a>Index zprávy protokolu

Verze protokolu *1.0.0* zprávy:

1.  Zavřít
    * Požádat o směr: NuGet -> modulu plug-in
    * Požadavek bude obsahovat žádné datové části
    * Není očekávána žádná odpověď.  Správné odpovědi je pro proces modulu plug-in k okamžitému ukončení.

2.  Kopírování souborů v balíčku
    * Požádat o směr: NuGet -> modulu plug-in
    * Požadavek bude obsahovat:
        * ID balíčku a verzi
        * umístění úložiště zdroje balíčku
        * cílový adresář
        * Výčtový objekt souborů v balíčku budou zkopírovány do cílovou cestu adresáře
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace
        * Výčtový objekt úplné cesty pro zkopírované soubory v cílovém adresáři, pokud operace byla úspěšná

3.  Zkopírujte soubor balíčku (.nupkg)
    * Požádat o směr: NuGet -> modulu plug-in
    * Požadavek bude obsahovat:
        * ID balíčku a verzi
        * umístění úložiště zdroje balíčku
        * Cesta k cílovému souboru
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace

4.  Získání přihlašovacích údajů
    * Požádat o směr: modul plug-in -> NuGet
    * Požadavek bude obsahovat:
        * umístění úložiště zdroje balíčku
        * Stavový kód HTTP získané z úložiště zdroje balíčků pomocí aktuální přihlašovací údaje
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace
        * uživatelské jméno, pokud je k dispozici
        * heslo, pokud je k dispozici

5.  Získání souborů v balíčku
    * Požádat o směr: NuGet -> modulu plug-in
    * Požadavek bude obsahovat:
        * ID balíčku a verzi
        * umístění úložiště zdroje balíčku
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace
        * Výčtový objekt cesty k souborům v balíčku, pokud operace byla úspěšná

6.  Získat deklarace operací 
    * Požádat o směr: NuGet -> modulu plug-in
    * Požadavek bude obsahovat:
        * Služba index.json zdroje balíčku.
        * umístění úložiště zdroje balíčku
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace
        * Výčtový objekt podporované operace (např: stahování balíčku) Pokud operace byla úspěšná.  Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.

> [!Note]
> Aktualizovali jsme tuto zprávu ve verzi *2.0.0*. Je na klientovi pro zachování zpětné kompatibility.

7.  Získá hodnotu hash balíčku
    * Požádat o směr: NuGet -> modulu plug-in
    * Požadavek bude obsahovat:
        * ID balíčku a verzi
        * umístění úložiště zdroje balíčku
        * Hashovací algoritmus
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace
        * Hodnota hash souboru balíčku pomocí požadované hashovacího algoritmu, pokud operace byla úspěšná

8.  Získání verze balíčku
    * Požádat o směr: NuGet -> modulu plug-in
    * Požadavek bude obsahovat:
        * ID balíčku
        * umístění úložiště zdroje balíčku
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace
        * Výčtový objekt verze balíčku, pokud operace byla úspěšná

9.  Získat index služby
    * Požádat o směr: modul plug-in -> NuGet
    * Požadavek bude obsahovat:
        * umístění úložiště zdroje balíčku
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace
        * index služby, pokud operace byla úspěšná

10.  Metoda Handshake
     * Požádat o směr: NuGet <> – modulu plug-in
     * Požadavek bude obsahovat:
         * aktuální verze protokolu modulu plug-in
         * Minimální podporovaná verze protokolu modulu plug-in
     * Odpověď bude obsahovat:
         * Kód odpovědi udávající výsledek operace
         * vyjednávaný protocol verze, pokud byla operace úspěšná.  Selhání způsobí ukončení modulu plug-in.

11.  Inicializace
     * Požádat o směr: NuGet -> modulu plug-in
     * Požadavek bude obsahovat:
         * Nástroj pro verzi klienta NuGet
         * jazyk efektivní klienta nástroje NuGet.  To vezme v úvahu ForceEnglishOutput nastavení, pokud se používá.
         * Výchozí časový limit požadavku, která nahrazuje výchozí protokolu.
     * Odpověď bude obsahovat:
         * Kód odpovědi udávající výsledek operace.  Selhání způsobí ukončení modulu plug-in.

12.  protokol
     * Požádat o směr: modul plug-in -> NuGet
     * Požadavek bude obsahovat:
         * úroveň protokolu pro žádost
         * zaznamenávané zprávy
     * Odpověď bude obsahovat:
         * Kód odpovědi udávající výsledek operace.

13.  Ukončení procesu monitorování NuGet
     * Požádat o směr: NuGet -> modulu plug-in
     * Požadavek bude obsahovat:
         * ID procesu NuGet
     * Odpověď bude obsahovat:
         * Kód odpovědi udávající výsledek operace.

14.  Předběžné načtení balíčku
     * Požádat o směr: NuGet -> modulu plug-in
     * Požadavek bude obsahovat:
         * ID balíčku a verzi
         * umístění úložiště zdroje balíčku
     * Odpověď bude obsahovat:
         * Kód odpovědi udávající výsledek operace

15.  Nastavení přihlašovacích údajů
     * Požádat o směr: NuGet -> modulu plug-in
     * Požadavek bude obsahovat:
         * umístění úložiště zdroje balíčku
         * poslední známý balíček zdroj uživatelské jméno, pokud je k dispozici
         * poslední známý zdroj heslo balíčku, pokud je k dispozici
         * poslední známé proxy uživatelské jméno, pokud je k dispozici
         * poslední známé heslo k proxy serveru, pokud je k dispozici
     * Odpověď bude obsahovat:
         * Kód odpovědi udávající výsledek operace

16.  Úroveň protokolu sady
     * Požádat o směr: NuGet -> modulu plug-in
     * Požadavek bude obsahovat:
         * Výchozí úroveň protokolování
     * Odpověď bude obsahovat:
         * Kód odpovědi udávající výsledek operace

Verze protokolu *2.0.0* zprávy

17. Získat deklarace operací

* Požádat o směr: NuGet -> modulu plug-in
    * Požadavek bude obsahovat:
        * Služba index.json zdroje balíčku.
        * umístění úložiště zdroje balíčku
    * Odpověď bude obsahovat:
        * Kód odpovědi udávající výsledek operace
        * Výčtový objekt podporované operace, pokud byla operace úspěšná.  Pokud modul plug-in nepodporuje zdroj balíčku, modul plug-in musí vrátit prázdnou sadu podporovaných operací.

    Pokud zdroj index a balíček služby mají hodnotu null, modul plug-in lze odpovědět pomocí ověřování.

18. Získání přihlašovacích údajů pro ověřování

* Požádat o směr: NuGet -> modulu plug-in
* Požadavek bude obsahovat:
    * Identifikátor URI
    * isRetry
    * Neinteraktivní
    * CanShowDialog
* Odpověď bude obsahovat.
    * uživatelské jméno
    * Heslo
    * Zpráva
    * Seznam typů ověřování
    * MessageResponseCode