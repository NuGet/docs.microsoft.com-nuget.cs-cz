1. Změnit na složku obsahující `.nupkg` souboru.

1. Spusťte následující příkaz, zadávání názvu balíčku a nahraďte hodnotu klíče svůj klíč rozhraní API:

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. DotNet zobrazuje výsledky procesu publikování:

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Zobrazit [dotnet nuget nabízených](/dotnet/core/tools/dotnet-nuget-push).