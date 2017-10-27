---
title: Generieren von gleichgeordneten Elementen mit einer geschachtelten AUTO-Modusabfrage
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [XML in SQL Server], nested AUTO mode
- nested AUTO mode query
ms.assetid: 748d9899-589d-4420-8048-1258e9e67c20
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6d85a1b59656222cf07338d2eb98925e30a5c658
ms.contentlocale: de-de
ms.lasthandoff: 08/18/2017

---
# <a name="generate-siblings-with-a-nested-auto-mode-query"></a>Generieren von gleichgeordneten Elementen mit einer geschachtelten AUTO-Modusabfrage
  Im folgenden Beispiel wird das Generieren von gleichgeordneten Elementen durch Verwenden einer geschachtelten Abfrage im AUTO-Modus dargestellt. Die einzige Möglichkeit zum Generieren von derartigem XML-Code besteht im Verwenden des EXPLICIT-Modus. Dies kann jedoch sehr aufwändig sein.  
  
## <a name="example"></a>Beispiel  
 Diese Abfrage konstruiert XML-Code, der Bestellinformationen bereitstellt. Dazu gehören:  
  
-   Auftragskopfzeileninformationen, `SalesOrderID`, `SalesPersonID`und `OrderDate`. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] speichert diese Informationen in der `SalesOrderHeader` -Tabelle.  
  
-   Detaillierte Bestellinformationen. Dazu gehören Angaben zu einem oder mehreren bestellten Produkten, zum Einzelpreis und zur bestellten Menge. Diese Informationen werden in der `SalesOrderDetail` -Tabelle gespeichert.  
  
-   Informationen zum Vertriebsmitarbeiter. Dies ist der Vertriebsmitarbeiter, der die Bestellung entgegengenommen hat. Die `SalesPerson` -Tabelle stellt die Angaben für `SalesPersonID`bereit. Für diese Abfrage müssen Sie diese Tabelle mit der `Employee` -Tabelle verknüpfen, um den Namen des Vertriebsmitarbeiters zu finden.  
  
 Die beiden folgenden unterschiedlichen `SELECT`-Abfragen generieren XML-Code, der in seiner Form einen kleinen Unterschied aufweist.  
  
 Die erste Abfrage generiert XML-Code, in dem <`SalesPerson`> und <`SalesOrderHeader`> als gleichgeordnete Unterelemente von <`SalesOrder`> erscheinen:  
  
```  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID =   
                   SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
        FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
        for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As   
                     SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
```  
  
 In der vorherigen Abfrage bewirkt die äußerste `SELECT`-Anweisung Folgendes:  
  
-   Sie fragt das Rowset `SalesOrder` ab, das in der `FROM`-Klausel angegeben ist. Das Ergebnis ist ein XML-Code mit einem oder mehreren <`SalesOrder`>-Elementen.  
  
-   Gibt den `AUTO` -Modus und die `TYPE` -Direktive an. `AUTO` -Modus wird das Abfrageergebnis in XML umgewandelt, und von der `TYPE` -Direktive wird das Ergebnis als **xml** -Typ zurückgegeben.  
  
-   Sie schließt zwei geschachtelte `SELECT` -Anweisungen ein, die durch ein Komma voneinander getrennt sind. Die erste geschachtelte `SELECT` -Anweisung ruft die Bestellinformationen (Kopfzeile und Details) ab, und die zweite geschachtelte `SELECT` -Anweisung ruft die Informationen zum Vertriebsmitarbeiter ab.  
  
    -   Die `SELECT` -Anweisung, die `SalesOrderID`, `SalesPersonID`und `CustomerID` abruft, enthält eine weitere geschachtelte `SELECT ... FOR XML` -Anweisung (mit `AUTO` -Modus und `TYPE` -Direktive), die Detailinformationen zur Bestellung zurückgibt.  
  
 Die `SELECT` -Anweisung, mit der die Informationen zum Vertriebsmitarbeiter abgerufen werden, fragt ein Rowset ( `SalesPerson`) ab, das in der `FROM` -Klausel erstellt wird. Damit `FOR XML` -Abfragen funktionsfähig sind, müssen Sie einen Namen für das anonyme Rowset bereitstellen, das in der `FROM` -Klausel generiert wird. In diesem Fall ist der bereitgestellte Name `SalesPerson`.  
  
 Dies ist das Teilergebnis:  
  
```  
<SalesOrder>  
  <Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  </Sales.SalesOrderHeader>  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</SalesOrder>  
...  
```  
  
 Die folgende Abfrage generiert dieselben Bestellinformationen, außer dass im resultierenden XML-Code das <`SalesPerson`>-Element als gleichgeordnetes Element von <`SalesOrderDetail`> erscheint:  
  
```  
<SalesOrder>  
    <SalesOrderHeader ...>  
          <SalesOrderDetail .../>  
          <SalesOrderDetail .../>  
          ...  
          <SalesPerson .../>  
    </SalesOrderHeader>  
  
</SalesOrder>  
<SalesOrder>  
  ...  
</SalesOrder>  
```  
  
 Im Folgenden wird die Abfrage aufgeführt:  
  
```  
SELECT SalesOrderID, SalesPersonID, CustomerID,  
             (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
              from Sales.SalesOrderDetail  
              WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
              FOR XML AUTO, TYPE),  
              (SELECT *   
               FROM  (SELECT SalesPersonID, EmployeeID  
                    FROM Sales.SalesPerson, HumanResources.Employee  
                    WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
               WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
         FOR XML AUTO, TYPE)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID=43659 or SalesOrderID=43660  
FOR XML AUTO, TYPE  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
<Sales.SalesOrderHeader SalesOrderID="43660" SalesPersonID="279" CustomerID="117">  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="762" OrderQty="1" UnitPrice="419.4589" />  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="758" OrderQty="1" UnitPrice="874.7940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
```  
  
 Da die `TYPE` -Direktive Abfrageergebnisse als **xml** -Typ zurückgibt, können Sie den resultierenden XML-Code mithilfe verschiedener **xml** -Datentypmethoden abfragen. Weitere Informationen finden Sie unter [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md). Beachten Sie in der nächsten Abfrage Folgendes:  
  
-   Die vorherige Abfrage wird in der `FROM` -Klausel hinzugefügt. Das Abfrageergebnis wird als Tabelle zurückgegeben. Beachten Sie den hinzugefügten `XmlCol` -Alias.  
  
-   Die `SELECT` -Klausel gibt eine XQuery-Abfrage für `XmlCol` an, das in der `FROM` -Klausel zurückgegeben wird. Die Methode **query()** des Datentyps **xml** wird zum Angeben der XQuery verwendet. Weitere Informationen finden Sie unter [query&#40;&#41;-Methode &#40;xml-Datentyp&#41;](../../t-sql/xml/query-method-xml-data-type.md).  
  
    ```  
    SELECT XmlCol.query('<Root> { /* } </Root>')  
    FROM (  
    SELECT SalesOrderID, SalesPersonID, CustomerID,  
                 (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
                  from Sales.SalesOrderDetail  
                  WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
                  FOR XML AUTO, TYPE),  
                  (SELECT *   
                   FROM  (SELECT SalesPersonID, EmployeeID  
                        FROM Sales.SalesPerson, HumanResources.Employee  
                        WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
                   WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
             FOR XML AUTO, TYPE)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesOrderID='43659' or SalesOrderID='43660'  
    FOR XML AUTO, TYPE ) as T(XmlCol)  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von geschachtelten FOR XML-Abfragen](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  

