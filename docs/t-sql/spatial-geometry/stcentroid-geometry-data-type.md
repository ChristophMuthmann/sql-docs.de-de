---
title: STCentroid (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STCentroid_TSQL
- STCentroid (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STCentroid (geometry Data Type)
ms.assetid: 4dc5a004-7a53-4cce-81dd-9f5e1dd0db78
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c34e8eb334190b72a560086a9d5e862ba6667dec
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stcentroid-geometry-data-type"></a>STCentroid (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt das geometrische Zentrum einer **Geometry** Instanz, die aus einem oder mehreren Polygonen besteht.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STCentroid ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
 Open Geospatial Consortium (OGC)-Typ: **Point**  
  
## <a name="remarks"></a>Hinweise  
 `STCentroid()`Gibt null zurück, wenn die **Geometrie** -Instanz ist eine **Polygon, CurvePolygon**, oder **MultiPolygon** Typ.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-computing-the-centroid-of-a-polygon-instance"></a>A. Berechnen des Schwerpunkts einer Polygon-Instanz  
 Im folgenden Beispiel wird `STCentroid()` zum Berechnen des Schwerpunkts einer `polygon``geometry` Instanz:  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STCentroid().ToString();  
```  
  
### <a name="b-computing-the-centroid-of-a-curvepolygon-instance"></a>B. Berechnen des Schwerpunkts einer CurvePolygon-Instanz  
 Im folgenden Beispiel wird der Schwerpunkt für eine `CurvePolygon`-Instanz berechnet:  
  
 `DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))';`  
  
 `SELECT @g.STCentroid().ToString() AS Centroid`  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


