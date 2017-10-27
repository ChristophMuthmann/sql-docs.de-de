---
title: Spalten mit als Platzhalterzeichen angegebenen Namen | Microsoft-Dokumentation
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
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e03000db7890bd87e22799b6bf525b9a1194c2a4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>Spalten mit als Platzhalterzeichen angegebenen Namen
  Wenn der angegebene Spaltenname aus einem Platzhalterzeichen (\*) besteht, wird der Inhalt der betroffenen Spalte so eingefügt, als wäre kein Spaltenname angegeben. Wenn die Spalte nicht vom Typ**xml** ist, wird der Inhalt der Spalte als Textknoten eingefügt, wie im folgenden Beispiel gezeigt:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 Dies ist das Ergebnis:  
  
 `<row EmpID="1">KenJSánchez</row>`  
  
 Wenn die Spalte vom Typ **xml** ist, wird die entsprechende XML-Struktur eingefügt. Die folgende Abfrage gibt beispielsweise "*" als Name der Spalte an, die den XML-Code enthält, der von der XQuery für die Instructions-Spalte zurückgegeben wurde.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
GO  
```  
  
 Dies ist das Ergebnis. Der von der XQuery zurückgegebene XML-Code wird ohne Wrapperelement eingefügt.  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location LocationID="10">...</MI:Location>`  
  
 `<MI:Location LocationID="20">...</MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des PATH-Modus mit FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  

