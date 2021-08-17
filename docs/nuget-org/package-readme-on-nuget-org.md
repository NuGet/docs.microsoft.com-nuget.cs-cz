---
title: soubor readme pro balíček NuGet. org
description: podrobné vysvětlení způsobu, jakým se soubory readme na NuGet. org se vykreslují a co dělat, když narazíte na problémy.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: ac0e89c1f5ef9eb19c29646bcc76bcb0b460c5cd
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209940"
---
# <a name="package-readme-on-nugetorg"></a>soubor readme pro balíček NuGet. org

[zahrňte do balíčku NuGet soubor readme](/nuget/reference/msbuild-targets#packagereadmefile) , abyste měli podrobné informace o balíčku pro uživatele.

je to nejspíš jedna z prvních prvků, které se uživatelům zobrazí při zobrazení stránky s podrobnostmi balíčku na NuGet. org a je zásadní pro zajištění dobrého dojmu!

> [!IMPORTANT]
> NuGet. org podporuje pouze soubory readme v [markdownu](https://daringfireball.net/projects/markdown/) a image z omezené sady domén. podívejte se na naše [povolené domény pro image](#allowed-domains-for-images-and-badges) a [podporované funkce markdownu](#supported-markdown-features) , abyste zajistili, že se váš soubor readme správně vykresluje na NuGet. org.

## <a name="what-should-my-readme-include"></a>Co by měl můj soubor ready zahrnovat?

V souboru Readme zvažte zahrnutí následujících položek:
* Úvod k tomu, co váš balíček dělá a které problémy řeší?
* Jak začít s balíčkem – existují nějaké zvláštní požadavky?
* Odkazy na komplexnější dokumentaci, pokud nejsou součástí samotného souboru Readme.
* Alespoň pár fragmentů kódu/ukázky nebo příklady imagí.
* Kde a jak můžete opustit svou zpětnou vazbu, jako je například odkaz na problémy projektu, Twitter, sledování chyb nebo na jinou platformu.
* Jak přispívat, pokud je k dispozici.

Mějte na paměti, že soubory Readme s vysokou kvalitou můžou pocházet z nejrůznějších formátů, tvarů a velikostí. pokud již máte balíček k dispozici na NuGet. org, je pravděpodobné, že `readme.md` v úložišti již máte jiný soubor dokumentace, který by měl být vhodným doplňkem na stránku s podrobnostmi NuGet. org.

## <a name="preview-your-readme"></a>Náhled souboru Readme

chcete-li zobrazit náhled souboru readme předtím, než bude aktivní na NuGet. org, nahrajte balíček pomocí [webového portálu Upload balíček na NuGet. org](/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) a přejděte dolů do části soubor readme v náhledu metadat. Měl by vypadat přibližně takto:

![Náhled souboru Readme](media\readme-upload-preview.PNG)

Vezměte v úvahu čas na kontrolu a náhled souboru Readme pro kontrolu [kompatibility imagí](#allowed-domains-for-images-and-badges) a [podporovaného formátování](#supported-markdown-features) , abyste se ujistili, že nabízí skvělý první dojem potenciálním uživatelům. pokud chcete opravit chyby v souboru readme balíčku po jeho publikování na NuGet. org, budete muset nainstalovat aktualizovanou verzi balíčku s touto opravou. Aby se zajistilo, že všechno vypadá dobře, může vám to ušetřit starostí.
## <a name="allowed-domains-for-images-and-badges"></a>Povolené domény pro obrázky a symboly

vzhledem k tomu, že se týká zabezpečení a ochrany osobních údajů, NuGet. org omezuje domény, ze kterých lze obrázky a znaky vykreslovat důvěryhodným hostitelům. 

NuGet. org umožňuje vykreslovat všechny image včetně označení z následujících důvěryhodných domén:
* api.bintray.com
* api.codacy.com
* app.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* cdn.jsdelivr.net
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* i.imgur.com
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Pokud se domníváte, že by měla být do seznamu povolených souborů přidána jiná doména, je vhodné [zaslat soubor problému](https://github.com/NuGet/NuGetGallery/issues) a ten bude přezkoumán technickým týmem pro zajištění ochrany osobních údajů a dodržování předpisů zabezpečení. Image s relativními místními cestami a imagemi hostovanými z nepodporovaných domén se nebudou vykreslovat a na stránce s podrobnostmi balíčku Readme se zobrazí upozornění, které je viditelné jenom pro vlastníky balíčku.

## <a name="supported-markdown-features"></a>Podporované funkce Markdownu
[Markdownu](https://daringfireball.net/projects/markdown/) je jednoduchý jazyk využívající značky s syntaxí formátování prostého textu. soubory readme. NuGet. org podporují markdownu vyhovující [CommonMark](https://commonmark.org/) prostřednictvím modulu analýzy [Markdig](https://github.com/lunet-io/markdig) .

NuGet. org aktuálně podporuje následující funkce markdownu:
* [Hlavičky](https://spec.commonmark.org/0.29/#atx-headings)
* [Image](https://spec.commonmark.org/0.29/#images)
* [Extra zdůraznění](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Seznamy](https://spec.commonmark.org/0.29/#lists)
* [Odkazy](https://spec.commonmark.org/0.29/#links)
* [Blokovat uvozovky](https://spec.commonmark.org/0.29/#block-quotes)
* [Řídicí znaky zpětného lomítka](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Rozsahy kódu](https://spec.commonmark.org/0.29/#code-spans)
* [Seznamy úloh](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tabulky](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emoji](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Automatické odkazy](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

