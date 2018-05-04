---
title: UPDATE CUBE-Anweisung (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Cube
- UPDATE CUBE
- UPDATE_CUBE
- UPDATE
dev_langs:
- kbMDX
helpviewer_keywords:
- updating cubes
- cubes [Analysis Services], modifying
- modifying cubes
- UPDATE CUBE statement
ms.assetid: 6c8f23bb-401b-49de-843a-5324ac977239
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: e27b11836c0619c1415718cce3e38029ac8359d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-manipulation---update-cube"></a>Datenbearbeitung für MDX - UPDATE CUBE
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Mithilfe der UPDATE CUBE-Anweisung werden Daten in eine beliebige Zelle in einem Cube zurückgeschrieben, der mit der SUM-Aggregation in den übergeordneten Cube aggregiert wird. Weitere erläuterungen und ein Beispiel finden Sie unter "Grundlagen zu Zuordnungen" in diesem Blogbeitrag: [Erstellen einer Rückschreibeanwendung mit Analysis Services (Blog)](http://go.microsoft.com/fwlink/?LinkId=394977).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Eine gültige Zeichenfolge, die den Namen eines Cubes bereitstellt.  
  
 *Tuple_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Tupel zurückgibt.  
  
 *Neuer_Wert*  
 Ein gültiger numerischer Ausdruck.  
  
 *Weight_Expression*  
 Ein gültiger numerischer MDX-Ausdruck (Multidimensional Expressions), der einen Dezimalwert zwischen 0 und 1 zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Sie können den Wert einer angegebenen Blatt- oder Nichtblattzelle in einem Cube aktualisieren. Dabei wird den abhängigen Blattzellen optional der Wert für eine angegebene Nichtblattzelle zugeordnet. Bei der durch den Tupelausdruck angegebenen Zelle kann es sich um eine beliebige gültige Zelle im mehrdimensionalen Raum handeln (d. h., die Zelle muss keine Blattzelle sein). Allerdings muss die Zelle aggregiert werden, mit der [Summe](../mdx/sum-mdx.md) -Aggregatfunktion und dürfen kein berechnetes Element im Tupel, die verwendet wird, um die Zelle zu identifizieren.  
  
 Es kann hilfreich sein, vorstellen der **UPDATE CUBE** Anweisung als Unterroutine vorstellen, die automatisch eine Reihe von einzelnen Vorgänge zum Zellenrückschreiben Blatt- und inneren Zellen generiert, die eine angegebene Summe Rollup wird.  
  
 Im folgenden ist eine Beschreibung der Methoden der Zuordnung.  
  
 **USE_EQUAL_ALLOCATION:** jeder Blattzelle, die zur aktualisierten Zelle beiträgt wird basierten auf den folgenden Ausdruck derselbe Wert zugewiesen werden.  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:** jeder Blattzelle, die zur aktualisierten Zelle beiträgt, wird entsprechend dem folgenden Ausdruck geändert werden.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** jeder Blattzelle, die zur aktualisierten Zelle beiträgt zugewiesen wird derselbe Wert, der auf den folgenden Ausdruck basiert.  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** jeder Blattzelle, die zur aktualisierten Zelle beiträgt, wird entsprechend dem folgenden Ausdruck geändert werden.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 Wenn ein Gewichtungsausdruck nicht angegeben wird, die **UPDATE CUBE** Anweisung implizit den folgenden Ausdruck verwendet.  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 Ein Gewichtungsausdruck sollte als Dezimalwert zwischen 0 (null) und 1 ausgedrückt werden. Dieser Wert gibt das Verhältnis zum zugeordneten Wert an, den Sie den Blattzellen zuweisen möchten, die von der Zuordnung betroffen sind. Der Programmierer der Clientanwendung ist dafür verantwortlich, Ausdrücke zu erstellen, deren Rollupaggregatwerte gleich dem zugeordneten Wert des Ausdrucks sind.  
  
> [!CAUTION]  
>  Die Clientanwendung muss die gleichzeitige Zuordnung aller Dimensionen berücksichtigen, um unerwartete Ergebnisse, einschließlich falscher Rollupwerte oder inkonsistenter Daten, zu vermeiden.  
  
 Jede **UPDATE CUBE** Zuordnung sollte für transaktionale Zwecke atomar berücksichtigt werden. Das bedeutet, dass beim Fehlschlagen eines einzelnen Zuordnungsvorgangs, z. B. wegen eines Fehlers in einer Formel oder einer Sicherheitsverletzung, der gesamte UPDATE CUBE-Vorgang fehlschlägt. Bevor die Berechnungen der einzelnen Zuordnungsvorgänge verarbeitet werden, wird eine Momentaufnahme der Daten erstellt, um sicherzustellen, dass die sich ergebenden Berechnungen richtig sind.  
  
> [!CAUTION]  
>  Wenn die USE_WEIGHTED_ALLOCATION-Methode für ein Measure verwendet wird, das ganze Zahlen enthält, gibt die Methode möglicherweise aufgrund von inkrementellen Rundungsänderungen ungenaue Ergebnisse zurück.  
  
> [!IMPORTANT]  
>  Wenn sich die aktualisierten Zellen nicht überlagern, kann mithilfe der **Update Isolation Level** -Eigenschaft der Verbindungszeichenfolge das Leistungsverhalten in Bezug auf UPDATE CUBE verbessert werden.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [MDX-Datenbearbeitungsanweisungen &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
