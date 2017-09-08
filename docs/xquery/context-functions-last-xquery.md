---
title: Last-Funktion (XQuery) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
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
- last function [XQuery]
- fn:last function
ms.assetid: dc92086e-3b01-4b0b-9f54-3bbf306cf7ae
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6b2ef17f93cf24b3a481fa172498f9acca75f95d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="context-functions---last-xquery"></a>Kontextfunktionen - Last (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt die Anzahl der Elemente in der Sequenz zurück, die zurzeit verarbeitet wird. Insbesondere wird der ganzzahlige Index des letzten Elements in der Sequenz zurückgegeben. Das erste Element in der Sequenz besitzt den Indexwert 1.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>Hinweise  
 In SQL Server **Fn:Last()** kann nur im Kontext eines kontextabhängigen Prädikats verwendet werden. Insbesondere kann die Funktion nur innerhalb von Klammern (`[ ]`) verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>A. Verwenden der last()-Funktion von XQuery zum Abrufen der letzten beiden Fertigungsschritte  
 Die folgende Abfrage ruft die letzten beiden Fertigungsschritte für ein bestimmtes Produktmodell ab. Der Wert, der die Anzahl der Fertigungsschritte, zurückgegebenes der **last()** Funktion wird in dieser Abfrage zum Abrufen der letzten beiden Fertigungsschritte verwendet.  
  
```  
SELECT ProductModelID, Instructions.query('   
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 In der vorherigen Abfrage die **last()** -Funktion in /`/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]` gibt die Anzahl der Fertigungsschritte zurück. Dieser Wert wird zum Abrufen des letzten Fertigungsschritts am Arbeitsplatzstandort verwendet.  
  
 Dies ist das Ergebnis:  
  
```  
ProductModelID Result    
-------------- -------------------------------------  
7      <LastTwoManuSteps>  
         <Last-1Step>  
            When finished, inspect the forms for defects per   
            Inspection Specification .  
         </Last-1Step>  
         <LastStep>Remove the frames from the tool and place them   
            in the Completed or Rejected bin as appropriate.  
         </LastStep>  
       </LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
