1. [Přihlaste se k účtu nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) nebo si vytvořte účet, pokud již nemáte.

1. Vyberte své uživatelské jméno (v pravém horním rohu) a pak vyberte **klíče rozhraní API**.

1. Vyberte **vytvořit**, zadejte název pro svůj klíč, vyberte **vyberte obory > nabízená**. V části **klíč rozhraní API**, zadejte * pro **Glob vzor**a pak vyberte **vytvořit**. (Viz níže Další informace o oborech.)

1. Jakmile se vytvoří klíč, vyberte **kopírování** pro přístup k načtení klíčů budete potřebovat v rozhraní příkazového řádku:

    ![Zkopírování klíče rozhraní API do schránky.](../media/QS_Create-02-APIKey.png)

1. **Důležité**: Uložit klíč v zabezpečeném umístění, protože nelze zkopírovat klíč znovu dále. Pokud se vrátíte na stránku klíče rozhraní API, musíte znovu vygenerovat klíč, který chcete zkopírovat. Klíč rozhraní API můžete také odebrat, pokud už nechcete push balíčky pomocí rozhraní příkazového řádku.

Vymezení oboru umožňuje vytvářet různé klíče rozhraní API pro různé účely. Každý klíč má časový rámec jeho vypršení platnosti a se dají vymezit na konkrétní balíčky (nebo vzory glob). Každý klíč působí také na určité operace: z nové balíčky a aktualizace, vložení aktualizace pouze nebo výmazem zápisu nasdílení změn. Pomocí oborů, můžete vytvořit klíče rozhraní API pro jiné uživatele, kteří spravovat balíčky pro vaši organizaci, aby měli oprávnění, které potřebují. Další informace najdete v tématu [Introducing s rozsahem klíče rozhraní API](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).