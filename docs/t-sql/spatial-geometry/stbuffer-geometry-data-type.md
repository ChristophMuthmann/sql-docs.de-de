---
title: STBuffer (geometry-Datentyp) | Microsoft-Dokumentation
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
- STBuffer (geometry Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geometry Data Type)
ms.assetid: ca6bf2dc-1d38-4503-b87e-f2ea033d36ba
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1bd6a6d96afc57058db986f921d70afee4e9b7fb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stbuffer-geometry-data-type"></a>STBuffer (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt ein geometrisches Objekt zurück, dass die Vereinigung aller Punkte darstellt, deren Abstand zu einer **geometry** -Instanz kleiner oder gleich einem angegebenen Wert ist.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>Argumente  
 *distance*  
 Ein Wert vom Typ **float** (**double** in .NET-Framework), der den Abstand zu der geometry-Instanz angibt, um die der Puffer berechnet werden soll.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geometry**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STBuffer()` berechnet einen Puffer wie [BufferWithTolerance](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md), wobei *tolerance* = distance \* 0,001 und *relative* = **false** ist.  
  
 Wenn *distance* > 0, wird eine **Polygon**- oder **MultiPolygon**-Instanz zurückgegeben.  
  
> [!NOTE]  
>  Da der Abstand ein **float**-Wert ist, kann ein sehr kleiner Wert in den Berechnungen mit 0 gleichgesetzt werden.  In diesem Fall wird eine Kopie der aufrufenden Instanz von **geometry** zurückgegeben.  Informationen hierzu finden Sie unter [float und real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
  
 Wenn *distance* = 0 ist, wird eine Kopie der aufrufenden Instanz von **geometry** zurückgegeben.  
  
 Wenn *distance* < 0, gilt Folgendes:  
  
-   wird eine leere Instanz von **GeometryCollection** zurückgegeben, wenn die Dimensionen der Instanz 0 oder 1 betragen.  
  
-   Ein negativer Puffer wird zurückgegeben, wenn die Dimensionen der Instanz 2 oder mehr betragen.  
  
    > [!NOTE]  
    >  Ein negativer Puffer erstellt auch möglicherweise eine leere Instanz von **GeometryCollection** .  
  
 Ein negativer Puffer entfernt alle Punkte innerhalb des gegebenen Abstands der Begrenzung der geometry-Instanz.  
  
 Die Abweichung zwischen dem theoretischen und dem berechnetem Puffer beträgt max(tolerance, extents * 1,0E-7), wobei tolerance = distance \* 0,001 ist. Weitere Informationen zu Erweiterungen finden Sie unter [geometry-Datentyp-Methodenverweis](http://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-calling-stbuffer-with-parametervalue--0-on-one-dimensional-geometry-instance"></a>A. Aufrufen von STBuffer() mit einem Parameterwert < 0 für eine eindimensionale geometry-Instanz  
 Im folgenden Beispiel wird eine leere Instanz von `GeometryCollection` zurückgegeben:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="b-calling-stbuffer-with-parametervalue--0-on-a-polygon-instance"></a>B. Aufrufen von STBuffer() mit parameter_value < 0 für eine Polygon-Instanz  
 Im folgenden Beispiel wird eine Instanz von `Polygon` mit einem negativen Puffer zurückgegeben:  
  
```
 DECLARE @g geometry = 'POLYGON((1 1, 1 5, 5 5, 5 1, 1 1))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
### <a name="c-calling-stbuffer-with-parametervalue--0-on-a-curvepolygon-instance"></a>C. Aufrufen von STBuffer() mit parameter_value < 0 für eine CurvePolygon-Instanz  
 Im folgenden Beispiel wird eine Instanz von `Polygon` mit einem negativen Puffer von einer `CurvePolygon` -Instanz zurückgegeben:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-1).ToString();
 ```  
  
> [!NOTE]  
>  Anstelle einer Instanz von `Polygon` wird eine Instanz von `CurvePolygon` zurückgegeben.  Informationen zum Zurückgeben einer `CurvePolygon`-Instanz finden Sie unter [BufferWithCurves &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
### <a name="d-calling-stbuffer-with-a-negative-parameter-value-that-returns-an-empty-instance"></a>D. Aufrufen von STBuffer() mit einem negativen Parameterwert zur Rückgabe einer leeren Instanz  
 Im folgenden Beispiel wird gezeigt, was geschieht, wenn der *distance* -Parameter aus dem vorangehenden Beispiel -2 entspricht.  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.STBuffer(-2).ToString();
 ```  
  
 Diese **SELECT**-Anweisung gibt `GEOMETRYCOLLECTION EMPTY.` zurück.  
  
### <a name="e-calling-stbuffer-with-parametervalue--0"></a>E. Aufrufen von STBuffer() mit parameter_value = 0  
 Im folgenden Beispiel wird eine Kopie der aufrufenden Instanz von `geometry` zurückgegeben:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(0).ToString();
 ```  
  
### <a name="f-calling-stbuffer-with-a-non-zero-parameter-value-that-is-extremely-small"></a>F. Aufrufen von STBuffer() mit einem äußerst kleinen Parameterwert ungleich 0  
 Im folgenden Beispiel wird auch eine Kopie der aufrufenden Instanz von `geometry` zurückgegeben:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.STBuffer(@distance).ToString();
 ```  
  
### <a name="g-calling-stbuffer-with-parametervalue--0"></a>G. Aufrufen von STBuffer() mit parameter_value > 0  
 Im folgenden Beispiel wird eine Instanz von `Polygon` zurückgegeben:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer(2).ToString();
 ```  
  
### <a name="h-calling-stbuffer-with-a-string-parameter-value"></a>H. Aufrufen von STBuffer() mit einem Zeichenfolgenparameterwert  
 Im folgenden Beispiel wird die gleiche Instanz von `Polygon` zurückgegeben, die bereits erwähnt wurde, es wird jedoch ein Zeichenfolgenparameter an die Methode übergeben:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('2').ToString();
 ```  
  
 Im folgenden Beispiel wird ein Fehler ausgelöst:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.STBuffer('a').ToString();
 ```  
  
> [!NOTE]  
>  In den beiden vorangehenden Beispielen wurde ein Zeichenfolgenliteral an den `STBuffer()`übergeben.  Das erste Beispiel kann ordnungsgemäß ausgeführt werden, da das Zeichenfolgenliteral in einen numerischen Wert konvertiert werden kann. Im zweiten Beispiel wird allerdings eine `ArgumentException`ausgelöst.  
  
### <a name="i-calling-stbuffer-on-a-multipoint-instance"></a>I. Aufrufen von STBuffer() für eine MultiPoint-Instanz  
 Im folgenden Beispiel werden zwei Instanzen von `MultiPolygon` sowie eine Instanz von `Polygon` zurückgegeben:  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.STBuffer(1).ToString(); 
 SELECT @g.STBuffer(1.5).ToString(); 
 SELECT @g.STBuffer(1.6).ToString();
 ```  
  
 Von den ersten beiden **SELECT** -Anweisungen wird eine Instanz von `MultiPolygon` zurückgegeben, da der *distance* -Parameter kleiner oder gleich 1/2 des Abstands zwischen den beiden Punkten (1 1) und (1 4) ist. Von der dritten **SELECT**-Anweisung gibt `Polygon` zurückgegeben, da sich die zwischengespeicherten Instanzen der beiden Punkte (1 1) und (1 4) überschneiden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BufferWithTolerance &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type.md)   
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

