Chyby z `push` příkaz obvykle označuje potíže. Například zapomněli aktualizovat číslo verze ve vašem projektu a jsou proto pokusu o publikování balíčku, který již existuje.

Také se zobrazí chyby při pokusu o publikování balíčku pomocí identifikátor, který již existuje v hostiteli. Název "AppLogger", například již, existuje. V takovém případě `push` příkaz poskytuje k následující chybě:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Pokud používáte platný klíč rozhraní API, kterou jste právě vytvořili, tato zpráva znamená ke konfliktu názvů, který není úplně vymazat z části "oprávnění" chyby. Změnit identifikátor balíčku, projekt znovu sestavte, znovu vytvořte `.nupkg` souboru a opakujte `push` příkaz.