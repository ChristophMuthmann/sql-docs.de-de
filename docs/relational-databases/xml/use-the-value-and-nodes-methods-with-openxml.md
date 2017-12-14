---
title: Verwenden der value()-Methode und der nodes()-Methode mit OPENXML | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OpenXML method [XML in SQL Server]
- value method [XML in SQL Server]
- nodes method [XML in SQL Server]
ms.assetid: c73dbe55-d685-42eb-b0ee-9f3c5b9d97f3
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82e2e1da18b277dc23ab249505e27907ab8d39e0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="use-the-value-and-nodes-methods-with-openxml"></a>Verwenden der value()-Methode und der nodes()-Methode mit OPENXML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Sie können mehrere **value()**-Methoden für den **xml**-Datentyp in einer **SELECT**-Klausel verwenden, um ein Rowset aus extrahierten Werten zu generieren. Die **nodes()** -Methode ergibt einen internen Verweis für jeden ausgewählten Knoten, der für zusätzliche Abfragen verwendet werden kann. Die Kombination der Methoden **nodes()** und **value()** kann beim Generieren des Rowsets effizienter sein, wenn es über mehrere Spalten verfügt und möglicherweise auch, wenn die zu seiner Generierung verwendeten Pfadausdrücke komplex sind.  
  
 Die **nodes()**-Methode ergibt Instanzen eines speziellen **xml**-Datentyps, wobei bei jedem der Kontext auf einen unterschiedlichen ausgewählten Knoten festgelegt ist. Diese Art der XML-Instanz unterstützt **query()**-, **value()**-, **nodes()**- und **exist()**-Methoden und kann in **count(\*)**-Aggregationen verwendet werden. Alle anderen Verwendungen verursachen einen Fehler.  
  
## <a name="example-using-nodes"></a>Beispiel: Verwenden von nodes()  
 Angenommen, Sie wollen die Vornamen und Nachnamen von Autoren extrahieren, und der Vorname soll nicht "David" sein. Außerdem wollen Sie diese Informationen als ein Rowset extrahieren, das die beiden Spalten FirstName und LastName enthält. Durch Verwenden der Methoden **nodes()** und **value()** können Sie dieses Ziel erreichen, wie im folgenden Beispiel gezeigt:  
  
```  
SELECT nref.value('(first-name/text())[1]', 'nvarchar(50)') FirstName,  
       nref.value('(last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T CROSS APPLY xCol.nodes('//author') AS R(nref)  
WHERE  nref.exist('first-name[. != "David"]') = 1  
```  
  
 In diesem Beispiel ergibt `nodes('//author')` ein Rowset aus Verweisen auf `<author>` -Elemente für jede XML-Instanz. Die Vor- und Nachnamen der Autoren werden abgerufen, indem die **value()** -Methoden im Verhältnis zu diesen Verweisen ausgewertet werden.  
  
 SQL Server 2000 bietet die Möglichkeit zum Generieren eines Rowsets aus einer XML-Instanz durch Verwenden von **OpenXml()**. Sie können das relationale Schema für das Rowset angeben sowie, wie die Werte in der XML-Instanz den Spalten im Rowset zugeordnet sind.  
  
## <a name="example-using-openxml-on-the-xml-data-type"></a>Beispiel: Verwenden von OpenXml() für den xml-Datentyp  
 Die Abfrage aus dem vorherigen Beispiel kann mithilfe von **OpenXml()** umgeschrieben werden, wie im folgenden Beispiel gezeigt. Dies geschieht durch Erstellen eines Cursors, der jede XML-Instanz in eine XML-Variable einliest und dann für OpenXML auf sie anwendet:  
  
```  
DECLARE name_cursor CURSOR  
FOR  
   SELECT xCol   
   FROM   T  
OPEN name_cursor  
DECLARE @xmlVal XML  
DECLARE @idoc int  
FETCH NEXT FROM name_cursor INTO @xmlVal  
  
WHILE (@@FETCH_STATUS = 0)  
BEGIN  
   EXEC sp_xml_preparedocument @idoc OUTPUT, @xmlVal  
   SELECT   *  
   FROM   OPENXML (@idoc, '//author')  
          WITH (FirstName  varchar(50) 'first-name',  
                LastName   varchar(50) 'last-name') R  
   WHERE  R.FirstName != 'David'  
  
   EXEC sp_xml_removedocument @idoc  
   FETCH NEXT FROM name_cursor INTO @xmlVal  
END  
CLOSE name_cursor  
DEALLOCATE name_cursor   
```  
  
 **OpenXml()** erstellt eine arbeitsspeicherinterne Darstellung und verwendet Arbeitstabellen anstelle des Abfrageprozessors. Sie greift nicht auf das XQuery-Modul zurück, sondern auf den XPath-Prozessor Version 1.0 von MSXML Version 3.0. Die Arbeitstabellen werden nicht von mehreren Aufrufen von **OpenXml()**gemeinsam genutzt, selbst auf der gleichen XML-Instanz nicht. Damit ist ihre Skalierbarkeit eingeschränkt. **OpenXml()** ermöglicht Ihnen das Zugreifen auf ein Rahmentabellenformat für die XML-Daten, wenn die WITH-Klausel nicht angegeben ist. Außerdem ermöglicht es Ihnen das Verwenden des übrigen XML-Wertes in einer getrennten "Überlaufspalte".  
  
 Die Kombination aus den **nodes()** - und **value()** -Funktionen sorgt für eine effektive XML-Indizierung. Im Ergebnis kann diese Kombination eine größere Skalierbarkeit als **OpenXml**aufweisen.  
  
## <a name="see-also"></a>Siehe auch  
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
