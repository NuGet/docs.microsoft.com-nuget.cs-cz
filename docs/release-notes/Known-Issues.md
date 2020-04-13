---
title: Známé problémy
description: Známé problémy s NuGet, včetně ověřování, instalace balíčku a nástroje.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8f2b33a7290301bd16db3b1979ae496eee602f55
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "75383655"
---
# <a name="known-issues-with-nuget"></a>Známé problémy s NuGet

Jedná se o nejčastější známé problémy s NuGet, které jsou opakovaně hlášeny. Pokud máte potíže s instalací NuGet nebo správu balíčků, podívejte se na tyto známé problémy a jejich řešení.

> [!Note]
> Počínaje NuGet 4.0 známé problémy jsou součástí příslušné poznámky k verzi.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problémy s ověřováním s informačními kanály NuGet v VSTS pomocí nuget.exe v3.4.3

**Problém:**

Při použití následujícího příkazu k uložení pověření, skončíme dvojité šifrování tokenu osobního přístupu.

$PAT = "Váš osobní přístupový token" $Feed = "Vaše url" .\nuget.exe zdroje přidat -Name Test -Source $Feed -UserName $UserName -Password $PAT

**Alternativní řešení:**

Uklápěte hesla ve stavu prostého textu pomocí volby [-StorePasswordInClearText.](../reference/cli-reference/cli-ref-sources.md)

## <a name="error-installing-packages-with-nuget-34-341"></a>Při instalaci balíčků s NuGet 3.4, 3.4.1 došlo k chybě.

**Problém:**

V NuGet 3.4 a 3.4.1 při použití doplňku NuGet žádné zdroje jsou hlášeny jako dostupné a nemůžete přidat nové zdroje v okně konfigurace. Výsledek je podobný obrázku níže:

![Konfigurace NuGet bez zdrojů](./media/knownIssue-34-NoSources.PNG)

Soubor `NuGet.Config` ve `%AppData%\NuGet\` složce (Windows) nebo `~/.nuget/` (Mac/Linux) byl omylem vyprázdněn. Chcete-li tento problém vyřešit: zavřete Visual `NuGet.Config` Studio (v systému Windows, pokud je to možné), odstraňte soubor a opakujte operaci. NuGet vygeneroval nový `NuGet.Config` a měli byste být schopni pokračovat.

## <a name="error-installing-packages-with-nuget-27"></a>Při instalaci balíčků s aplikací NuGet 2.7 došlo k chybě.

**Problém:**

V NuGet 2.7 nebo vyšší, při pokusu o instalaci libovolného balíčku, který obsahuje odkazy na sestavení, se může zobrazit chybová zpráva **"Vstupní řetězec nebyl ve správném formátu."**, jako je níže:

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

To je způsobeno tím, `VSLangProj.dll` že knihovna typů pro komponentu MODELU COM není v systému registrována. K tomu může dojít například v případě, že máte dvě verze sady Visual Studio nainstalované vedle sebe a potom odinstalujete starší verzi. Pokud tak učiníte, může neúmyslně zrušit registraci výše uvedené knihovny COM.

**Řešení:**:

Spusťte tento příkaz z **výzvy se zvýšenými oprávněními** a znovu zaregistrujte knihovnu typů`VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Pokud se příkaz nezdaří, zkontrolujte, zda soubor v tomto umístění existuje.

Další informace o této chybě naleznete v této [pracovní položce](https://nuget.codeplex.com/workitem/3609 "Pracovní položka 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Selhání sestavení po aktualizaci balíčku ve VS 2012

Problém: Používáte VS 2012 RTM. Při aktualizaci balíčků NuGet se zobrazí tato zpráva: "Jeden nebo více balíčků nelze dokončit odinstalovat." a budete vyzváni k restartování sady Visual Studio. Po restartu VS, dostanete podivné chyby sestavení.

Příčinou je, že některé soubory ve starých balíčcích jsou uzamčeny procesem MSBuild na pozadí. I po restartování VS proces MSBuild na pozadí stále používá soubory ve starých balíčcích, což způsobuje selhání sestavení.

Oprava je instalace Aktualizace VS 2012, například VS 2012 Update 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Upgrade na nejnovější NuGet ze starší verze způsobí chybu ověření podpisu

Pokud používáte VS 2010 SP1, můžete spustit do následující chybové zprávy při pokusu o upgrade NuGet, pokud máte nainstalovanou starší verzi.

![Instalační program rozšíření sady Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Při prohlížení protokolů se může zobrazit `SignatureMismatchException`zmínka o .

Chcete-li tomu zabránit, je k dispozici [oprava hotfix visual studio 2010 SP1,](http://bit.ly/vsixcertfix) kterou můžete nainstalovat.
Alternativně je řešení jednoduše odinstalovat NuGet (při spuštění sady Visual Studio jako správce) a potom jej nainstalovat z Galerie rozšíření VS. Další informace naleznete v tématu <https://support.microsoft.com/kb/2581019>.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Konzola Správce balíčků vyvolá výjimku, když je nainstalován také doplněk Visual Studio Reflector.

Při spuštění konzoly Správce balíčků můžete spustit následující zprávu o výjimce, pokud máte nainstalovaný doplněk Reflector VS.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

– nebo –

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

Kontaktovali jsme autora doplňku v naději, že vypracujeme řešení.

<p class="info">Aktualizace: Ověřili jsme, že nejnovější verze Reflectoru, 6.5, již nezpůsobuje tuto výjimku v konzoli.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Otevření konzoly Správce balíčků se nezdaří s výjimkou objectsecurity

Při pokusu o otevření konzoly Správce balíčků se mohou zobrazit tyto chyby:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Pokud ano, postupujte podle řešení [popsané na StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) opravit.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Dialogové okno Přidat odkaz na knihovnu balíčků vyvolá výjimku, pokud řešení obsahuje aplikaci InstallShield Limited Edition Project.

Zjistili jsme, že pokud vaše řešení obsahuje jeden nebo více instaltických edicí projektu InstallShield, dialogové okno **Přidat odkaz na knihovnu balíčků** vyvolá při otevření výjimku. V současné době neexistuje žádné řešení ještě s výjimkou odebrání InstallShield projekty nebo jejich uvolnění.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Odinstalovat tlačítko šedě ven? NuGet vyžaduje oprávnění správce k instalaci nebo odinstalaci

Pokud se pokusíte odinstalovat NuGet prostřednictvím Správce rozšíření sady Visual Studio, můžete si všimnout, že tlačítko Odinstalovat je zakázáno. NuGet vyžaduje přístup správce k instalaci a odinstalaci. Znovu spusťte Visual Studio jako správce a odinstalujte rozšíření. NuGet nevyžaduje přístup správce k jeho použití.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Konzola Správce balíčků se při otevření v systému Windows XP zhroutí. Co je?

NuGet vyžaduje prostředí runtime prostředí Powershell 2.0. Systém Windows XP ve výchozím nastavení nemá aplikaci Powershell 2.0. Runtime aplikace Powershell 2.0 <https://support.microsoft.com/kb/968929>si můžete stáhnout z aplikace . Po instalaci restartujte aplikaci Visual Studio a měli byste být schopni spustit konzolu Správce balíčků.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Visual Studio 2010 SP1 Beta dojde k chybě při ukončení, pokud je otevřena konzola Správce balíčků.

Pokud jste nainstalovali Visual Studio 2010 SP1 Beta, můžete si všimnout, že pokud necháte konzolu Správce balíčků otevřenou a zavřete visual studio, dojde k chybě. Toto je známé vydání sady Visual Studio a bude opraveno ve verzi RTM SP1. Pro tuto chvíli, stačí ignorovat havárii nebo odinstalovat SP1 Beta, pokud je to možné.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Prvek 'metadata' ... Dojde k neplatné výjimce podřízeného prvku.

Pokud jste nainstalovali balíčky vytvořené s předběžnou verzí NuGet, může dojít k chybové zprávě s uvedením "Element 'metadata' v oboru názvů 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' má neplatný podřízený prvek" při spuštění rtm verze NuGet s tímto projektem. Je třeba odinstalovat a znovu nainstalovat každý balíček pomocí RTM verze NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Při pokusu o instalaci nebo odinstalaci dojde k chybě "Nelze vytvořit soubor, pokud soubor již existuje."

Z nějakého důvodu rozšíření sady Visual Studio může získat v podivném stavu, kde jste odinstalovali rozšíření VSIX, ale některé soubory byly ponechány za sebou. Náhradní řešení tohoto problému:

1. Ukončení sady Visual Studio
1. Otevřete následující složku (může být na jiné jednotce v počítači)

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\<Corporation\NuGet Package Manager verze>\

1. Odstraňte všechny soubory s příponami *DELETEMe.*
1. Opětovné otevření sady Visual Studio

Po provedení těchto kroků byste měli být schopni pokračovat.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Ve výjimečných případech kompilace s analýzou kódu zapnuta způsobí chybu.

Pokud nainstalujete aplikaci FluentNHibernate s konzolou Správce balíčků a potom zkompilujete projekt se zapnutou analýzou kódu, může se zobrazit následující chyba.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Ve výchozím nastavení fluentnhibernate vyžaduje NHibernate 3.0.0.2001. Však podle návrhu NuGet nainstaluje NHibernate 3.0.0.4000 v projektu a přidejte příslušné vazby přesměrování tak, aby to bude fungovat. Projekt se zkompiluje v pořádku, pokud není zapnuta analýza kódu. Na rozdíl od kompilátoru nástroj pro analýzu kódu není správně postupujte podle přesměrování vazby použít 3.0.0.4000 namísto 3.0.0.2001. Problém můžete vyřešit buď instalací NHibernate 3.0.0.2001, nebo sdělit nástroji pro analýzu kódu, aby se choval stejně jako kompilátor, a to následujícím způsobem:

1. Přejít na *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Týmové nástroje\Nástroje statické analýzy\FxCop*
1. Otevřete Soubor FxCopCmd.exe.config a změňte `AssemblyReferenceResolveMode` z `StrongName` na `StrongNameIgnoringVersion`.
1. Uložte změnu a znovu vytvořte projekt.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Příkaz Write-Error nefunguje uvnitř souboru install.ps1/uninstall.ps1/init.ps1

Jedná se o známý problém. Místo volání Write-Error zkuste volat throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalace nugetu s omezeným přístupem v systému Windows 2003 může chybět v sadě Visual Studio

Při pokusu o instalaci NuGet pomocí Správce rozšíření sady Visual Studio a není spuštěn jako správce, &#8220;Spustit jako&#8221; dialogové okno se zobrazí se zaškrtávacím políčkem s názvem &#8220;Spustit tento program s omezeným přístupem&#8221; zaškrtnuto ve výchozím nastavení.

![Dialogové okno Spustit jako omezený](./media/RunAsRestricted.png)

Kliknutím na OK s zaškrtnutou chyby dojde k selhání visual studio. Ujistěte se, že zrušit zaškrtnutí této možnosti před instalací NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Aplikaci NuGet pro nástroje pro Windows Phone nelze odinstalovat.

Nástroje Pro Windows Phone nemá podporu pro Správce rozšíření sady Visual Studio. Chcete-li odinstalovat NuGet, spusťte následující příkaz.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Změna velkých písmen ID balíčku NuGet přeruší obnovení balíčku

Jak je podrobně popsáno na [tomto problému GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), změna velkých písmen balíčků NuGet lze provést podporou NuGet, ale způsobuje komplikace během obnovení balíčku pro uživatele, kteří mají existující, různě cased, balíčky ve své složce *globální balíčky.* Doporučujeme pouze požadovat změnu případu, pokud máte způsob, jak komunikovat s existujícími uživateli balíčku o přestávce, které mohou nastat jejich obnovení balíčku sestavení.

## <a name="reporting-issues"></a>Hlášení problémů

Chcete-li nahlásit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)problémy nuget, navštivte .
