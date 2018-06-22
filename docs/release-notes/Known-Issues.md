---
title: Známé problémy
description: Známé problémy s NuGet, včetně ověřování, instalace balíčku a nástroje.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f170f377a3394694e953a794f2c814388656c21
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822016"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="d14ae-103">Známé problémy s nástrojem NuGet</span><span class="sxs-lookup"><span data-stu-id="d14ae-103">Known Issues with NuGet</span></span>

<span data-ttu-id="d14ae-104">Toto jsou nejběžnější známé problémy s NuGet opakovaně hlášený.</span><span class="sxs-lookup"><span data-stu-id="d14ae-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="d14ae-105">Pokud máte potíže s instalací NuGet nebo spravovat balíčky, proveďte prosím vzhled prostřednictvím těchto známé problémy a jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="d14ae-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="d14ae-106">Od verze NuGet 4.0, známé problémy jsou součástí příslušného poznámky.</span><span class="sxs-lookup"><span data-stu-id="d14ae-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="d14ae-107">Problémy s ověřením s NuGet kanály v služby VSTS s nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="d14ae-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="d14ae-108">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="d14ae-108">**Problem:**</span></span>

<span data-ttu-id="d14ae-109">Když jsme k uložení pověření, použijte následující příkaz, jsme skončili dvojité šifrování tokenu osobní přístup.</span><span class="sxs-lookup"><span data-stu-id="d14ae-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="d14ae-110">$PAT = "Váš osobní přístupový token" $Feed = "url".\nuget.exe zdroje přidat – název Test-zdroj $Feed - UserName $UserName-$PAT heslo</span><span class="sxs-lookup"><span data-stu-id="d14ae-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="d14ae-111">**Alternativní řešení:**</span><span class="sxs-lookup"><span data-stu-id="d14ae-111">**Workaround:**</span></span>

<span data-ttu-id="d14ae-112">Uložení hesla v nešifrovaném textu pomocí [- StorePasswordInClearText](../tools/cli-ref-sources.md) možnost.</span><span class="sxs-lookup"><span data-stu-id="d14ae-112">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="d14ae-113">Chyba při instalaci balíčků s NuGet 3.4, 3.4.1</span><span class="sxs-lookup"><span data-stu-id="d14ae-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="d14ae-114">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="d14ae-114">**Problem:**</span></span>

<span data-ttu-id="d14ae-115">V NuGet 3.4 a 3.4.1 při použití doplňku NuGet, jsou hlášeny jako dostupné žádné zdroje a nemůžete přidat nového zdroje v okně konfigurace.</span><span class="sxs-lookup"><span data-stu-id="d14ae-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="d14ae-116">Výsledkem je podobná následující obrázek:</span><span class="sxs-lookup"><span data-stu-id="d14ae-116">The result is similar to the image below:</span></span>

![Konfigurace NuGet se žádné zdroje](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="d14ae-118">`NuGet.Config` Ve vaší `%AppData%\NuGet\` (Windows) nebo `~/.nuget/` (Mac/Linux) omylem vyprázdnění složky.</span><span class="sxs-lookup"><span data-stu-id="d14ae-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="d14ae-119">Chcete-li: zavřete Visual Studio (v systému Windows, pokud je k dispozici), odstraňte `NuGet.Config` souboru a operaci opakujte.</span><span class="sxs-lookup"><span data-stu-id="d14ae-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="d14ae-120">NuGet vygeneroval nový `NuGet.Config` a mělo by být možné pokračovat.</span><span class="sxs-lookup"><span data-stu-id="d14ae-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="d14ae-121">Chyba při instalaci balíčků s NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="d14ae-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="d14ae-122">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="d14ae-122">**Problem:**</span></span>

<span data-ttu-id="d14ae-123">V NuGet 2.7 nebo vyšší, když se pokusíte nainstalovat libovolný balíček, který obsahuje odkazy na sestavení, může se zobrazit chybová zpráva **"vstupní řetězec nebyla ve správném formátu."** , například níže:</span><span class="sxs-lookup"><span data-stu-id="d14ae-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="d14ae-124">Je to způsobeno knihovnu typů pro `VSLangProj.dll` komponenty modelu COM rušena ve vašem systému.</span><span class="sxs-lookup"><span data-stu-id="d14ae-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="d14ae-125">K tomu může dojít, například když máte dvě verze sady Visual Studio nainstalované souběžně sdílená a pak odinstalujte starší verzi.</span><span class="sxs-lookup"><span data-stu-id="d14ae-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="d14ae-126">Díky tomu může nechtěně registraci výše uvedené knihovny COM.</span><span class="sxs-lookup"><span data-stu-id="d14ae-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="d14ae-127">**Řešení:**:</span><span class="sxs-lookup"><span data-stu-id="d14ae-127">**Solution:**:</span></span>

<span data-ttu-id="d14ae-128">Spusťte tento příkaz z **řádku se zvýšenými oprávněními** znovu zaregistrovat knihovnu typů pro `VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="d14ae-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="d14ae-129">Pokud se příkaz nezdaří, zkontrolujte, zda soubor existuje v tomto umístění.</span><span class="sxs-lookup"><span data-stu-id="d14ae-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="d14ae-130">Další informace o této chybě naleznete v tématu to [pracovní položka](https://nuget.codeplex.com/workitem/3609 "pracovní položka 3609").</span><span class="sxs-lookup"><span data-stu-id="d14ae-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="d14ae-131">Chyba sestavení po aktualizace balíčku v VS 2012</span><span class="sxs-lookup"><span data-stu-id="d14ae-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="d14ae-132">Problém: používáte VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="d14ae-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="d14ae-133">Při aktualizaci balíčků NuGet se vám tato zpráva: "jeden nebo více balíčků nelze dokončit, odinstalovat."</span><span class="sxs-lookup"><span data-stu-id="d14ae-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="d14ae-134">a zobrazí se výzva k restartování sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d14ae-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="d14ae-135">Po restartování VS, dojde k chybám divné sestavení.</span><span class="sxs-lookup"><span data-stu-id="d14ae-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="d14ae-136">Příčinou je, některé soubory v původním balíčcích je uzamčený MSBuild proces na pozadí.</span><span class="sxs-lookup"><span data-stu-id="d14ae-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="d14ae-137">I po restartování VS, MSBuild proces na pozadí pořád používají soubory v původním balíčcích způsobuje selhání sestavení.</span><span class="sxs-lookup"><span data-stu-id="d14ae-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="d14ae-138">Je k instalaci aktualizace produktu VS 2012, například VS 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="d14ae-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="d14ae-139">Upgrade na nejnovější NuGet ze starší verze způsobí chybu ověření podpisu</span><span class="sxs-lookup"><span data-stu-id="d14ae-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="d14ae-140">Pokud používáte VS 2010 SP1, může dojít k následující chybová zpráva při pokusech o upgradu Nugetu, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="d14ae-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalační program rozšíření sady Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="d14ae-142">Při prohlížení protokolů, může se zobrazit poznámku o `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="d14ae-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="d14ae-143">Chcete-li tomu zabránit, že je [oprava hotfix Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) můžete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="d14ae-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="d14ae-144">Alternativně řešením je jednoduše odinstalovat NuGet (při spuštění sady Visual Studio jako správce) a nainstalujte ji z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="d14ae-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="d14ae-145">V tématu [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace.</span><span class="sxs-lookup"><span data-stu-id="d14ae-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="d14ae-146">Konzola správce balíčků vyvolá výjimku, pokud Reflector Visual Studio Add-In je také nainstalován.</span><span class="sxs-lookup"><span data-stu-id="d14ae-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="d14ae-147">Při spuštění konzoly Správce balíčků, můžete spustit do zpráva o výjimce Pokud máte Reflector VS doplněk nainstalován.</span><span class="sxs-lookup"><span data-stu-id="d14ae-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="d14ae-148">or</span><span class="sxs-lookup"><span data-stu-id="d14ae-148">or</span></span>

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

<span data-ttu-id="d14ae-149">Jsme jsme kontaktovat Autor doplněk v šancí pracovat na řešení.</span><span class="sxs-lookup"><span data-stu-id="d14ae-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="d14ae-150">Aktualizace: Jsme ověříte, že nejnovější verzi Reflector, 6.5, už způsobí, že tato výjimka v konzole.</span><span class="sxs-lookup"><span data-stu-id="d14ae-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="d14ae-151">Konzola správce balíčků otevírání selže s výjimkou ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="d14ae-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="d14ae-152">Může se zobrazí tyto chyby při pokusu o otevření konzole Správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="d14ae-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="d14ae-153">Pokud ano, využijte řešení [popsané na StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) opravit je.</span><span class="sxs-lookup"><span data-stu-id="d14ae-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="d14ae-154">Dialogové okno Přidat odkaz na balíček knihovny vyvolá výjimku, pokud řešení obsahuje projekt InstallShield Limited Edition</span><span class="sxs-lookup"><span data-stu-id="d14ae-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="d14ae-155">Myslíme, že by, pokud vaše řešení obsahuje jeden nebo více projekt InstallShield Limited Edition, **přidat odkaz na balíček knihovny** dialogové okno vyvolá výjimku při otevření.</span><span class="sxs-lookup"><span data-stu-id="d14ae-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="d14ae-156">Aktuálně neexistuje žádné řešení ještě kromě odebrání InstallShield projekty nebo jejich uvolnění.</span><span class="sxs-lookup"><span data-stu-id="d14ae-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="d14ae-157">Odinstalovat, tlačítko šedá?</span><span class="sxs-lookup"><span data-stu-id="d14ae-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="d14ae-158">NuGet vyžaduje oprávnění správce pro instalace nebo odinstalace</span><span class="sxs-lookup"><span data-stu-id="d14ae-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="d14ae-159">Pokud se pokusíte odinstalovat NuGet prostřednictvím Správce rozšíření sady Visual Studio, můžete si všimnout, že k dispozici tlačítko odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="d14ae-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="d14ae-160">NuGet potřebuje přístup správce k instalaci a odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="d14ae-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="d14ae-161">Visual Studio spusťte jako správce a odinstalovat rozšíření.</span><span class="sxs-lookup"><span data-stu-id="d14ae-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="d14ae-162">NuGet nevyžaduje přístup správce ke ho použít.</span><span class="sxs-lookup"><span data-stu-id="d14ae-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="d14ae-163">Konzola správce balíčků dojde k chybě při otevírání v systému Windows XP.</span><span class="sxs-lookup"><span data-stu-id="d14ae-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="d14ae-164">Co je?</span><span class="sxs-lookup"><span data-stu-id="d14ae-164">What's wrong?</span></span>

<span data-ttu-id="d14ae-165">NuGet vyžaduje modul runtime Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="d14ae-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="d14ae-166">Windows XP, nemá ve výchozím nastavení, prostředí Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="d14ae-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="d14ae-167">Můžete si stáhnout modul runtime Powershell 2.0 z [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="d14ae-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="d14ae-168">Po instalaci, restartujte Visual Studio a nyní byste měli mít otevřete konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="d14ae-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="d14ae-169">Visual Studio 2010 SP1 Beta chyby při ukončení, pokud Konzola správce balíčků je otevřený.</span><span class="sxs-lookup"><span data-stu-id="d14ae-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="d14ae-170">Pokud jste nainstalovali Visual Studio 2010 SP1 Beta, můžete si všimnout, že pokud zůstat otevřeno, konzola Správce balíčků a zavřete Visual Studio, ho dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="d14ae-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="d14ae-171">Toto je známý problém sady Visual Studio a bude vyřešený v SP1 RTM verzi.</span><span class="sxs-lookup"><span data-stu-id="d14ae-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="d14ae-172">Prozatím ignorovat havárii nebo odinstalovat beta verzi SP1, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="d14ae-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="d14ae-173">Element 'metadata'... má neplatný podřízený element výjimce dochází</span><span class="sxs-lookup"><span data-stu-id="d14ae-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="d14ae-174">Pokud jste nainstalovali balíčky vytvořené s nástroji předběžné verze balíčku nuget, chybová zpráva s oznámením "elementu 'metadata" v oboru názvů "schemas.microsoft.com/packaging/2010/07/nuspec.xsd" má neplatným podřízeným elementem"může dojít při spuštění verzi RTM verze balíčku NuGet s daného projektu.</span><span class="sxs-lookup"><span data-stu-id="d14ae-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="d14ae-175">Budete muset odinstalovat a potom znovu nainstalovat každý balíček pomocí verzi RTM programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="d14ae-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="d14ae-176">Probíhá pokus o instalaci nebo odinstalaci výsledkem chyba "Nelze vytvořit soubor tento soubor již existuje."</span><span class="sxs-lookup"><span data-stu-id="d14ae-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="d14ae-177">Z nějakého důvodu můžete v divné stavu, kde jste odinstalována VSIX rozšíření, ale některé soubory byly ponechány získat rozšíření Visual Studia.</span><span class="sxs-lookup"><span data-stu-id="d14ae-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="d14ae-178">Alternativní řešení tohoto problému:</span><span class="sxs-lookup"><span data-stu-id="d14ae-178">To work around this issue:</span></span>

1. <span data-ttu-id="d14ae-179">Ukončení Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d14ae-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="d14ae-180">Otevřete následující složku (může být na jinou jednotku na počítači)</span><span class="sxs-lookup"><span data-stu-id="d14ae-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="d14ae-181">C:\Program soubory (x86) \Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Správce balíčků Corporation\NuGet\<verze > \\</span><span class="sxs-lookup"><span data-stu-id="d14ae-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="d14ae-182">Odstraní všechny soubory s *.deleteme* rozšíření.</span><span class="sxs-lookup"><span data-stu-id="d14ae-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="d14ae-183">Znovu otevřete Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d14ae-183">Re-open Visual Studio</span></span>

<span data-ttu-id="d14ae-184">Po následujícím postupem, byste měli moci pokračovat.</span><span class="sxs-lookup"><span data-stu-id="d14ae-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="d14ae-185">Ve výjimečných případech kompilujete s analýza kódu zapnutá výsledkem chyba.</span><span class="sxs-lookup"><span data-stu-id="d14ae-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="d14ae-186">Můžete získat následující chyby, pokud nainstaluje FluentNHibernate s konzolou Správce balíčků a pak kompilace projektu s "Analýza kódu" zapnutý.</span><span class="sxs-lookup"><span data-stu-id="d14ae-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="d14ae-187">Ve výchozím nastavení vyžaduje FluentNHibernate NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="d14ae-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="d14ae-188">Ale záměrné NuGet nainstaluje NHibernate 3.0.0.4000 ve vašem projektu a přidat že přesměrování odpovídající vazby tak, že bude fungovat.</span><span class="sxs-lookup"><span data-stu-id="d14ae-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="d14ae-189">Projekt je zkompiluje správně, pokud analýza kódu není zapnutá.</span><span class="sxs-lookup"><span data-stu-id="d14ae-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="d14ae-190">Na rozdíl od kompilátoru nebude nástroj pro analýzu kódu správně podle přesměrování vazby pro použití 3.0.0.4000 místo 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="d14ae-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="d14ae-191">Můžete pomocí buď instalaci NHibernate 3.0.0.2001 tento problém obejít nebo řekněte nástroj pro analýzu kódu se bude chovat stejná jako kompilátor následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d14ae-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="d14ae-192">Přejděte na *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="d14ae-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="d14ae-193">Otevřete FxCopCmd.exe.config a změňte `AssemblyReferenceResolveMode` z `StrongName` k `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="d14ae-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="d14ae-194">Změnu uložíte a znovu sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="d14ae-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="d14ae-195">Chyba při zápisu příkaz nefunguje uvnitř install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="d14ae-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="d14ae-196">Jedná se o známý problém.</span><span class="sxs-lookup"><span data-stu-id="d14ae-196">This is a known issue.</span></span> <span data-ttu-id="d14ae-197">Namísto volání Write-Error, zkuste volání throw.</span><span class="sxs-lookup"><span data-stu-id="d14ae-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="d14ae-198">Instalace NuGet s omezeným přístupem v systému Windows 2003 můžete chybu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d14ae-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="d14ae-199">Při pokusu o instalaci NuGet pomocí Správce rozšíření Visual Studio a není spuštěna jako správce, &#8220;spustit jako&#8221; zobrazí dialog s zaškrtávací políčko s názvem bez přípony &#8220;spuštění tohoto programu s omezeným přístupem&#8221; zkontrolovat nástrojem výchozí.</span><span class="sxs-lookup"><span data-stu-id="d14ae-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Spustit jako dialogové okno s omezeným přístupem](./media/RunAsRestricted.png)

<span data-ttu-id="d14ae-201">Kliknutím na OK s třídou zaškrtnuto, dojde k chybě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d14ae-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="d14ae-202">Ujistěte se, zrušte tuto možnost před instalací NuGet.</span><span class="sxs-lookup"><span data-stu-id="d14ae-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="d14ae-203">Nelze odinstalovat nástroje NuGet pro Windows Phone</span><span class="sxs-lookup"><span data-stu-id="d14ae-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="d14ae-204">Nástroje pro Windows Phone nemá podporu pro správce rozšíření sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d14ae-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="d14ae-205">Chcete-li odinstalovat NuGet, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="d14ae-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="d14ae-206">Změna velikosti písmen ID balíčků NuGet dělí obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="d14ae-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="d14ae-207">Jak je popsáno v length na [potíže Githubu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), změna velikosti písmen balíčků NuGet se dá dělat formou podporu NuGet, ale příčiny komplikace při obnovování balíčků pro uživatele, kteří mají existující, jinak použita, balíčky v jejich *globální balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="d14ae-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="d14ae-208">Doporučujeme, abyste pouze požaduje případu změnu, když máte způsob, jak komunikovat s stávající uživatele vašeho balíčku o přerušení, ke kterému může dojít k jejich obnovení balíčků čase vytvoření buildu.</span><span class="sxs-lookup"><span data-stu-id="d14ae-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="d14ae-209">Hlášení problémů</span><span class="sxs-lookup"><span data-stu-id="d14ae-209">Reporting issues</span></span>

<span data-ttu-id="d14ae-210">Chcete-li nahlásit problém NuGet, navštivte [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="d14ae-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
