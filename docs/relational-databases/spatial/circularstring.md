---
title: CircularString | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-spatial
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a866d003f23cfbeea4b56478e607825266b06709
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="circularstring"></a>CircularString
  Ein **CircularString** ist eine Auflistung von 0 (null) oder mehr stetigen Kreisbogensegmenten. Ein Kreisbogensegment ist ein von drei Punkten in einer zweidimensionalen Ebene definierter gekrümmter Abschnitt; der erste Punkt darf nicht mit dem dritten Punkt identisch sein. Wenn alle drei Punkte eines Kreisbogensegments kollinear sind, wird das Bogensegment als Liniensegment behandelt.  
  
> [!IMPORTANT]  
>  Um eine ausführliche Beschreibung und Beispiele der in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]eingeführten neuen räumlichen Funktionen (z.B. zum **CircularString** -Untertyp) zu erhalten, laden Sie das Whitepaper [New Spatial Features in SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407)(Neue räumliche Funktionen in SQL Server 2012) herunter.  
  
## <a name="circularstring-instances"></a>CircularString-Instanzen  
 In der unten stehenden Zeichnung sind gültige **CircularString** -Instanzen dargestellt:  
  
 ![5ff17e34-b578-4873-9d33-79500940d0bc](../../relational-databases/spatial/media/5ff17e34-b578-4873-9d33-79500940d0bc.gif)
  
### <a name="accepted-instances"></a>Akzeptierte Instanzen  
 Eine **CircularString**-Instanz wird akzeptiert, wenn sie entweder leer ist oder eine ungerade Anzahl von Punkten n enthält, wobei n > 1 gilt. Die folgenden **CircularString** -Instanzen werden akzeptiert.  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';  
```  
  
 `@g3` zeigt, dass eine **CircularString** -Instanz zwar akzeptiert werden kann, möglicherweise jedoch nicht gültig ist. Die folgende Deklaration einer CircularString-Instanz wird nicht akzeptiert. Diese Deklaration löst eine `System.FormatException`aus.  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1)';  
```  
  
### <a name="valid-instances"></a>Gültige Instanzen  
 Eine gültige **CircularString** -Instanz muss leer sein oder über die folgenden Attribute verfügen:  
  
-   Sie muss mindestens ein Kreisbogensegment enthalten (d. h., sie muss mindestens über drei Punkte verfügen).  
  
-   Der letzte Endpunkt für jedes Kreisbogensegment in der Sequenz (mit Ausnahme des letzten Segments) muss dem ersten Endpunkt für das jeweils nächste Segment in der Sequenz entsprechen.  
  
-   Sie muss eine ungerade Anzahl von Punkten aufweisen.  
  
-   Sie darf sich über ein Intervalls nicht selbst überlappen.  
  
-   **CircularString** -Instanzen können zwar Liniensegmente enthalten, diese Liniensegmente müssen jedoch durch drei kollineare Punkte definiert werden.  
  
 Im folgenden Beispiel werden gültige **CircularString** -Instanzen veranschaulicht.  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';  
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();  
```  
  
 Eine **CircularString** -Instanz muss mindestens zwei Kreisbogensegmente enthalten, damit ein vollständiger Kreis definiert wird. In einer **CircularString** -Instanz kann kein einzelnes Kreisbogensegment, z.B. (1 1, 3 1, 1 1), verwendet werden, um einen vollständigen Kreis zu definieren. Definieren Sie den Kreis mit (1 1, 2 2, 3 1, 2 0, 1 1).  
  
 Im folgenden Beispiel werden CircularString-Instanzen veranschaulicht, die nicht gültig sind.  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING(1 1, 2 0, 1 1)';  
DECLARE @g2 geometry = 'CIRCULARSTRING(0 0, 0 0, 0 0)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
### <a name="instances-with-collinear-points"></a>Instanzen mit kollinearen Punkten  
 In den folgenden Fällen wird ein Kreisbogensegment als Liniensegment behandelt:  
  
-   Wenn alle drei Punkte kollinear (z. B. 1 3, 4 4, 7 5) sind.  
  
-   Wenn der erste und der mittlere Punkt identisch sind und sich beide vom dritten Punkt unterscheiden (z. B. 1 3, 1 3, 7 5).  
  
-   Wenn der mittlere und der letzte Punkt identisch sind und sich beide vom ersten Punkt unterscheiden (z. B. 1 3, 4 4, 4 4).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-circularstring"></a>A. Instanziieren einer Geometry-Instanz mit einem leeren CircularString  
 In diesem Beispiel wird veranschaulicht, wie eine leere **CircularString** -Instanz erstellt wird:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING EMPTY');  
```  
  
### <a name="b-instantiating-a-geometry-instance-using-a-circularstring-with-one-circular-arc-segment"></a>B. Instanziieren einer Geometry-Instanz, die einen CircularString mit einem Kreisbogensegment verwendet  
 Im folgenden Beispiel wird veranschaulicht, wie eine **CircularString** -Instanz mit einem einzelnen Kreisbogensegment (Halbkreis) erstellt wird:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="c-instantiating-a-geometry-instance-using-a-circularstring-with-multiple-circular-arc-segments"></a>C. Instanziieren einer Geometry-Instanz, die einen CircularString mit mehreren Kreisbogensegmenten verwendet  
 Im folgenden Beispiel wird veranschaulicht, wie eine **CircularString** -Instanz mit mehreren Kreisbogensegmenten (vollständiger Kreis) erstellt wird:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING(2 1, 1 2, 0 1, 1 0, 2 1)');  
SELECT 'Circumference = ' + CAST(@g.STLength() AS NVARCHAR(10));    
```  
  
 Hierdurch wird folgende Ausgabe generiert:  
  
```  
Circumference = 6.28319  
```  
  
 Vergleichen Sie die Ausgabe, wenn **LineString** anstelle von **CircularString**verwendet wird:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(2 1, 1 2, 0 1, 1 0, 2 1)', 0);  
SELECT 'Perimeter = ' + CAST(@g.STLength() AS NVARCHAR(10));  
```  
  
 Hierdurch wird folgende Ausgabe generiert:  
  
```  
Perimeter = 5.65685  
```  
  
 Beachten Sie, dass der Wert für das **CircularString** -Beispiel annähernd 2∏ beträgt (der tatsächliche Umfang des Kreises).  
  
### <a name="d-declaring-and-instantiating-a-geometry-instance-with-a-circularstring-in-the-same-statement"></a>D. Deklarieren und Instanziieren einer Geometry-Instanz mit einem CircularString in derselben Anweisung  
 In diesem Codeausschnitt wird veranschaulicht, wie eine **geometry** -Instanz mit einem **CircularString** in derselben Anweisung deklariert und instanziiert wird:  
  
```tsql  
DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
```  
  
### <a name="e-instantiating-a-geography-instance-with-a-circularstring"></a>E. Instanziieren einer Geography-Instanz mit einem CircularString  
 Im folgenden Beispiel wird veranschaulicht, wie eine **geography** -Instanz mit einem **CircularString**deklariert und instanziiert wird:  
  
```tsql  
DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
```  
  
### <a name="f-instantiating-a-geometry-instance-with-a-circularstring-that-is-a-straight-line"></a>F. Instanziieren einer Geometry-Instanz mit einem CircularString, der eine Gerade darstellt  
 Im folgenden Beispiel wird veranschaulicht, wie eine **CircularString** -Instanz erstellt wird, die eine Gerade darstellt:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('CIRCULARSTRING(0 0, 1 2, 2 4)', 0);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)   
 [MakeValid &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [MakeValid &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [STIsValid &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [STIsValid &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)   
 [STLength &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [STPointN &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [STNumPoints &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STIsRing &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)   
 [STIsClosed &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STPointOnSurface &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)  
  
  
