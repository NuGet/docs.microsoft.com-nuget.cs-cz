1. <span data-ttu-id="58d27-101">Změnit na složku, která obsahuje `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="58d27-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="58d27-102">Spusťte následující příkaz, zadáte název balíčku a nahraďte hodnotu klíče klíč rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="58d27-102">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="58d27-103">DotNet zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="58d27-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="58d27-104">V tématu [dotnet nuget nabízené](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="58d27-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>