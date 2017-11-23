---
title: Upper-Case-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- upper-case
- upper-case Function (XQuery)
ms.assetid: 5bd01ad2-7adf-48fb-bf42-41e200419d37
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5297bbdf2cd1129142c2b33e633fafb0ca0bab2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="functions-on-string-values---upper-case"></a>Funktionen für Zeichenfolgenwerte - Großbuchstaben
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Diese Funktion konvertiert jedes Zeichen in *$arg* auf entsprechende großgeschriebene Variante. Die binäre Konvertierung der Groß-/Kleinschreibung für Unicode-Codepunkte von Microsoft Windows gibt an, wie Zeichen in Großbuchstaben konvertiert werden. Dieser Standard unterscheidet sich vom Unicode-Standard für die Zuordnung von Codepunkten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:upper-case($arg as xs:string?) as xs:string  
```  
  
## <a name="arguments"></a>Argumente  
  
|||  
|-|-|  
|Begriff|Definition|  
|*$arg*|Der Zeichenfolgenwert, der in Großbuchstaben konvertiert werden soll.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Wert der *$arg* ist leer, wird eine leere Zeichenfolge zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-a-string-to-upper-case"></a>A. Ändern einer Zeichenfolge in Großbuchstaben  
 Im folgenden Beispiel wird die Eingabezeichenfolge ' AbcDEF! @4"in Großbuchstaben.  
  
```  
DECLARE @x xml = N'abcDEF!@4';  
SELECT @x.value('fn:upper-case(/text()[1])', 'nvarchar(10)');  
```  
  
### <a name="b-search-for-a-specific-character-string"></a>B. Suchen nach einer bestimmten Zeichenfolge  
 In diesem Beispiel wird gezeigt, wie die upper-case-Funktion in einer Suche verwendet wird, bei der nicht zwischen Groß- und Kleinschreibung unterschieden werden soll.  
  
```  
USE AdventureWorks  
GO  
--WITH XMLNAMESPACES clause specifies the namespace prefix  
--to use.   
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
--The XQuery contains() function is used to determine whether  
--any of the text nodes below the <Summary> element contain  
--the word 'frame'. The upper-case() function is used to make  
--the search case-insensitive.  
  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
/pd:ProductDescription/pd:Summary//text()[  
          contains(upper-case(.), "FRAME")]')  = 1  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `19     <Prod ProductModelID="19">`  
  
 `<pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike.`  
  
 `Performance-enhancing options include the innovative HL Frame,`  
  
 `super-smooth front suspension, and traction for all terrain.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
 `25     <Prod ProductModelID="25">`  
  
 `<pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">This bike is ridden by race winners. Developed with the`  
  
 `Adventure Works Cycles professional race team, it has a extremely light`  
  
 `heat-treated aluminum frame, and steering that allows precision control.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
