---
title: Verwenden von XML in berechneten Spalten | Microsoft-Dokumentation
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
- computed columns, XML
- XML [SQL Server], computed columns
ms.assetid: 1313b889-69b4-4018-9868-0496dd83bf44
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f156afc96d002d1db972fb3060676c7043563a25
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="use-xml-in-computed-columns"></a>Verwenden von XML in berechneten Spalten
  XML-Instanzen können als Quelle für eine berechnete Spalte oder als Typ einer berechneten Spalte auftreten. In den Beispielen in diesem Thema wird gezeigt, wie XML mit berechneten Spalten verwendet wird.  
  
## <a name="creating-computed-columns-from-xml-columns"></a>Erstellen berechneter Spalten aus XML-Spalten  
 In der folgenden `CREATE TABLE` -Anweisung wird eine Spalte vom Typ `xml` (`col2`) aus `col1`berechnet:  
  
```  
CREATE TABLE T(col1 varchar(max), col2 AS CAST(col1 AS xml) )    
```  
  
 Der `xml` -Datentyp kann auch als Quelle für das Erstellen einer berechneten Spalte dienen, wie es in der folgenden `CREATE TABLE` -Anweisung gezeigt wird:  
  
```  
CREATE TABLE T (col1 xml, col2 as cast(col1 as varchar(1000) ))   
```  
  
 Sie können eine berechnete Spalte erstellen, indem Sie einen Wert aus einer Spalte vom Typ `xml` extrahieren, wie es im folgenden Beispiel gezeigt wird. Da die **XML** -Datentypmethoden nicht direkt zum Erstellen von berechneten Spalten verwendet werden können, wird in diesem Beispiel zunächst eine Funktion definiert (`my_udf`), die einen Wert aus einer XML-Instanz zurückgibt. Die Funktion dient als Wrapper für die `value()` -Methode des `xml` -Typs. Der Name der Funktion wird dann in der `CREATE TABLE` -Anweisung für die berechnete Spalte angegeben.  
  
```  
CREATE FUNCTION my_udf(@var xml) returns int  
AS BEGIN   
RETURN @var.value('(/ProductDescription/@ProductModelID)[1]' , 'int')  
END  
GO  
-- Use the function in CREATE TABLE.  
CREATE TABLE T (col1 xml, col2 as dbo.my_udf(col1) )  
GO  
-- Try adding a row.   
INSERT INTO T values('<ProductDescription ProductModelID="1" />')  
GO  
-- Verify results.  
SELECT col2, col1  
FROM T  
  
```  
  
 Wie im vorherigen Beispiel wird auch im folgenden Beispiel eine Funktion definiert, um für eine berechnete Spalte eine Instanz des **xml** -Typs zurückzugeben. Innerhalb der Funktion ruft die `query()` -Methode des `xml` -Datentyps einen Wert aus einem Parameter vom Typ `xml` ab.  
  
```  
CREATE FUNCTION my_udf(@var xml)   
  RETURNS xml AS   
BEGIN   
   RETURN @var.query('ProductDescription/Features')  
END  
```  
  
 In der folgenden `CREATE TABLE` -Anweisung ist `Col2` eine berechnete Spalte, die die von der Funktion zurückgegebenen XML-Daten (das`<Features>` -Element) verwendet:  
  
```  
CREATE TABLE T (Col1 xml, Col2 as dbo.my_udf(Col1) )  
-- Insert a row in table T.  
INSERT INTO T VALUES('  
<ProductDescription ProductModelID="1" >  
  <Features>  
    <Feature1>description</Feature1>  
    <Feature2>description</Feature2>  
  </Features>  
</ProductDescription>')  
-- Verify the results.  
SELECT *  
FROM T  
```  
  
### <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[Heraufstufen häufig verwendeter XML-Werte mit berechneten Spalten](../../relational-databases/xml/promote-frequently-used-xml-values-with-computed-columns.md)|Beschreibt, wie die Eigenschaftenhöherstufung mit berechneten Spalten und Eigenschaftentabellen verwendet wird.|  
  
  
