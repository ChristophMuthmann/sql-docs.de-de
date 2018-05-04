---
title: Logische Ausdrücke (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- logical operators [SQL Server], XQuery
- effective Boolean value [XQuery]
- logical expressions [XQuery]
- EBV
- expressions [XQuery], logical
ms.assetid: de94cd2e-2d48-49fb-9ebd-a2d90c79bf62
caps.latest.revision: 26
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b36d995313828b32de0c7d5762c8b6bd289b4064
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="logical-expressions-xquery"></a>Logische Ausdrücke (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery unterstützt die logischen **und** und **oder** Operatoren.  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 Die Testausdrücke `expression1,``expression2`in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kann dazu führen, eine leere Sequenz, die eine Sequenz von einem oder mehreren Knoten oder einen einzelnen booleschen Wert. Basierend auf dem Ergebnis wird der effektive boolesche Wert auf folgende Weise bestimmt:  
  
-   Wenn der Testausdruck eine leere Sequenz ergibt, ist das Ergebnis des Ausdrucks False.  
  
-   Wenn der Testausdruck einen einzelnen booleschen Wert ergibt, gilt dieser Wert als Ergebnis des Ausdrucks.  
  
-   Wenn der Testausdruck eine Sequenz aus einem oder mehreren Knoten ergibt, ist das Ergebnis des Ausdrucks True.  
  
-   Anderenfalls wird ein statischer Fehler ausgegeben.  
  
 Die logische **und** und **oder** -Operator klicken Sie dann auf den sich ergebenden booleschen Werte der Ausdrücke mit der logischen Standardsemantik angewendet wird.  
  
 Mit der folgenden Abfrage werden die Miniaturbilder mit der Frontansicht, d. h. das <`Picture`>-Element, für ein bestimmtes Produktmodell aus dem Produktkatalog abgerufen. Beachten Sie, dass der Katalog für jedes Produktbeschreibungsdokument eine oder mehrere Produktabbildungen mit verschiedenen Attributen wie z. B. Größe und Ansicht speichern kann.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $F in /PD:ProductDescription/PD:Picture[PD:Size="small"   
                                                 and PD:Angle="front"]  
     return   
         $F   
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 Dies ist das Ergebnis:  
  
```  
<PD:Picture   
  xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  <PD:Angle>front</PD:Angle>  
  <PD:Size>small</PD:Size>  
  <PD:ProductPhotoID>31</PD:ProductPhotoID>  
</PD:Picture>  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Expressions (XQuery-Ausdrücke)](../xquery/xquery-expressions.md)  
  
  
