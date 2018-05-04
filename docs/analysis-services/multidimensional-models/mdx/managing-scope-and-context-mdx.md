---
title: Verwalten von Gültigkeitsbereich und Kontext (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c28d82a47821af0903f5b60747c47b4f4ca86c75
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="managing-scope-and-context-mdx"></a>Verwalten von Gültigkeitsbereich und Kontext (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] kann ein MDX-Skript (Multidimensional Expressions) für den gesamten Cube oder, an bestimmten Stellen in der Ausführung des Skripts, für bestimmte Bereiche des Cubes gelten. Ein MDX-Skript kann, indem Berechnungsdurchläufe verwendet werden, einen mehrstufigen Ansatz für Berechnungen in einem Cube haben.  
  
> [!NOTE]  
>  Weitere Informationen über die Auswirkungen von Berechnungsdurchläufe auf Berechnungen finden Sie unter [Grundlegendes zu Durchlauf- und Lösungsreihenfolge &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
 Um den Berechnungsdurchlauf, den Gültigkeitsbereich und den Kontext in einem MDX-Skript zu steuern, verwenden Sie speziell die CACULATE-Anweisung, die **This** -Funktion und die SCOPE-Anweisung.  
  
## <a name="using-the-calculate-statement"></a>Verwenden der CALCULATE-Anweisung  
 Die CALCULATE-Anweisung füllt jede Zelle im Cube mit aggregierten Daten auf. Im MDX-Standardskript gibt es z. B. eine einzelne CALCULATE-Anweisung am Anfang des Skripts.  
  
 Weitere Informationen zur Syntax der CALCULATE-Anweisung finden Sie unter [CALCULATE-Anweisung &#40;MDX&#41;](../../../mdx/mdx-scripting-calculate.md).  
  
> [!NOTE]  
>  Enthält das Skript eine SCOPE-Anweisung, die eine CALCULATE-Anweisung enthält, wertet MDX die CALCULATE-Anweisung nicht für den gesamten Cube, sondern im Kontext des Teilcubes aus, der durch die SCOPE-Anweisung definiert ist.  
  
## <a name="using-the-this-function"></a>Verwenden der This-Funktion  
 Mit der **This** -Funktion können Sie in einem MDX-Skript den aktuellen Teilcube abrufen. Sie können die **This** -Funktion dazu verwenden, die Werte von Zellen im aktuellen Teilcube auf einen MDX-Ausdruck festzulegen. Die **This** -Funktion wird häufig zusammen mit der SCOPE-Anweisung verwendet, um den Inhalt eines bestimmten Teilcubes im Verlauf eines bestimmten Berechnungsdurchlaufs zu ändern.  
  
> [!NOTE]  
>  Enthält das Skript eine SCOPE-Anweisung, die eine **This** -Funktion enthält, wertet MDX die **This** -Funktion nicht für den gesamten Cube, sondern im Kontext des Teilcubes aus, der durch die SCOPE-Anweisung definiert ist.  
  
### <a name="this-function-example"></a>Beispiel zur This-Funktion  
 Im folgenden Beispiel eines MDX-Skriptbefehls wird die **This**-Funktion dazu verwendet, den Wert der Gruppe „Amount measure“ (in der Gruppe „Finance measure“ des [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]-Beispielcubes) für die untergeordneten Elemente des Redmond-Elements in der Customer-Dimension (Kunden) um 10 % zu erhöhen:  
  
```  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 Weitere Informationen zur Syntax der **This**-Funktion finden Sie unter [This &#40;MDX&#41;](../../../mdx/this-mdx.md).  
  
## <a name="using-the-scope-statement"></a>Verwenden der SCOPE-Anweisung  
 Die SCOPE-Anweisung definiert in einem MDX-Skript den aktuellen Teilcube, der weitere MDX-Ausdrücke und -Anweisungen enthält sowie deren Gültigkeitsbereich angibt. MDX wertet diese weiteren MDX-Ausdrücke und -Anweisungen einschließlich der **This** -Funktion und der CALCULATE-Anweisung im Kontext des Teilcubes aus.  
  
 Eine SCOPE-Anweisung ist dynamisch, aber nicht iterativ. Die Anweisungen, die in einer SCOPE-Anweisung enthalten sind, werden einmal ausgeführt, der Teilcube selbst kann aber dynamisch festgelegt werden. Angenommen, Sie haben einen Teilcube mit dem Namen SampleCube. Sie führen die folgende SCOPE-Anweisung für den SampleCube-Cube aus, um einen Teilcube zu definieren, der den Kontext als ALLMEMBERS in der Measures-Dimension definiert:  
  
 `SCOPE([Measures].ALLMEMBERS);`  
  
 `THIS = [Measures].ALLMEMBERS.COUNT;`  
  
 `END SCOPE;`  
  
 Die Anweisungen und Ausdrücke in dieser SCOPE-Anweisung werden einmal ausgeführt.  
  
 Jetzt führt ein Anwender im geschäftlichen Bereich die folgende MDX-Abfrage, die ein Measure mit dem Namen ExistingMeasure enthält, für den SampleCube-Cube aus:  
  
 `WITH MEMBER [Measures].[NewMeasure] AS '1'`  
  
 `SELECT`  
  
 `[Measures].ALLMEMBERS ON COLUMNS,`  
  
 `[Customer].DEFAULTMEMBER ON ROWS`  
  
 `FROM`  
  
 `[SampleCube]`  
  
 Das von der Abfrage zurückgegebene Cellset sieht in etwa so aus, wie die in der folgenden Tabelle gezeigte Ausgabe.  
  
||[ExistingMeasure]|[NewMeasure]|  
|-|-------------------------|--------------------|  
|[Customer].[All]|2|2|  
  
 Anhand des zurückgegebenen Cellsets können Sie sehen, wie der ExistingMeasure-Wert, der im MDX-Skript in der SCOPE-Anweisung enthalten ist, dynamisch aktualisiert wird, nachdem das NewMeasure-Measure definiert wurde.  
  
 SCOPE-Anweisungen können ineinander geschachtelt werden. Da die SCOPE-Anweisung aber nicht iterativ ist, besteht der Hauptzweck für das Schachteln von SCOPE-Anweisungen darin, einen Teilcube für eine spezielle Bearbeitung weiter zu unterteilen.  
  
### <a name="scope-statement-example"></a>Beispiel für die SCOPE-Anweisung  
 Im folgenden MDX-Skriptbeispiel wird eine SCOPE-Anweisung dazu verwendet, den Wert des Amount-Measures (in der Finance-Measuregruppe des [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] -Beispielcubes) für die untergeordneten Elemente des Redmond-Elements in der Customer-Dimension um 10 % zu erhöhen. Eine weitere SCOPE-Anweisung ändert allerdings den Teilcube so, dass er das Amount-Measure für die untergeordneten Elemente des Kalenderjahres 2002 enthält. Schließlich wird das Amount-Measure nur für diesen Teilcube aggregiert, sodass die aggregierten Werte für das Amount-Measure für andere Kalenderjahre nicht geändert werden.  
  
```  
/* Calculate the entire cube first. */  
CALCULATE;  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 Weitere Informationen zur Syntax der SCOPE-Anweisung finden Sie unter [SCOPE-Anweisung &#40;MDX&#41;](../../../mdx/mdx-scripting-scope.md).  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Sprachreferenz & #40; MDX & #41;](../../../mdx/mdx-language-reference-mdx.md)   
 [Die grundlegende MDX-Skripts & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)   
 [Grundlegendes zu MDX-Abfrage & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
