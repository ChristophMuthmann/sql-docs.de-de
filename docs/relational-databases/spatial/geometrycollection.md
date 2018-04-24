---
title: GeometryCollection | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: spatial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 29a98f512542ed6c2b9bc07fcd7f25a76fee8cd0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="geometrycollection"></a>GeometryCollection
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Ein **GeometryCollection** -Objekt ist eine Auflistung von null oder mehr **geometry** - oder **geography** -Instanzen. Eine **GeometryCollection** kann leer sein.  
  
## <a name="geometrycollection-instances"></a>GeometryCollection-Instanzen  
  
### <a name="accepted-instances"></a>Akzeptierte Instanzen  
 Damit eine **GeometryCollection** -Instanz akzeptiert wird, muss es sich um eine leere **GeometryCollection** -Instanz handeln, oder alle Instanzen, die die **GeometryCollection** beinhalten, müssen akzeptierte Instanzen sein. Im folgenden Beispiel werden akzeptierte Instanzen veranschaulicht.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 Das folgende Beispiel löst eine `System.FormatException` aus, weil die **LineString** -Instanz in der **GeometryCollection** -Instanz nicht akzeptiert wird.  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>Gültige Instanzen  
 Eine **GeometryCollection** -Instanz ist gültig, wenn alle Instanzen, die die **GeometryCollection** -Instanz beinhalten, gültig sind. Im folgenden Beispiel werden drei gültige **GeometryCollection** -Instanzen und eine nicht gültige Instanz gezeigt.  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` ist nicht gültig, da die **Polygon** -Instanz in der **GeometryCollection** -Instanz nicht gültig ist.  
  
 Weitere Informationen über akzeptierte und gültige Instanzen finden Sie unter [Point](../../relational-databases/spatial/point.md), [MultiPoint](../../relational-databases/spatial/multipoint.md), [LineString](../../relational-databases/spatial/linestring.md), [MultiLineString](../../relational-databases/spatial/multilinestring.md), [Polygon](../../relational-databases/spatial/polygon.md)und [MultiPolygon](../../relational-databases/spatial/multipolygon.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `geometry``GeometryCollection` mit Z-Werten im SRID 1 instanziiert, der eine `Point` -Instanz und eine `Polygon` -Instanz enthält.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
