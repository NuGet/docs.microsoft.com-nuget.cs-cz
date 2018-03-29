1. [Přihlaste se k účtu nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) nebo vytvoření účtu, pokud již nemáte.

1. Vyberte jméno uživatele (v pravém horním rohu) a pak vyberte **klíče rozhraní API**.

1. Vyberte **vytvořit**, zadejte název klíče, vyberte **vyberte obory > Push**. V části **klíč rozhraní API**, zadejte * pro **Glob vzor**, pak vyberte **vytvořit**. (Viz níže Další informace o oborech.)

1. Po vytvoření klíče, vyberte **kopie** načíst přístup klíče je nutné v rozhraní příkazového řádku:

    ![Klíč rozhraní API kopírování do schránky.](../media/QS_Create-02-APIKey.png)

1. **Důležité**: Uložit klíč v zabezpečeném umístění, protože nelze zkopírovat klíč znovu později na. Pokud se vrátíte na stránku klíče rozhraní API, budete muset znovu vygenerovat klíč a zkopírujte ho. Klíč rozhraní API můžete také odebrat, pokud již nechcete push balíčky prostřednictvím rozhraní příkazového řádku.

Obor, můžete vytvořit různé klíče rozhraní API pro jiné účely. Každý klíč má časový rámec jeho vypršení platnosti a můžete omezená na konkrétní balíčky (nebo glob vzory). Každý klíč je také vymezen na určité operace: nabízené nové balíčky a aktualizace, nabízené jenom aktualizace nebo výmazem zápisu. Pomocí oborů, můžete vytvořit klíče rozhraní API pro různé uživatele, kteří tak, že mají jenom oprávnění, které potřebují spravovat balíčky pro vaši organizaci. Další informace najdete v tématu [Introducing obor klíče rozhraní API](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).