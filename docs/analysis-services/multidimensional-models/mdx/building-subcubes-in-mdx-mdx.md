---
title: "Erstellen von Teilcubes in MDX (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Abfragen [MDX], Teilcubes"
  - "Teilcubes [MDX]"
  - "Gefilterte Sichten [MDX]"
  - "MDX [Analysis Services], Teilcubes"
  - "Mehrdimensionale Ausdrücke [Analysis Services], Teilcubes"
  - "CREATE SUBCUBE-Anweisung"
ms.assetid: 5403a62b-99ac-4d83-b02a-89bf78bf0f46
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 31
---
# Erstellen von Teilcubes in MDX (MDX)
  Ein Teilcube ist eine Teilmenge eines Cubes, die einer gefilterten Sicht der zugrunde liegenden Daten entspricht. Durch Begrenzen des Cubes auf einen Teilcube können Sie die Abfrageleistung verbessern.  
  
 Zum Definieren eines Teilcubes verwenden Sie die in diesem Thema beschriebene [CREATE SUBCUBE](../Topic/CREATE%20SUBCUBE%20Statement%20\(MDX\).md) -Anweisung.  
  
## Syntax von CREATE SUBCUBE  
 Verwenden Sie die folgende Syntax, um einen Teilcube zu erstellen:  
  
```  
CREATE SUBCUBE Subcube_Identifier AS Subcube_Expression  
```  
  
 Die Syntax von CREATE SUBCUBE ist recht einfach. Der *Subcube_Identifier*-Parameter gibt den Cube an, auf dem der Teilcube basieren soll. Der *Subcube_Expression*-Parameter wählt den Teil des Cubes aus, der zum Teilcube werden soll.  
  
 Nachdem Sie einen Teilcube erstellt haben, wird dieser Teilcube so lange der Kontext für alle MDX-Abfragen, bis Sie die Sitzung geschlossen oder die [DROP SUBCUBE](../Topic/DROP%20SUBCUBE%20Statement%20\(MDX\).md) -Anweisung ausgeführt haben.  
  
### Inhalt eines Teilcubes  
 Obwohl die CREATE SUBCUBE-Anweisung recht einfach zu verwenden ist, zeigt die Anweisung selbst nicht explizit alle Elemente, die Bestandteil eines Teilcubes werden. Für das Definieren eines Teilcubes gelten folgende Regeln:  
  
-   Wenn Sie das **(All)**-Element einer Hierarchie einfügen, fügen Sie jedes Element dieser Hierarchie ein.  
  
-   Wenn Sie ein Element einfügen, fügen Sie auch die Vorgänger und Nachfolger dieses Elements ein.  
  
-   Wenn Sie jedes Element einer Ebene einfügen, fügen Sie alle Elemente aus der Hierarchie ein. Elemente aus anderen Hierarchien werden ausgeschlossen, wenn diese Elemente keine Elemente auf der Ebene haben (beispielsweise eine unausgeglichene Hierarchie: etwa eine Stadt, für die es keine Kunden gibt).  
  
-   Ein Teilcube enthält immer jedes **(All)**-Element aus dem Cube.  
  
 Aggregatwerte im Teilcube werden visuell summiert. Ein Teilcube enthält beispielsweise `USA`, `WA`und `OR`. Der Aggregatwert für `USA` ist die Summe aus `{WA,OR}` , weil `WA` und `OR` die einzigen Staaten sind, die durch den Teilcube definiert sind. Alle anderen Staaten werden ignoriert.  
  
 Explizite Verweise auf Zellen, die sich außerhalb des Teilcubes befinden, geben Zellwerte zurück, die im Kontext des gesamten Cubes ausgewertet wurden. Beispielsweise erstellen Sie einen Teilcube, der auf das aktuelle Jahr beschränkt ist. Sie verwenden dann die [ParallelPeriod](../../../mdx/parallelperiod-mdx.md) -Funktion, um das aktuelle Jahr mit dem vorherigen Jahr zu vergleichen. Der Unterschied der Werte wird zurückgegeben, obwohl sich der Wert des vorherigen Jahres außerhalb des Teilcubes befindet.  
  
 Wenn der ursprüngliche Kontext nicht überschrieben wurde, werden SET-Funktionen, die in einer untergeordneten SELECT-Anweisung ausgewertet werden, im Kontext dieser Anweisung ausgewertet. Wurde der Kontext überschrieben, werden SET-Funktionen im Kontext des gesamten Cubes ausgewertet.  
  
## Beispiel zu CREATE SUBCUBE  
 Im folgenden Beispiel wird ein Teilcube erstellt, der den Budget-Cube auf die Konten 4200 und 4300 beschränkt:  
  
 `CREATE SUBCUBE Budget AS SELECT {[Account].[Account].&[4200], [Account].[Account].&[4300] } ON 0 FROM Budget`  
  
 Nachdem für die Sitzung ein Teilcube erstellt wurde, werden alle weiteren Abfragen nicht mehr für den gesamten Cube, sondern nur noch für den Teilcube ausgeführt. Sie führen beispielsweise die folgende Abfrage aus. Diese Abfrage gibt nur Elemente von den Konten 4200 und 4300 zurück.  
  
 `SELECT [Account].[Account].Members ON 0, Measures.Members ON 1 FROM Budget`  
  
## Siehe auch  
 [Festlegen des Cubekontexts in einer Abfrage &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)   
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  