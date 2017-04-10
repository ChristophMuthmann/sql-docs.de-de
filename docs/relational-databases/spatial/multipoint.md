---
title: "MultiPoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-spatial"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "geometry-Untertyp MultiPoint [SQL Server]"
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MultiPoint
  Ein **MultiPoint** ist eine Auflistung von null oder mehr Punkten. Die Begrenzung einer **MultiPoint** -Instanz ist leer.  
  
## Beispiele  
 Im folgenden Beispiel wird eine `geometry MultiPoint`-Instanz mit dem SRID 23 und zwei Punkten erstellt: ein Punkt mit den Koordinaten (2, 3), ein Punkt mit den Koordinaten (7, 8) und ein Z-Wert von 9,5.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 Diese `MultiPoint`-Instanz kann auch mit `STMPointFromText()` ausgedrückt werden, wie unten dargestellt.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 Im folgenden Beispiel wird mit der Methode `STGeometryN()` eine Beschreibung des ersten Punkts der Auflistung abgerufen.  
  
```  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## Siehe auch  
 [Punkt](../../relational-databases/spatial/point.md)   
 [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  