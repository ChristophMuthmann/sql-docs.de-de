---
title: BufferWithCurves (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d248c248d4b5d9b4a4e90954e01f15841d305319
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Gibt eine **Geometrie** -Instanz, die für die Menge aller Punkte, deren Abstand von der aufrufenden **Geometrie** Instanz ist kleiner als oder gleich der *Abstand* Parameter.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>Argumente  
 *distance*  
 Ist eine **"float"** , der angibt, der maximalen Abstands der Punkte, den Puffer bilden kann einen Wert von der **Geometrie** Instanz.  
  
## <a name="return-types"></a>Rückgabetypen  
SQL Server-Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="exceptions"></a>Ausnahmen  
 Die folgenden Kriterien lösen eine **ArgumentException**.  
  
-   Kein Parameter ist an die Methode, wie z. B. übergeben.`@g.BufferWithCurves()`  
  
-   Ein nicht numerische Parameter wird an die Methode, wie z. B. übergeben.`@g.BufferWithCurves('a')`  
  
-   **NULL** wie z. B. an die Methode übergeben wird`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Abbildung zeigt ein Beispiel für eine geometry-Instanz an, die von dieser Methode zurückgegeben wurde.  
  
 ![BufferedCurve](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 Die folgende Tabelle zeigt die Ergebnisse an, die für verschiedene Entfernungswerte zurückgegeben wurden.  
  
|distance-Wert|Type-Dimensionen|Räumlicher Rückgabetyp|  
|--------------------|---------------------|---------------------------|  
|distance < 0|NULL oder eins|Leere Instanz von **GeometryCollection**|  
|distance < 0|Zwei oder mehr|Ein **CurvePolygon** oder **GeometryCollection** Instanz mit einem negativen Puffer. **Hinweis:** ein negativer Puffer erstellt möglicherweise eine leere **GeometryCollection**|  
|distance = 0|Alle Dimensionen|Kopie der aufrufenden **Geometrie** Instanz|  
|distance > 0|Alle Dimensionen|**CurvePolygon** oder **GeometryCollection** Instanz|  
  
> [!NOTE]  
>  Da *Abstand* ist ein **"float"**, ein sehr kleiner Wert kann sich in den Berechnungen mit 0 gleichgesetzt. Wenn dies geschieht dann eine Kopie der aufrufenden **Geometrie** Instanz zurückgegeben. Finden Sie unter [Float und Real &#40; Transact-SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Ein negativer Puffer entfernt alle Punkte innerhalb des angegebenen Abstands der Begrenzung der Geometry-Instanz. In der folgenden Abbildung wird ein negativer Puffer als heller schattierter Bereich des Kreises angezeigt. Die gepunktete Linie ist die Grenze des ursprünglichen Polygons, und die durchgezogenen Linie ist die Grenze des resultierenden Polygons.  
  
 Wenn eine **Zeichenfolge** Parameter an die Methode übergeben wird, dann erfolgt eine Konvertierung zu einem **"float"** oder löst eine `ArgumentException`.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geometry-instance"></a>A. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 für eine eindimensionale geometry-Instanz  
 Im folgenden Beispiel wird eine leere Instanz von `GeometryCollection` zurückgegeben:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(-1).ToString(); 
 ```
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geometry-instance"></a>B. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 für eine zweidimensionale geometry-Instanz  
 Das folgende Beispiel gibt eine `CurvePolygon` Instanz mit einem negativen Puffer:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 zur Rückgabe einer leeren GeometryCollection  
 Das folgende Beispiel zeigt, was geschieht, wenn die *Abstand* Parameter-2 entspricht:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Dies **wählen** -Anweisung zurückgibt`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Aufrufen von BufferWithCurves() mit einem Parameterwert = 0  
 Das folgende Beispiel gibt eine Kopie der aufrufenden **Geometrie** Instanz:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Aufrufen von BufferWithCurves() mit einem sehr kleinen Parameterwert ungleich 0  
 Das folgende Beispiel gibt auch eine Kopie der aufrufenden **Geometrie** Instanz:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 DECLARE @distance float = 1e-20; 
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Aufrufen von BufferWithCurves() mit einem Parameterwert > 0  
 Das folgende Beispiel gibt eine `CurvePolygon` Instanz:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
  
### <a name="g-passing-a-valid-string-parameter"></a>G. Übergeben eines gültigen Zeichenfolgenparameters  
 Im folgende Beispiel gibt denselben Wert zurück `CurvePolygon` Instanz fest, wie bereits erwähnt, jedoch ein Zeichenfolgenparameter an die Methode übergeben wird:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves('2').ToString();
 ```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. Übergeben eines ungültigen Zeichenfolgenparameters  
 Im folgenden Beispiel wird ein Fehler ausgelöst:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)' 
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 Beachten Sie, dass in den beiden vorangehenden Beispielen ein Zeichenfolgenliteral an die `BufferWithCurves()`-Methode übergeben wurde. Das erste Beispiel kann ordnungsgemäß ausgeführt werden, da das Zeichenfolgenliteral in einen numerischen Wert konvertiert werden kann. Im zweiten Beispiel wird allerdings eine `ArgumentException`ausgelöst.  
  
### <a name="i-calling-bufferwithcurves-on-multipoint-instance"></a>I. Aufrufen von BufferWithCurves() für eine MultiPoint-Instanz  
 Im folgenden Beispiel werden zwei Instanzen von `GeometryCollection` sowie eine Instanz von `CurvePolygon` zurückgegeben:  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.BufferWithCurves(1).ToString(); 
 SELECT @g.BufferWithCurves(1.5).ToString(); 
 SELECT @g.BufferWithCurves(1.6).ToString();
 ```  
  
 Die ersten beiden **wählen** Anweisungen zurückzugeben eine `GeometryCollection` Instanz, da der Parameter *Abstand* ist kleiner als oder gleich 1/2-der Abstand zwischen den beiden Punkte (1 1) und (1 4). Das dritte **wählen** Anweisung gibt eine `CurvePolygon` Instanz, da die zwischengespeicherten Instanzen der beiden Punkte (1 1) und (1 4) überschneiden.  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 
