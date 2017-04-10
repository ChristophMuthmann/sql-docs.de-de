---
title: "GeometryCollection | Microsoft Docs"
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
  - "geometry-Untertyp GeomCollection [SQL Server]"
  - "geometry-Untertypen [SQL Server]"
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# GeometryCollection
  Ein **GeometryCollection** -Objekt ist eine Auflistung von null oder mehr **geometry** - oder **geography** -Instanzen. Eine **GeometryCollection** kann leer sein.  
  
## GeometryCollection-Instanzen  
  
### Akzeptierte Instanzen  
 Damit eine **GeometryCollection** -Instanz akzeptiert wird, muss es sich um eine leere **GeometryCollection** -Instanz handeln, oder alle Instanzen, die die **GeometryCollection** beinhalten, müssen akzeptierte Instanzen sein. Im folgenden Beispiel werden akzeptierte Instanzen veranschaulicht.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 Das folgende Beispiel löst eine `System.FormatException` aus, weil die **LineString**-Instanz in der **GeometryCollection**-Instanz nicht akzeptiert wird.  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### Gültige Instanzen  
 Eine **GeometryCollection** -Instanz ist gültig, wenn alle Instanzen, die die **GeometryCollection** -Instanz beinhalten, gültig sind. Im folgenden Beispiel werden drei gültige **GeometryCollection** -Instanzen und eine nicht gültige Instanz gezeigt.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` ist nicht gültig, da die **Polygon**-Instanz in der **GeometryCollection**-Instanz nicht gültig ist.  
  
 Weitere Informationen über akzeptierte und gültige Instanzen finden Sie unter [Point](../../relational-databases/spatial/point.md), [MultiPoint](../../relational-databases/spatial/multipoint.md), [LineString](../../relational-databases/spatial/linestring.md), [MultiLineString](../../relational-databases/spatial/multilinestring.md), [Polygon](../../relational-databases/spatial/polygon.md)und [MultiPolygon](../../relational-databases/spatial/multipolygon.md).  
  
## Beispiele  
 Im folgenden Beispiel wird eine `geometry``GeometryCollection` mit Z-Werten im SRID 1 instanziiert, der eine `Point` -Instanz und eine `Polygon` -Instanz enthält.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## Siehe auch  
 [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  