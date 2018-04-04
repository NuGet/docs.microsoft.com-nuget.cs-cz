#### <a name="windows"></a>Windows
1. Navštivte [nuget.org/downloads](https://nuget.org/downloads) a vyberte NuGet 3.3 nebo vyšší (2.8.6 přílohy není kompatibilní s Mono). Vždy doporučujeme nejnovější verzi a 4.1.0+ je potřeba publikovat balíčky do nuget.org.
2. Každého stažení je `nuget.exe` souboru přímo. Určit, aby váš prohlížeč k uložení souboru do složky podle svého výběru. Soubor je *není* na instalační program; nic nebude zobrazeno, pokud ho spustit přímo z prohlížeče.
3. Přidat složku, kam jste umístili `nuget.exe` do vaší proměnné prostředí PATH použít nástroj příkazového řádku z libovolného místa.

#### <a name="macoslinux"></a>macOS/Linux
Chování se může mírně liší podle operačního systému distribučního.

1. Nainstalujte [Mono 4.4.2 nebo novější](http://www.mono-project.com/docs/getting-started/install/).
2. Spuštěním následujících příkazů v řádku prostředí:
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. Vytvořte alias přidáním následující skript k příslušnému souboru pro váš operační systém (obvykle `~/.bash_aliases` nebo `~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. Znovu načte prostředí.  Testování instalace zadáním `nuget` bez parametrů. Rozhraní příkazového řádku NuGet nápovědy má zobrazit.