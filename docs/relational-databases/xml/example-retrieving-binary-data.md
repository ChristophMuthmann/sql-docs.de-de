---
title: "Beispiel: Abrufen von Bin&#228;rdaten | Microsoft Docs"
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
  - "RAW-Modus, Abrufen von Binärdaten, Beispiel"
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# Beispiel: Abrufen von Bin&#228;rdaten
  Die folgende Abfrage gibt das Produktfoto zurück, das in einer Spalte des **varbinary(max)**-Typs gespeichert ist. Durch die Angabe der Option `BINARY BASE64` in der Abfrage werden die Binärdaten im Base64-codierten Format zurückgegeben.  
  
## Beispiel  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM Production.ProductPhoto  
WHERE ProductPhotoID=1  
FOR XML RAW, BINARY BASE64 ;  
GO  
```  
  
 Dies ist das Ergebnis:  
  
```  
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>  
```  
  
## Siehe auch  
 [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  