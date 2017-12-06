---
title: Atomisierung (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1b35d5e55a2d0e913586e7c60d161e4e2e85c6cb
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="atomization-xquery"></a>Atomisierung (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atomisierung ist das Verfahren, durch das der typisierte Wert eines Elements extrahiert wird. Dieses Verfahren wird unter bestimmten Umständen implizit verwendet. Bestimmte XQuery-Operatoren, wie z. B. arithmetische und Vergleichsoperatoren, sind von diesem Verfahren abhängig. Beispielsweise, wenn Sie arithmetische Operatoren direkt auf Knoten anwenden, der typisierte Wert eines Knotens wird zuerst abgerufen, implizit Aufrufen der [Data-Funktion](../xquery/data-accessor-functions-data-xquery.md). Auf diese Weise wird der atomare Wert dem arithmetischen Operator als Operand übergeben.  
  
 Die folgende Abfrage gibt beispielsweise den Gesamtwert der LaborHours-Attribute zurück. In diesem Fall **data()** implizit auf die Attributknoten angewendet wird.  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 Obwohl nicht erforderlich, Sie können auch explizit festlegen, die **data()** Funktion:  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 Ein anderes Beispiel für die implizite Atomisierung ist das Verwenden von arithmetischen Operatoren. Die  **+**  Operator erfordert atomare Werten und **data()** implizit angewendet, um den atomaren Wert des LaborHours-Attributs abzurufen. Die Abfrage wird angegeben, für die Instructions-Spalte von der **Xml** Typ in der ProductModel-Tabelle. Die folgende Abfrage gibt das LaborHours-Attribut dreimal zurück. Beachten Sie in der Abfrage Folgendes:  
  
-   Bei der Konstruktion des OriginalLaborHours-Attributs wird die Atomisierung implizit auf die von (`$WC/@LaborHours`) zurückgegebene Singleton-Sequenz angewendet. Der typisierte Wert des LaborHours-Attributs wird anschließend dem OriginalLaborHours-Attribut zugewiesen.  
  
-   Bei der Konstruktion des UpdatedLaborHoursV1-Attributs macht der arithmetische Operator atomare Werte erforderlich. Aus diesem Grund **data()** implizit auf das zurückgegebene LaborHours-Attribut angewendet wird (`$WC/@LaborHours`). Anschließend wird dem Attribut der atomare Wert 1 hinzugefügt. Die Konstruktion des updatedlaborhoursv2 zeigt die explizite Anwendung von **data()**, ist jedoch nicht erforderlich.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location[1]  
        return  
            <WC OriginalLaborHours = "{ $WC/@LaborHours }"  
                UpdatedLaborHoursV1 = "{ $WC/@LaborHours + 1 }"   
                UpdatedLaborHoursV2 = "{ data($WC/@LaborHours) + 1 }" >  
            </WC>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Dies ist das Ergebnis:  
  
```  
<WC OriginalLaborHours="2.5"   
    UpdatedLaborHoursV1="3.5"   
    UpdatedLaborHoursV2="3.5" />  
```  
  
 Aus der Atomisierung ergibt sich eine Instanz eines einfachen Datentyps, ein leeres Dataset oder ein Fehler bezüglich des statischen Typs.  
  
 Atomisierung tritt auch in Parametern an Funktionen, Rückgabewerte von Funktionen übergeben **cast()** Ausdrücke und Reihenfolge in der Order by-Klausel übergebenen Ausdrücken.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Grundlagen](../xquery/xquery-basics.md)   
 [Vergleichsausdrücke &#40; XQuery &#41;](../xquery/comparison-expressions-xquery.md)   
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
