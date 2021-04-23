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
# <a name="package-readme-on-nugetorg"></a>Soubor Readme balíčku na NuGet.org

[Zahrňte do svého balíčku NuGet soubor Readme](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) , abyste měli podrobné informace o balíčku pro vaše uživatele.

Je to nejspíš jedna z prvních prvků, které se uživatelům zobrazí při zobrazení stránky s podrobnostmi balíčku na NuGet.org a je zásadní pro zajištění dobrého dojmu!

> [!IMPORTANT]
> NuGet.org podporuje pouze soubory Readme v [Markdownu](https://daringfireball.net/projects/markdown/) a image z omezené sady domén. Podívejte se na naše [povolené domény pro Image](#allowed-domains-for-images-and-badges) a [podporované funkce Markdownu](#supported-markdown-features) , abyste zajistili, že se Váš soubor Readme správně vykresluje na NuGet.org.

## <a name="what-should-my-readme-include"></a>Co by měl můj soubor ready zahrnovat?

V souboru Readme zvažte zahrnutí následujících položek:
* Úvod k tomu, co váš balíček dělá a které problémy řeší?
* Jak začít s balíčkem – existují nějaké zvláštní požadavky?
* Odkazy na komplexnější dokumentaci, pokud nejsou součástí samotného souboru Readme.
* Alespoň pár fragmentů kódu/ukázky nebo příklady imagí.
* Kde a jak můžete opustit svou zpětnou vazbu, jako je například odkaz na problémy projektu, Twitter, sledování chyb nebo na jinou platformu.
* Jak přispívat, pokud je k dispozici.

Mějte na paměti, že soubory Readme s vysokou kvalitou můžou pocházet z nejrůznějších formátů, tvarů a velikostí. Pokud už máte balíček dostupný na NuGet.org, je pravděpodobné, že `readme.md` v úložišti už máte jiný soubor dokumentace, který by měl být na stránce podrobností NuGet.org skvělého dodatku.

## <a name="preview-your-readme"></a>Náhled souboru Readme

Pokud chcete zobrazit náhled souboru Readme předtím, než bude aktivní na NuGet.org, nahrajte balíček pomocí [webového portálu nahrát balíček na NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) a posuňte se dolů do části "soubor Readme" v náhledu metadat. Měl by vypadat přibližně takto:

![Náhled souboru Readme](media\readme-upload-preview.PNG)

Vezměte v úvahu čas na kontrolu a náhled souboru Readme pro kontrolu [kompatibility imagí](#allowed-domains-for-images-and-badges) a [podporovaného formátování](#supported-markdown-features) , abyste se ujistili, že nabízí skvělý první dojem potenciálním uživatelům. Pokud chcete opravit chyby v souboru Readme balíčku po jeho publikování na NuGet.org, bude nutné nainstalovat aktualizovanou verzi balíčku s opravou. Aby se zajistilo, že všechno vypadá dobře, může vám to ušetřit starostí.
## <a name="allowed-domains-for-images-and-badges"></a>Povolené domény pro obrázky a symboly

Vzhledem k problémům se zabezpečením a ochranou osobních údajů NuGet.org omezuje domény, ze kterých lze obrázky a oznámení vykreslovat důvěryhodným hostitelům. 

NuGet.org umožňuje vykreslit všechny image včetně označení z následujících důvěryhodných domén:
* api.bintray.com
* api.codacy.com
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
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Pokud se domníváte, že by měla být do seznamu povolených souborů přidána jiná doména, je vhodné [zaslat soubor problému](https://github.com/NuGet/NuGetGallery/issues) a ten bude přezkoumán technickým týmem pro zajištění ochrany osobních údajů a dodržování předpisů zabezpečení. Image s relativními místními cestami a imagemi hostovanými z nepodporovaných domén se nebudou vykreslovat a na stránce s podrobnostmi balíčku Readme se zobrazí upozornění, které je viditelné jenom pro vlastníky balíčku.

## <a name="supported-markdown-features"></a>Podporované funkce Markdownu
[Markdownu](https://daringfireball.net/projects/markdown/) je jednoduchý jazyk využívající značky s syntaxí formátování prostého textu. Soubory Readme NuGet.org podporují [CommonMark](https://commonmark.org/) splňující Markdownu prostřednictvím modulu analýzy [Markdig](https://github.com/lunet-io/markdig) .

NuGet.org aktuálně podporuje následující funkce Markdownu:
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

