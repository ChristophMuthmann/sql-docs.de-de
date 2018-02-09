---
title: Namespace-Uri-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d765c32fc0387a1aff755a59d454f9b5797eb297
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-nodes---namespace-uri"></a>Funktionen für Knoten - Namespace-uri
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Namespace-URI des im angegebenen QName *$arg* als xs: String.  
  
## <a name="syntax"></a>Syntax  
  
```  
fn:namespace-uri() as xs:string  
fn:namespace-uri($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Knotenname, dessen Namespace-URI-Teil abgerufen wird.  
  
## <a name="remarks"></a>Hinweise  
  
-   Wird das Argument nicht angegeben, wird standardmäßig der Kontextknoten verwendet.  
  
-   In SQL Server **Fn:Namespace-URI()** ohne Argument nur im Kontext eines kontextabhängigen Prädikats verwendet werden kann. Insbesondere kann die Funktion nur innerhalb von Klammern ([ ]) verwendet werden.  
  
-   Wenn *$arg* ist die leere Sequenz ist, wird die leere Zeichenfolge zurückgegeben.  
  
-   Wenn *$arg* ein Element- oder Attributknoten, dessen expanded-QName nicht in einem Namespace, die Funktion ist, gibt die Zeichenfolge der Länge 0 (null) zurück.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen in verschiedenen gespeicherten **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. Abrufen eines Namespace-URI eines bestimmten Knotens  
 Die folgende Abfrage wird für eine nicht typisierte XML-Instanz angegeben. Der Abfrageausdruck `namespace-uri(/ROOT[1])` ruft den Namespace-URI-Teil des angegebenen Knotens ab.  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 Da der angegebene QName nicht über den URI-Teil des Namespace verfügt, sondern lediglich über den lokalen Teil des Namens, ist das Ergebnis eine leere Zeichenfolge.  
  
 Die folgende Abfrage wird angegeben, für die Instructions typisierte **Xml** Spalte. Der Ausdruck `namespace-uri(/AWMI:root[1]/AWMI:Location[1])` gibt den Namespace-URI des ersten untergeordneten <`Location`>-Elements des <`root`>-Elements zurück.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Dies ist das Ergebnis:  
  
```  
http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. Verwenden von namespace-uri() ohne Argument in einem Prädikat  
 Die folgende Abfrage wird für die CatalogDescription-Spalte vom Typ XML angegeben. Der Ausdruck gibt alle Elementknoten zurück, deren Namespace-URI `http://www.adventure-works.com/schemas/OtherFeatures` ist. Der Namespace -**uri()** Funktion ohne Argument angegeben ist, und verwendet den Kontextknoten.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "http://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Dies ist die Teilergebnis:  
  
```  
<p1:wheel xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="http://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
…  
```  
  
 Sie können den Namespace-URI in der vorherigen Abfrage zu `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain` ändern. Auf diese Weise erhalten Sie alle untergeordneten Elemente des <`ProductDescription`>-Elementknotens, dessen Namespace-URI-Teil des expanded-QName `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain` ist.  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **namespace-uri()** -Funktion gibt Instanzen des Typs xs: String anstelle von xs: anyURI.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen für Knoten](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [Local-Name Function &#40; XQuery &#41;](../xquery/functions-on-nodes-local-name.md)  
  
  
