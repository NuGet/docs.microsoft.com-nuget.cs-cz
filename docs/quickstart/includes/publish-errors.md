Chyby z `push` příkaz obvykle signalizují potíže. Například možná jste zapomněli aktualizovat číslo verze ve vašem projektu a pokoušíte se publikovat balíček, který již existuje.

Také se zobrazí chyby při pokusu o publikování balíčku pomocí identifikátor, který již existuje v hostiteli. Název "AppLogger", například už. V takovém případě `push` příkaz dochází k následující chybě:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Pokud používáte platný klíč rozhraní API, kterou jste právě vytvořili, tato zpráva znamená konfliktu názvů, která není zcela zřejmé z část "oprávnění" chyby. Změnit identifikátor balíčku, sestavte projekt znovu, znovu vytvořit `.nupkg` souboru a zkuste to znovu `push` příkazu.