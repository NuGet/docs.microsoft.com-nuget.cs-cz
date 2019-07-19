---
title: Známé problémy
description: Známé problémy s nástrojem NuGet, včetně ověřování, instalace balíčků a nástrojů.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b104eb39ddeacd9ca1ea45937cf98ad57531112a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317144"
---
# <a name="known-issues-with-nuget"></a>Známé problémy s NuGet

Jedná se o nejběžnější známé problémy se systémem NuGet, který se opakovaně hlásí. Pokud máte potíže s instalací NuGet nebo správou balíčků, Projděte si tyto známé problémy a jejich řešení.

> [!Note]
> Počínaje verzí NuGet 4,0 jsou známé problémy součástí odpovídajících poznámek k verzi.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problémy s ověřováním pomocí kanálů NuGet v VSTS s NuGet. exe v 3.4.3

**Řešení**

Když použijeme následující příkaz k uložení přihlašovacích údajů, ukončíme dvojitou šifrování osobního přístupového tokenu.

$PAT = "váš osobní přístupový token" $Feed = "vaše adresa URL" .\nuget.exe sources add-name test-source $Feed-UserName $UserName-Password $PAT

**Odstraníte**

Ukládejte hesla jako nešifrovaný text pomocí možnosti [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) .

## <a name="error-installing-packages-with-nuget-34-341"></a>Chyba při instalaci balíčků pomocí NuGet 3,4, 3.4.1

**Řešení**

V NuGet 3,4 a 3.4.1 při použití doplňku NuGet nejsou žádné zdroje hlášeny jako dostupné a v okně Konfigurace nemůžete přidávat nové zdroje. Výsledek je podobný následujícímu obrázku:

![Konfigurace NuGet bez zdrojů](./media/knownIssue-34-NoSources.PNG)

Soubor ve složce (Windows`~/.nuget/` ) nebo (Mac/Linux) byl omylem vyprázdněn. `%AppData%\NuGet\` `NuGet.Config` Oprava: Ukončete aplikaci Visual Studio (v systému Windows, pokud je k dispozici) `NuGet.Config` , odstraňte soubor a opakujte operaci. NuGet vygeneroval nové `NuGet.Config` a mělo by být možné pokračovat.

## <a name="error-installing-packages-with-nuget-27"></a>Chyba při instalaci balíčků pomocí NuGet 2,7

**Řešení**

Pokud se při pokusu o instalaci balíčku obsahujícího odkazy na sestavení v NuGet 2,7 nebo vyšší, může se zobrazit chybová zpráva **"vstupní řetězec nebyl ve správném formátu"** , například níže:

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

To je způsobeno tím, že knihovna typů `VSLangProj.dll` pro komponentu modelu COM je v systému odregistrována. K tomu může dojít například v případě, že máte nainstalovanou dvě verze sady Visual Studio vedle sebe a pak odinstalujete starší verzi. V takovém případě může neúmyslně zrušit registraci výše uvedené knihovny COM.

**Řešení:** :

Spusťte tento příkaz z **příkazového řádku se zvýšenými oprávněními** a znovu Zaregistrujte knihovnu typů pro`VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Pokud se příkaz nezdařil, zkontrolujte, zda soubor v tomto umístění existuje.

Další informace o této chybě naleznete v části Tato pracovní [Položka pracovní položky](https://nuget.codeplex.com/workitem/3609 "3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Chyba sestavení po aktualizaci balíčku ve VS 2012

Problém: Používáte VS 2012 RTM. Při aktualizaci balíčků NuGet se zobrazí tato zpráva: Nepovedlo se dokončit odinstalaci jednoho nebo víc balíčků. a zobrazí se výzva k restartování sady Visual Studio. Po restartování VS se zobrazí chyby sestavení divné.

Příčinou je, že některé soubory ve starších balíčcích jsou uzamčeny procesem MSBuild na pozadí. I po restartování VS, proces MSBuild na pozadí stále používá soubory ve starších balíčcích, což způsobuje selhání sestavení.

Opravou je instalace VS 2012 Update, například VS 2012 Update 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Upgrade na nejnovější verzi NuGet ze starší verze způsobí chybu při ověřování podpisu.

Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, použít následující chybovou zprávu.

![Instalační program rozšíření sady Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Při prohlížení protokolů se může zobrazit zmínka `SignatureMismatchException`o.

Aby k tomu nedošlo, je k dispozici [oprava hotfix sady Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) , kterou můžete nainstalovat.
Alternativně je alternativním řešením jednoduše odinstalovat NuGet (při spuštění sady Visual Studio jako správce) a pak ji nainstalovat z galerie rozšíření VS.  Další [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) informace najdete v tématu.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Konzola správce balíčků vyvolá výjimku, pokud je nainstalován i doplněk pro odrážející sadu Visual Studio.

Při spuštění konzoly Správce balíčků můžete spustit následující zprávu o výjimce, pokud máte nainstalovanou odrážející doplněk VS.

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

Kontaktovali jsme autora doplňku v hodlá řešení problému.

<p class="info">Aktualizace: Ověřili jsme, že nejnovější verze Odrazer, 6,5, už tuto výjimku nezpůsobuje v konzole nástroje.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Spuštění konzoly Správce balíčků se nezdařilo s výjimkou ObjectSecurity

Tyto chyby se můžou zobrazit při pokusu o otevření konzoly Správce balíčků:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Pokud ano, opravte je podle řešení [v tématu StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) .

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Dialogové okno Přidat knihovnu balíčků vyvolá výjimku, pokud řešení obsahuje projekt InstallShield Limited Edition

Zjistili jsme, že pokud vaše řešení obsahuje jeden nebo více projektů InstallShield s omezeným voláním, dialogové okno **přidat knihovnu balíčků** vyvolá při otevření výjimku. V současné době zatím neexistuje alternativní řešení s výjimkou odebrání projektů InstallShield nebo jejich uvolnění.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Tlačítko odinstalovat šedé? NuGet vyžaduje oprávnění správce k instalaci/odinstalaci.

Pokud se pokusíte odinstalovat NuGet pomocí Správce rozšíření sady Visual Studio, můžete si všimnout, že je tlačítko odinstalovat zakázané. NuGet vyžaduje přístup správce k instalaci a odinstalaci. Pokud chcete rozšíření odinstalovat, znovu spusťte Visual Studio jako správce. NuGet nevyžaduje přístup správce k jeho použití.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Konzola správce balíčků při otevření v systému Windows XP dojde k chybě. Co je?

NuGet vyžaduje prostředí PowerShell 2,0 Runtime. Windows XP ve výchozím nastavení nemá PowerShell 2,0. Modul runtime PowerShellu 2,0 si můžete stáhnout [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929)z. Po instalaci nástroje restartujte sadu Visual Studio a měli byste být schopni spustit konzolu Správce balíčků.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Po otevření konzoly Správce balíčků dojde k chybě sady Visual Studio 2010 SP1 Beta.

Pokud jste nainstalovali sadu Visual Studio 2010 SP1 Beta verze, můžete si všimnout, že pokud ponecháte konzolu Správce balíčků otevřenou a zavřete Visual Studio, dojde k chybě. Toto je známý problém sady Visual Studio a bude opraven ve verzi SP1 RTM. Prozatím tuto chybu ignorujte nebo odinstalujte SP1 Beta, pokud můžete.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Element ' metadata '... Vyvolá se neplatná výjimka podřízeného elementu.

Pokud jste nainstalovali balíčky sestavené s předběžnou verzí NuGet, může se zobrazit chybová zpráva s oznámením, že při spuštění RTM má element metadata v oboru názvů schemas.microsoft.com/packaging/2010/07/nuspec.xsd neplatný podřízený element. verze NuGetu s tímto projektem Každý balíček musíte odinstalovat a znovu nainstalovat pomocí verze RTM balíčku NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Při pokusu o instalaci nebo odinstalaci dojde k chybě "nelze vytvořit soubor, pokud tento soubor již existuje".

Z nějakého důvodu můžou rozšíření sady Visual Studio získat ve stavu divné, kdy jste odinstalovali rozšíření VSIX, ale některé soubory zůstaly na pozadí. Alternativní řešení tohoto problému:

1. Ukončení sady Visual Studio
1. Otevřete následující složku (může to být na jiné jednotce počítače).

    C:\Program Files (x86) \Microsoft Visual Studio 10.0 \ Common7\IDE\Extensions\Microsoft Corporation\NuGet – správce\<balíčků verze > \

1. Odstraňte všechny soubory s příponou *. Deleteme* .
1. Znovu otevřít Visual Studio

Po provedení tohoto postupu byste měli být schopní pokračovat.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Ve výjimečných případech se při kompilování se zapnutou analýzou kódu vynutí chyba.

Pokud nainstalujete FluentNHibernate s konzolou správce balíčků a potom zkompilujete projekt pomocí funkce Analýza kódu, může se zobrazit následující chyba.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Ve výchozím nastavení FluentNHibernate vyžaduje NHibernate 3.0.0.2001. Nicméně návrh NuGet nainstaluje do projektu NHibernate 3.0.0.4000 a přidá odpovídající přesměrování vazby, aby fungoval. Projekt bude zkompilován pouze v případě, že analýza kódu není zapnuta. Na rozdíl od kompilátoru Nástroj Analýza kódu nesprávně dodržuje přesměrování vazby na použití 3.0.0.4000 namísto 3.0.0.2001. Problém můžete obejít buď instalací NHibernate 3.0.0.2001, nebo oznámením, že nástroj pro analýzu kódu se chová stejně jako kompilátor, a to následujícím způsobem:

1. Přejít na *%ProgramFiles%\Microsoft Visual Studio 10.0 \ Team Tools\Static Analysis Tools\FxCop*
1. Otevřete soubor FxCopCmd. exe. config a `AssemblyReferenceResolveMode` změňte `StrongName` z `StrongNameIgnoringVersion`na.
1. Uložte změnu a znovu sestavte projekt.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Příkaz Write-Error nefunguje v průběhu instalace. ps1/Uninstall. ps1/init. ps1

Jedná se o známý problém. Namísto volání metody Write-Error Zkuste zavolat throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalace NuGet s omezeným přístupem v systému Windows 2003 může selhat se sadou Visual Studio

Když se pokusíte nainstalovat NuGet pomocí Správce rozšíření sady Visual Studio a neběží jako správce, zobrazí se &#8220;dialogové okno&#8221; spustit jako s popiskem &#8220;spustit tento program s omezeným přístupem&#8221; . výchozí.

![Dialogové okno Spustit jako s omezením](./media/RunAsRestricted.png)

Kliknutím na OK s zaškrtnutými chybami sady Visual Studio. Než nainstalujete NuGet, nezapomeňte tuto možnost zrušit.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Nejde odinstalovat NuGet pro nástroje Windows Phone.

Windows Phone nástroje nepodporují Správce rozšíření sady Visual Studio. Chcete-li odinstalovat NuGet, spusťte následující příkaz.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Změna velkých a malých písmen ID balíčků NuGet – obnovení balíčků

Jak je popsáno u [tohoto problému GitHubu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), změna velkých a malých písmen balíčků NuGet je možné provést prostřednictvím podpory NuGet, ale způsobí komplikace při obnovení balíčku pro uživatele, kteří mají existující, různě použita, balíčky v jejich  *Složka Global-Packages* . Doporučujeme, abyste požádali o změnu velikosti písmen, pokud máte způsob, jak komunikovat se stávajícími uživateli balíčku o přerušení, ke kterému může dojít při obnovení balíčku při sestavení.

## <a name="reporting-issues"></a>Hlášení problémů s

Chcete-li ohlásit problémy NuGet [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues), navštivte.
