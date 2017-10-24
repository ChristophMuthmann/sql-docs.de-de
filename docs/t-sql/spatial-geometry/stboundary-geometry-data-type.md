---
title: STBoundary (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STBoundary (geometry Data Type)
- STBoundary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBoundary (geometry Data Type)
ms.assetid: f0551674-e6e8-4926-9038-df03f2c807d7
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a582d1c730fa8e11b6ddd684494588b69a01bf64
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stboundary-geometry-data-type"></a>STBoundary (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Begrenzung einer **Geometrie** Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STBoundary ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 `STBoundary()`Gibt ein leeres **GeometryCollection** Wenn die Endpunkte für einen **LineString**, **CircularString**, oder **CompoundCurve** Instanz sind identisch.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-stboundary-on-a-linestring-instance-with-different-endpoints"></a>A. Verwenden von STBoundary() in einer LINESTRING-Instanz mit verschiedenen Endpunkten  
 Das folgende Beispiel erstellt eine `LineString``geometry` Instanz. `STBoundary()`Gibt die Begrenzung der `LineString`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STBoundary().ToString();  
```  
  
### <a name="b-using-stboundary-on-a-linestring-instance-with-the-same-endpoints"></a>B. Verwenden von STBoundary() in einer LINESTRING-Instanz mit übereinstimmenden Endpunkten  
 Im folgenden Beispiel wird eine gültige `LineString`-Instanz mit den gleichen Endpunkten erstellt. `STBoundary()` gibt eine leere `GeometryCollection` zurück.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, -2 2, 0 0)', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
### <a name="c-using-stboundary-on-a-curvepolygon-instance"></a>C. Verwenden von STBoundary() in einer CurvePolygon-Instanz  
 Im folgenden Beispiel wird `STBoundary()` in einer `CurvePolygon`-Instanz verwendet. `STBoundary()` gibt eine `CircularString`-Instanz zurück.  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(0 0, 2 2, 0 2, -2 2, 0 0))', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

