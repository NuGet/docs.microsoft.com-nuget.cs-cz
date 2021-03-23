---
ms.openlocfilehash: 585537c5e3c7b27e0c7c312db19723d952421ce3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859550"
---
Žádný příspěvek je moc velký nebo moc malý.

1. Přejděte na stránku, kterou upravíte v [docs.Microsoft.com/NuGet](https://docs.microsoft.com/nuget/), a pak klikněte na tlačítko **Upravit** v pravém horním rohu. Tím se vám zobrazí příslušná stránka Markdownu v úložišti.
1. Upravte Markdownu:
    1. Pokud zahrnujete obrázky (obecně se používají PNGs), umístěte je do složky Media, která je ve složce tématu. Odkazy jsou pak `media/<image_name>.png` .
    1. Relativní odkazy na jiné stránky v tomto docset by měly být ve formě, `../<folder>/<topic-file>.md` včetně školení `.md` . Pokud vytváříte odkaz na jiné téma ve stejné složce, `../<folder>/` můžete ho vynechat. Při použití kotev vždy nezapomeňte zahrnout `.md` před `#` .
    1. Pokud používáte externí odkazy, zejména pro docs.microsoft.com (nebo msdn.microsoft.com pro libovolný starší obsah), vynechejte libovolnou značku jazyka, jako je "en-US", aby čtenář v jiném jazyce mohl mít cílovou stránku v tomto jazyce, pokud je k dispozici.
1. Až skončíte, zadejte níže potvrzující zprávu a klikněte na **navrhnout změnu souboru**.
1. Odešlete žádost o přijetí změn pro vaši změnu. Pravidelně kontrolujte pr.
1. Děkujeme!

Pokud vytváříte nové téma, mějte na paměti i následující:

1. Nové téma vždy umístěte do příslušné podsložky a podle toho, jak se tady zobrazí, postupujte podle konvencí pro názvy souborů.
1. Blok metadat musíte zahrnout, když vidíte v jiných tématech. Typické výchozí hodnoty (například pro MS. zatížení a MS. kontrolor) jsou nastaveny v rámci docs/docjx.jsna, takže potřebujete změnit pouze následující:

  - title: název, který se zobrazí ve výsledcích hledání. Pro SEO to ideální není totéž jako # (H1) na nejvyšší úrovni článku.
  - Popis: abstrakce článku, který se zobrazí ve výsledcích hledání.
  - Autor: ID GitHubu autora, ke kterému se přiřadí soubory pro tento článek.
  - MS. Author: Pokud je autor zaměstnancem Microsoftu, jedná se o alias společnosti Microsoft. Slouží k vytváření sestav a předávání zpětné vazby z jiných kanálů.
  - manažer: alias společnosti Microsoft manažera autora, pokud je k dispozici.
  - MS. Date: datum poslední revize nebo revize článku ve formátu mm/dd/rrrr (použití počátečních nul). Toto je komunikace ke čtečce o aktuálnosti, takže se neaktualizovala na menší změny, jenom pro důležitější revize nebo na to, že se článek znovu ověřil, i když se nemění.
  - MS. téma: používá se k kategorizaci článku v sestavách. Viz tabulka níže. Většina článků je "koncepční". 
1. Kromě přidání stránky přidejte do složky docs/TOC. MD odkaz na tuto stránku.
1. Pokud přidáváte uzel nejvyšší úrovně do obsahu, vytvořte také pro něj záznam v docs/index. MD.

| kategorie MS. téma | Popis |
| --- | --- |
| ilustrační | Použijte pro jakýkoliv obsah, který nepatří do jiného. Tato hodnota je nastavena jako výchozí v docfx.jsna. |
| overview | Tato možnost se používá pro všechny články s přehledem nebo s uživatelskými příručkami, obvykle jenom těch, které jsou v obsahu v uzlu "Přehled". |
| rychlý Start | Cokoli pod uzlem "rychlý Start" v obsahu, který je vytvořen podle pokynů pro rychlý Start. |
| tutoriál | Cokoli pod uzlem "kurz" v obsahu, který je vytvořen podle pokynů pro kurzy. |
| reference | Jakýkoli článek typu odkazu, který není automaticky vygenerován. |
| article | Použijte k obsahu poskytovanému komunitou (to znamená cokoli mimo technický tým nebo tým docs v Microsoftu. |
