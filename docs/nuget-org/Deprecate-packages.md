---
title: Zastaralé balíčky na nuget.org
description: Podrobný popis procesu zastaralých balíčků a způsobu, jakým klienti tyto informace zobrazují
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726961"
---
# <a name="deprecating-packages"></a>Zastaralé balíčky

Pokud už balíček neuchováváte, nebo pokud chcete, aby se příjemci balíčku mohli přesunout na jiný balíček, můžete ho zařadit do zastaralého. 

Vyřazení balíčku se **liší od** odbalení balíčku, jak je vysvětleno níže:
*  Odhlášení balíčku brání jeho zjištění, protože je ve výsledcích hledání skryté. 
* Když zařadíte **balíček,** umožníte stávajícím příjemcům balíčku zjistit, jestli mají nainstalované nebo používané ve svých projektech. Také jim umožňuje zjistit důvod vyřazení a alternativní doporučený balíček, který jste určili (Vydavatel balíčku). Zastaralost balíčku neodstraní balíček. 

Jako vydavatel se můžete rozhodnout, jak odpisovat, tak i jako zastaralé balíčky.

## <a name="deprecation-workflow"></a>Pracovní postup vyřazení
1. Pokud chcete balíček zařadit **, klikněte** na **Spravovat balíčky** a vyberte vyřazení:

    ![Možnost přejít na nepoužívaného balíčku](media/deprecation-select-option.png)

2. Vyberte verzi, kterou chcete vyřadit jako nevybranou. Pokud chcete vyřadit všechny verze, zvolte možnost **Vybrat všechny verze** .

    ![Vybrat verze balíčku k vyřazení](media/deprecation-select-version.png)

3. Vyberte důvod pro vyřazení. Pokud se balíček již neuchovává, vyberte možnost **starší verze** . Pokud má konkrétní verze kritickou chybu, vyberte možnost **má kritické chyby** . Z jakéhokoli jiného důvodu vyberte **jiný**. Pro vlastníky můžete vždy zadat alternativní doporučený balíček (a verzi) a vlastní zprávu. 

    ![Vyberte důvody alternativního balíčku doporučení a vlastní zpráva.](media/deprecation-save.png)

> [!Note]
> Vlastní zpráva se zobrazuje jenom na nuget.org, ale ne z klientů. v současné době klienti jako `dotnet.exe` a NuGet Správce balíčků nezobrazují vlastní zprávu.

## <a name="client-experience-for-deprecated-packages"></a>Prostředí klienta pro zastaralé balíčky
Jakmile je balíček zastaralý, jeho příjemci se o tom dozví v následujících způsobech (v závislosti na použitém klientovi).

### <a name="visual-studio"></a>Visual Studio 
*k dispozici od verze Visual Studio 2019 16,3*

Visual Studio upozorňuje na použití zastaralého balíčku na `Installed` kartě. Zobrazí se upozornění pro balíček a informace o jeho zastaralosti (včetně důvodu, že byl zastaralý a místo toho alternativního balíčku, pokud je k dispozici).

   ![zastaralé balíčky na kartě nainstalované na Visual Studio správce balíčků](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*K dispozici od .NET SDK 3,0*

Pokud používáte dotnet.exe, můžete spustit příkaz `dotnet list package --deprecated` ve složce řešení nebo projektu a získat tak seznam zastaralých balíčků spolu s informacemi o vyřazení:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>Přenos oblíbenosti do novějšího balíčku

Autoři balíčku, kteří si zastarali starší verzi balíčku, se můžou rozhodnout přenést jeho oblíbenou položku do novějšího balíčku, aby se zvýšilo pořadí hledání v novějším balíčku. To pomáhá zákazníkům vyhledat novější balíček namísto zastaralého balíčku.

Řekněme například, že mám dva balíčky:

* Můj zastaralý starší balíček `Contoso.Legacy` s 3 000 000 soubory ke stažení
* Můj poslední balíček `Contoso.Latest` s 5 soubory ke stažení

NuGet. org dává přednost výsledkům hledání s vyššími soubory ke stažení nebo oblíbenou položkou. Má-li vyhledávací dotaz "contoso", měl by vyřazený balíček `Contoso.Legacy` nad výsledky hledání nad posledním balíčkem `Contoso.Latest` .

Chcete-li tento problém vyřešit, můžete použít pro přenos oblíbenosti zastaralého staršího balíčku do mého nejnovějšího balíčku. To by znamenalo `Contoso.Latest` , že ve výsledcích hledání dojde k vyššímu pořadí, zatímco `Contoso.Legacy` by byl nižší. Ovlivněny jsou jenom interní hodnoty oblíbenosti pro balíčky, což nebude mít vliv na skutečný počet stažení pro každý balíček.

> [!Note]
> Přenosy oblíbenosti můžou uživatelům významně ztížit nalezení starší verze balíčku.

V následující tabulce získáte konkrétní představu o tom, jak může přenos oblíbenosti ovlivnit pořadí vyhledávání pro dotaz "contoso":

| Pořadí hledání    | Před přenosem oblíbenosti        | Po přenosu oblíbenosti         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso. Legacy, 3M stažení*    | *Contoso. nejnovější, 5 stažení*     |
| 2                 | Contoso. Scanner, 2 min stažení     | Contoso. Scanner, 2 min stažení     |
| 3                 | Soubory contoso. Core, 1,5 M ke stažení     | Soubory contoso. Core, 1,5 M ke stažení     |
| 4                 | Contoso. UI, 1M stažení          | Contoso. UI, 1M stažení          |
| ...               | ...                               | ...                               |
| 20                | *Contoso. nejnovější, 5 stažení*     | *Contoso. Legacy, 3M stažení*    |

### <a name="popularity-transfer-application-process"></a>Proces aplikace pro přenos oblíbenosti

1. Zkontrolujte [požadavky na přenos oblíbenosti](#popularity-transfer-requirements).
2. E-mail [account@nuget.org](mailto:account@nuget.org) se zastaralým balíčkem, jehož oblíbenost se má přenést, a seznam stabilních balíčků, které by měly obdržet přenos oblíbenosti.

Po odeslání aplikace vás pošleme na přijetí nebo odmítnutí vaší aplikace (s kritérii, která způsobila zamítnutí). Pro potvrzení identity vlastníka možná budete muset požádat o další identifikační otázky.

#### <a name="popularity-transfer-requirements"></a>Požadavky na přenos oblíbenosti

* Starší balíčky a nové balíčky musí sdílet všechny vlastníky.
* Nové balíčky musí být jasně spojené se staršími balíčky v pojmenovávání a funkci (tzn. vývoj nebo další generace).
* Všechny verze starších balíčků musí být zastaralé a odkazují na nové balíčky přijímající přenos.
* přenos oblíbenosti nesmí způsobit nejasnost u NuGet uživatelů ani zhoršit možnosti hledání NuGet.
* Nové balíčky musí mít stabilní verzi.
* Starší balíček nesmí přijímat přenosy oblíbenosti z jiného zastaralého balíčku.

### <a name="advanced-popularity-transfer-scenarios"></a>Pokročilé scénáře přenosu oblíbenosti

#### <a name="package-consolidations"></a>Sloučení balíčků

Můžu přenést oblíbenou více zazastaralých balíčků, a to ve prospěch jednoho nového balíčku. Řekněme například, že mám 3 balíčky:

* Můj první zastaralý balíček starší verze `Contoso.Legacy1`
* Druhý zastaralý starší balíček `Contoso.Legacy2`
* Můj nový konsolidovaný balíček `Contoso.Latest`

Po odsouhlasení `Contoso.Legacy1` a `Contoso.Legacy2` můžete použít pro přenos své oblíbenosti na `Contoso.Latest` .

#### <a name="package-splits"></a>Rozdělení balíčků

Oblíbenou oblíbenou verzi balíčku můžete přenášet do a dělené mezi až 5 novějšími balíčky. To je užitečné, pokud byla funkce zastaralého balíčku rozdělená mezi několik nových balíčků. Řekněme například, že mám 3 balíčky:

* Můj zastaralý starší balíček `Contoso.Legacy`
* Můj první nový balíček `Contoso.Web`
* Druhý nový balíček `Contoso.Cloud`

`Contoso.Legacy` zahrnuje webové i cloudové funkce, ale rozhodli jste se tyto funkce oddělit do různých balíčků pro novou generaci. Po zastaralosti `Contoso.Legacy` se dá použít pro přenos své oblíbenosti do obou `Contoso.Web` i `Contoso.Cloud` .

> [!Warning]
> Přenesená oblíbená část bude rovnoměrně rozdělena mezi všechny nové balíčky. V důsledku toho doporučujeme, abyste nepoužívané oblíbené balíčky převedli na co nejmenší možný počet balíčků.

#### <a name="popularity-transfer-chains"></a>Řetězce přenosů oblíbenosti

Zastaralý balíček nemůže přenést jeho oblíbenou hodnotu, pokud už z jiného zastaralého balíčku přinese oblíbenou oblíbenku. Řekněme například, že mám 3 balíčky:

* Můj zastaralý starší balíček `Contoso.First`
* Můj zastaralý starší balíček `Contoso.Second`
* Můj nový balíček, `Contoso.Latest`

Pokud `Contoso.First` převede svou oblíbenou `Contoso.Second,` operaci na `Contoso.Second` , nemůže přenést svou oblíbenou akci do `Contoso.Latest` . Místo toho doporučujeme, `Contoso.First` `Contoso.Second` abyste v `Contoso.Latest` případě scénáře [sloučení balíčků](#package-consolidations) převedli oblíbenosti obou i na.
