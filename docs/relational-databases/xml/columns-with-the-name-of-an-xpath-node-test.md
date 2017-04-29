---
title: Spalten mit dem Namen eines XPath-Knotentests | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- names [SQL Server], columns with
- XPath node test
ms.assetid: b48adccd-3b6b-486a-b326-20f57170186f
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 41bc7b31ff9f5185dcdfde4a90bbfe631fbef089
ms.lasthandoff: 04/11/2017

---
# <a name="columns-with-the-name-of-an-xpath-node-test"></a>Spalten mit Namen von XPath-Knotentests
  Wenn es sich bei dem Spaltennamen um einen der XPath-Knotentests handelt, wird der Inhalt zugeordnet, wie in der folgenden Tabelle gezeigt. Wenn der Spaltenname ein XPath-Knotentest ist, wird der Inhalt dem entsprechenden Knoten zugeordnet. Wenn der SQL-Typ der Spalte **xml**ist, wird ein Fehler zurückgegeben.  
  
|Spaltenname|Verhalten|  
|-----------------|--------------|  
|text()|Für eine Spalte mit dem Namen text() wird der Zeichenfolgenwert in dieser Spalte als Textknoten hinzugefügt.|  
|comment()|Für eine Spalte mit dem Namen comment() wird der Zeichenfolgenwert in dieser Spalte als XML-Kommentar hinzugefügt.|  
|node()|Für eine Spalte mit dem Namen node() ist das Ergebnis mit dem eines Platzhalter-Spaltennamens (*) identisch.|  
|processing-instruction(name)|Für eine Spalte mit dem Namen einer Verarbeitungsanweisung wird der Zeichenfolgenwert in dieser Spalte als PI-Wert für den Zielnamen der Verarbeitungsanweisung hinzugefügt.|  
  
 Die folgende Abfrage zeigt die Verwendung der Knotentests als Spaltennamen an. Dabei werden Textknoten und Kommentare im XML-Ergebnis hinzugefügt.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
        'Example of using node tests such as text(), comment(), processing-instruction()'                as "comment()",  
        'Some PI'                   as "processing-instruction(PI)",  
        'Employee name and address data' as "text()",  
        'middle name is optional'        as "EmpName/text()",  
        FirstName                        as "EmpName/First",   
        MiddleName                       as "EmpName/Middle",   
        LastName                         as "EmpName/Last",  
        AddressLine1                     as "Address/AddrLine1",  
        AddressLine2                     as "Address/AddrLIne2",  
        City                             as "Address/City"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P   
    ON P.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS BAE  
    ON BAE.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BAE.AddressID = A.AddressID  
WHERE  E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 Dies ist das Ergebnis:  
  
 `<row EmpID="1">`  
  
 `<!--Example of using node tests such as text(), comment(), processing-instruction() -->`  
  
 `<?PI Some PI?>`  
  
 `Employee name and address data`  
  
 `<EmpName>middle name is optional`  
  
 `<First>Ken</First>`  
  
 `<Last>Sánchez</Last>`  
  
 `</EmpName>`  
  
 `<Address>`  
  
 `<AddrLine1>4350 Minute Dr.</AddrLine1>`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</row>`  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des PATH-Modus mit FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
