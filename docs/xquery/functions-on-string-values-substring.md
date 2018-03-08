---
title: SUBSTRING-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
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
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ae71eb26e93c65f853c5d1c842a1835cf40d866
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-string-values---substring"></a>Funktionen für Zeichenfolgenwerte - Teilzeichenfolge
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Teil des Werts der *$sourceString*, beginnend bei der durch den Wert der angegebenen Position *$startingLoc,* und weiterhin für die Anzahl der Zeichen, die durch den Wert der angegebenen *$ Länge*.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc  as as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumente  
 *$sourceString*  
 Quellzeichenfolge.  
  
 *$startingLoc*  
 Ausgangspunkt in der Quellzeichenfolge, an dem die Unterzeichenfolge beginnt. Wenn dieser Wert negativ oder 0 ist, werden nur die Zeichen an Positionen größer null zurückgegeben. Wenn sie größer als die Länge ist die *$sourceString*, wird die leere Zeichenfolge zurückgegeben.  
  
 *$length*  
 [optional] Anzahl der abzurufenden Zeichen. Wenn nicht angegeben, gibt alle Zeichen aus dem im angegebenen Speicherort zurück *$startingLoc* bis zum Ende der Zeichenfolge.  
  
## <a name="remarks"></a>Hinweise  
 Die Version der Funktion mit drei Argumenten gibt die Zeichen in `$sourceString` zurück, deren Position `$p` genügt:  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 Der Wert der *$length* kann größer sein als die Anzahl der Zeichen im Wert des *$sourceString* der Startposition. In diesem Fall gibt die Teilzeichenfolge zurück, die Zeichen bis zum Ende des *$sourceString*.  
  
 Das erste Zeichen einer Zeichenfolge befindet sich an Position 1.  
  
 Wenn der Wert der *$sourceString* ist die leere Sequenz ist, wird er als die Zeichenfolge der Länge 0 (null) behandelt. Andernfalls, wenn entweder *$startingLoc* oder *$length* leere Sequenz ist, wird die leere Sequenz zurückgegeben.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Das Verhalten von Ersatzzeichenpaaren in XQuery-Funktionen hängt vom Kompatibilitätsgrad der Datenbank ab und in einigen Fällen vom Standardnamespace-URI für Funktionen. Weitere Informationen finden Sie im Abschnitt "XQuery-Funktionen sind Ersatzzeichenabhängig" im Thema [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Siehe auch [ALTER DATABASE Kompatibilitätsgrad &#40; Transact-SQL &#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) und [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 SQL Server erfordert die *$startingLoc* und *$length Parameter* vom Typ xs: decimal anstelle von xs: Double.  
  
 SQL Server unterstützt das *$startingLoc* und *$length* leere Sequenz ist, werden, weil die leere Sequenz ein möglicher Wert aus, wenn dynamische Fehler () zugeordnet werden wird.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen in verschiedenen gespeicherten **Xml** in Spalten vom Typ der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Datenbank.  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. Verwenden der substring()-Funktion von XQuery zum Abrufen von Teilzusammenfassungsbeschreibungen der Produktmodelle  
 Die Abfrage ruft die ersten 50 Zeichen vom Text ab, in dem das Produktmodell beschrieben wird, das <`Summary`>-Element im Dokument.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die **string()** Funktion gibt den Zeichenfolgenwert der <`Summary`> Element. Diese Funktion wird verwendet, da das <`Summary`>-Element sowohl den Text als auch die Unterelemente (HTML-Formatierungselemente) enthält, und da Sie diese Elemente überspringen und den gesamten Text abrufen.  
  
-   Die **substring()** Funktion ruft die ersten 50 Zeichen ab, von der String-Wert abgerufen, indem die **string()**.  
  
 Dies ist ein Teilergebnis:  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
