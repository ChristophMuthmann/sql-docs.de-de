---
title: Reduce (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs: TSQL
helpviewer_keywords: Reduce method
ms.assetid: 132184bf-c4d2-4a27-900d-8373445dce2a
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb6c4a66f3233620ef5d24506d41e7659fc3b82d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="reduce-geometry-data-type"></a>Reduce (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt einen Näherungswert der gegebenen **geometry** -Instanz zurück. Dieser Näherungswert wird unter Verwendung einer Erweiterung des Douglas-Peucker-Algorithmus mit der angegebenen Toleranz ermittelt.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumente  
 *tolerance*  
 Ein Wert vom Typ **float**. *tolerance* gibt die Toleranz an, die als Eingabe für den Näherungsalgorithmus verwendet werden soll.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 Bei Auflistungstypen arbeitet dieser Algorithmus unabhängig für jeden **geometry** -Wert, der in der Instanz enthalten ist.  
  
 Dieser Algorithmus ändert keine **Point** -Instanzen.  
  
 Bei Instanzen von **LineString**, **CircularString**und **CompoundCurve** behält der Näherungsalgorithmus die ursprünglichen Anfangs- und Endpunkte der Instanz bei und fügt iterativ so lange die Punkte der ursprünglichen Instanz wieder ein, die am stärksten vom Ergebnis abweichen, bis kein weiterer Punkt stärker abweicht, als die angegebene Toleranz erlaubt.  
  
 `Reduce()`Gibt eine **LineString**, **CircularString**, oder **CompoundCurve** -Instanz für **CircularString** Instanzen.  `Reduce()`Gibt eine **CompoundCurve** oder **LineString** -Instanz für **CompoundCurve** Instanzen.  
  
 Auf **Polygon** -Instanzen wird der Näherungsalgorithmus unabhängig für jeden Ring angewendet. Die Methode erzeugt eine `FormatException` , wenn die zurückgegebene **Polygon** -Instanz ungültig ist. Eine ungültige **MultiPolygon** -Instanz wird beispielsweise dann erstellt, wenn `Reduce()` zur Vereinfachung jedes Rings in der Instanz angewendet wird, und sich die ergebenden Ringe überschneiden.  Bei Instanzen von **CurvePolygon** mit einem äußeren Ring und ohne innere Ringe wird von `Reduce()` gibt eine Instanz von **CurvePolygon**, **LineString**oder **Point** zurückgegeben.  Wenn **CurvePolygon** innere Ringe aufweist, wird eine Instanz von **CurvePolygon** oder eine Instanz von **MultiPoint** zurückgegeben.  
  
 Wenn ein Kreisbogensegment gefunden wird, überprüft der Näherungsalgorithmus, ob eine näherungsweise Bestimmung des Bogens durch die Sehne innerhalb der Hälfte der angegebenen Toleranz möglich ist.  Wenn die Sehne diese Kriterien erfüllt, wird der Kreisbogen in den Berechnungen durch die Sehne ersetzt. Andernfalls wird der Kreisbogen beibehalten, und der Näherungsalgorithmus wird für die verbleibenden Segmente übernommen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-reduce-to-simplify-a-linestring"></a>A. Vereinfachen eines LineString mithilfe von Reduce()  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und `Reduce()` verwendet, um die Instanz zu vereinfachen.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0, 2 1, 3 0, 4 1)', 0);  
SELECT @g.Reduce(.75).ToString();  
```  
  
### <a name="b-using-reduce-with-varying-tolerance-levels-on-a-circularstring"></a>B. Verwenden von Reduce() in einem CircularString und veränderlichen Toleranzebenen  
 Im folgenden Beispiel wird `Reduce()` in einer **CircularString** -Instanz mit drei Toleranzebenen verwendet:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0)'; 
 SELECT @g.Reduce(5).ToString(); 
 SELECT @g.Reduce(15).ToString(); 
 SELECT @g.Reduce(16).ToString();
 ```  
  
 Hierdurch wird folgende Ausgabe generiert:  
  
 ```
 CIRCULARSTRING (0 0, 8 8, 16 0, 20 -4, 24 0) 
 COMPOUNDCURVE (CIRCULARSTRING (0 0, 8 8, 16 0), (16 0, 24 0)) 
 LINESTRING (0 0, 24 0)
 ```  
  
 Alle zurückgegebenen Instanzen enthalten die Endpunkte (0 0) und (24 0).  
  
### <a name="c-using-reduce-with-varying-tolerance-levels-on-a-compoundcurve"></a>C. Verwenden von Reduce() in einer CompoundCurve mit veränderlichen Toleranzebenen  
 Im folgenden Beispiel wird `Reduce()` in einer **CompoundCurve** -Instanz mit drei Toleranzebenen verwendet:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 8 8, 16 0, 20 -4, 24 0),(24 0, 20 4, 16 0))';  
 SELECT @g.Reduce(15).ToString();  
 SELECT @g.Reduce(16).ToString();
 ```  
  
 Beachten Sie in diesem Beispiel, dass die zweite **SELECT** -Anweisung die **LineString** -Instanz mit drei Toleranzebenen verwendet: `LineString(0 0, 16 0)`.  
  
### <a name="showing-an-example-where-the-original-start-and-end-points-are-lost"></a>Anzeigen eines Beispiels mit verloren gegangenem Ausgangs- und Endpunkt  
 Im folgenden Beispiel wird gezeigt, dass der ursprüngliche Ausgangs- und Endpunkt von der resultierenden Instanz möglicherweise nicht beibehalten werden. Die Ursache hierfür liegt darin, dass andernfalls eine ungültige Instanz von **LineString** erzeugt würde.  
  
```  
DECLARE @g geometry = 'LINESTRING(0 0, 4 0, 2 .01, 1 0)';  
DECLARE @h geometry = @g.Reduce(1);  
SELECT @g.STIsValid() AS Valid  
SELECT @g.ToString() AS Original, @h.ToString() AS Reduced;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte statische geometry-Methoden](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

