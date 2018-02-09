---
title: Local-Name-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 043593b488085c5d35fa356c955138eb66f82643
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-nodes---local-name"></a>Funktionen für Knoten - Local-name
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt den lokalen Teil des Namens des *$arg* als xs: String, die wird entweder die Zeichenfolge der Länge 0 (null) sein oder die lexikalische Form einen xs: NCName müssen. Wenn das Argument nicht bereitgestellt wird, ist der Standardwert der Kontextknoten.  
  
## <a name="syntax"></a>Syntax  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Knotenname, dessen lokaler Namensanteil abgerufen wird.  
  
## <a name="remarks"></a>Hinweise  
  
-   In SQL Server **Fn:Local-Name()** ohne Argument nur im Kontext eines kontextabhängigen Prädikats verwendet werden kann. Insbesondere kann die Funktion nur innerhalb von Klammern (`[ ]`) verwendet werden.  
  
-   Wenn das Argument angegeben wird und wenn es die leere Sequenz ist, gibt die Funktion die Zeichenfolge mit der Länge null zurück.  
  
-   Wenn der Zielknoten keinen Namen besitzt, weil es sich um einen Dokumentknoten, einen Kommentar oder einen Textknoten handelt, gibt die Funktion die Zeichenfolge mit der Länge null zurück.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-retrieve-local-name-of-a-specific-node"></a>A. Abrufen des lokalen Namens eines bestimmten Knotens  
 Die folgende Abfrage wird für eine nicht typisierte XML-Instanz angegeben. Der Abfrageausdruck `local-name(/ROOT[1])` ruft den lokalen Namensanteil des angegebenen Knotens ab.  
  
```  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('local-name(/ROOT[1])')  
-- result = ROOT  
```  
  
 Die folgende Abfrage wird für die Instructions-Spalte, eine typisierte xml-Spalte, der ProductModel-Tabelle angegeben. Der Ausdruck `local-name(/AWMI:root[1]/AWMI:Location[1])` gibt den lokalen Namen (`Location`) des angegebenen Knotens zurück.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>B. Verwenden von local-name ohne Argument in einem Prädikat  
 Die folgende Abfrage wird angegeben, für die Instructions-Spalte, die typisierte **Xml** Spalte der ProductModel-Tabelle. Der Ausdruck gibt alle untergeordneten Elemente des <`root`>-Elements zurück, deren lokaler Namensbestandteil für den QName "Location" lautet. Die **local-name()** Funktion wird im Prädikat angegeben und besitzt keine Argumente, die der Kontextknoten wird von der Funktion verwendet.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Die Abfrage gibt alle untergeordneten <`Location`>-Elemente des <`root`>-Elements zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen für Knoten](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [Namespace-Uri Function &#40; XQuery &#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
  
