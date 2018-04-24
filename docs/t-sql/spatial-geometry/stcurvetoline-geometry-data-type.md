---
title: STCurveToLine (geometry-Datentyp) | Microsoft-Dokumentation
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
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9133d5dff6e884c9f34ed1851c9471070964cbd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt eine polygonale Näherung einer Instanz von **geometry** mit Kreisbogensegmenten zurück.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geometry**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 Gibt eine leere **GeometryCollection**-Instanz für leere **geometry**-Instanzvariablen und **NULL** für nicht initialisierte **geometry**-Variablen zurück.  
  
 Die polygonale Näherung, die die Methode zurückgibt, hängt von der **geometry**-Instanz ab, mit der Sie die Methode aufrufen:  
  
-   Gibt eine **LineString** -Instanz für eine **CircularString** - oder **CompoundCurve** -Instanz zurück.  
  
-   Gibt eine **Polygon** -Instanz für eine **CurvePolygon** -Instanz zurück.  
  
-   Gibt eine Kopie der **geometry**-Instanz zurück, wenn diese keine **CircularString**-, **CompoundCurve**- oder **CurvePolygon**-Instanz ist. Beispielsweise gibt die `STCurveToLine`-Methode eine **Point**-Instanz für eine **geometry**-Instanz zurück, die eine **Point**-Instanz darstellt.  
  
 Im Gegensatz zur SQL/MM-Spezifikation werden bei der `STCurveToLine`-Methode keine Z-Koordinatenwerte zur Berechnung der polygonalen Näherung verwendet. Die Methode berücksichtigt keine in der aufrufenden **geometry**-Instanz enthaltenen Werte der Z-Koordinate.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. Verwenden einer nicht initialisierten geometry-Variablen und einer leeren Instanz  
 In diesem Beispiel verwendet die erste **SELECT**-Anweisung eine nicht initialisierte **geometry**-Instanz, um die `STCurveToLine`-Methode aufzurufen, und die zweite **SELECT**-Anweisung verwendet eine leere **geometry**-Instanz. Daher gibt die Methode **NULL** an die erste Anweisung zurück und eine **GeometryCollection**-Collection an die zweite Anweisung.  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. Verwenden einer LineString-Instanz  
 Die **SELECT**-Anweisung in den folgenden Beispielen verwendet eine **LineString**-Instanz, um die STCurveToLine-Methode aufzurufen. Daher wird von der Methode eine **LineString**-Instanz zurückgegeben.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. Verwenden einer CircularString-Instanz  
 Die erste **SELECT**-Anweisung in den folgenden Beispielen verwendet eine **CircularString**-Instanz, um die STCurveToLine-Methode aufzurufen. Daher wird von der Methode eine **LineString**-Instanz zurückgegeben. Mit dieser **SELECT**-Anweisung wird auch die Länge der beiden Instanzen verglichen, die in etwa gleich ist.  Abschließend wird von der zweiten **SELECT**-Anweisung die Anzahl der Punkte für jede Instanz zurückgegeben.  Es werden nur 5 Punkte für die **CircularString**-Instanz, aber 65 Punkte für die **LineString**-Instanz zurückgegeben.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. Verwenden einer CurvePolygon-Instanz  
 Die **SELECT**-Anweisung in den folgenden Beispielen verwendet eine **CurvePolygon**-Instanz, um die STCurveToLine-Methode aufzurufen. Daher wird von der Methode eine **Polygon**-Instanz zurückgegeben.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  

