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
# <a name="known-issues-with-nuget"></a><span data-ttu-id="5a46d-103">Známé problémy s NuGet</span><span class="sxs-lookup"><span data-stu-id="5a46d-103">Known Issues with NuGet</span></span>

<span data-ttu-id="5a46d-104">Jedná se nejčastěji používané známé problémy s NuGet, které jsou hlášeny opakovaně.</span><span class="sxs-lookup"><span data-stu-id="5a46d-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="5a46d-105">Pokud máte potíže s instalací NuGet nebo správu balíčků, věnujte prosím najdete pomocí těchto známých problémů a jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="5a46d-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="5a46d-106">Od verze NuGet 4.0, známé problémy jsou součástí příslušné poznámky.</span><span class="sxs-lookup"><span data-stu-id="5a46d-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="5a46d-107">Problémy s ověřováním pomocí NuGet informační kanály ve službě VSTS s nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="5a46d-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="5a46d-108">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="5a46d-108">**Problem:**</span></span>

<span data-ttu-id="5a46d-109">Pokud použijeme následující příkaz k uložení přihlašovacích údajů, jsme skončit double šifrováním osobní přístupový Token.</span><span class="sxs-lookup"><span data-stu-id="5a46d-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="5a46d-110">$PAT = "Svůj osobní přístupový token" $Feed = "url".\nuget.exe zdroje přidat – název testu-$UserName $Feed zdroje - UserName-$PAT heslo</span><span class="sxs-lookup"><span data-stu-id="5a46d-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="5a46d-111">**Alternativní řešení:**</span><span class="sxs-lookup"><span data-stu-id="5a46d-111">**Workaround:**</span></span>

<span data-ttu-id="5a46d-112">Store hesla v nešifrovaném textu pomocí [- StorePasswordInClearText](../tools/cli-ref-sources.md) možnost.</span><span class="sxs-lookup"><span data-stu-id="5a46d-112">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="5a46d-113">Chyba při instalaci balíčků pomocí NuGet 3.4, 3.4.1</span><span class="sxs-lookup"><span data-stu-id="5a46d-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="5a46d-114">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="5a46d-114">**Problem:**</span></span>

<span data-ttu-id="5a46d-115">NuGet 3.4 a 3.4.1 při použití – v NuGet, jsou hlášeny jako k dispozici žádné zdroje a nejde přidat nové zdroje v okně konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5a46d-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="5a46d-116">Výsledkem je podobně jako na následujícím obrázku:</span><span class="sxs-lookup"><span data-stu-id="5a46d-116">The result is similar to the image below:</span></span>

![NuGet config s žádné zdroje](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="5a46d-118">`NuGet.Config` Ve vašich `%AppData%\NuGet\` (Windows) nebo `~/.nuget/` (Mac/Linux) složka omylem byla vyprázdněna.</span><span class="sxs-lookup"><span data-stu-id="5a46d-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="5a46d-119">Chcete-li tento problém vyřešit: Zavřete sadu Visual Studio (ve Windows, pokud je k dispozici), odstranit `NuGet.Config` soubor a zkuste operaci zopakovat.</span><span class="sxs-lookup"><span data-stu-id="5a46d-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="5a46d-120">NuGet vygeneroval nový `NuGet.Config` a musí být možné pokračovat.</span><span class="sxs-lookup"><span data-stu-id="5a46d-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="5a46d-121">Chyba při instalaci balíčků pomocí NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="5a46d-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="5a46d-122">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="5a46d-122">**Problem:**</span></span>

<span data-ttu-id="5a46d-123">NuGet 2.7 nebo výše, při pokusu nainstalovat libovolný balíček, který obsahuje odkazy na sestavení, můžete obdržet chybovou zprávu **"vstupní řetězec nemá správný formát."** , třeba níže:</span><span class="sxs-lookup"><span data-stu-id="5a46d-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="5a46d-124">To je způsobeno knihovnu typů pro `VSLangProj.dll` komponenty modelu COM, jejíž registrace se ruší ve vašem systému.</span><span class="sxs-lookup"><span data-stu-id="5a46d-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="5a46d-125">K tomu může dojít například až budete mít dvě verze sady Visual Studio nainstalovat vedle sebe a potom odinstalujte starší verzi.</span><span class="sxs-lookup"><span data-stu-id="5a46d-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="5a46d-126">To může nechtěně zrušit registraci výše uvedené knihovny COM.</span><span class="sxs-lookup"><span data-stu-id="5a46d-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="5a46d-127">**Řešení:**:</span><span class="sxs-lookup"><span data-stu-id="5a46d-127">**Solution:**:</span></span>

<span data-ttu-id="5a46d-128">Spusťte tento příkaz z **řádku se zvýšenými oprávněními** znovu zaregistrovat knihovnu typů pro `VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="5a46d-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="5a46d-129">Pokud se příkaz nezdaří, zkontrolujte, jestli soubor existuje v dané oblasti.</span><span class="sxs-lookup"><span data-stu-id="5a46d-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="5a46d-130">Další informace o této chybě najdete v tomto [pracovní položku](https://nuget.codeplex.com/workitem/3609 "pracovní položku 3609").</span><span class="sxs-lookup"><span data-stu-id="5a46d-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="5a46d-131">Selhání sestavení po aktualizaci balíčku v VS 2012</span><span class="sxs-lookup"><span data-stu-id="5a46d-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="5a46d-132">Problém: používáte VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="5a46d-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="5a46d-133">Při aktualizaci balíčků NuGet, se zobrazí tato zpráva: "jeden nebo více balíčků nešlo dokončit, odinstalovat."</span><span class="sxs-lookup"><span data-stu-id="5a46d-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="5a46d-134">a zobrazí se výzva k restartování sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a46d-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="5a46d-135">Po restartu VS, dojde k chybám divné sestavení.</span><span class="sxs-lookup"><span data-stu-id="5a46d-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="5a46d-136">Příčinou je, že určité soubory do staré balíčků uzamkla MSBuild proces na pozadí.</span><span class="sxs-lookup"><span data-stu-id="5a46d-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="5a46d-137">I po restartování VS pozadí procesu MSBuild dál používá soubory do staré balíčků způsobuje selhání sestavení.</span><span class="sxs-lookup"><span data-stu-id="5a46d-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="5a46d-138">Opravou je instalace VS 2012 aktualizace, například VS 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="5a46d-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="5a46d-139">Upgrade na nejnovější NuGet ze starší verze způsobí chybu ověření podpisu</span><span class="sxs-lookup"><span data-stu-id="5a46d-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="5a46d-140">Pokud spustíte VS 2010 SP1, můžete narazit na následující chybová zpráva při pokusech o upgradu Nugetu, pokud máte nainstalovaný starší verze.</span><span class="sxs-lookup"><span data-stu-id="5a46d-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalační služba rozšíření sady Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="5a46d-142">Při prohlížení protokolů, může se zobrazit poznámku o `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="5a46d-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="5a46d-143">Pokud chcete zabránit tím, že je [oprava hotfix Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) můžete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="5a46d-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="5a46d-144">Alternativním řešením je můžete také jednoduše odinstalovat NuGet (při spuštění sady Visual Studio jako správce) a nainstalujte ho z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="5a46d-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="5a46d-145">Zobrazit [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Další informace.</span><span class="sxs-lookup"><span data-stu-id="5a46d-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="5a46d-146">Konzola správce balíčků vyvolá výjimku, když Reflector Visual Studio Add-In je také nainstalována.</span><span class="sxs-lookup"><span data-stu-id="5a46d-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="5a46d-147">Při spuštění konzoly Správce balíčků, můžete jej spustit do následující zpráva o výjimce Pokud máte Reflector VS doplněk nainstalovaný.</span><span class="sxs-lookup"><span data-stu-id="5a46d-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="5a46d-148">or</span><span class="sxs-lookup"><span data-stu-id="5a46d-148">or</span></span>

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

<span data-ttu-id="5a46d-149">Kontaktovali jsme autorem tohoto doplňku v šancí práce na řešení.</span><span class="sxs-lookup"><span data-stu-id="5a46d-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="5a46d-150">Aktualizace: Jsme ověřili, že nejnovější verze Reflector, 6.5, již nezpůsobuje, že tato výjimka v konzole.</span><span class="sxs-lookup"><span data-stu-id="5a46d-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="5a46d-151">Konzola správce balíčků otevírání selže s výjimkou ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="5a46d-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="5a46d-152">Při pokusu o otevření konzole Správce balíčků, může se zobrazit tyto chyby:</span><span class="sxs-lookup"><span data-stu-id="5a46d-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="5a46d-153">Pokud ano, postupujte podle řešení [popsané na StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) a opravte je.</span><span class="sxs-lookup"><span data-stu-id="5a46d-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="5a46d-154">Dialogové okno Přidat odkaz na balíček knihovny vyvolá výjimku, pokud řešení obsahuje projekt InstallShield Limited Edition</span><span class="sxs-lookup"><span data-stu-id="5a46d-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="5a46d-155">Jste zjistili jsme, že pokud vaše řešení obsahuje nejmíň jeden projekt InstallShield Limited Edition, **přidat odkaz na balíček knihovny** vyvolá výjimku při otevření dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="5a46d-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="5a46d-156">Aktuálně neexistuje žádné alternativní řešení ještě s výjimkou odebírání projektů InstallShield nebo jejich uvolnění.</span><span class="sxs-lookup"><span data-stu-id="5a46d-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="5a46d-157">Odinstalovat tlačítko šedě?</span><span class="sxs-lookup"><span data-stu-id="5a46d-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="5a46d-158">NuGet vyžaduje oprávnění správce, aby instalace/odinstalace</span><span class="sxs-lookup"><span data-stu-id="5a46d-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="5a46d-159">Pokud se pokusíte odinstalovat pomocí správce sady Visual Studio rozšíření NuGet, můžete si všimnout, že k dispozici tlačítko odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="5a46d-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="5a46d-160">NuGet vyžaduje přístup správce k instalaci a odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="5a46d-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="5a46d-161">Znovu spusťte Visual Studio jako správce a odinstalujte rozšíření.</span><span class="sxs-lookup"><span data-stu-id="5a46d-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="5a46d-162">NuGet nevyžaduje přístup správce k jeho použití.</span><span class="sxs-lookup"><span data-stu-id="5a46d-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="5a46d-163">Když otevřete ve Windows XP dojde k chybě konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="5a46d-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="5a46d-164">Co je?</span><span class="sxs-lookup"><span data-stu-id="5a46d-164">What's wrong?</span></span>

<span data-ttu-id="5a46d-165">NuGet vyžaduje modul runtime Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="5a46d-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="5a46d-166">Windows XP, nemá ve výchozím nastavení, prostředí Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="5a46d-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="5a46d-167">Můžete si stáhnout modul runtime Powershell 2.0 z [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="5a46d-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="5a46d-168">Po instalaci, restartujte Visual Studio a byste měli používat konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="5a46d-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="5a46d-169">Visual Studio 2010 SP1 Beta chyby při ukončení, pokud je otevřená Konzola správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="5a46d-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="5a46d-170">Pokud jste nainstalovali Visual Studio 2010 SP1 Beta, můžete si všimnout, že pokud zůstat otevřeno, konzola Správce balíčků a zavřete sadu Visual Studio, jeho dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="5a46d-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="5a46d-171">Toto je známý problém nástroje Visual Studio a bude vyřešen v aktualizaci SP1 RTM verze.</span><span class="sxs-lookup"><span data-stu-id="5a46d-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="5a46d-172">Prozatím ignorovat selhání nebo odinstalovat beta verzi SP1, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="5a46d-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="5a46d-173">Element 'metadat'... má neplatný podřízený element výjimka nastane</span><span class="sxs-lookup"><span data-stu-id="5a46d-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="5a46d-174">Pokud jste nainstalovali balíčky sestavené s předběžnou verzi verzi Nugetu, chybová zpráva s oznámením "element"metadat' v oboru názvů "schemas.microsoft.com/packaging/2010/07/nuspec.xsd" má neplatný podřízený element"může dojít při spuštění verzi RTM verze balíčku nuget s tímto projektem.</span><span class="sxs-lookup"><span data-stu-id="5a46d-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="5a46d-175">Budete muset odinstalovat a znovu nainstalovat každý balíček pomocí RTM verze balíčku nuget.</span><span class="sxs-lookup"><span data-stu-id="5a46d-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="5a46d-176">Pokus o instalaci nebo odinstalaci výsledkem chyba "Nelze vytvořit soubor, který již existuje."</span><span class="sxs-lookup"><span data-stu-id="5a46d-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="5a46d-177">Z nějakého důvodu rozšíření sady Visual Studio můžete získat v divné stavu, ve kterém jste odinstalovat rozšíření VSIX, ale některé soubory byly zachovají.</span><span class="sxs-lookup"><span data-stu-id="5a46d-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="5a46d-178">Alternativní řešení tohoto problému:</span><span class="sxs-lookup"><span data-stu-id="5a46d-178">To work around this issue:</span></span>

1. <span data-ttu-id="5a46d-179">Ukončení sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a46d-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="5a46d-180">Otevřete následující složku (může být na jinou jednotku na počítači)</span><span class="sxs-lookup"><span data-stu-id="5a46d-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="5a46d-181">C:\Program soubory (x86) \Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Správce balíčků Corporation\NuGet\<verze > \\</span><span class="sxs-lookup"><span data-stu-id="5a46d-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="5a46d-182">Odstranit všechny soubory s *.deleteme* rozšíření.</span><span class="sxs-lookup"><span data-stu-id="5a46d-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="5a46d-183">Znovu otevřete Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a46d-183">Re-open Visual Studio</span></span>

<span data-ttu-id="5a46d-184">Po provedení těchto kroků, by měl být pokračovat.</span><span class="sxs-lookup"><span data-stu-id="5a46d-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="5a46d-185">Ve výjimečných případech kompilaci pomocí analýzy kódu zapnuté způsobí chybu.</span><span class="sxs-lookup"><span data-stu-id="5a46d-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="5a46d-186">Může být zobrazí následující chyba, pokud nainstaluje FluentNHibernate pomocí konzole Správce balíčků a poté zkompilovat váš projekt s "Analýzu kódu" zapnuté.</span><span class="sxs-lookup"><span data-stu-id="5a46d-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="5a46d-187">Ve výchozím nastavení vyžaduje FluentNHibernate NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="5a46d-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="5a46d-188">Ale záměrné NuGet se do svého projektu nainstalovat NHibernate 3.0.0.4000 a přidat že příslušnou datovou vazbu přesměruje tak, že bude fungovat.</span><span class="sxs-lookup"><span data-stu-id="5a46d-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="5a46d-189">Projekt zkompiluje bez potíží, pokud analýza kódu není zapnutá.</span><span class="sxs-lookup"><span data-stu-id="5a46d-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="5a46d-190">Na rozdíl od kompilátor nástroj pro analýzu kódu není postupujte z správně 3.0.0.4000 nahrazujícím 3.0.0.2001 přesměrování vazby.</span><span class="sxs-lookup"><span data-stu-id="5a46d-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="5a46d-191">Můžete tak buď instalaci NHibernate 3.0.0.2001 tento problém obejít nebo řekněte nástroj pro analýzu kódu se chová stejně jako kompilátor následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="5a46d-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="5a46d-192">Přejděte na *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static analýzy Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="5a46d-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="5a46d-193">Otevřete FxCopCmd.exe.config a změňte `AssemblyReferenceResolveMode` z `StrongName` k `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="5a46d-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="5a46d-194">Změnu uložíte a znovu sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="5a46d-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="5a46d-195">Chyba při zápisu příkaz nefunguje uvnitř install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="5a46d-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="5a46d-196">Jedná se o známý problém.</span><span class="sxs-lookup"><span data-stu-id="5a46d-196">This is a known issue.</span></span> <span data-ttu-id="5a46d-197">Namísto volání Write-Error, zkuste volat vyvolání výjimky.</span><span class="sxs-lookup"><span data-stu-id="5a46d-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="5a46d-198">Instalace NuGet s omezeným přístupem na Windows serveru 2003, můžete chybu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a46d-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="5a46d-199">Při pokusu o instalaci balíčku NuGet pomocí Správce rozšíření sady Visual Studio a není spuštěna jako správce &#8220;spustit jako&#8221; zobrazí dialogové okno s zaškrtávací políčko s popiskem &#8220;spustit tento program s omezeným přístupem&#8221; vráceno uživatelem Výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="5a46d-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Spustit jako s omezeným přístupem dialogového okna](./media/RunAsRestricted.png)

<span data-ttu-id="5a46d-201">Kliknutím na tlačítko OK se specifikací zaškrtnuto, dojde k chybě sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a46d-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="5a46d-202">Ujistěte se, že zrušit zaškrtnutí této možnosti před instalací NuGet.</span><span class="sxs-lookup"><span data-stu-id="5a46d-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="5a46d-203">Nelze odinstalovat nástroje NuGet pro Windows Phone</span><span class="sxs-lookup"><span data-stu-id="5a46d-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="5a46d-204">Nástroje Windows Phone nemá podporu doplňku Správce rozšíření pro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a46d-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="5a46d-205">Pokud chcete odinstalovat NuGet, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="5a46d-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="5a46d-206">Změna velikosti písmen ID balíčku NuGet přestane fungovat obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="5a46d-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="5a46d-207">Jak Dlouze na [tento problém Githubu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), změna velikosti písmen balíčků NuGet je možné díky podpoře NuGet, ale způsobí komplikace během obnovení balíčků pro uživatele, kteří mají stávající, jinak malými a velkými písmeny, balíčky v jejich *global-packages* složky.</span><span class="sxs-lookup"><span data-stu-id="5a46d-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="5a46d-208">Doporučujeme pouze žádosti o změnu velikosti písmen, až budete mít způsob, jak komunikovat s existující uživateli vašeho balíčku o přerušení, ke kterému může dojít k jejich obnovení balíčku čas sestavení.</span><span class="sxs-lookup"><span data-stu-id="5a46d-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="5a46d-209">Hlášení problémů s</span><span class="sxs-lookup"><span data-stu-id="5a46d-209">Reporting issues</span></span>

<span data-ttu-id="5a46d-210">K hlášení problémů NuGet, navštivte [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="5a46d-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
