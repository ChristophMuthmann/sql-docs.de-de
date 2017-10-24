---
title: STCurveToLine (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a0601e93e3763ca184ecf599da2cc7f9b36dd6f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt eine polygonale Näherung einer Instanz von **geometry** mit Kreisbogensegmenten zurück.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 Gibt ein leeres **GeometryCollection**-Instanz für leere **Geometrie** Instanz Variablen und gibt **NULL** für nicht initialisierte **Geometrie** Variablen.  
  
 Die polygonale Näherung, die die Methode zurückgibt, hängt die **Geometry** Instanz, mit denen Sie die Methode aufrufen:  
  
-   Gibt eine **LineString** -Instanz für eine **CircularString** - oder **CompoundCurve** -Instanz zurück.  
  
-   Gibt eine **Polygon** -Instanz für eine **CurvePolygon** -Instanz zurück.  
  
-   Gibt eine Kopie des der **Geometrie** Instanz, wenn diese Instanz nicht ist eine **CircularString**, **CompoundCurve**, oder **CurvePolygon** Instanz . Z. B. die `STCurveToLine` Methode gibt ein **Punkt** -Instanz für eine **Geometry** Instanz, die eine **Punkt** Instanz.  
  
 Im Gegensatz zur SQL/MM-Spezifikation die `STCurveToLine` Methode verwendet keinen Z-Koordinate Werte zum Berechnen der polygonalen Näherung verwendet. Die Methode ignoriert alle Z-Koordinate Werte in die aufrufende **Geometrie** Instanz.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. Verwenden einer nicht initialisierten geometry-Variablen und einer leeren Instanz  
 Im folgenden Beispiel das erste **wählen** Anweisung mit einer nicht initialisierten **Geometrie** Instanz zum Aufrufen der `STCurveToLine` -Methode und die zweite **wählen** -Anweisung verwendet eine leere **Geometrie** Instanz. Daher gibt die Methode zurück **NULL** an die erste Anweisung und eine **GeometryCollection** Auflistung für die zweite Anweisung.  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. Verwenden einer LineString-Instanz  
 Die **wählen** -Anweisung in das folgende Beispiel verwendet eine **LineString** Instanz zum Aufrufen der Methode ' stcurvetoline '. Daher die Methode gibt ein **LineString** Instanz.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. Verwenden einer CircularString-Instanz  
 Die erste **wählen** -Anweisung in das folgende Beispiel verwendet eine **CircularString** Instanz zum Aufrufen der Methode ' stcurvetoline '. Daher die Methode gibt ein **LineString** Instanz. Dies **wählen** Anweisung vergleicht auch die Längen der beiden Instanzen, die ungefähr gleich sind.  Zum Schluss das zweite **wählen** -Anweisung gibt die Anzahl der Punkte für jede Instanz zurück.  Es gibt nur 5 Punkte für die **CircularString** Instanz, jedoch 65 Punkte für die **LineString**Instanz.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. Verwenden einer CurvePolygon-Instanz  
 Die **wählen** -Anweisung in das folgende Beispiel verwendet eine **CurvePolygon** Instanz zum Aufrufen der Methode ' stcurvetoline '. Daher die Methode gibt ein **Polygon** Instanz.  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  


