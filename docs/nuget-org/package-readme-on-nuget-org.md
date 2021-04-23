---
title: Soubor Readme balíčku na NuGet.org
description: Podrobné vysvětlení toho, jak se vykreslují soubory Readme na NuGet.org a co dělat při nastavování problémů.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902246"
---
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="7e5f6-103">Soubor Readme balíčku na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="7e5f6-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="7e5f6-104">[Zahrňte do svého balíčku NuGet soubor Readme](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) , abyste měli podrobné informace o balíčku pro vaše uživatele.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="7e5f6-105">Je to nejspíš jedna z prvních prvků, které se uživatelům zobrazí při zobrazení stránky s podrobnostmi balíčku na NuGet.org a je zásadní pro zajištění dobrého dojmu!</span><span class="sxs-lookup"><span data-stu-id="7e5f6-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e5f6-106">NuGet.org podporuje pouze soubory Readme v [Markdownu](https://daringfireball.net/projects/markdown/) a image z omezené sady domén.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="7e5f6-107">Podívejte se na naše [povolené domény pro Image](#allowed-domains-for-images-and-badges) a [podporované funkce Markdownu](#supported-markdown-features) , abyste zajistili, že se Váš soubor Readme správně vykresluje na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="7e5f6-108">Co by měl můj soubor ready zahrnovat?</span><span class="sxs-lookup"><span data-stu-id="7e5f6-108">What should my readme include?</span></span>

<span data-ttu-id="7e5f6-109">V souboru Readme zvažte zahrnutí následujících položek:</span><span class="sxs-lookup"><span data-stu-id="7e5f6-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="7e5f6-110">Úvod k tomu, co váš balíček dělá a které problémy řeší?</span><span class="sxs-lookup"><span data-stu-id="7e5f6-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="7e5f6-111">Jak začít s balíčkem – existují nějaké zvláštní požadavky?</span><span class="sxs-lookup"><span data-stu-id="7e5f6-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="7e5f6-112">Odkazy na komplexnější dokumentaci, pokud nejsou součástí samotného souboru Readme.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="7e5f6-113">Alespoň pár fragmentů kódu/ukázky nebo příklady imagí.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="7e5f6-114">Kde a jak můžete opustit svou zpětnou vazbu, jako je například odkaz na problémy projektu, Twitter, sledování chyb nebo na jinou platformu.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="7e5f6-115">Jak přispívat, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="7e5f6-116">Mějte na paměti, že soubory Readme s vysokou kvalitou můžou pocházet z nejrůznějších formátů, tvarů a velikostí.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="7e5f6-117">Pokud už máte balíček dostupný na NuGet.org, je pravděpodobné, že `readme.md` v úložišti už máte jiný soubor dokumentace, který by měl být na stránce podrobností NuGet.org skvělého dodatku.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="7e5f6-118">Náhled souboru Readme</span><span class="sxs-lookup"><span data-stu-id="7e5f6-118">Preview your readme</span></span>

<span data-ttu-id="7e5f6-119">Pokud chcete zobrazit náhled souboru Readme předtím, než bude aktivní na NuGet.org, nahrajte balíček pomocí [webového portálu nahrát balíček na NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) a posuňte se dolů do části "soubor Readme" v náhledu metadat.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="7e5f6-120">Měl by vypadat přibližně takto:</span><span class="sxs-lookup"><span data-stu-id="7e5f6-120">It should look something like this:</span></span>

![Náhled souboru Readme](media\readme-upload-preview.PNG)

<span data-ttu-id="7e5f6-122">Vezměte v úvahu čas na kontrolu a náhled souboru Readme pro kontrolu [kompatibility imagí](#allowed-domains-for-images-and-badges) a [podporovaného formátování](#supported-markdown-features) , abyste se ujistili, že nabízí skvělý první dojem potenciálním uživatelům.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="7e5f6-123">Pokud chcete opravit chyby v souboru Readme balíčku po jeho publikování na NuGet.org, bude nutné nainstalovat aktualizovanou verzi balíčku s opravou.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="7e5f6-124">Aby se zajistilo, že všechno vypadá dobře, může vám to ušetřit starostí.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="7e5f6-125">Povolené domény pro obrázky a symboly</span><span class="sxs-lookup"><span data-stu-id="7e5f6-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="7e5f6-126">Vzhledem k problémům se zabezpečením a ochranou osobních údajů NuGet.org omezuje domény, ze kterých lze obrázky a oznámení vykreslovat důvěryhodným hostitelům.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="7e5f6-127">NuGet.org umožňuje vykreslit všechny image včetně označení z následujících důvěryhodných domén:</span><span class="sxs-lookup"><span data-stu-id="7e5f6-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="7e5f6-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-128">api.bintray.com</span></span>
* <span data-ttu-id="7e5f6-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-129">api.codacy.com</span></span>
* <span data-ttu-id="7e5f6-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-130">api.codeclimate.com</span></span>
* <span data-ttu-id="7e5f6-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-131">api.dependabot.com</span></span>
* <span data-ttu-id="7e5f6-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-132">api.travis-ci.com</span></span>
* <span data-ttu-id="7e5f6-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="7e5f6-133">api.travis-ci.org</span></span>
* <span data-ttu-id="7e5f6-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="7e5f6-134">app.fossa.io</span></span>
* <span data-ttu-id="7e5f6-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="7e5f6-135">badge.fury.io</span></span>
* <span data-ttu-id="7e5f6-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="7e5f6-136">badgen.net</span></span>
* <span data-ttu-id="7e5f6-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="7e5f6-137">badges.gitter.im</span></span>
* <span data-ttu-id="7e5f6-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-138">bettercodehub.com</span></span>
* <span data-ttu-id="7e5f6-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="7e5f6-139">buildstats.info</span></span>
* <span data-ttu-id="7e5f6-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="7e5f6-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-141">ci.appveyor.com</span></span>
* <span data-ttu-id="7e5f6-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-142">circleci.com</span></span>
* <span data-ttu-id="7e5f6-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="7e5f6-143">codecov.io</span></span>
* <span data-ttu-id="7e5f6-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="7e5f6-144">codefactor.io</span></span>
* <span data-ttu-id="7e5f6-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="7e5f6-145">coveralls.io</span></span>
* <span data-ttu-id="7e5f6-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-146">dev.azure.com</span></span>
* <span data-ttu-id="7e5f6-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="7e5f6-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="7e5f6-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-148">gitlab.com</span></span>
* <span data-ttu-id="7e5f6-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="7e5f6-149">img.shields.io</span></span>
* <span data-ttu-id="7e5f6-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-150">isitmaintained.com</span></span>
* <span data-ttu-id="7e5f6-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-151">opencollective.com</span></span>
* <span data-ttu-id="7e5f6-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-152">raw.github.com</span></span>
* <span data-ttu-id="7e5f6-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="7e5f6-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="7e5f6-154">snyk.io</span></span>
* <span data-ttu-id="7e5f6-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="7e5f6-155">sonarcloud.io</span></span>
* <span data-ttu-id="7e5f6-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="7e5f6-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="7e5f6-157">Pokud se domníváte, že by měla být do seznamu povolených souborů přidána jiná doména, je vhodné [zaslat soubor problému](https://github.com/NuGet/NuGetGallery/issues) a ten bude přezkoumán technickým týmem pro zajištění ochrany osobních údajů a dodržování předpisů zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="7e5f6-158">Image s relativními místními cestami a imagemi hostovanými z nepodporovaných domén se nebudou vykreslovat a na stránce s podrobnostmi balíčku Readme se zobrazí upozornění, které je viditelné jenom pro vlastníky balíčku.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="7e5f6-159">Podporované funkce Markdownu</span><span class="sxs-lookup"><span data-stu-id="7e5f6-159">Supported Markdown features</span></span>
<span data-ttu-id="7e5f6-160">[Markdownu](https://daringfireball.net/projects/markdown/) je jednoduchý jazyk využívající značky s syntaxí formátování prostého textu.</span><span class="sxs-lookup"><span data-stu-id="7e5f6-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="7e5f6-161">Soubory Readme NuGet.org podporují [CommonMark](https://commonmark.org/) splňující Markdownu prostřednictvím modulu analýzy [Markdig](https://github.com/lunet-io/markdig) .</span><span class="sxs-lookup"><span data-stu-id="7e5f6-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="7e5f6-162">NuGet.org aktuálně podporuje následující funkce Markdownu:</span><span class="sxs-lookup"><span data-stu-id="7e5f6-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="7e5f6-163">Hlavičky</span><span class="sxs-lookup"><span data-stu-id="7e5f6-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="7e5f6-164">Image</span><span class="sxs-lookup"><span data-stu-id="7e5f6-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="7e5f6-165">Extra zdůraznění</span><span class="sxs-lookup"><span data-stu-id="7e5f6-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="7e5f6-166">Seznamy</span><span class="sxs-lookup"><span data-stu-id="7e5f6-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="7e5f6-167">Odkazy</span><span class="sxs-lookup"><span data-stu-id="7e5f6-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="7e5f6-168">Blokovat uvozovky</span><span class="sxs-lookup"><span data-stu-id="7e5f6-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="7e5f6-169">Řídicí znaky zpětného lomítka</span><span class="sxs-lookup"><span data-stu-id="7e5f6-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="7e5f6-170">Rozsahy kódu</span><span class="sxs-lookup"><span data-stu-id="7e5f6-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="7e5f6-171">Seznamy úloh</span><span class="sxs-lookup"><span data-stu-id="7e5f6-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="7e5f6-172">Tabulky</span><span class="sxs-lookup"><span data-stu-id="7e5f6-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="7e5f6-173">Emoji</span><span class="sxs-lookup"><span data-stu-id="7e5f6-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="7e5f6-174">Automatické odkazy</span><span class="sxs-lookup"><span data-stu-id="7e5f6-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

