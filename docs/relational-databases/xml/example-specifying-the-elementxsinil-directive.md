---
title: 'Beispiel: Angeben der ELEMENTXSINIL-Direktive | Microsoft-Dokumentation'
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
- ELEMENTXSINIL directive
ms.assetid: bbcb6f9e-a51b-4775-9795-947c9d6d758f
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 42f40e0a22457f365e27a6f1560bd2f496366294
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="example-specifying-the-elementxsinil-directive"></a>Beispiel: Angeben der ELEMENTXSINIL-Direktive
  Wenn Sie zum Abrufen einer elementzentrierten XML-Ausgabe die ELEMENT-Direktive angeben, und eine Spalte einen NULL-Wert aufweist, wird das entsprechende Element im EXPLICIT-Modus nicht generiert. Sie können optional die ELEMENTXSINIL-Direktive angeben, um das Generieren von Elementen für NULL-Werte anzufordern, wenn das **xsi:nil** -Attribut auf TRUE festgelegt ist.  
  
 Die folgende Abfrage konstruiert eine XML-Ausgabe, die die Adressen der Mitarbeiter enthält. Für die Spalten `AddressLine2` und `City` ist in den Spaltennamen die `ELEMENTXSINIL` -Direktive angegeben. So werden für NULL-Werte in der `AddressLine2` - und `City` -Spalte des Rowsets Elemente generiert.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID  as [Employee!1!EmpID],  
       BEA.AddressID as [Employee!1!AddressID],  
       NULL        as [Address!2!AddressID],  
       NULL        as [Address!2!AddressLine1!ELEMENT],  
       NULL        as [Address!2!AddressLine2!ELEMENTXSINIL],  
       NULL        as [Address!2!City!ELEMENTXSINIL]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       BEA.AddressID,  
       A.AddressID,  
       AddressLine1,   
       AddressLine2,  
       City   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BEA.AddressID = A.AddressID  
ORDER BY [Employee!1!EmpID],[Address!2!AddressID]  
FOR XML EXPLICIT;  
```  
  
 Dies ist das Teilergebnis:  
  
 `<Employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `EmpID="1" AddressID="249">`  
  
 `<Address AddressID="249">`  
  
 `<AddressLine1>4350 Minute Dr.</AddressLine1>`  
  
 `<AddressLine2 xsi:nil="true" />`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</Employee>`  
  
 `...`  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des EXPLICIT-Modus mit FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
