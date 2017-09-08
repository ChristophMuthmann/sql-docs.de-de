---
title: Typsystem (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- type system [XQuery]
- typed values [XQuery]
- XQuery, sequence
- string values [XQuery]
- XQuery, XPath data type namespace
- xdt prefix [XML in SQL Server]
- XQuery, type system
- built-in XML schema types [SQL Server]
- xs prefix [XML in SQL Server]
ms.assetid: 22d6f861-d058-47ee-b550-cbe9092dcb12
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e84467e5f4ec58e1601868f1406c8c7cfd972a94
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="type-system-xquery"></a>Typensystem (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery ist eine stark typisierte Sprache für Schematypen und eine schwach typisierte Sprache für nicht typisierte Daten. Zu den vordefinierten Typen von XQuery zählen folgende Typen:  
  
-   Integrierte Typen des XML-Schemas in der **http://www.w3.org/2001/XMLSchema** Namespace.  
  
-   Typen, die definiert, der **http://www.w3.org/2004/07/xpath-datatypes** Namespace.  
  
 In diesem Thema wird auch Folgendes beschrieben:  
  
-   Der Unterschied zwischen dem typisierten Wert und dem Zeichenfolgenwert eines Knotens.  
  
-   Die [Funktion von Daten &#40; XQuery &#41; ](../xquery/data-accessor-functions-data-xquery.md) und [Zeichenfolge Function &#40; XQuery &#41; ](../xquery/data-accessor-functions-string-xquery.md).  
  
-   Zuordnen des von einem Ausdruck zurückgegebenen Sequenztyps  
  
## <a name="built-in-types-of-xml-schema"></a>Integrierte Typen des XML-Schemas  
 Die integrierten Typen des XML-Schemas besitzen das vordefinierte Namespacepräfix xs. Zu diesen Typen zählen **xs: Integer** und **xs: String**. Alle diese integrierten Typen werden unterstützt. Sie können diese Typen verwenden, wenn Sie eine XML-Schemaauflistung erstellen.  
  
 Beim Abfragen von typisiertem XML-Code wird der statische und dynamische Typ der Knoten durch die XML-Schemaauflistung bestimmt, die der abgefragten Spalte oder Variablen zugeordnet ist. Weitere Informationen zu statischen und dynamischen Typen finden Sie unter [Ausdruckskontext und Ausdrucksauswertung &#40; XQuery &#41; ](../xquery/expression-context-and-query-evaluation-xquery.md). Die folgende Abfrage wird angegeben, z. B. für eine typisierte **Xml** Spalte (`Instructions`). Der Ausdruck verwendet `instance of`, um zu überprüfen, ob der typisierte Wert des zurückgegebenen `LotSize`-Attributs den `xs:decimal`-Typ aufweist.  
  
```  
SELECT Instructions.query('  
   DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   data(/AWMI:root[1]/AWMI:Location[@LocationID=10][1]/@LotSize)[1] instance of xs:decimal  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Diese Typisierungsinformationen werden durch die XML-Schemaauflistung bereitgestellt, die der Spalte zugeordnet sind.  
  
## <a name="types-defined-in-xpath-data-types-namespace"></a>Im Namespace für XPath-Datentypen definierte Typen  
 Die in definierten Typen der **http://www.w3.org/2004/07/xpath-datatypes** Namespace besitzen das vordefinierte Präfix des **Xdt**. Für diese Typen gilt Folgendes:  
  
-   Sie können diese Typen nicht verwenden, wenn Sie eine XML-Schemaauflistung erstellen. Diese Typen werden in der XQuery-Typsystem verwendet und dienen zur [XQuery and Static Typing](../xquery/xquery-and-static-typing.md). Sie können eine Umwandlung in die atomaren Typen, z. B. **xdt: UntypedAtomic**in der **Xdt** Namespace.  
  
-   Wenn Sie nicht typisiertes XML Abfragen, die statische und dynamische Typ der Elementknoten ist **Xdt: nicht typisierte**, und der Typ der Attributwerte ist **xdt: UntypedAtomic**. Das Ergebnis einer **query()** -Methode generiert nicht typisierten XML-Code. Dies bedeutet, dass die XML-Knoten, als zurückgegeben werden **Xdt: nicht typisierte** und **xdt: UntypedAtomic**zugeordnet.  
  
-   Die **dayTimeDuration** und **xdt: yearmonthduration** Typen werden nicht unterstützt.  
  
 Im folgenden Beispiel wird die Abfrage für eine nicht typisierte XML-Variable angegeben. Der Ausdruck `data(/a[1]`) gibt eine Sequenz eines atomaren Werts zurück. Die `data()`-Funktion gibt den typisierten Wert des `<a>`-Elements zurück. Da der abgefragte XML-Code nicht typisiert ist, ist der Typ des zurückgegebenen Werts `xdt:untypedAtomic`. Deshalb gibt `instance of` den Wert True zurück.  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
SELECT @x.query( 'data(/a[1]) instance of xdt:untypedAtomic' )  
```  
  
 Statt den typisierten Wert abzurufen, gibt der Ausdruck (`/a[1]`) im folgenden Beispiel eine Sequenz aus einem Element (dem `<a>`-Element) zurück. Der `instance of`-Ausdruck verwendet den Elementtest, um zu überprüfen, ob der vom Ausdruck zurückgegebene Wert ein `xdt:untyped type`-Elementknoten ist.  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
-- Is this an element node whose name is "a" and type is xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(a, xdt:untyped?)')  
-- Is this an element node of type xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(*, xdt:untyped?)')  
-- Is this an element node?  
SELECT @x.query( '/a[1] instance of element()')  
```  
  
> [!NOTE]  
>  Wenn Sie eine typisierte XML-Instanz abfragen und der Abfrageausdruck schließt die übergeordnete Achse ein, sind die Informationen zum statischen Typ der resultierenden Knoten nicht weiter verfügbar. Der dynamische Typ ist jedoch weiterhin den Knoten zugeordnet.  
  
## <a name="typed-value-vs-string-value"></a>Typisierter Wert und Zeichenfolgenwert  
 Jeder Knoten besitzt einen typisierten Wert und einen Zeichenfolgenwert. Für typisierte XML-Daten wird der Typ des typisierten Werts durch die XML-Schemaauflistung bereitgestellt, die der abgefragten Spalte oder Variablen zugeordnet ist. Für nicht typisierte XML-Daten ist der Typ des typisierten Werts **xdt: UntypedAtomic**.  
  
 Sie können die **data()** oder **string()** Funktion zum Abrufen des Werts eines Knotens:  
  
-   Die [Funktion von Daten &#40; XQuery &#41; ](../xquery/data-accessor-functions-data-xquery.md) den typisierten Wert eines Knotens zurückgibt.  
  
-   Die [Zeichenfolge Function &#40; XQuery &#41; ](../xquery/data-accessor-functions-string-xquery.md) gibt den Zeichenfolgenwert des Knotens zurück.  
  
 In der folgenden XML-Schemaauflistung wird das <`root`>-Element des ganzzahligen Typs definiert:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="integer"/>  
</schema>'  
GO  
```  
  
 Im folgenden Beispiel ruft der Ausdruck zuerst den typisierten Wert von `/root[1]` ab und fügt ihm anschließend `3` hinzu.  
  
```  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('data(/root[1]) + 3')  
```  
  
 Im nächsten Beispiel schlägt der Ausdruck fehl, weil die `string(/root[1])`-Anweisung im Ausdruck einen Wert des Zeichenfolgentyps zurückgibt. Dieser Wert wird dann an einen arithmetischen Operator übergeben, der nur Werte des numerischen Typs als Operand akzeptiert.  
  
```  
-- Fails because the argument is string type (must be numeric primitive type).  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('string(/root[1]) + 3')  
```  
  
 Im folgenden Beispiel wird der Gesamtwert der `LaborHours`-Attribute berechnet. Die `data()` Funktion ruft die typisierten Werte der `LaborHours` Attribute sämtlicher der <`Location`>-Elemente für ein Produktmodell. Gemäß dem XML-Schema zugeordneten der `Instruction` Spalte `LaborHours` vom **xs: decimal** Typ.  
  
```  
SELECT Instructions.query('   
DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
             sum(data(//AWMI:Location/@LaborHours))   
') AS Result   
FROM Production.ProductModel   
WHERE ProductModelID=7  
```  
  
 Diese Abfrage gibt 12.75 als Ergebnis zurück.  
  
> [!NOTE]  
>  Die explizite Verwendung von der **data()** Funktion in diesem Beispiel dient nur zur Veranschaulichung. Wenn sie nicht angegeben ist, **sum()** implizit gilt die **data()** Funktion, um die typisierten Werte der Knoten zu extrahieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Vorlagen und Berechtigungen in SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [XQuery Basics (XQuery-Grundlagen)](../xquery/xquery-basics.md)  
  
  

