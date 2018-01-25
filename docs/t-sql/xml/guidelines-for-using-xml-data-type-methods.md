---
title: "Richtlinien für die Verwendung von Xml-Datentypmethoden | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79f10b22ba88d6dd860c608c9468e20a27615650
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>Richtlinien zum Verwenden von Methoden des xml-Datentyps
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dieses Thema enthält Richtlinien zum Verwenden der **Xml** -Datentypmethoden.  
  
## <a name="the-print-statement"></a>Die PRINT-Anweisung  
 Die **Xml** -Datentypmethoden können nicht in der PRINT-Anweisung verwendet werden, wie im folgenden Beispiel gezeigt. Die **Xml** -Datentypmethoden werden als Unterabfragen behandelt und Unterabfragen sind in der PRINT-Anweisung nicht zulässig. Aus diesem Grund gibt das folgende Beispiel einen Fehler zurück:  
  
```  
DECLARE @x xml  
SET @x = '<root>Hello</root>'  
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)   
```  
  
 Eine Lösung besteht darin, zuerst das Ergebnis des Zuweisen der **value()** Methode, um eine Variable des **Xml** geben, und geben Sie die Variable in der Abfrage.  
  
```  
DECLARE @x xml  
DECLARE @c varchar(max)  
SET @x = '<root>Hello</root>'  
SET @c = @x.value('/root[1]', 'varchar(11)')  
PRINT @c                                                        
```  
  
## <a name="the-group-by-clause"></a>Die GROUP BY-Klausel  
 Die **Xml** -Datentypmethoden werden intern als Unterabfragen behandelt. Da GROUP BY einen Skalarwert erfordert und keine Aggregate oder Unterabfragen lässt, Sie können keine angeben der **Xml** -Datentypmethoden in der GROUP BY-Klausel. Eine mögliche Lösung besteht im Aufrufen einer benutzerdefinierten Funktion, innerhalb derer XML-Methoden verwendet werden.  
  
## <a name="reporting-errors"></a>Erstellen von Fehlerberichten  
 Beim Melden von Fehlern, **Xml** -Datentypmethoden auslösen einen einzelnen Fehler in das folgende Format:  
  
```  
Msg errorNumber, Level levelNumber, State stateNumber:  
XQuery [database.table.method]: description_of_error  
```  
  
 Beispiel:  
  
```  
Msg 2396, Level 16, State 1:  
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element  
```  
  
## <a name="singleton-checks"></a>Singleton-Überprüfungen  
 Positionsschritte, Funktionsparameter und Operatoren, die Singleton-Elemente benötigen, geben einen Fehler zurück, wenn der Compiler nicht ermitteln kann, ob zur Laufzeit ein Singleton-Element sichergestellt ist. Dieses Problem tritt häufig bei nicht typisierten Daten auf. So erfordert z. B. die Suche eines Attributs ein übergeordnetes Singleton-Element. Dabei ist eine Ordinalzahl ausreichend, die einen einzelnen übergeordneten Knoten auswählt. Die Auswertung einer **node()**-**value()** Kombination zum Extrahieren von Attributwerten erfordern ggf. keine der Ordinalzahl. Dies ist im nächsten Beispiel dargestellt.  
  
### <a name="example-known-singleton"></a>Beispiel: Bekanntes Singleton  
 In diesem Beispiel wird die **nodes()** Methode generiert eine separate Zeile für jeden <`book`> Element. Die **value()** -Methode, die auf ausgewertet wird ein <`book`> Knoten extrahiert den Wert des @genre und ein Attribut ist ein Singleton.  
  
```  
SELECT nref.value('@genre', 'varchar(max)') LastName  
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)  
```  
  
 Das XML-Schema wird zur Typprüfung von typisiertem XML verwendet. Wenn ein Knoten im XML-Schema als ein Singleton angegeben ist, verwendet der Compiler diese Informationen, und es tritt kein Fehler auf. Ansonsten ist eine Ordinalzahl erforderlich, die einen einzelnen Knoten auswählt. Insbesondere wird die Verwendung von Descendant-or-Self-Achse (/ /) wie in/Book / / title geht die Singleton-Kardinalität Typrückschluss für verliert die \<Title > Element, auch wenn das XML-Schema gibt an, um entsteht. Deshalb sollten Sie ihn als (/book//title)[1] umschreiben.  
  
 Sie müssen sich des Unterschiedes zwischen //first-name[1] und (//first-name)[1] für die Typüberprüfung bewusst sein. Die erste gibt eine Sequenz von \<First-Name > Knoten in der jeder Knoten der am weitesten links stehende ist \<First-Name >-Knoten der gleichgeordneten. Der zweite Wert gibt den ersten Singleton \<First-Name > Knoten in Dokumentreihenfolge der XML-Instanz.  
  
### <a name="example-using-value"></a>Beispiel: Verwenden von value()  
 Die folgende Abfrage für eine nicht typisierte XML-Spalte führt zu einem statischen Kompilierungsfehler. Grund hierfür ist, **value()** erwartet einen Singleton-Knoten als erstes Argument und der Compiler bestimmen können, ob nur ein \<Last-Name > Knoten wird zur Laufzeit auftreten:  
  
```  
SELECT xCol.value('//author/last-name', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 Es folgt eine Projektmappe, die Sie in Betracht ziehen könnten:  
  
```  
SELECT xCol.value('//author/last-name[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 Der Fehler wird auf diese Weise jedoch nicht behoben, da in jeder XML-Instanz mehrere <`author`>-Knoten vorhanden sein können. Die folgende umgeschriebene Version ist jedoch funktionsfähig:  
  
```  
SELECT xCol.value('(//author/last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 Diese Abfrage gibt den Wert des ersten `<last-name>`-Elements in jeder XML-Instanz zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [xml Data Type Methods (xml-Datentypmethoden)](../../t-sql/xml/xml-data-type-methods.md)  
  
  
