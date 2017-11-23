---
title: Number-Funktion (XQuery) | Microsoft Docs
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac925d16aa7a63c2c32748d71074117aa63e8486
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="functions-on-nodes---number"></a>Funktionen für Knoten - Anzahl
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt den numerischen Wert des Knotens, der durch angegebenen *$arg*.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>Argumente  
 *$arg*  
 Knoten, dessen Wert als Zahl zurückgegeben wird.  
  
## <a name="remarks"></a>Hinweise  
 Wenn *$arg* ist nicht angegeben wird, wird der numerische Wert des Kontextknotens, in einen Double konvertiert zurückgegeben. In SQL Server **Fn:Number()** ohne Argument nur im Kontext eines kontextabhängigen Prädikats verwendet werden kann. Insbesondere kann die Funktion nur innerhalb von Klammern ([ ]) verwendet werden. Beispielsweise gibt der folgende Ausdruck das <`ROOT`>-Element zurück.  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 Wenn der Wert des Knotens nicht gültige lexikalische Darstellung eines numerischen simple-Typs gemäß **XML Schema Part 2: Datatypes, W3C Recommendation**, die Funktion eine leere Sequenz zurückgibt. NaN wird nicht unterstützt.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen in verschiedenen gespeicherten **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. Verwenden der number()-Funktion von XQuery zum Abrufen des numerischen Werts eines Attributs  
 Die folgende Abfrage ruft den numerischen Wert des LotSize-Attributs aus dem ersten Arbeitsplatzstandort im Fertigungsvorgang von Produktmodell 7 ab.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in (//AWMI:root//AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"   
                   LotSizeA="{  $i/@LotSize }"  
                   LotSizeB="{  number($i/@LotSize) }"  
                   LotSizeC="{ number($i/@LotSize) + 1 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Beachten Sie hinsichtlich der vorherigen Abfrage Folgendes:  
  
-   Die **number()** Funktion ist nicht erforderlich, wie durch die Abfrage für die **LotSizeA** Attribut. Es handelt sich dabei um eine XPath 1.0-Funktion, die hauptsächlich aus Gründen der Abwärtskompatibilität enthalten ist.  
  
-   Die XQuery für **LotSizeB** gibt die Number-Funktion und ist redundant.  
  
-   Die Abfrage für **LotSizeD** veranschaulicht die Verwendung eines Number-Werts in einer arithmetischen Operation.  
  
 Dies ist das Ergebnis:  
  
```  
ProductModelID   Result  
----------------------------------------------  
7              <Location LocationID="10"   
                         LotSizeA="100"   
                         LotSizeB="100"   
                         LotSizeC="101" />  
```  
  
### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Die **number()** -Funktion nimmt nur Knoten. Sie nimmt keine atomaren Werte an.  
  
-   Wenn Werte als Zahl zurückgegeben werden, können die **number()** Funktion gibt die leere Sequenz statt NaN zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
