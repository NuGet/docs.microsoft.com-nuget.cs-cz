---
title: Známé problémy
description: Známé problémy s NuGet, včetně ověřování, instalace balíčku a nástroje.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fc338ba3810a125f638a937cf14456bf519a24a8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548471"
---
# <a name="known-issues-with-nuget"></a>Známé problémy s NuGet

Jedná se nejčastěji používané známé problémy s NuGet, které jsou hlášeny opakovaně. Pokud máte potíže s instalací NuGet nebo správu balíčků, věnujte prosím najdete pomocí těchto známých problémů a jejich řešení.

> [!Note]
> Od verze NuGet 4.0, známé problémy jsou součástí příslušné poznámky.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problémy s ověřováním pomocí NuGet informační kanály ve službě VSTS s nuget.exe v3.4.3

**Problém:**

Pokud použijeme následující příkaz k uložení přihlašovacích údajů, jsme skončit double šifrováním osobní přístupový Token.

$PAT = "Svůj osobní přístupový token" $Feed = "url".\nuget.exe zdroje přidat – název testu-$UserName $Feed zdroje - UserName-$PAT heslo

**Alternativní řešení:**

Store hesla v nešifrovaném textu pomocí [- StorePasswordInClearText](../tools/cli-ref-sources.md) možnost.

## <a name="error-installing-packages-with-nuget-34-341"></a>Chyba při instalaci balíčků pomocí NuGet 3.4, 3.4.1

**Problém:**

NuGet 3.4 a 3.4.1 při použití – v NuGet, jsou hlášeny jako k dispozici žádné zdroje a nejde přidat nové zdroje v okně konfigurace. Výsledkem je podobně jako na následujícím obrázku:

![NuGet config s žádné zdroje](./media/knownIssue-34-NoSources.PNG)

`NuGet.Config` Ve vašich `%AppData%\NuGet\` (Windows) nebo `~/.nuget/` (Mac/Linux) složka omylem byla vyprázdněna. Chcete-li tento problém vyřešit: Zavřete sadu Visual Studio (ve Windows, pokud je k dispozici), odstranit `NuGet.Config` soubor a zkuste operaci zopakovat. NuGet vygeneroval nový `NuGet.Config` a musí být možné pokračovat.

## <a name="error-installing-packages-with-nuget-27"></a>Chyba při instalaci balíčků pomocí NuGet 2.7

**Problém:**

NuGet 2.7 nebo výše, při pokusu nainstalovat libovolný balíček, který obsahuje odkazy na sestavení, můžete obdržet chybovou zprávu **"vstupní řetězec nemá správný formát."** , třeba níže:

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

To je způsobeno knihovnu typů pro `VSLangProj.dll` komponenty modelu COM, jejíž registrace se ruší ve vašem systému. K tomu může dojít například až budete mít dvě verze sady Visual Studio nainstalovat vedle sebe a potom odinstalujte starší verzi. To může nechtěně zrušit registraci výše uvedené knihovny COM.

**Řešení:**:

Spusťte tento příkaz z **řádku se zvýšenými oprávněními** znovu zaregistrovat knihovnu typů pro `VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Pokud se příkaz nezdaří, zkontrolujte, jestli soubor existuje v dané oblasti.

Další informace o této chybě najdete v tomto [pracovní položku](https://nuget.codeplex.com/workitem/3609 "pracovní položku 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Selhání sestavení po aktualizaci balíčku v VS 2012

Problém: používáte VS 2012 RTM. Při aktualizaci balíčků NuGet, se zobrazí tato zpráva: "jeden nebo více balíčků nešlo dokončit, odinstalovat." a zobrazí se výzva k restartování sady Visual Studio. Po restartu VS, dojde k chybám divné sestavení.

Příčinou je, že určité soubory do staré balíčků uzamkla MSBuild proces na pozadí. I po restartování VS pozadí procesu MSBuild dál používá soubory do staré balíčků způsobuje selhání sestavení.

Opravou je instalace VS 2012 aktualizace, například VS 2012 Update 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Upgrade na nejnovější NuGet ze starší verze způsobí chybu ověření podpisu

Pokud spustíte VS 2010 SP1, můžete narazit na následující chybová zpráva při pokusech o upgradu Nugetu, pokud máte nainstalovaný starší verze.

![Instalační služba rozšíření sady Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Při prohlížení protokolů, může se zobrazit poznámku o `SignatureMismatchException`.

Pokud chcete zabránit tím, že je [oprava hotfix Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) můžete nainstalovat.
Alternativním řešením je můžete také jednoduše odinstalovat NuGet (při spuštění sady Visual Studio jako správce) a nainstalujte ho z Galerie rozšíření VS.  Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Konzola správce balíčků vyvolá výjimku, když Reflector Visual Studio Add-In je také nainstalována.

Při spuštění konzoly Správce balíčků, můžete jej spustit do následující zpráva o výjimce Pokud máte Reflector VS doplněk nainstalovaný.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

or

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

Kontaktovali jsme autorem tohoto doplňku v šancí práce na řešení.

<p class="info">Aktualizace: Jsme ověřili, že nejnovější verze Reflector, 6.5, již nezpůsobuje, že tato výjimka v konzole.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Konzola správce balíčků otevírání selže s výjimkou ObjectSecurity

Při pokusu o otevření konzole Správce balíčků, může se zobrazit tyto chyby:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Pokud ano, postupujte podle řešení [popsané na StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) a opravte je.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Dialogové okno Přidat odkaz na balíček knihovny vyvolá výjimku, pokud řešení obsahuje projekt InstallShield Limited Edition

Jste zjistili jsme, že pokud vaše řešení obsahuje nejmíň jeden projekt InstallShield Limited Edition, **přidat odkaz na balíček knihovny** vyvolá výjimku při otevření dialogového okna. Aktuálně neexistuje žádné alternativní řešení ještě s výjimkou odebírání projektů InstallShield nebo jejich uvolnění.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Odinstalovat tlačítko šedě? NuGet vyžaduje oprávnění správce, aby instalace/odinstalace

Pokud se pokusíte odinstalovat pomocí správce sady Visual Studio rozšíření NuGet, můžete si všimnout, že k dispozici tlačítko odinstalovat. NuGet vyžaduje přístup správce k instalaci a odinstalaci. Znovu spusťte Visual Studio jako správce a odinstalujte rozšíření. NuGet nevyžaduje přístup správce k jeho použití.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Když otevřete ve Windows XP dojde k chybě konzole Správce balíčků. Co je?

NuGet vyžaduje modul runtime Powershell 2.0. Windows XP, nemá ve výchozím nastavení, prostředí Powershell 2.0. Můžete si stáhnout modul runtime Powershell 2.0 z [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929). Po instalaci, restartujte Visual Studio a byste měli používat konzolu Správce balíčků.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Visual Studio 2010 SP1 Beta chyby při ukončení, pokud je otevřená Konzola správce balíčků.

Pokud jste nainstalovali Visual Studio 2010 SP1 Beta, můžete si všimnout, že pokud zůstat otevřeno, konzola Správce balíčků a zavřete sadu Visual Studio, jeho dojde k chybě. Toto je známý problém nástroje Visual Studio a bude vyřešen v aktualizaci SP1 RTM verze. Prozatím ignorovat selhání nebo odinstalovat beta verzi SP1, pokud je to možné.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Element 'metadat'... má neplatný podřízený element výjimka nastane

Pokud jste nainstalovali balíčky sestavené s předběžnou verzi verzi Nugetu, chybová zpráva s oznámením "element"metadat' v oboru názvů "schemas.microsoft.com/packaging/2010/07/nuspec.xsd" má neplatný podřízený element"může dojít při spuštění verzi RTM verze balíčku nuget s tímto projektem. Budete muset odinstalovat a znovu nainstalovat každý balíček pomocí RTM verze balíčku nuget.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Pokus o instalaci nebo odinstalaci výsledkem chyba "Nelze vytvořit soubor, který již existuje."

Z nějakého důvodu rozšíření sady Visual Studio můžete získat v divné stavu, ve kterém jste odinstalovat rozšíření VSIX, ale některé soubory byly zachovají. Alternativní řešení tohoto problému:

1. Ukončení sady Visual Studio
1. Otevřete následující složku (může být na jinou jednotku na počítači)

    C:\Program soubory (x86) \Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Správce balíčků Corporation\NuGet\<verze > \

1. Odstranit všechny soubory s *.deleteme* rozšíření.
1. Znovu otevřete Visual Studio

Po provedení těchto kroků, by měl být pokračovat.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Ve výjimečných případech kompilaci pomocí analýzy kódu zapnuté způsobí chybu.

Může být zobrazí následující chyba, pokud nainstaluje FluentNHibernate pomocí konzole Správce balíčků a poté zkompilovat váš projekt s "Analýzu kódu" zapnuté.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Ve výchozím nastavení vyžaduje FluentNHibernate NHibernate 3.0.0.2001. Ale záměrné NuGet se do svého projektu nainstalovat NHibernate 3.0.0.4000 a přidat že příslušnou datovou vazbu přesměruje tak, že bude fungovat. Projekt zkompiluje bez potíží, pokud analýza kódu není zapnutá. Na rozdíl od kompilátor nástroj pro analýzu kódu není postupujte z správně 3.0.0.4000 nahrazujícím 3.0.0.2001 přesměrování vazby. Můžete tak buď instalaci NHibernate 3.0.0.2001 tento problém obejít nebo řekněte nástroj pro analýzu kódu se chová stejně jako kompilátor následujícím způsobem:

1. Přejděte na *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static analýzy Tools\FxCop*
1. Otevřete FxCopCmd.exe.config a změňte `AssemblyReferenceResolveMode` z `StrongName` k `StrongNameIgnoringVersion`.
1. Změnu uložíte a znovu sestavte projekt.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Chyba při zápisu příkaz nefunguje uvnitř install.ps1/uninstall.ps1/init.ps1

Jedná se o známý problém. Namísto volání Write-Error, zkuste volat vyvolání výjimky.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalace NuGet s omezeným přístupem na Windows serveru 2003, můžete chybu sady Visual Studio

Při pokusu o instalaci balíčku NuGet pomocí Správce rozšíření sady Visual Studio a není spuštěna jako správce &#8220;spustit jako&#8221; zobrazí dialogové okno s zaškrtávací políčko s popiskem &#8220;spustit tento program s omezeným přístupem&#8221; vráceno uživatelem Výchozí nastavení.

![Spustit jako s omezeným přístupem dialogového okna](./media/RunAsRestricted.png)

Kliknutím na tlačítko OK se specifikací zaškrtnuto, dojde k chybě sady Visual Studio. Ujistěte se, že zrušit zaškrtnutí této možnosti před instalací NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Nelze odinstalovat nástroje NuGet pro Windows Phone

Nástroje Windows Phone nemá podporu doplňku Správce rozšíření pro Visual Studio. Pokud chcete odinstalovat NuGet, spusťte následující příkaz.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Změna velikosti písmen ID balíčku NuGet přestane fungovat obnovení balíčku

Jak Dlouze na [tento problém Githubu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), změna velikosti písmen balíčků NuGet je možné díky podpoře NuGet, ale způsobí komplikace během obnovení balíčků pro uživatele, kteří mají stávající, jinak malými a velkými písmeny, balíčky v jejich *global-packages* složky. Doporučujeme pouze žádosti o změnu velikosti písmen, až budete mít způsob, jak komunikovat s existující uživateli vašeho balíčku o přerušení, ke kterému může dojít k jejich obnovení balíčku čas sestavení.

## <a name="reporting-issues"></a>Hlášení problémů s

K hlášení problémů NuGet, navštivte [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).
