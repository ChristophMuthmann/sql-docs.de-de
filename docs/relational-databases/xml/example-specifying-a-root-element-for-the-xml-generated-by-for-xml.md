---
title: "Beispiel: Angeben eines Stammelements f&#252;r das durch FOR XML generierte XML | Microsoft Docs"
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
  - "RAW-Modus, Angeben eines Stammelements (Beispiel)"
  - "RAW-Modus mit FOR XML-Beispiel"
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# Beispiel: Angeben eines Stammelements f&#252;r das durch FOR XML generierte XML
  Indem Sie die Option `ROOT` in der `FOR XML`-Abfrage angeben, können Sie ein einzelnes Element der obersten Ebene für die resultierenden XML-Daten anfordern, wie es in der folgenden Abfrage gezeigt wird. Das für die `ROOT`-Direktive angegebene Argument stellt den Namen des Stammelements bereit.  
  
## Beispiel  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
go  
```  
  
 Dies ist das Ergebnis:  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## Siehe auch  
 [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  