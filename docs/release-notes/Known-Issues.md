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
# <a name="known-issues-with-nuget"></a><span data-ttu-id="b920a-103">Známé problémy s NuGet</span><span class="sxs-lookup"><span data-stu-id="b920a-103">Known Issues with NuGet</span></span>

<span data-ttu-id="b920a-104">Jedná se o nejčastější známé problémy s NuGet, které jsou opakovaně hlášeny.</span><span class="sxs-lookup"><span data-stu-id="b920a-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="b920a-105">Pokud máte potíže s instalací NuGet nebo správu balíčků, podívejte se na tyto známé problémy a jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="b920a-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="b920a-106">Počínaje NuGet 4.0 známé problémy jsou součástí příslušné poznámky k verzi.</span><span class="sxs-lookup"><span data-stu-id="b920a-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="b920a-107">Problémy s ověřováním s informačními kanály NuGet v VSTS pomocí nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="b920a-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="b920a-108">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="b920a-108">**Problem:**</span></span>

<span data-ttu-id="b920a-109">Při použití následujícího příkazu k uložení pověření, skončíme dvojité šifrování tokenu osobního přístupu.</span><span class="sxs-lookup"><span data-stu-id="b920a-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="b920a-110">$PAT = "Váš osobní přístupový token" $Feed = "Vaše url" .\nuget.exe zdroje přidat -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="b920a-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="b920a-111">**Alternativní řešení:**</span><span class="sxs-lookup"><span data-stu-id="b920a-111">**Workaround:**</span></span>

<span data-ttu-id="b920a-112">Uklápěte hesla ve stavu prostého textu pomocí volby [-StorePasswordInClearText.](../reference/cli-reference/cli-ref-sources.md)</span><span class="sxs-lookup"><span data-stu-id="b920a-112">Store passwords in clear text using the [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="b920a-113">Při instalaci balíčků s NuGet 3.4, 3.4.1 došlo k chybě.</span><span class="sxs-lookup"><span data-stu-id="b920a-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="b920a-114">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="b920a-114">**Problem:**</span></span>

<span data-ttu-id="b920a-115">V NuGet 3.4 a 3.4.1 při použití doplňku NuGet žádné zdroje jsou hlášeny jako dostupné a nemůžete přidat nové zdroje v okně konfigurace.</span><span class="sxs-lookup"><span data-stu-id="b920a-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="b920a-116">Výsledek je podobný obrázku níže:</span><span class="sxs-lookup"><span data-stu-id="b920a-116">The result is similar to the image below:</span></span>

![Konfigurace NuGet bez zdrojů](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="b920a-118">Soubor `NuGet.Config` ve `%AppData%\NuGet\` složce (Windows) nebo `~/.nuget/` (Mac/Linux) byl omylem vyprázdněn.</span><span class="sxs-lookup"><span data-stu-id="b920a-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="b920a-119">Chcete-li tento problém vyřešit: zavřete Visual `NuGet.Config` Studio (v systému Windows, pokud je to možné), odstraňte soubor a opakujte operaci.</span><span class="sxs-lookup"><span data-stu-id="b920a-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="b920a-120">NuGet vygeneroval nový `NuGet.Config` a měli byste být schopni pokračovat.</span><span class="sxs-lookup"><span data-stu-id="b920a-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="b920a-121">Při instalaci balíčků s aplikací NuGet 2.7 došlo k chybě.</span><span class="sxs-lookup"><span data-stu-id="b920a-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="b920a-122">**Problém:**</span><span class="sxs-lookup"><span data-stu-id="b920a-122">**Problem:**</span></span>

<span data-ttu-id="b920a-123">V NuGet 2.7 nebo vyšší, při pokusu o instalaci libovolného balíčku, který obsahuje odkazy na sestavení, se může zobrazit chybová zpráva **"Vstupní řetězec nebyl ve správném formátu."**, jako je níže:</span><span class="sxs-lookup"><span data-stu-id="b920a-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="b920a-124">To je způsobeno tím, `VSLangProj.dll` že knihovna typů pro komponentu MODELU COM není v systému registrována.</span><span class="sxs-lookup"><span data-stu-id="b920a-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="b920a-125">K tomu může dojít například v případě, že máte dvě verze sady Visual Studio nainstalované vedle sebe a potom odinstalujete starší verzi.</span><span class="sxs-lookup"><span data-stu-id="b920a-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="b920a-126">Pokud tak učiníte, může neúmyslně zrušit registraci výše uvedené knihovny COM.</span><span class="sxs-lookup"><span data-stu-id="b920a-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="b920a-127">**Řešení:**:</span><span class="sxs-lookup"><span data-stu-id="b920a-127">**Solution:**:</span></span>

<span data-ttu-id="b920a-128">Spusťte tento příkaz z **výzvy se zvýšenými oprávněními** a znovu zaregistrujte knihovnu typů`VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="b920a-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="b920a-129">Pokud se příkaz nezdaří, zkontrolujte, zda soubor v tomto umístění existuje.</span><span class="sxs-lookup"><span data-stu-id="b920a-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="b920a-130">Další informace o této chybě naleznete v této [pracovní položce](https://nuget.codeplex.com/workitem/3609 "Pracovní položka 3609").</span><span class="sxs-lookup"><span data-stu-id="b920a-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="b920a-131">Selhání sestavení po aktualizaci balíčku ve VS 2012</span><span class="sxs-lookup"><span data-stu-id="b920a-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="b920a-132">Problém: Používáte VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="b920a-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="b920a-133">Při aktualizaci balíčků NuGet se zobrazí tato zpráva: "Jeden nebo více balíčků nelze dokončit odinstalovat."</span><span class="sxs-lookup"><span data-stu-id="b920a-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="b920a-134">a budete vyzváni k restartování sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b920a-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="b920a-135">Po restartu VS, dostanete podivné chyby sestavení.</span><span class="sxs-lookup"><span data-stu-id="b920a-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="b920a-136">Příčinou je, že některé soubory ve starých balíčcích jsou uzamčeny procesem MSBuild na pozadí.</span><span class="sxs-lookup"><span data-stu-id="b920a-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="b920a-137">I po restartování VS proces MSBuild na pozadí stále používá soubory ve starých balíčcích, což způsobuje selhání sestavení.</span><span class="sxs-lookup"><span data-stu-id="b920a-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="b920a-138">Oprava je instalace Aktualizace VS 2012, například VS 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="b920a-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="b920a-139">Upgrade na nejnovější NuGet ze starší verze způsobí chybu ověření podpisu</span><span class="sxs-lookup"><span data-stu-id="b920a-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="b920a-140">Pokud používáte VS 2010 SP1, můžete spustit do následující chybové zprávy při pokusu o upgrade NuGet, pokud máte nainstalovanou starší verzi.</span><span class="sxs-lookup"><span data-stu-id="b920a-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalační program rozšíření sady Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="b920a-142">Při prohlížení protokolů se může zobrazit `SignatureMismatchException`zmínka o .</span><span class="sxs-lookup"><span data-stu-id="b920a-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="b920a-143">Chcete-li tomu zabránit, je k dispozici [oprava hotfix visual studio 2010 SP1,](http://bit.ly/vsixcertfix) kterou můžete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="b920a-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="b920a-144">Alternativně je řešení jednoduše odinstalovat NuGet (při spuštění sady Visual Studio jako správce) a potom jej nainstalovat z Galerie rozšíření VS.</span><span class="sxs-lookup"><span data-stu-id="b920a-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span> <span data-ttu-id="b920a-145">Další informace naleznete v tématu <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="b920a-145">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="b920a-146">Konzola Správce balíčků vyvolá výjimku, když je nainstalován také doplněk Visual Studio Reflector.</span><span class="sxs-lookup"><span data-stu-id="b920a-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="b920a-147">Při spuštění konzoly Správce balíčků můžete spustit následující zprávu o výjimce, pokud máte nainstalovaný doplněk Reflector VS.</span><span class="sxs-lookup"><span data-stu-id="b920a-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="b920a-148">– nebo –</span><span class="sxs-lookup"><span data-stu-id="b920a-148">or</span></span>

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

<span data-ttu-id="b920a-149">Kontaktovali jsme autora doplňku v naději, že vypracujeme řešení.</span><span class="sxs-lookup"><span data-stu-id="b920a-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="b920a-150">Aktualizace: Ověřili jsme, že nejnovější verze Reflectoru, 6.5, již nezpůsobuje tuto výjimku v konzoli.</span><span class="sxs-lookup"><span data-stu-id="b920a-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="b920a-151">Otevření konzoly Správce balíčků se nezdaří s výjimkou objectsecurity</span><span class="sxs-lookup"><span data-stu-id="b920a-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="b920a-152">Při pokusu o otevření konzoly Správce balíčků se mohou zobrazit tyto chyby:</span><span class="sxs-lookup"><span data-stu-id="b920a-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="b920a-153">Pokud ano, postupujte podle řešení [popsané na StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) opravit.</span><span class="sxs-lookup"><span data-stu-id="b920a-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="b920a-154">Dialogové okno Přidat odkaz na knihovnu balíčků vyvolá výjimku, pokud řešení obsahuje aplikaci InstallShield Limited Edition Project.</span><span class="sxs-lookup"><span data-stu-id="b920a-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="b920a-155">Zjistili jsme, že pokud vaše řešení obsahuje jeden nebo více instaltických edicí projektu InstallShield, dialogové okno **Přidat odkaz na knihovnu balíčků** vyvolá při otevření výjimku.</span><span class="sxs-lookup"><span data-stu-id="b920a-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="b920a-156">V současné době neexistuje žádné řešení ještě s výjimkou odebrání InstallShield projekty nebo jejich uvolnění.</span><span class="sxs-lookup"><span data-stu-id="b920a-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="b920a-157">Odinstalovat tlačítko šedě ven?</span><span class="sxs-lookup"><span data-stu-id="b920a-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="b920a-158">NuGet vyžaduje oprávnění správce k instalaci nebo odinstalaci</span><span class="sxs-lookup"><span data-stu-id="b920a-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="b920a-159">Pokud se pokusíte odinstalovat NuGet prostřednictvím Správce rozšíření sady Visual Studio, můžete si všimnout, že tlačítko Odinstalovat je zakázáno.</span><span class="sxs-lookup"><span data-stu-id="b920a-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="b920a-160">NuGet vyžaduje přístup správce k instalaci a odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="b920a-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="b920a-161">Znovu spusťte Visual Studio jako správce a odinstalujte rozšíření.</span><span class="sxs-lookup"><span data-stu-id="b920a-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="b920a-162">NuGet nevyžaduje přístup správce k jeho použití.</span><span class="sxs-lookup"><span data-stu-id="b920a-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="b920a-163">Konzola Správce balíčků se při otevření v systému Windows XP zhroutí.</span><span class="sxs-lookup"><span data-stu-id="b920a-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="b920a-164">Co je?</span><span class="sxs-lookup"><span data-stu-id="b920a-164">What's wrong?</span></span>

<span data-ttu-id="b920a-165">NuGet vyžaduje prostředí runtime prostředí Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="b920a-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="b920a-166">Systém Windows XP ve výchozím nastavení nemá aplikaci Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="b920a-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="b920a-167">Runtime aplikace Powershell 2.0 <https://support.microsoft.com/kb/968929>si můžete stáhnout z aplikace .</span><span class="sxs-lookup"><span data-stu-id="b920a-167">You can download the Powershell 2.0 runtime from <https://support.microsoft.com/kb/968929>.</span></span> <span data-ttu-id="b920a-168">Po instalaci restartujte aplikaci Visual Studio a měli byste být schopni spustit konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="b920a-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="b920a-169">Visual Studio 2010 SP1 Beta dojde k chybě při ukončení, pokud je otevřena konzola Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="b920a-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="b920a-170">Pokud jste nainstalovali Visual Studio 2010 SP1 Beta, můžete si všimnout, že pokud necháte konzolu Správce balíčků otevřenou a zavřete visual studio, dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="b920a-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="b920a-171">Toto je známé vydání sady Visual Studio a bude opraveno ve verzi RTM SP1.</span><span class="sxs-lookup"><span data-stu-id="b920a-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="b920a-172">Pro tuto chvíli, stačí ignorovat havárii nebo odinstalovat SP1 Beta, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="b920a-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="b920a-173">Prvek 'metadata' ... Dojde k neplatné výjimce podřízeného prvku.</span><span class="sxs-lookup"><span data-stu-id="b920a-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="b920a-174">Pokud jste nainstalovali balíčky vytvořené s předběžnou verzí NuGet, může dojít k chybové zprávě s uvedením "Element 'metadata' v oboru názvů 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' má neplatný podřízený prvek" při spuštění rtm verze NuGet s tímto projektem.</span><span class="sxs-lookup"><span data-stu-id="b920a-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="b920a-175">Je třeba odinstalovat a znovu nainstalovat každý balíček pomocí RTM verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="b920a-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="b920a-176">Při pokusu o instalaci nebo odinstalaci dojde k chybě "Nelze vytvořit soubor, pokud soubor již existuje."</span><span class="sxs-lookup"><span data-stu-id="b920a-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="b920a-177">Z nějakého důvodu rozšíření sady Visual Studio může získat v podivném stavu, kde jste odinstalovali rozšíření VSIX, ale některé soubory byly ponechány za sebou.</span><span class="sxs-lookup"><span data-stu-id="b920a-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="b920a-178">Náhradní řešení tohoto problému:</span><span class="sxs-lookup"><span data-stu-id="b920a-178">To work around this issue:</span></span>

1. <span data-ttu-id="b920a-179">Ukončení sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b920a-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="b920a-180">Otevřete následující složku (může být na jiné jednotce v počítači)</span><span class="sxs-lookup"><span data-stu-id="b920a-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="b920a-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\<Corporation\NuGet Package Manager verze></span><span class="sxs-lookup"><span data-stu-id="b920a-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version></span></span>\

1. <span data-ttu-id="b920a-182">Odstraňte všechny soubory s příponami *DELETEMe.*</span><span class="sxs-lookup"><span data-stu-id="b920a-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="b920a-183">Opětovné otevření sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b920a-183">Re-open Visual Studio</span></span>

<span data-ttu-id="b920a-184">Po provedení těchto kroků byste měli být schopni pokračovat.</span><span class="sxs-lookup"><span data-stu-id="b920a-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="b920a-185">Ve výjimečných případech kompilace s analýzou kódu zapnuta způsobí chybu.</span><span class="sxs-lookup"><span data-stu-id="b920a-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="b920a-186">Pokud nainstalujete aplikaci FluentNHibernate s konzolou Správce balíčků a potom zkompilujete projekt se zapnutou analýzou kódu, může se zobrazit následující chyba.</span><span class="sxs-lookup"><span data-stu-id="b920a-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="b920a-187">Ve výchozím nastavení fluentnhibernate vyžaduje NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="b920a-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="b920a-188">Však podle návrhu NuGet nainstaluje NHibernate 3.0.0.4000 v projektu a přidejte příslušné vazby přesměrování tak, aby to bude fungovat.</span><span class="sxs-lookup"><span data-stu-id="b920a-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="b920a-189">Projekt se zkompiluje v pořádku, pokud není zapnuta analýza kódu.</span><span class="sxs-lookup"><span data-stu-id="b920a-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="b920a-190">Na rozdíl od kompilátoru nástroj pro analýzu kódu není správně postupujte podle přesměrování vazby použít 3.0.0.4000 namísto 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="b920a-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="b920a-191">Problém můžete vyřešit buď instalací NHibernate 3.0.0.2001, nebo sdělit nástroji pro analýzu kódu, aby se choval stejně jako kompilátor, a to následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="b920a-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="b920a-192">Přejít na *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Týmové nástroje\Nástroje statické analýzy\FxCop*</span><span class="sxs-lookup"><span data-stu-id="b920a-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="b920a-193">Otevřete Soubor FxCopCmd.exe.config a změňte `AssemblyReferenceResolveMode` z `StrongName` na `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="b920a-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="b920a-194">Uložte změnu a znovu vytvořte projekt.</span><span class="sxs-lookup"><span data-stu-id="b920a-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="b920a-195">Příkaz Write-Error nefunguje uvnitř souboru install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="b920a-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="b920a-196">Jedná se o známý problém.</span><span class="sxs-lookup"><span data-stu-id="b920a-196">This is a known issue.</span></span> <span data-ttu-id="b920a-197">Místo volání Write-Error zkuste volat throw.</span><span class="sxs-lookup"><span data-stu-id="b920a-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="b920a-198">Instalace nugetu s omezeným přístupem v systému Windows 2003 může chybět v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b920a-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="b920a-199">Při pokusu o instalaci NuGet pomocí Správce rozšíření sady Visual Studio a není spuštěn jako správce, &#8220;Spustit jako&#8221; dialogové okno se zobrazí se zaškrtávacím políčkem s názvem &#8220;Spustit tento program s omezeným přístupem&#8221; zaškrtnuto ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="b920a-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Dialogové okno Spustit jako omezený](./media/RunAsRestricted.png)

<span data-ttu-id="b920a-201">Kliknutím na OK s zaškrtnutou chyby dojde k selhání visual studio.</span><span class="sxs-lookup"><span data-stu-id="b920a-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="b920a-202">Ujistěte se, že zrušit zaškrtnutí této možnosti před instalací NuGet.</span><span class="sxs-lookup"><span data-stu-id="b920a-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="b920a-203">Aplikaci NuGet pro nástroje pro Windows Phone nelze odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="b920a-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="b920a-204">Nástroje Pro Windows Phone nemá podporu pro Správce rozšíření sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b920a-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="b920a-205">Chcete-li odinstalovat NuGet, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="b920a-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="b920a-206">Změna velkých písmen ID balíčku NuGet přeruší obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="b920a-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="b920a-207">Jak je podrobně popsáno na [tomto problému GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), změna velkých písmen balíčků NuGet lze provést podporou NuGet, ale způsobuje komplikace během obnovení balíčku pro uživatele, kteří mají existující, různě cased, balíčky ve své složce *globální balíčky.*</span><span class="sxs-lookup"><span data-stu-id="b920a-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="b920a-208">Doporučujeme pouze požadovat změnu případu, pokud máte způsob, jak komunikovat s existujícími uživateli balíčku o přestávce, které mohou nastat jejich obnovení balíčku sestavení.</span><span class="sxs-lookup"><span data-stu-id="b920a-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="b920a-209">Hlášení problémů</span><span class="sxs-lookup"><span data-stu-id="b920a-209">Reporting issues</span></span>

<span data-ttu-id="b920a-210">Chcete-li nahlásit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)problémy nuget, navštivte .</span><span class="sxs-lookup"><span data-stu-id="b920a-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
