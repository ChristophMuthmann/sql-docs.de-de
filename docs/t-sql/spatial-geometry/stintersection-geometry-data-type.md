---
title: STIntersection (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIntersection_TSQL
- STIntersection (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersection (geometry Data Type)
ms.assetid: 354843f5-cc14-478c-974a-04f363f9530f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f6b2674cbd4c1443a3762459a543fb9712253d8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="stintersection-geometry-data-type"></a>STIntersection (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt ein Objekt zurück, das die Punkte darstellt, an denen eine **geometry** -Instanz eine andere **geometry** -Instanz überschneidet.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STIntersection ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geometry*  
 Eine andere **geometry** -Instanz für den Vergleich mit der Instanz, in der `STIntersection()` aufgerufen wird, um zu bestimmen, wo sich die beiden Instanzen überschneiden.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 `STIntersection()`immer null zurück, wenn das spatial Reference IDs (SRIDs) auf, der die **Geometrie** -Instanzen nicht übereinstimmen. Im Ergebnis können nur dann Kreisbogensegmente enthalten sein, wenn die Eingabeinstanzen auch Kreisbogensegmente enthalten.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-stintersection-on-polygon-instances"></a>A. Verwenden von STIntersection() auf Polygoninstanzen  
 Im folgenden Beispiel wird `STIntersection()` zum Berechnen der Schnittmenge zweier Polygone verwendet.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STIntersection(@h).ToString();  
```  
  
### <a name="b-using-stintersection-with-curvepolygon-instance"></a>B. Verwenden von STIntersection() mit CurvePolygon-Instanzen  
 Im folgenden Beispiel wird eine Instanz zurückgegeben, die ein Kreisbogensegment enthält.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STIntersection(@g).ToString();
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

