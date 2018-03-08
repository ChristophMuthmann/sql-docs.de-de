---
title: 'Beispiel: Erstellen von gleichgeordneten Elementen im EXPLICIT-Modus | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EXPLICIT FOR XML mode
ms.assetid: 8a57b765-a890-46a3-8b5f-5754e921ea6e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8fa42e6f30f7a37a2e438bb76b52916c8d710504
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="example-constructing-siblings-with-explicit-mode"></a>Beispiel: Erstellen von gleichgeordneten Elementen im EXPLICIT-Modus
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Angenommen, Sie möchten eine XML-Ausgabe mit Informationen zu Bestellungen konstruieren. Beachten Sie, dass das <`SalesPerson`>-Element und <`OrderDetail`>-Element gleichgeordnete Elemente sind. Jede Reihenfolge verfügt über ein <`OrderHeader`>-Element, ein <`SalesPerson`>-Element und mindestens ein <`OrderDetail`>-Element.  
  
```  
<OrderHeader SalesOrderID=... OrderDate=... CustomerID=... >  
  <SalesPerson SalesPersonID=... />  
  <OrderDetail SalesOrderID=... LineTotal=... ProductID=... OrderQty=... />  
  <OrderDetail SalesOrderID=... LineTotal=... ProductID=... OrderQty=.../>  
      ...  
</OrderHeader>  
<OrderHeader ...</OrderHeader>  
```  
  
 Die folgende Abfrage im EXPLICIT-Modus konstruiert diese XML-Ausgabe. Beachten Sie, dass die Abfrage den `Tag`-Wert 1 für das <`OrderHeader`>-Element, den Wert 2 für das <`SalesPerson`>-Element und den Wert 3 für das <`OrderDetail`>-Element angibt. Da <`SalesPerson`> und <`OrderDetail`> gleichgeordnet sind, gibt die Abfrage für beide denselben `Parent`-Tagwert 1 für das <`OrderHeader`>-Element an.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        SalesOrderID  as [OrderHeader!1!SalesOrderID],  
        OrderDate     as [OrderHeader!1!OrderDate],  
        CustomerID    as [OrderHeader!1!CustomerID],  
        NULL          as [SalesPerson!2!SalesPersonID],  
        NULL          as [OrderDetail!3!SalesOrderID],  
        NULL          as [OrderDetail!3!LineTotal],  
        NULL          as [OrderDetail!3!ProductID],  
        NULL          as [OrderDetail!3!OrderQty]  
FROM   Sales.SalesOrderHeader  
WHERE     SalesOrderID=43659 or SalesOrderID=43661  
UNION ALL   
SELECT 2 as Tag,  
       1 as Parent,  
        SalesOrderID,  
        NULL,  
        NULL,  
        SalesPersonID,    
        NULL,           
        NULL,           
        NULL,  
        NULL           
FROM   Sales.SalesOrderHeader  
WHERE     SalesOrderID=43659 or SalesOrderID=43661  
UNION ALL  
SELECT 3 as Tag,  
       1 as Parent,  
        SOD.SalesOrderID,  
        NULL,  
        NULL,  
        SalesPersonID,  
        SOH.SalesOrderID,  
        LineTotal,  
        ProductID,  
        OrderQty     
FROM    Sales.SalesOrderHeader SOH,Sales.SalesOrderDetail SOD  
WHERE   SOH.SalesOrderID = SOD.SalesOrderID  
AND     (SOH.SalesOrderID=43659 or SOH.SalesOrderID=43661)  
ORDER BY [OrderHeader!1!SalesOrderID], [SalesPerson!2!SalesPersonID],  
         [OrderDetail!3!SalesOrderID],[OrderDetail!3!LineTotal]  
FOR XML EXPLICIT;  
```  
  
 Dies ist das Teilergebnis:  
  
 `<OrderHeader SalesOrderID="43659" OrderDate="2005-07-01T00:00:00" CustomerID="676">`  
  
 `<SalesPerson SalesPersonID="279" />`  
  
 `<OrderDetail SalesOrderID="43659" LineTotal="10.373000" ProductID="712" OrderQty="2" />`  
  
 `<OrderDetail SalesOrderID="43659" LineTotal="28.840400" ProductID="716" OrderQty="1" />`  
  
 `<OrderDetail SalesOrderID="43659" LineTotal="34.200000" ProductID="709" OrderQty="6" />`  
  
 `...`  
  
 `</OrderHeader>`  
  
 `<OrderHeader SalesOrderID="43661" OrderDate="2005-07-01T00:00:00" CustomerID="442">`  
  
 `<SalesPerson SalesPersonID="282" />`  
  
 `<OrderDetail SalesOrderID="43661" LineTotal="20.746000" ProductID="712" OrderQty="4" />`  
  
 `<OrderDetail SalesOrderID="43661" LineTotal="40.373000" ProductID="711" OrderQty="2" />`  
  
 `...`  
  
 `</OrderHeader>`  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwenden des EXPLICIT-Modus mit FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
