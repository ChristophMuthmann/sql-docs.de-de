---
title: Value()-Methode (Xml-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- value method
- value() method
ms.assetid: 298a7361-dc9a-4902-9b1e-49a093cd831d
caps.latest.revision: "38"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4370076afa9255cc7e83acaa6fe4dffeb73bc958
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="value-method-xml-data-type"></a>value()-Methode (xml-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Führt eine XQuery-Abfrage für den XML-Code aus und gibt einen Wert im SQL-Typ zurück. Diese Methode gibt einen Skalarwert zurück.  
  
 Sie verwenden diese Methode üblicherweise, um einen Wert aus einer XML-Instanz zu extrahieren, die in einer Spalte, einem Parameter oder einer Variablen des **xml** -Datentyps gespeichert ist. Auf diese Weise können Sie SELECT-Abfragen angeben, die XML-Daten mit Daten in Nicht-XML-Spalten kombinieren oder vergleichen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>Argumente  
 *XQuery*  
 Ist der *XQuery* -Ausdruck (ein Zeichenfolgenliteral), der Daten innerhalb der XML-Instanz abruft. Die XQuery muss mindestens einen Wert zurückgeben. Ansonsten wird ein Fehler zurückgegeben.  
  
 *SQLType*  
 Ist der bevorzugte SQL-Typ (ein Zeichenfolgenliteral), der zurückgegeben werden soll. Der Rückgabetyp dieser Methode entspricht dem *SQLType* -Parameter. *SQLType* kann kein **xml** -Datentyp, benutzerdefinierter CLR-Typ (Common Language Runtime) sowie kein **image**-, **text**-, **ntext**- oder **sql_variant** -Datentyp sein. *SQLType* kann ein benutzerdefinierter SQL-Datentyp sein.  
  
 Die **value()** -Methode verwendet die [!INCLUDE[tsql](../../includes/tsql-md.md)] implizit-Operator CONVERT und versucht, das Ergebnis des XQuery-Ausdrucks die serialisierte Zeichenfolgendarstellung von XSD-Typ mit dem entsprechenden gemäßSQL-Datentypkonvertieren[!INCLUDE[tsql](../../includes/tsql-md.md)] Konvertierung. Weitere Informationen zu Typ Umwandlungsregeln für CONVERT, finden Sie unter [CAST und CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
> [!NOTE]  
>  Aus Leistungsgründen sollten Sie zum Vergleichen mit einem relationalen Wert die **exist()** -Methode mit **sql:column()** verwenden und nicht die **value()**-Methode in einem Prädikat. Dies wird im folgenden Beispiel D gezeigt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-the-value-method-against-an-xml-type-variable"></a>A. Verwenden der value()-Methode mit einer Variablen vom Typ XML  
 Im folgenden Beispiel ist eine XML-Instanz in einer Variablen des `xml` -Typs gespeichert. Mit der `value()` -Methode wird der Wert des `ProductID` -Attributs aus der XML-Instanz abgerufen. Dieser Wert wird dann einer `int` -Variablen zugewiesen.  
  
```  
DECLARE @myDoc xml  
DECLARE @ProdID int  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
  
SET @ProdID =  @myDoc.value('(/Root/ProductDescription/@ProductID)[1]', 'int' )  
SELECT @ProdID  
```  
  
 Als Ergebnis wird Wert 1 zurückgegeben.  
  
 Obwohl es nur ein `ProductID` -Attribut in der XML-Instanz gibt, müssen Sie aufgrund der statischen Typisierungsregeln explizit angeben, dass der Pfadausdruck ein Singleton zurückgibt. Deshalb wird zusätzlich `[1]` am Ende des Pfadausdrucks angegeben. Weitere Informationen zur statischen Typisierung finden Sie unter [XQuery and Static Typing](../../xquery/xquery-and-static-typing.md).  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>B. Verwenden der value()-Methode zum Abrufen eines Werts aus einer Spalte vom Typ XML  
 Die folgende Abfrage wird für eine Spalte vom Typ **xml** (`CatalogDescription`) in der `AdventureWorks` -Datenbank angegeben. Die Abfrage ruft die Werte des Attributs `ProductModelID` aus jeder in der Spalte gespeicherten XML-Instanz ab.  
  
```  
SELECT CatalogDescription.value('             
    declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";             
       (/PD:ProductDescription/@ProductModelID)[1]', 'int') AS Result             
FROM Production.ProductModel             
WHERE CatalogDescription IS NOT NULL             
ORDER BY Result desc             
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Das `namespace` -Schlüsselwort wird verwendet, um ein Namespacepräfix zu definieren.  
  
-   Gemäß den Anforderungen der statischen Typisierung wird `[1]` am Ende des Pfadausdrucks in der `value()` -Methode hinzugefügt, um explizit anzugeben, dass der Pfadausdruck ein Singleton zurückgibt.  
  
 Dies ist das Teilergebnis:  
  
```  
-----------  
35           
34           
...  
```  
  
### <a name="c-using-the-value-and-exist-methods-to-retrieve-values-from-an-xml-type-column"></a>C. Verwenden der value()- und der exist()-Methode zum Abrufen von Werten aus einer Spalte vom Typ XML  
 Das folgende Beispiel zeigt die Verwendung sowohl die `value()` Methode und die [EXIST()-Methode](../../t-sql/xml/exist-method-xml-data-type.md) von der **Xml** -Datentyp. Die `value()` -Methode wird zum Abrufen von `ProductModelID` -Attributwerten aus der XML-Instanz verwendet. Mit der `exist()` -Methode in der `WHERE` -Klausel werden die Zeilen aus der Tabelle gefiltert.  
  
 Mit der Abfrage werden Produktmodell-IDs aus XML-Instanzen mit Garantieinformationen (<`Warranty`>-Element) als eine der Funktionen abgerufen. Die Bedingung in der `WHERE` -Klausel verwendet die `exist()` -Methode, um nur solche Zeilen abzurufen, die diese Bedingung erfüllen.  
  
```  
SELECT CatalogDescription.value('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           (/PD:ProductDescription/@ProductModelID)[1] ', 'int') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die `CatalogDescription` -Spalte ist eine typisierte XML-Spalte. Das bedeutet, dass ihr eine Schemaauflistung zugeordnet ist. In der [XQuery-Prolog](../../xquery/modules-and-prologs-xquery-prolog.md), die Namespacedeklaration wird verwendet, um das Präfix, das verwendet wird, wird später im Hauptteil Abfrage definieren.  
  
-   Wenn die `exist()`-Methode `1` (True) zurückgibt, bedeutet dies, dass die XML-Instanz das untergeordnete <`Warranty`>-Element als eine der Funktionen enthält.  
  
-   Die `value()` -Methode in der `SELECT` -Klausel ruft dann die `ProductModelID` -Attributwerte als ganze Zahlen ab.  
  
 Dies ist das Teilergebnis:  
  
```  
Result       
-----------  
19           
23           
...  
```  
  
### <a name="d-using-the-exist-method-instead-of-the-value-method"></a>D. Verwenden der exist()-Methode anstelle der value()-Methode  
 Aus Leistungsgründen sollten Sie zum Vergleichen mit einem relationalen Wert die `value()` -Methode mit `exist()` verwenden und nicht die `sql:column()`-Methode in einem Prädikat. Zum Beispiel:  
  
```  
CREATE TABLE T (c1 int, c2 varchar(10), c3 xml)  
GO  
  
SELECT c1, c2, c3   
FROM T  
WHERE c3.value( '/root[1]/@a', 'integer') = c1  
GO  
```  
  
 Dies kann in der folgenden Weise geschrieben werden:  
  
```  
SELECT c1, c2, c3   
FROM T  
WHERE c3.exist( '/root[@a=sql:column("c1")]') = 1  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML Data Modification Language &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
