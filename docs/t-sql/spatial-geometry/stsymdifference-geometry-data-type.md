---
title: STSymDifference (Geometry-Datentyp) | Microsoft Docs
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
- STSymDifference_TSQL
- STSymDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geometry Data Type)
ms.assetid: 1d4cf35a-ca89-4aa4-ae30-e61a0ff18b53
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b83e2ef917f76f615588327c8a3c2721f30e347a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stsymdifference-geometry-data-type"></a>STSymDifference (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt ein Objekt zurück, das alle Punkte darstellt, die sich entweder in einer **geometry** -Instanz oder in einer anderen **geometry** -Instanz befinden, nicht jedoch die Punkte, die sich innerhalb beider Instanzen befinden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STSymDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geometry*  
 Eine andere **geometry** -Instanz zusätzlich zu der Instanz, in der `STSymDistance()` aufgerufen wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt immer NULL zurück, wenn die SRIDs (Spatial Reference IDs) der **geometry** -Instanzen nicht übereinstimmen. Im Ergebnis können nur dann Kreisbogensegmente enthalten sein, wenn die Eingabeinstanzen auch Kreisbogensegmente enthalten.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygon-instances"></a>A. Berechnen des symmetrischen Unterschiedes zweier Polygon-Instanzen  
 Im folgenden Beispiel wird `STSymDifference()` zum Berechnen der symmetrischen Differenz zweier `Polygon` -Instanzen verwendet.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-between-a-curvepolygon-and-a-polygon-instance"></a>B. Berechnen des symmetrischen Unterschiedes zwischen einer CurvePolygon- und einer Polygon-Instanz  
 Im folgenden Beispiel wird eine `GeometryCollection` zurückgegeben, die den symmetrischen Unterschied zwischen einem `CurvePolygon` und einem `Polygon`darstellt.  
  
 `DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';`  
  
 `DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';`  
  
 `SELECT @h.STSymDifference(@g).ToString();`  
  
## <a name="c-using-stsymdifference-on-curvepolygon-instance-with-an-inscribed-polygon-instance"></a>C. Verwenden von STSymDifference() in einer CurvePolygon-Instanz mit einer Polygoninstanz  
 Im folgenden Beispiel wird eine Instanz von `CurvePolygon` mit dem inneren Ring einer Instanz von `Polygon` zurückgegeben, der den symmetrischen Unterschied zwischen den beiden Instanzen darstellt.  
  
 `DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';`  
  
 `DECLARE @h geometry = 'POLYGON ((1 -1, 2 -1, 2 1, 1 1, 1 -1))';`  
  
 `SELECT @h.STSymDifference(@g).ToString();`  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

