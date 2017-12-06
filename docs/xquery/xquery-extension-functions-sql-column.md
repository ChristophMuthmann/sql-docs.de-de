---
title: SQL:Column()-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- sql:column function
- sql:column() function
ms.assetid: e8f67bdf-b489-49a9-9d0f-2069c1750467
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a2edc76979e76a83125a53bf98609f263c9b9051
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="xquery-extension-functions---sqlcolumn"></a>XQuery-Erweiterungsfunktionen - SQL:Column()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Im Thema beschriebene [einbinden relationaler Daten in XML-Daten](../t-sql/xml/binding-relational-data-inside-xml-data.md), können Sie die **SQL:Column()** funktionieren bei Verwendung von [XML-Datentypmethoden](../t-sql/xml/xml-data-type-methods.md) zum Verfügbarmachen eines relationalen Werts in XQuery.  
  
 Z. B. die [Query()-Methode (XML-Datentyp)](../t-sql/xml/query-method-xml-data-type.md) wird verwendet, um eine Abfrage für eine XML-Instanz angeben, in einer Variablen oder Spalte gespeichert ist **Xml** Typ. Manchmal kann es auch wünschenswert sein, dass eine Abfrage Werte aus einer anderen Nicht-XML-Spalte verwendet, um relationale und XML-Daten zu verbinden. Zu diesem Zweck verwenden Sie die **SQL:Column()** Funktion.  
  
 Der SQL-Wert wird einem entsprechenden XQuery-Wert zugeordnet, und sein Datentyp ist ein XQuery-Basistyp, der mit dem entsprechenden SQL-Typ äquivalent ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sql:column("columnName")  
```  
  
## <a name="remarks"></a>Hinweise  
 Beachten Sie diesen Verweis auf eine Spalte angegeben wird, der **SQL:Column()** -Funktion in einer XQuery bezieht sich auf eine Spalte in der Zeile, die verarbeitet wird.  
  
 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Sie verweisen nur auf eine **Xml** Instanz im Zusammenhang mit dem quellenausdruck einer XML-DML-insert-Anweisung; andernfalls, Sie nicht auf Spalten vom Typ verweisen **Xml** oder eine CLR einen benutzerdefinierten Typ.  
  
 Die **SQL:Column()** Funktion wird im JOIN-Vorgänge nicht unterstützt. Stattdessen kann der APPLY-Vorgang verwendet werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-sqlcolumn-to-retrieve-the-relational-value-inside-xml"></a>A. Abrufen des relationalen Werts in XML mit sql:column()  
 Das folgende Beispiel zeigt beim Erstellen von XML, wie Werte aus einer relationalen Nicht-XML-Spalte abgerufen werden, um XML und relationale Daten zu binden.  
  
 Die Abfrage erstellt XML in der folgenden Form:  
  
```  
<Product ProductID="771" ProductName="Mountain-100 Silver, 38" ProductPrice="3399.99" ProductModelID="19"   
  ProductModelName="Mountain 100" />  
```  
  
 Beachten Sie im erstellten XML Folgendes:  
  
-   Die **"ProductID"**, **ProductName**, und **ProductPrice** Attributwerte werden abgerufen, von der **Produkt** Tabelle.  
  
-   Die **ProductModelID** -Attributwert abgerufen wird, aus der **ProductModel** Tabelle.  
  
-   Um die Abfrage interessanter zu gestalten die **ProductModelName** Attributwert abgerufen wird, aus der **CatalogDescription** Spalte **XML-Typ**. Da die XML-Produktmodell-Kataloginformationen nicht für alle Produktmodelle gespeichert werden, wird die `if`-Anweisung nur zum Abrufen des Werts verwendet, wenn dieser vorhanden ist.  
  
    ```  
    SELECT P.ProductID, CatalogDescription.query('  
    declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           <Product   
               ProductID=       "{ sql:column("P.ProductID") }"  
               ProductName=     "{ sql:column("P.Name") }"  
               ProductPrice=    "{ sql:column("P.ListPrice") }"  
               ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
               { if (not(empty(/pd:ProductDescription))) then  
                 attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
                else   
                   ()  
    }  
            </Product>  
    ') as Result  
    FROM Production.ProductModel PM, Production.Product P  
    WHERE PM.ProductModelID = P.ProductModelID  
    AND   CatalogDescription is not NULL  
    ORDER By PM.ProductModelID  
    ```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Da die Werte aus zwei verschiedenen Tabellen abgerufen werden, gibt die FROM-Klausel zwei Tabellen an. Die Bedingung in der WHERE-Klausel filtert das Ergebnis und ruft nur Produkte ab, deren Produktmodelle über Katalogbeschreibungen verfügen.  
  
-   Die **Namespace** -Schlüsselwort in der [XQuery-Prolog](../xquery/modules-and-prologs-xquery-prolog.md) definiert das XML-Namespacepräfix "pd", das im Abfragetext verwendet wird. Beachten Sie, dass die Tabellenaliasse "P" und "PM" in der FROM-Klausel der Abfrage selbst definiert werden.  
  
-   Die **SQL:Column()** Funktion wird verwendet, um nicht-XML-Werte in XML zu bringen.  
  
 Dies ist das Teilergebnis:  
  
```  
ProductID               Result  
-----------------------------------------------------------------  
771         <Product ProductID="771"                   ProductName="Mountain-100 Silver, 38"   
                  ProductPrice="3399.99" ProductModelID="19"   
                  ProductModelName="Mountain 100" />  
...  
```  
  
 Die folgende Abfrage erstellt XML, das produktspezifische Informationen enthält. Diese Informationen umfassen die Werte ProductID, ProductName, ProductPrice und, wenn verfügbar, ProductModelName für alle Produkte, die zu einem bestimmten Produktmodell, ProductModelID=19, gehören. Der XML-Code wird anschließend zugewiesen der @x -Variable der **Xml** Typ.  
  
```  
declare @x xml  
SELECT @x = CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <Product   
           ProductID=       "{ sql:column("P.ProductID") }"  
           ProductName=     "{ sql:column("P.Name") }"  
           ProductPrice=    "{ sql:column("P.ListPrice") }"  
           ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
           { if (not(empty(/pd:ProductDescription))) then  
             attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
            else   
               ()  
}  
        </Product>  
')   
FROM Production.ProductModel PM, Production.Product P  
WHERE PM.ProductModelID = P.ProductModelID  
And P.ProductModelID = 19  
select @x  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server XQuery-Erweiterungsfunktionen](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Erstellen von Instanzen der XML-Daten](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml-Datentypmethoden](../t-sql/xml/xml-data-type-methods.md)   
 [XML Data Modification Language &#40; XML DML &#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
