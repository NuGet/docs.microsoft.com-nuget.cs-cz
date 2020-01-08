---
title: Známé problémy
description: Známé problémy s nástrojem NuGet, včetně ověřování, instalace balíčků a nástrojů.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8f2b33a7290301bd16db3b1979ae496eee602f55
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383655"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="e19e6-103">Známé problémy s NuGet</span><span class="sxs-lookup"><span data-stu-id="e19e6-103">Known Issues with NuGet</span></span>

<span data-ttu-id="e19e6-104">Jedná se o nejběžnější známé problémy se systémem NuGet, který se opakovaně hlásí.</span><span class="sxs-lookup"><span data-stu-id="e19e6-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="e19e6-105">Pokud máte potíže s instalací NuGet nebo správou balíčků, Projděte si tyto známé problémy a jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="e19e6-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="e19e6-106">Počínaje verzí NuGet 4,0 jsou známé problémy součástí odpovídajících poznámek k verzi.</span><span class="sxs-lookup"><span data-stu-id="e19e6-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="e19e6-107">Problémy s ověřováním pomocí kanálů NuGet v VSTS s NuGet. exe v 3.4.3</span><span class="sxs-lookup"><span data-stu-id="e19e6-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="e19e6-108">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="e19e6-108">**Problem:**</span></span>

<span data-ttu-id="e19e6-109">Když použijeme následující příkaz k uložení přihlašovacích údajů, ukončíme dvojitou šifrování osobního přístupového tokenu.</span><span class="sxs-lookup"><span data-stu-id="e19e6-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="e19e6-110">$PAT = "váš osobní přístupový token" $Feed = "vaše adresa URL" .\nuget.exe sources add-name test-source $Feed-UserName $UserName-Password $PAT</span><span class="sxs-lookup"><span data-stu-id="e19e6-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="e19e6-111">**Alternativní řešení:**</span><span class="sxs-lookup"><span data-stu-id="e19e6-111">**Workaround:**</span></span>

<span data-ttu-id="e19e6-112">Ukládejte hesla jako nešifrovaný text pomocí možnosti [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="e19e6-112">Store passwords in clear text using the [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="e19e6-113">Chyba při instalaci balíčků pomocí NuGet 3,4, 3.4.1</span><span class="sxs-lookup"><span data-stu-id="e19e6-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="e19e6-114">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="e19e6-114">**Problem:**</span></span>

<span data-ttu-id="e19e6-115">V NuGet 3,4 a 3.4.1 při použití doplňku NuGet nejsou žádné zdroje hlášeny jako dostupné a v okně Konfigurace nemůžete přidávat nové zdroje.</span><span class="sxs-lookup"><span data-stu-id="e19e6-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="e19e6-116">Výsledek je podobný následujícímu obrázku:</span><span class="sxs-lookup"><span data-stu-id="e19e6-116">The result is similar to the image below:</span></span>

![Konfigurace NuGet bez zdrojů](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="e19e6-118">Soubor `NuGet.Config` ve složce `%AppData%\NuGet\` (Windows) nebo `~/.nuget/` (Mac/Linux) byl omylem vyprázdněn.</span><span class="sxs-lookup"><span data-stu-id="e19e6-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="e19e6-119">Chcete-li tento problém vyřešit: Ukončete aplikaci Visual Studio (v systému Windows, pokud je k dispozici), odstraňte soubor `NuGet.Config` a operaci opakujte.</span><span class="sxs-lookup"><span data-stu-id="e19e6-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="e19e6-120">NuGet vygeneroval novou `NuGet.Config` a měli byste být schopni pokračovat.</span><span class="sxs-lookup"><span data-stu-id="e19e6-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="e19e6-121">Chyba při instalaci balíčků pomocí NuGet 2,7</span><span class="sxs-lookup"><span data-stu-id="e19e6-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="e19e6-122">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="e19e6-122">**Problem:**</span></span>

<span data-ttu-id="e19e6-123">Pokud se při pokusu o instalaci balíčku obsahujícího odkazy na sestavení v NuGet 2,7 nebo vyšší, může se zobrazit chybová zpráva **"vstupní řetězec nebyl ve správném formátu"** , například níže:</span><span class="sxs-lookup"><span data-stu-id="e19e6-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="e19e6-124">To je způsobeno tím, že knihovna typů pro součást `VSLangProj.dll` COM je v systému odregistrována.</span><span class="sxs-lookup"><span data-stu-id="e19e6-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="e19e6-125">K tomu může dojít například v případě, že máte nainstalovanou dvě verze sady Visual Studio vedle sebe a pak odinstalujete starší verzi.</span><span class="sxs-lookup"><span data-stu-id="e19e6-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="e19e6-126">V takovém případě může neúmyslně zrušit registraci výše uvedené knihovny COM.</span><span class="sxs-lookup"><span data-stu-id="e19e6-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="e19e6-127">**Řešení:** :</span><span class="sxs-lookup"><span data-stu-id="e19e6-127">**Solution:**:</span></span>

<span data-ttu-id="e19e6-128">Spusťte tento příkaz z **příkazového řádku se zvýšenými oprávněními** a znovu Zaregistrujte knihovnu typů pro `VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="e19e6-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="e19e6-129">Pokud se příkaz nezdařil, zkontrolujte, zda soubor v tomto umístění existuje.</span><span class="sxs-lookup"><span data-stu-id="e19e6-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="e19e6-130">Další informace o této chybě naleznete v části tato [pracovní položka](https://nuget.codeplex.com/workitem/3609 "Pracovní položka 3609").</span><span class="sxs-lookup"><span data-stu-id="e19e6-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="e19e6-131">Chyba sestavení po aktualizaci balíčku ve VS 2012</span><span class="sxs-lookup"><span data-stu-id="e19e6-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="e19e6-132">Problém: používáte VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="e19e6-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="e19e6-133">Při aktualizaci balíčků NuGet se zobrazí tato zpráva: "jeden nebo víc balíčků se nepovedlo dokončit odinstalací".</span><span class="sxs-lookup"><span data-stu-id="e19e6-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="e19e6-134">a zobrazí se výzva k restartování sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e19e6-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="e19e6-135">Po restartování VS se zobrazí chyby sestavení divné.</span><span class="sxs-lookup"><span data-stu-id="e19e6-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="e19e6-136">Příčinou je, že některé soubory ve starších balíčcích jsou uzamčeny procesem MSBuild na pozadí.</span><span class="sxs-lookup"><span data-stu-id="e19e6-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="e19e6-137">I po restartování VS, proces MSBuild na pozadí stále používá soubory ve starších balíčcích, což způsobuje selhání sestavení.</span><span class="sxs-lookup"><span data-stu-id="e19e6-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="e19e6-138">Opravou je instalace VS 2012 Update, například VS 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="e19e6-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="e19e6-139">Upgrade na nejnovější verzi NuGet ze starší verze způsobí chybu při ověřování podpisu.</span><span class="sxs-lookup"><span data-stu-id="e19e6-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="e19e6-140">Pokud používáte VS 2010 SP1, můžete při pokusu o upgrade NuGetu v případě, že máte nainstalovanou starší verzi, použít následující chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="e19e6-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalační program rozšíření sady Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="e19e6-142">Při prohlížení protokolů se může zobrazit zmínka o `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="e19e6-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="e19e6-143">Aby k tomu nedošlo, je k dispozici [oprava hotfix sady Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) , kterou můžete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="e19e6-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="e19e6-144">Alternativně je alternativním řešením jednoduše odinstalovat NuGet (při spuštění sady Visual Studio jako správce) a pak ji nainstalovat z galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="e19e6-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span> <span data-ttu-id="e19e6-145">Další informace naleznete v tématu <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="e19e6-145">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="e19e6-146">Konzola správce balíčků vyvolá výjimku, pokud je nainstalován i doplněk pro odrážející sadu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e19e6-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="e19e6-147">Při spuštění konzoly Správce balíčků můžete spustit následující zprávu o výjimce, pokud máte nainstalovanou odrážející doplněk VS.</span><span class="sxs-lookup"><span data-stu-id="e19e6-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="e19e6-148">nebo</span><span class="sxs-lookup"><span data-stu-id="e19e6-148">or</span></span>

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

<span data-ttu-id="e19e6-149">Kontaktovali jsme autora doplňku v hodlá řešení problému.</span><span class="sxs-lookup"><span data-stu-id="e19e6-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="e19e6-150">Aktualizace: ověřili jsme, že nejnovější verze Odrazer, 6,5, už tuto výjimku nezpůsobuje v konzole nástroje.</span><span class="sxs-lookup"><span data-stu-id="e19e6-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="e19e6-151">Spuštění konzoly Správce balíčků se nezdařilo s výjimkou ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="e19e6-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="e19e6-152">Tyto chyby se můžou zobrazit při pokusu o otevření konzoly Správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="e19e6-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="e19e6-153">Pokud ano, opravte je podle řešení [v tématu StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) .</span><span class="sxs-lookup"><span data-stu-id="e19e6-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="e19e6-154">Dialogové okno Přidat knihovnu balíčků vyvolá výjimku, pokud řešení obsahuje projekt InstallShield Limited Edition</span><span class="sxs-lookup"><span data-stu-id="e19e6-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="e19e6-155">Zjistili jsme, že pokud vaše řešení obsahuje jeden nebo více projektů InstallShield s omezeným voláním, dialogové okno **přidat knihovnu balíčků** vyvolá při otevření výjimku.</span><span class="sxs-lookup"><span data-stu-id="e19e6-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="e19e6-156">V současné době zatím neexistuje alternativní řešení s výjimkou odebrání projektů InstallShield nebo jejich uvolnění.</span><span class="sxs-lookup"><span data-stu-id="e19e6-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="e19e6-157">Tlačítko odinstalovat šedé?</span><span class="sxs-lookup"><span data-stu-id="e19e6-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="e19e6-158">NuGet vyžaduje oprávnění správce k instalaci/odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="e19e6-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="e19e6-159">Pokud se pokusíte odinstalovat NuGet pomocí Správce rozšíření sady Visual Studio, můžete si všimnout, že je tlačítko odinstalovat zakázané.</span><span class="sxs-lookup"><span data-stu-id="e19e6-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="e19e6-160">NuGet vyžaduje přístup správce k instalaci a odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="e19e6-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="e19e6-161">Pokud chcete rozšíření odinstalovat, znovu spusťte Visual Studio jako správce.</span><span class="sxs-lookup"><span data-stu-id="e19e6-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="e19e6-162">NuGet nevyžaduje přístup správce k jeho použití.</span><span class="sxs-lookup"><span data-stu-id="e19e6-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="e19e6-163">Konzola správce balíčků při otevření v systému Windows XP dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="e19e6-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="e19e6-164">Co je?</span><span class="sxs-lookup"><span data-stu-id="e19e6-164">What's wrong?</span></span>

<span data-ttu-id="e19e6-165">NuGet vyžaduje prostředí PowerShell 2,0 Runtime.</span><span class="sxs-lookup"><span data-stu-id="e19e6-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="e19e6-166">Windows XP ve výchozím nastavení nemá PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="e19e6-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="e19e6-167">Modul runtime PowerShellu 2,0 si můžete stáhnout z <https://support.microsoft.com/kb/968929>.</span><span class="sxs-lookup"><span data-stu-id="e19e6-167">You can download the Powershell 2.0 runtime from <https://support.microsoft.com/kb/968929>.</span></span> <span data-ttu-id="e19e6-168">Po instalaci nástroje restartujte sadu Visual Studio a měli byste být schopni spustit konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="e19e6-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="e19e6-169">Po otevření konzoly Správce balíčků dojde k chybě sady Visual Studio 2010 SP1 Beta.</span><span class="sxs-lookup"><span data-stu-id="e19e6-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="e19e6-170">Pokud jste nainstalovali sadu Visual Studio 2010 SP1 Beta verze, můžete si všimnout, že pokud ponecháte konzolu Správce balíčků otevřenou a zavřete Visual Studio, dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="e19e6-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="e19e6-171">Toto je známý problém sady Visual Studio a bude opraven ve verzi SP1 RTM.</span><span class="sxs-lookup"><span data-stu-id="e19e6-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="e19e6-172">Prozatím tuto chybu ignorujte nebo odinstalujte SP1 Beta, pokud můžete.</span><span class="sxs-lookup"><span data-stu-id="e19e6-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="e19e6-173">Element ' metadata '... Vyvolá se neplatná výjimka podřízeného elementu.</span><span class="sxs-lookup"><span data-stu-id="e19e6-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="e19e6-174">Pokud jste nainstalovali balíčky vytvořené pomocí předběžné verze NuGet, může se zobrazit chybová zpráva s oznámením, že "element" metadata "v oboru názvů" schemas.microsoft.com/packaging/2010/07/nuspec.xsd "má neplatný podřízený element" při spuštění verze RTM balíčku NuGet s tímto projektem.</span><span class="sxs-lookup"><span data-stu-id="e19e6-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="e19e6-175">Každý balíček musíte odinstalovat a znovu nainstalovat pomocí verze RTM balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="e19e6-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="e19e6-176">Při pokusu o instalaci nebo odinstalaci dojde k chybě "nelze vytvořit soubor, pokud tento soubor již existuje".</span><span class="sxs-lookup"><span data-stu-id="e19e6-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="e19e6-177">Z nějakého důvodu můžou rozšíření sady Visual Studio získat ve stavu divné, kdy jste odinstalovali rozšíření VSIX, ale některé soubory zůstaly na pozadí.</span><span class="sxs-lookup"><span data-stu-id="e19e6-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="e19e6-178">Alternativní řešení tohoto problému:</span><span class="sxs-lookup"><span data-stu-id="e19e6-178">To work around this issue:</span></span>

1. <span data-ttu-id="e19e6-179">Ukončení sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e19e6-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="e19e6-180">Otevřete následující složku (může to být na jiné jednotce počítače).</span><span class="sxs-lookup"><span data-stu-id="e19e6-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="e19e6-181">C:\Program Files (x86) \Microsoft Visual Studio 10.0 \ Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<verze > </span><span class="sxs-lookup"><span data-stu-id="e19e6-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version></span></span>\

1. <span data-ttu-id="e19e6-182">Odstraňte všechny soubory s příponou *. Deleteme* .</span><span class="sxs-lookup"><span data-stu-id="e19e6-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="e19e6-183">Znovu otevřít Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e19e6-183">Re-open Visual Studio</span></span>

<span data-ttu-id="e19e6-184">Po provedení tohoto postupu byste měli být schopní pokračovat.</span><span class="sxs-lookup"><span data-stu-id="e19e6-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="e19e6-185">Ve výjimečných případech se při kompilování se zapnutou analýzou kódu vynutí chyba.</span><span class="sxs-lookup"><span data-stu-id="e19e6-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="e19e6-186">Pokud nainstalujete FluentNHibernate s konzolou správce balíčků a potom zkompilujete projekt pomocí funkce Analýza kódu, může se zobrazit následující chyba.</span><span class="sxs-lookup"><span data-stu-id="e19e6-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="e19e6-187">Ve výchozím nastavení FluentNHibernate vyžaduje NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="e19e6-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="e19e6-188">Nicméně návrh NuGet nainstaluje do projektu NHibernate 3.0.0.4000 a přidá odpovídající přesměrování vazby, aby fungoval.</span><span class="sxs-lookup"><span data-stu-id="e19e6-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="e19e6-189">Projekt bude zkompilován pouze v případě, že analýza kódu není zapnuta.</span><span class="sxs-lookup"><span data-stu-id="e19e6-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="e19e6-190">Na rozdíl od kompilátoru Nástroj Analýza kódu nesprávně dodržuje přesměrování vazby na použití 3.0.0.4000 namísto 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="e19e6-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="e19e6-191">Problém můžete obejít buď instalací NHibernate 3.0.0.2001, nebo oznámením, že nástroj pro analýzu kódu se chová stejně jako kompilátor, a to následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="e19e6-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="e19e6-192">Přejít na *%ProgramFiles%\Microsoft Visual Studio 10.0 \ Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="e19e6-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="e19e6-193">Otevřete soubor FxCopCmd. exe. config a změňte `AssemblyReferenceResolveMode` z `StrongName` na `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="e19e6-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="e19e6-194">Uložte změnu a znovu sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="e19e6-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="e19e6-195">Příkaz Write-Error nefunguje v průběhu instalace. ps1/Uninstall. ps1/init. ps1</span><span class="sxs-lookup"><span data-stu-id="e19e6-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="e19e6-196">Toto je známý problém.</span><span class="sxs-lookup"><span data-stu-id="e19e6-196">This is a known issue.</span></span> <span data-ttu-id="e19e6-197">Namísto volání metody Write-Error Zkuste zavolat throw.</span><span class="sxs-lookup"><span data-stu-id="e19e6-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="e19e6-198">Instalace NuGet s omezeným přístupem v systému Windows 2003 může selhat se sadou Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e19e6-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="e19e6-199">Když se pokusíte nainstalovat NuGet pomocí Správce rozšíření sady Visual Studio a neběží jako správce, zobrazí se &#8220;dialogové okno&#8221; spustit jako se zaškrtávacím políčkem s označením &#8220;spustit tento program s omezeným přístupem&#8221; , který je ve výchozím nastavení zaškrtnutý.</span><span class="sxs-lookup"><span data-stu-id="e19e6-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Dialogové okno Spustit jako s omezením](./media/RunAsRestricted.png)

<span data-ttu-id="e19e6-201">Kliknutím na OK s zaškrtnutými chybami sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e19e6-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="e19e6-202">Než nainstalujete NuGet, nezapomeňte tuto možnost zrušit.</span><span class="sxs-lookup"><span data-stu-id="e19e6-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="e19e6-203">Nejde odinstalovat NuGet pro nástroje Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e19e6-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="e19e6-204">Windows Phone nástroje nepodporují Správce rozšíření sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e19e6-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="e19e6-205">Chcete-li odinstalovat NuGet, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="e19e6-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="e19e6-206">Změna velkých a malých písmen ID balíčků NuGet – obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="e19e6-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="e19e6-207">Jak je popsáno u [tohoto problému GitHubu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), změna velkých a malých písmen balíčků NuGet je možné provést prostřednictvím podpory NuGet, ale způsobí komplikace při obnovení balíčku pro uživatele, kteří mají existující, různě použita, balíčky ve složce *globálních balíčků* .</span><span class="sxs-lookup"><span data-stu-id="e19e6-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="e19e6-208">Doporučujeme, abyste požádali o změnu velikosti písmen, pokud máte způsob, jak komunikovat se stávajícími uživateli balíčku o přerušení, ke kterému může dojít při obnovení balíčku při sestavení.</span><span class="sxs-lookup"><span data-stu-id="e19e6-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="e19e6-209">Hlášení problémů s</span><span class="sxs-lookup"><span data-stu-id="e19e6-209">Reporting issues</span></span>

<span data-ttu-id="e19e6-210">Pokud chcete ohlásit problémy NuGet, navštivte [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="e19e6-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
