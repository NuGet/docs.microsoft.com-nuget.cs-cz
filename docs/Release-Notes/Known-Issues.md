---
title: "NuGet známé problémy | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Známé problémy s NuGet, včetně ověřování, instalace balíčku a nástroje."
keywords: "Známé problémy, problémy NuGet NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bd85d9da61753d25c8918c7d55fab775820b017b
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="known-issues-with-nuget"></a>Známé problémy s nástrojem NuGet

Toto jsou nejběžnější známé problémy s NuGet opakovaně hlášený. Pokud máte potíže s instalací NuGet nebo spravovat balíčky, proveďte prosím vzhled prostřednictvím těchto známé problémy a jejich řešení.

> [!Note]
> Od verze NuGet 4.0, známé problémy jsou součástí příslušného poznámky.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problémy s ověřením s NuGet kanály v služby VSTS s nuget.exe v3.4.3

**Problém:**

Když jsme k uložení pověření, použijte následující příkaz, jsme skončili dvojité šifrování tokenu osobní přístup.

$PAT = "Váš osobní přístupový token" $Feed = "url".\nuget.exe zdroje přidat – název Test-zdroj $Feed - UserName $UserName-$PAT heslo

**Alternativní řešení:**

Uložení hesla v nešifrovaném textu pomocí [- StorePasswordInClearText](../tools/cli-ref-sources.md) možnost.

## <a name="error-installing-packages-with-nuget-34-341"></a>Chyba při instalaci balíčků s NuGet 3.4, 3.4.1

**Problém:**

V NuGet 3.4 a 3.4.1 při použití doplňku NuGet, jsou hlášeny jako dostupné žádné zdroje a nemůžete přidat nového zdroje v okně konfigurace. Výsledkem je podobná následující obrázek:

![Konfigurace NuGet se žádné zdroje](./media/knownIssue-34-NoSources.PNG)

`NuGet.Config` Ve vaší `%AppData%\NuGet\` omylem vyprázdnění složky. Tento problém lze vyřešit: zavřete Visual Studio 2015, odstranit `NuGet.Config` v soubor `%AppData%\NuGet\` složky a restartujte Visual Studio.  Nový `NuGet.Config` soubor bude vytvořen a vy nebudete moci pokračovat.

## <a name="error-installing-packages-with-nuget-27"></a>Chyba při instalaci balíčků s NuGet 2.7

**Problém:**

V NuGet 2.7 nebo vyšší, když se pokusíte nainstalovat libovolný balíček, který obsahuje odkazy na sestavení, může se zobrazit chybová zpráva **"vstupní řetězec nebyla ve správném formátu."** , například níže:

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

Je to způsobeno knihovnu typů pro `VSLangProj.dll` komponenty modelu COM rušena ve vašem systému. K tomu může dojít, například když máte dvě verze sady Visual Studio nainstalované souběžně sdílená a pak odinstalujte starší verzi. Díky tomu může nechtěně registraci výše uvedené knihovny COM.

**Řešení:**:

Spusťte tento příkaz z **řádku se zvýšenými oprávněními** znovu zaregistrovat knihovnu typů pro`VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Pokud se příkaz nezdaří, zkontrolujte, zda soubor existuje v tomto umístění.

Další informace o této chybě naleznete v tématu to [pracovní položka](https://nuget.codeplex.com/workitem/3609 "pracovní položka 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Chyba sestavení po aktualizace balíčku v VS 2012

Problém: používáte VS 2012 RTM. Při aktualizaci balíčků NuGet se vám tato zpráva: "jeden nebo více balíčků nelze dokončit, odinstalovat." a zobrazí se výzva k restartování sady Visual Studio. Po restartování VS, dojde k chybám divné sestavení.

Příčinou je, některé soubory v původním balíčcích je uzamčený MSBuild proces na pozadí. I po restartování VS, MSBuild proces na pozadí pořád používají soubory v původním balíčcích způsobuje selhání sestavení.

Je k instalaci aktualizace produktu VS 2012, například VS 2012 Update 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Upgrade na nejnovější NuGet ze starší verze způsobí chybu ověření podpisu

Pokud používáte VS 2010 SP1, může dojít k následující chybová zpráva při pokusech o upgradu Nugetu, pokud máte nainstalovaný starší verze.

![Instalační program rozšíření sady Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Při prohlížení protokolů, může se zobrazit poznámku o `SignatureMismatchException`.

Chcete-li tomu zabránit, že je [oprava hotfix Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) můžete nainstalovat.
Alternativně řešením je jednoduše odinstalovat NuGet (při spuštění sady Visual Studio jako správce) a nainstalujte ji z Galerie rozšíření VS.  V tématu [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Další informace.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Konzola správce balíčků vyvolá výjimku, pokud Reflector Visual Studio Add-In je také nainstalován.

Při spuštění konzoly Správce balíčků, můžete spustit do zpráva o výjimce Pokud máte Reflector VS doplněk nainstalován.

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

Jsme jsme kontaktovat Autor doplněk v šancí pracovat na řešení.

<p class="info">Aktualizace: Jsme ověříte, že nejnovější verzi Reflector, 6.5, už způsobí, že tato výjimka v konzole.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Konzola správce balíčků otevírání selže s výjimkou ObjectSecurity

Může se zobrazí tyto chyby při pokusu o otevření konzole Správce balíčků:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Pokud ano, využijte řešení [popsané na StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) opravit je.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Dialogové okno Přidat odkaz na balíček knihovny vyvolá výjimku, pokud řešení obsahuje projekt InstallShield Limited Edition

Myslíme, že by, pokud vaše řešení obsahuje jeden nebo více projekt InstallShield Limited Edition, **přidat odkaz na balíček knihovny** dialogové okno vyvolá výjimku při otevření. Aktuálně neexistuje žádné řešení ještě kromě odebrání InstallShield projekty nebo jejich uvolnění.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Odinstalovat, tlačítko šedá? NuGet vyžaduje oprávnění správce pro instalace nebo odinstalace

Pokud se pokusíte odinstalovat NuGet prostřednictvím Správce rozšíření sady Visual Studio, můžete si všimnout, že k dispozici tlačítko odinstalovat. NuGet potřebuje přístup správce k instalaci a odinstalaci. Visual Studio spusťte jako správce a odinstalovat rozšíření. NuGet nevyžaduje přístup správce ke ho použít.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Konzola správce balíčků dojde k chybě při otevírání v systému Windows XP. Co je?

NuGet vyžaduje modul runtime Powershell 2.0. Windows XP, nemá ve výchozím nastavení, prostředí Powershell 2.0. Můžete si stáhnout modul runtime Powershell 2.0 z [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929). Po instalaci, restartujte Visual Studio a nyní byste měli mít otevřete konzolu Správce balíčků.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Visual Studio 2010 SP1 Beta chyby při ukončení, pokud Konzola správce balíčků je otevřený.

Pokud jste nainstalovali Visual Studio 2010 SP1 Beta, můžete si všimnout, že pokud zůstat otevřeno, konzola Správce balíčků a zavřete Visual Studio, ho dojde k chybě. Toto je známý problém sady Visual Studio a bude vyřešený v SP1 RTM verzi. Prozatím ignorovat havárii nebo odinstalovat beta verzi SP1, pokud je to možné.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Element 'metadata'... má neplatný podřízený element výjimce dochází

Pokud jste nainstalovali balíčky vytvořené s nástroji předběžné verze balíčku nuget, chybová zpráva s oznámením "elementu 'metadata" v oboru názvů "schemas.microsoft.com/packaging/2010/07/nuspec.xsd" má neplatným podřízeným elementem"může dojít při spuštění verzi RTM verze balíčku NuGet s daného projektu. Budete muset odinstalovat a potom znovu nainstalovat každý balíček pomocí verzi RTM programu NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Probíhá pokus o instalaci nebo odinstalaci výsledkem chyba "Nelze vytvořit soubor tento soubor již existuje."

Z nějakého důvodu můžete v divné stavu, kde jste odinstalována VSIX rozšíření, ale některé soubory byly ponechány získat rozšíření Visual Studia. Alternativní řešení tohoto problému:

1. Exit Visual Studio
1. Otevřete následující složku (může být na jinou jednotku na počítači)

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. Odstraní všechny soubory s *.deleteme* rozšíření.
1. Znovu otevřete Visual Studio

Po následujícím postupem, byste měli moci pokračovat.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Ve výjimečných případech kompilujete s analýza kódu zapnutá výsledkem chyba.

Můžete získat následující chyby, pokud nainstaluje FluentNHibernate s konzolou Správce balíčků a pak kompilace projektu s "Analýza kódu" zapnutý.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Ve výchozím nastavení vyžaduje FluentNHibernate NHibernate 3.0.0.2001. Ale záměrné NuGet nainstaluje NHibernate 3.0.0.4000 ve vašem projektu a přidat že přesměrování odpovídající vazby tak, že bude fungovat. Projekt je zkompiluje správně, pokud analýza kódu není zapnutá. Na rozdíl od kompilátoru nebude nástroj pro analýzu kódu správně podle přesměrování vazby pro použití 3.0.0.4000 místo 3.0.0.2001. Můžete pomocí buď instalaci NHibernate 3.0.0.2001 tento problém obejít nebo řekněte nástroj pro analýzu kódu se bude chovat stejná jako kompilátor následujícím způsobem:

1. Přejděte na *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*
1. Otevřete FxCopCmd.exe.config a změňte `AssemblyReferenceResolveMode` z `StrongName` k `StrongNameIgnoringVersion`.
1. Změnu uložíte a znovu sestavte projekt.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Chyba při zápisu příkaz nefunguje uvnitř install.ps1/uninstall.ps1/init.ps1

Jedná se o známý problém. Namísto volání Write-Error, zkuste volání throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalace NuGet s omezeným přístupem v systému Windows 2003 můžete chybu sady Visual Studio

Při pokusu o instalaci NuGet pomocí Správce rozšíření Visual Studio a není spuštěna jako správce &#8220; Spustit jako &#8221; Zobrazí se dialogové okno s zaškrtávací políčko s názvem bez přípony &#8220; Spuštění tohoto programu s omezeným přístupem &#8221; ve výchozím nastavení zaškrtnuto.

![Spustit jako dialogové okno s omezeným přístupem](./media/RunAsRestricted.png)

Kliknutím na OK s třídou zaškrtnuto, dojde k chybě Visual Studio. Ujistěte se, zrušte tuto možnost před instalací NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Nelze odinstalovat nástroje NuGet pro Windows Phone

Nástroje pro Windows Phone nemá podporu pro správce rozšíření sady Visual Studio. Chcete-li odinstalovat NuGet, spusťte následující příkaz.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Změna velikosti písmen ID balíčků NuGet dělí obnovení balíčků

Jak je popsáno v length na [potíže Githubu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), změna velikosti písmen balíčků NuGet se dá dělat formou podporu NuGet, ale příčiny komplikace při obnovování balíčků pro uživatele, kteří mají existující, jinak použita, balíčky v balíček místní mezipaměti. Doporučujeme, abyste pouze požaduje případu změnu, když máte způsob, jak komunikovat s stávající uživatele vašeho balíčku o přerušení, ke kterému může dojít k jejich obnovení balíčků čase vytvoření buildu.

## <a name="reporting-issues"></a>Hlášení problémů

Chcete-li nahlásit problém NuGet, navštivte [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).
