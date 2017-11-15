---
title: 'Beispiel: Angeben von XSINIL mit der ELEMENTS-Direktive | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RAW mode, specifying XSINIL example
ms.assetid: 07c873ff-1f9d-480e-8536-862c39eb8249
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 277d79a76cac65d132c925e4cd91ee1a77ade46f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="example-specifying-xsinil-with-the-elements-directive"></a>Beispiel: Angeben von XSINIL mit der ELEMENTS-Direktive
  In der folgenden Abfrage wird die `ELEMENTS` -Direktive angegeben, um elementzentrierte XML-Daten aus dem Abfrageergebnis zu generieren.  
  
## <a name="example"></a>Beispiel  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 Dies ist das Teilergebnis.  
  
```  
<row>  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
 Da die `Color`-Spalte NULL-Werte für einige Produkte aufweist, generieren die resultierenden XML-Daten nicht das entsprechende <`Color`>-Element. Indem die `XSINIL`-Direktive zusammen mit `ELEMENTS` hinzugefügt wird, können Sie das <`Color`>-Element auch für NULL-Farbwerte im Resultset generieren.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS XSINIL ;  
```  
  
 Dies ist das Teilergebnis:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
  <Color xsi:nil="true" />  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
