Instalace balíčku se stane třemi způsoby:

| Metoda | Popis | Odkaz |
| --- | --- | --- |
| nuget.exe rozhraní příkazového řádku:`nuget install <package_name>` | Stáhne balíček identifikovaný \<název_balíčku\> a rozšíří jeho obsah do složky v aktuálním adresáři. Pokud nejsou zadány žádné balíčky, nainstaluje všechny balíčky uvedené v projektu `packages.config` souboru. Všechny soubory projektu jsou provedeny žádné změny. Závislosti jsou také stáhnout a rozšířit. | [Referenční dokumentace rozhraní příkazového řádku](../tools/nuget-exe-CLI-Reference.md) |
| Konzola správce balíčků (Visual Studio):`Install-Package <package_name>` | Stáhne a nainstaluje balíček do aktuálního projektu a potom aktualizaci souboru projektu vypsat balíček jako závislost. | [Průvodce konzoly Správce balíčků](../tools/Package-Manager-Console.md) |
| Uživatelského rozhraní Správce balíčků (Visual Studio) | Poskytuje uživatelské rozhraní, pomocí kterého můžete procházet, vyberte a nainstalujte balíčky do projektu. Aktualizace souboru projektu vypsat balíček jako závislost. | [Odkaz uživatelského rozhraní Správce balíčků](../tools/Package-Manager-UI.md) |