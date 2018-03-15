---
title: BufferWithCurves (geography-Datentyp) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0978418fe682728d02f7c65b5bff581154ae231c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt eine Instanz von **geography** zurück, die die Menge aller Punkte darstellt, deren Abstand von der aufrufenden Instanz von **geography** kleiner oder gleich dem Wert des *distance*-Parameters ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>Argumente  
 *distance*  
 Ein **float**-Wert, der den maximalen Abstand der Punkte von der geography-Instanz angibt, die den Puffer bilden.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="exceptions"></a>Ausnahmen  
 Die folgenden Kriterien lösen eine **ArgumentException** aus.  
  
-   Es wird kein Parameter an die Methode übergeben, beispielsweise `@g.BufferWithCurves()`  
  
-   Es wird ein nicht numerischer Parameter an die Methode übergeben, beispielsweise `@g.BufferWithCurves('a')`  
  
-   **NULL** wird an die Methode übergeben, beispielsweise `@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Remarks  
 Die folgende Tabelle zeigt die Ergebnisse an, die für verschiedene Entfernungswerte zurückgegeben wurden.  
  
|distance-Wert|Type-Dimensionen|Räumlicher Rückgabetyp|  
|--------------------|---------------------|---------------------------|  
|distance < 0|Null oder eins|Leere Instanz von **GeometryCollection**|  
|distance \< 0|Zwei oder mehr|Eine Instanz von **CurvePolygon** oder **GeometryCollection** mit einem negativen Puffer.<br /><br /> Hinweis: Ein negativer Puffer erstellt möglicherweise eine leere Instanz von **GeometryCollection**.|
|distance = 0|Alle Dimensionen|Kopie der aufrufenden Instanz **geography**|  
|distance > 0|Alle Dimensionen|Instanz von **CurvePolygon** oder **GeometryCollection**|  
  
> [!NOTE]  
>  Da *distance* ein **float**-Wert ist, kann ein sehr kleiner Wert in den Berechnungen mit 0 gleichgesetzt werden.  In diesem Fall wird eine Kopie der aufrufenden Instanz von **geography** zurückgegeben.  
  
 Wenn ein **string**-Parameter an die Methode übergeben wird, erfolgt eine Konvertierung in einen **float**-Wert, oder eine `ArgumentException` wird ausgelöst.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>A. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 für eine eindimensionale geography-Instanz  
 Im folgenden Beispiel wird eine leere Instanz von `GeometryCollection` zurückgegeben:  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>B. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 für eine zweidimensionale geography-Instanz  
 Im folgenden Beispiel wird eine Instanz von `CurvePolygon` mit einem negativen Puffer zurückgegeben:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 zur Rückgabe einer leeren GeometryCollection  
 Im folgenden Beispiel wird gezeigt, was geschieht, wenn der *distance*-Parameter –2 entspricht:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Diese **SELECT**-Anweisung gibt `GEOMETRYCOLLECTION EMPTY` zurück.  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Aufrufen von BufferWithCurves() mit einem Parameterwert = 0  
 Im folgenden Beispiel wird eine Kopie der aufrufenden Instanz von **geography** zurückgegeben:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Aufrufen von BufferWithCurves() mit einem sehr kleinen Parameterwert ungleich 0  
 Im folgenden Beispiel wird ebenfalls eine Kopie der aufrufenden Instanz von **geography** zurückgegeben:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Aufrufen von BufferWithCurves() mit einem Parameterwert > 0  
 Im folgenden Beispiel wird eine Instanz von `CurvePolygon` zurückgegeben:  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>G. Übergeben eines gültigen Zeichenfolgenparameters  
 Im folgenden Beispiel wird die gleiche Instanz von `CurvePolygon` zurückgegeben, die bereits erwähnt wurde, es wird jedoch ein Zeichenfolgenparameter an die Methode übergeben:  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves('2').ToString();
```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. Übergeben eines ungültigen Zeichenfolgenparameters  
 Im folgenden Beispiel wird ein Fehler ausgelöst:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)'  
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 Beachten Sie, dass in den beiden vorangehenden Beispielen ein Zeichenfolgenliteral an die `BufferWithCurves()`-Methode übergeben wurde. Das erste Beispiel kann ordnungsgemäß ausgeführt werden, da das Zeichenfolgenliteral in einen numerischen Wert konvertiert werden kann. Im zweiten Beispiel wird allerdings eine `ArgumentException`ausgelöst.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
