---
title: CurveToLineWithTolerance (geometry-Datentyp) | Microsoft-Dokumentation
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
- CurveToLineWithTolerance method (geometry)
ms.assetid: 96871075-1998-4cd9-86b1-3fc55577aee4
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 252ceb0e9d9544615824b4ecb275cd1888e3c783
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="curvetolinewithtolerance-geometry-data-type"></a>CurveToLineWithTolerance (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt eine polygonale Näherung einer Instanz von **geometry** mit Kreisbogensegmenten zurück.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.CurveToLineWithTolerance ( tolerance, relative )  
```  
  
## <a name="arguments"></a>Argumente  
 *tolerance*  
 Ein **double** -Ausdruck, der die maximalen Fehler zwischen dem ursprünglichen Kreisbogensegment und der linearen Näherung definiert.  
  
 *relative*  
 Ein **bool** -Ausdruck, der angibt, ob ein relatives Maximum für die Abweichung verwendet werden soll. Wenn der relativer Wert auf false (0) festgelegt wird, wird ein absolutes Maximum für die Abweichung verwendet, die eine lineare Näherung aufweisen kann. Wenn der relative Wert auf true (1) festgelegt wird, wird die Toleranz als Produkt des tolerance-Parameters und des Durchmessers des Begrenzungsrahmens für das räumliche Objekt berechnet.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geometry**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="exceptions"></a>Ausnahmen  
 Wenn Sie die Toleranz auf <= 0 festlegen, wird eine `ArgumentOutOfRange`-Ausnahme ausgelöst.  
  
## <a name="remarks"></a>Remarks  
 Mit dieser Methode kann ein Umfang für die Fehlertoleranz in der resultierenden **LineString**angegeben werden.  
  
 In der folgenden Tabelle wird der von `CurveToLineWithTolerance()`zurückgegebene Instanzentyp für verschiedene Typen angezeigt.  
  
|Aufgerufener Instanzentyp|Räumlicher Rückgabetyp|  
|----------------------------|---------------------------|  
|Leere geometry-Instanz|Leere Instanz von **GeometryCollection**|  
|**Point** und **MultiPoint**|**Point** -Instanz|  
|**MultiPoint**|Instanz von**Point** oder **MultiPoint** |  
|**CircularString**, **CompoundCurve**oder **LineString**|**LineString** -Instanz|  
|**MultiLineString**|Instanz von**LineString** oder **MultiLineString** |  
|**CurvePolygon** und **Polygon**|**Polygon** -Instanz|  
|**MultiPolygon**|Instanz von**Polygon** oder **MultiPolygon** |  
|**GeometryCollection** mit einer einzelnen Instanz, die kein Kreisbogensegment enthält|Die Instanz, die im **GeometryCollection** enthalten ist, bestimmt den Typ der Instanz, die zurückgegeben wird.|  
|**GeometryCollection** mit einer einzelnen eindimensionalen Instanz eines Kreisbogensegments (**CircularString**, **CompoundCurve**)|**LineString** -Instanz|  
|**GeometryCollection** mit einer einzelnen zweidimensionalen Instanz eines Kreisbogensegments (**CurvePolygon**)|**Polygon** -Instanz|  
|**GeometryCollection** mit mehreren eindimensionalen Instanzen|**MultiLineString** -Instanz|  
|**GeometryCollection** mit mehreren zweidimensionalen Instanzen|**MultiPolygon** -Instanz|  
|**GeometryCollection** mit mehreren Instanzen verschiedener Dimensionen|**GeometryCollection** -Instanz|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-different-tolerance-values-on-a-circularstring-instance"></a>A. Verwenden verschiedener Toleranzwerte in einer CircularString-Instanz  
 Im folgenden Beispiel wird gezeigt, wie sich das Festlegen der Toleranz auf eine Instanz von `LineString`auswirkt, die von einer Instanz von `CircularString` zurückgegeben wird:  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.01, 0).STNumPoints();
 ```  
  
### <a name="b-using-the-method-on-a-multilinestring-instance-containing-one-linestring"></a>B. Verwenden der Methode in einer MultiLineString-Instanz mit einem LineString  
 Im folgenden Beispiel wird die Rückgabe einer Instanz von `MultiLineString` gezeigt, die nur eine `LineString` -Instanz enthält:  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="c-using-the-method-on-a-multilinestring-instance-containing-multiple-linestrings"></a>C. Verwenden der Methode in einer MultiLineString-Instanz mit mehreren LineStrings  
 Im folgenden Beispiel wird die Rückgabe einer Instanz von `MultiLineString` gezeigt, die mehrere `LineString` -Instanzen enthält:  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('MULTILINESTRING((1 3, 4 8, 6 9),(4 4, 9 18))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).ToString();
 ```  
  
### <a name="d-setting-relative-to-true-for-an-invoking-curvepolygon-instance"></a>D. Festlegen des relativen Werts für eine aufrufende CurvePolygon-Instanz auf true  
 Im folgenden Beispiel wird eine Instanz von `CurvePolygon` verwendet, um `CurveToLineWithTolerance()` mit *relative* und dem Wert true aufzurufen:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.CurveToLineWithTolerance(.5,1).ToString();
 ```  
  
### <a name="e-using-the-method-on-a-geometrycollection-instance"></a>E. Verwenden der Methode in einer GeometryCollection-Instanz  
 Im folgenden Beispiel wird `CurveToLineWithTolerance()` in einer `GeometryCollection` mit einer zweidimensionalen Instanz von `CurvePolygon` und einer eindimensionalen Instanz von `CircularString` aufgerufen. `CurveToLineWithTolerance()` wandelt die beiden Kreisbogensegmenttypen in Liniensegmenttypen um und gibt diese in einem `GeometryCollection`-Typ zurück.  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('GEOMETRYCOLLECTION(CURVEPOLYGON( COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))), CIRCULARSTRING(4 4, 8 6, 9 5))'); 
 SELECT @g.CurveToLineWithTolerance(0.1,0).STNumPoints(), @g.CurveToLineWithTolerance(0.1, 0).ToString();
 ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CurveToLineWithTolerance &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/curvetolinewithtolerance-geography-data-type.md)   
 [STCurveToLine &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stcurvetoline-geometry-data-type.md)  
  
  

