---
title: STUnion (geometry-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STUnion (geometry Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion (geometry Data Type)
ms.assetid: 5b168118-137d-402f-9173-fee3f365a89c
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa305eb44c53bdedf630d300e6f0a3b3c3a6d632
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stunion-geometry-data-type"></a>STUnion (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt ein Objekt zurück, das die Vereinigung einer **geometry** -Instanz mit einer weiteren **geometry** -Instanz darstellt.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STUnion ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geometry*  
 Eine andere **geometry** -Instanz zur Vereinigung mit der Instanz, in der `STUnion()` aufgerufen wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geometry**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Diese Methode gibt immer NULL zurück, wenn die SRIDs (Spatial Reference IDs) der **geometry** -Instanzen nicht übereinstimmen. Im Ergebnis können nur dann Kreisbogensegmente enthalten sein, wenn die Eingabeinstanzen auch Kreisbogensegmente enthalten.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-computing-the-union-of-two-polygon-instances"></a>A. Berechnen der Union von zwei Polygon-Instanzen  
 Im folgenden Beispiel wird `STUnion()` zum Berechnen der Vereinigung zweier `Polygon` -Instanzen verwendet.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-computing-the-union-of-a-polygon-instance-with-a-curvepolygon-instance"></a>B. Berechnen der Union einer Polygon-Instanz und einer CurvePolygon-Instanz  
 Im folgenden Beispiel wird eine `GeometryCollection` -Instanz zurückgegeben, die ein Kreisbogensegment enthält.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON((5 -1, 5 -3, 7 -3, 7 -1, 5 -1))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
 `STUnion()` gibt ein Ergebnis zurück, das ein Kreisbogensegment enthält, da die Instanz, die `STUnion()` aufgerufen hat, ein Kreisbogensegment enthält.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

