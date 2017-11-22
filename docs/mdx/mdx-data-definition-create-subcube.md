---
title: CREATE SUBCUBE-Anweisung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SUBCUBE
- CREATE SUBCUBE
- CREATE
- SUBCUBE
dev_langs: kbMDX
helpviewer_keywords:
- subcubes [MDX]
- CREATE SUBCUBE statement
ms.assetid: 15b6ac4c-b68a-4f9f-b33c-f5f7c4a74535
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5fd57d53dd07238781c452730f00e526fb6c2fff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---create-subcube"></a>MDX-Datendefinition - Erstellen von TEILCUBES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Definiert den Cuberaum eines angegebenen Cubes oder Teilcubes neu zu einem angegebenen Teilcube. Diese Anweisung ändert den scheinbaren Cuberaum für nachfolgende Operationen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE SUBCUBE Cube_Name AS Select_Statement  
                                                  | NON VISUAL ( Select_Statement )  
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Der gültige Zeichenfolgenausdruck, der den Namen des Cubes oder der Perspektive bereitstellt, der/die eingeschränkt wird, und der zur Benennung des Teilcubes verwendet wird.  
  
 *Select_Statement*  
 Ein gültiger SELECT-Ausdruck in MDX (Multidimensional Expressions), der keine WITH-, NON EMPTY- oder HAVING-Klausel enthält und keine Dimensions- oder Zelleigenschaften anfordert.  
  
 Finden Sie unter [Anweisung &#40; auswählen MDX &#41; ](../mdx/mdx-data-manipulation-select.md) für eine ausführliche Erläuterung der Syntax für Select-Anweisungen und die **NON VISUAL** Klausel.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Standardelemente in der Definition eines Teilcubes ausgeschlossen werden, ändern sich die Koordinaten entsprechend. Für Attribute, die aggregiert werden können, wird [All] zum Standardelement erklärt. Für Attribute, die nicht aggregiert werden können, wird ein im Teilcube vorhandenes Element zum Standardelement. In der folgenden Tabelle sind Beispiele für Kombinationen aus Teilcubes und Standardelementen aufgeführt.  
  
|Ursprüngliches Standardelement|Kann aggregiert werden|Untergeordneter SELECT-Ausdruck|Geändertes Standardelement|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|Time.Year.All|ja|{Time.Year.2003}|Keine Änderung|  
|Time.Year. [1997]|ja|{Time.Year.2003}|Time.Year.All|  
|Time.Year. [1997]|Nein|{Time.Year.2003}|Time.Year. [2003]|  
|Time.Year. [1997]|ja|{Time.Year.2003, Time.Year.2004}|Time.Year.All|  
|Time.Year. [1997]|Nein|{Time.Year.2003, Time.Year.2004}|Entweder Time.Year.[2003] oder<br /><br /> Time.Year.[2004]|  
  
 [All]-Elemente sind immer in einem Teilcube vorhanden.  
  
 Sitzungsobjekte, die im Kontext eines Teilcubes erstellt wurden, werden gelöscht, wenn der Teilcube gelöscht wird.  
  
 Weitere Informationen zu Teilcubes finden Sie unter [Erstellen von Teilcubes in MDX &#40; MDX &#41; ](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein Teilcube erstellt, der den scheinbaren Cuberaum auf Elemente einschränkt, die gemeinsam mit dem Land Kanada vorhanden sind. Es verwendet dann die **Elemente** Funktion, um alle Elemente der Country von der Geography eine benutzerdefinierte Hierarchie zurückzugeben, wobei lediglich das Land Kanada zurückgegeben.  
  
```  
CREATE SUBCUBE [Adventure Works] AS  
   SELECT [Geography].[Country].&[Canada] ON 0  
   FROM [Adventure Works]  
  
SELECT [Geography].[Country].[Country].MEMBERS ON 0  
   FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird ein Teilcube erstellt, der den sichtbaren Cuberaum auf die Elemente {Accessories, Clothing} in Products.Category und die Elemente {[Value Added Reseller], [Warehouse]} in Resellers.[Business Type] einschränkt.  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works]`  
  
 Die Abfrage des Teilcubes nach allen Elementen in Products.Category und Resellers.[Business Type] mit der folgenden MDX-Anweisung:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Führt zu folgenden Ergebnissen:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$2,031,079.39|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$767,388.52|$175,002.81|$592,385.71|  
|Warehouse|$1,263,690.86|$331,169.64|$932,521.23|  
  
 Durch das Löschen und erneute Erstellen des Teilcubes mit der NON VISUAL-Klausel wird ein Teilcube erstellt, der die tatsächlichen Gesamtsummen für alle Elemente in Products.Category und Resellers.[Business Type] beibehält, unabhängig davon, ob sie im Teilcube sichtbar sind.  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 Wird dieselbe MDX-Abfrage wie oben ausgeführt:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Ergibt dies die folgenden abweichenden Ergebnisse:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$80,450,596.98|$571,297.93|$1,777,840.84|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Die Spalte [All Products] und die Zeile [All Resellers] enthalten die Gesamtsummen für alle Elemente, nicht nur die Gesamtsummen der sichtbaren Elemente.  
  
## <a name="see-also"></a>Siehe auch  
 [Schlüsselkonzepte in MDX &#40; Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX-Skriptanweisungen &#40; MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [DROP SUBCUBE-Anweisung &#40; MDX &#41;](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT-Anweisung &#40; MDX &#41;](../mdx/mdx-data-manipulation-select.md)  
  
  
