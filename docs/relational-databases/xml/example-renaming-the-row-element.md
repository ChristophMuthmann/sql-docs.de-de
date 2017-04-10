---
title: "Beispiel: Umbenennen des &lt;row&gt;-Elements | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "RAW-Modus, Umbenennen von <row> (Beispiel)"
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Beispiel: Umbenennen des &lt;row&gt;-Elements
  Für jede Zeile im Resultset generiert der RAW-Modus ein `<row>`-Element. Sie können optional einen anderen Namen für dieses Element angeben, indem Sie ein optionales Argument für den RAW-Modus angeben, wie es in der folgenden Abfrage gezeigt wird. Die Abfrage gibt ein <`ProductModel`>-Element für jede Zeile im Rowset zurück.  
  
## Beispiel  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 Dies ist das Ergebnis. Da der Abfrage die `ELEMENTS`-Direktive hinzugefügt wurde, ist das Ergebnis elementzentriert.  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## Siehe auch  
 [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  