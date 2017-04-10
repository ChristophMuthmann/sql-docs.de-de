---
title: "Verwenden von geschachtelten FOR XML-Abfragen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR XML-Klausel, geschachtelte FOR XML-Abfragen"
  - "Abfragen [XML in SQL Server], geschachtelte FOR XML-"
  - "Geschachtelte FOR XML-Abfragen"
ms.assetid: 7604161a-a958-446d-b102-7dee432979d0
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Verwenden von geschachtelten FOR XML-Abfragen
  Der **xml** -Datentyp und die [TYPE-Direktive in FOR XML-Abfragen](../../relational-databases/xml/type-directive-in-for-xml-queries.md) ermöglichen, dass der von FOR XML-Abfragen zurückgegebene XML-Code sowohl auf dem Server als auch auf dem Client verarbeitet werden kann.  
  
## Verarbeiten mit XML-Typvariablen  
 Sie können das Ergebnis einer FOR XML-Abfrage einer **xml** -Typvariablen zuweisen oder das Ergebnis mithilfe einer XQuery-Abfrage abfragen und das daraus entstehende Ergebnis einer **xml** -Typvariablen zur weiteren Verarbeitung zuweisen.  
  
```  
DECLARE @x xml  
SET @x=(SELECT ProductModelID, Name  
        FROM Production.ProductModel  
        WHERE ProductModelID=122 or ProductModelID=119  
        FOR XML RAW, TYPE)  
SELECT @x  
-- Result  
--<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
--<row ProductModelID="119" Name="Bike Wash" />  
```  
  
 Sie können den in der Variablen `@x`zurückgegebenen XML-Code zusätzlich verarbeiten, indem Sie eine der **xml** -Datentypmethoden verwenden. So können Sie z. B. den Attributwert von `ProductModelID` mithilfe der [value()-Methode](../../t-sql/xml/value-method-xml-data-type.md) abrufen.  
  
```  
DECLARE @i int;  
SET @i = (SELECT @x.value('/row[1]/@ProductModelID[1]', 'int'));  
SELECT @i;  
```  
  
 Im folgenden Beispiel wird das Ergebnis der `FOR XML` -Abfrage als **xml** -Typ zurückgegeben, da in der `TYPE` -Klausel die `FOR XML` -Direktive angegeben wurde.  
  
```  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=119 or ProductModelID=122  
FOR XML RAW, TYPE,ROOT('myRoot');  
  
```  
  
 Dies ist das Ergebnis:  
  
```  
<myRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
</myRoot>  
```  
  
 Da das Ergebnis dem **xml** -Typ entspricht, können Sie eine der **xml** -Datentypmethoden direkt für diesen XML-Code angeben, wie es in der folgenden Abfrage gezeigt wird. In der Abfrage wird die [query()-Methode (XML-Datentyp)](../../t-sql/xml/query-method-xml-data-type.md) verwendet, um das erste untergeordnete <`row`>-Element des Elements <`myRoot`> abzurufen.  
  
```  
SELECT  (SELECT ProductModelID, Name  
         FROM Production.ProductModel  
         WHERE ProductModelID=119 or ProductModelID=122  
         FOR XML RAW, TYPE,ROOT('myRoot')).query('/myRoot[1]/row[1]');  
  
```  
  
 Dies ist das Ergebnis:  
  
```  
<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
```  
  
## Zurückgeben von Ergebnissen innerer FOR XML-Abfragen als XML-Typinstanzen an äußere Abfragen  
 Sie können geschachtelte `FOR XML` -Abfragen schreiben, bei denen das Ergebnis der inneren Abfrage als **xml** -Typ an die äußere Abfrage zurückgegeben wird. Beispiel:  
  
```  
SELECT Col1,   
       Col2,   
       ( SELECT Col3, Col4   
        FROM  T2  
        WHERE T2.Col = T1.Col  
        ...  
        FOR XML AUTO, TYPE )  
FROM T1  
WHERE ...  
FOR XML AUTO, TYPE;  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Der von der inneren `FOR XML` -Abfrage generierte XML-Code wird dem von der äußeren `FOR XML`-Abfrage generierten XML-Code hinzugefügt.  
  
-   Die innere Abfrage gibt die `TYPE` -Direktive an. Die von der inneren Abfrage zurückgegebenen XML-Daten gehören daher dem **xml** -Typ an. Wenn die TYPE-Direktive nicht angegeben wird, wird als Ergebnis der inneren `FOR XML`-Abfrage **nvarchar(max)** zurückgegeben, und die XML-Daten werden in Entitäten geändert.  
  
## Steuern der Form der resultierenden XML-Daten  
 Geschachtelte FOR XML-Abfragen ermöglichen eine bessere Steuerung der Form der resultierenden XML-Daten. Sie können jedoch mit geschachtelten FOR XML-Abfragen XML-Code erstellen, der zum Teil attributzentriert und zum Teil elementzentriert ist.  
  
 Weitere Informationen über das Angeben von attributzentrierter und elementzentrierter XML mit geschachtelten FOR XML-Abfragen finden Sie unter [FOR XML-Abfragen im Vergleich zu geschachtelten FOR XML-Abfragen](../../relational-databases/xml/for-xml-query-compared-to-nested-for-xml-query.md) und [Gestalten von XML mit geschachtelten FOR XML-Abfragen](../../relational-databases/xml/shape-xml-with-nested-for-xml-queries.md).  
  
 Sie können XML-Hierarchien generieren, die gleichgeordnete Elemente enthalten, indem Sie geschachtelte FOR XML-Abfragen im AUTO-Modus angeben. Weitere Informationen finden Sie unter [Generieren von gleichgeordneten Elementen mit einer geschachtelten AUTO-Modusabfrage](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md).  
  
 Unabhängig davon, welchen Modus Sie verwenden, bieten geschachtelte FOR XML-Abfragen größere Steuerungsmöglichkeiten beim Beschreiben der Form des resultierenden XML-Codes. Diese Abfragen können anstelle von Abfragen im EXPLICIT-Modus verwendet werden.  
  
## Beispiele  
 Die folgenden Themen enthalten Beispiele für geschachtelte FOR XML-Abfragen.  
  
 [FOR XML-Abfragen im Vergleich zu geschachtelten FOR XML-Abfragen](../../relational-databases/xml/for-xml-query-compared-to-nested-for-xml-query.md)  
 In diesem Thema wird eine einstufige FOR XML-Abfrage mit einer geschachtelten FOR XML-Abfrage verglichen. In diesem Beispiel wird unter Anderem veranschaulicht, wie sowohl attributzentriertes als auch elementzentriertes XML als Abfrageergebnis angegeben wird.  
  
 [Generieren von gleichgeordneten Elementen mit einer geschachtelten AUTO-Modusabfrage](../../relational-databases/xml/generate-siblings-with-a-nested-auto-mode-query.md)  
 Zeigt, wie gleichgeordnete Elemente durch Verwenden einer geschachtelten Abfrage im AUTO-Modus generiert werden.  
  
 [Verwenden geschachtelter FOR XML-Abfragen in ASP.NET](../../relational-databases/xml/use-nested-for-xml-queries-in-asp-net.md)  
 Veranschaulicht, wie eine ASPX-Anwendung FOR XML verwenden kann, um XML von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurückzugeben.  
  
 [Gestalten von XML mit geschachtelten FOR XML-Abfragen](../../relational-databases/xml/shape-xml-with-nested-for-xml-queries.md)  
 Zeigt, wie mit geschachtelten FOR XML-Abfragen die Struktur eines von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellten XML-Dokuments gesteuert werden kann.  
  
  