---
title: BufferWithCurves (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/11/2017
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
- BufferWithCurves
- BufferWithCurves_TSQL
dev_langs: TSQL
helpviewer_keywords: BufferWithCurves method (geography)
ms.assetid: abf0a11c-c99c-4faa-bf80-3ae8e04d7bfb
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0978418fe682728d02f7c65b5bff581154ae231c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="bufferwithcurves-geography-data-type"></a>BufferWithCurves (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt eine **Geography** -Instanz, die für die Menge aller Punkte, deren Abstand von der aufrufenden **Geography** Instanz ist kleiner als oder gleich der *Abstand* Parameter.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.BufferWithCurves ( distance )  
```  
  
## <a name="arguments"></a>Argumente  
 *distance*  
 Ist eine **"float"** aus der Geography-Instanz werden kann, der angibt, der maximalen Abstands der Punkte, den Puffer bilden.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="exceptions"></a>Ausnahmen  
 Die folgenden Kriterien lösen eine **ArgumentException**.  
  
-   Es wird kein Parameter an die Methode übergeben, beispielsweise `@g.BufferWithCurves()`  
  
-   Es wird ein nicht numerischer Parameter an die Methode übergeben, beispielsweise `@g.BufferWithCurves('a')`  
  
-   **NULL** wie z. B. an die Methode übergeben wird`@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Tabelle zeigt die Ergebnisse an, die für verschiedene Entfernungswerte zurückgegeben wurden.  
  
|distance-Wert|Type-Dimensionen|Räumlicher Rückgabetyp|  
|--------------------|---------------------|---------------------------|  
|distance < 0|NULL oder eins|Leere Instanz von **GeometryCollection**|  
|Abstand \< 0|Zwei oder mehr|Ein **CurvePolygon** oder **GeometryCollection** Instanz mit einem negativen Puffer.<br /><br /> Hinweis: Ein negativer Puffer erstellt möglicherweise eine leere **GeometryCollection**|
|distance = 0|Alle Dimensionen|Kopie der aufrufenden **Geography** Instanz|  
|distance > 0|Alle Dimensionen|**CurvePolygon** oder **GeometryCollection** Instanz|  
  
> [!NOTE]  
>  Da *Abstand* ist ein **"float"**, ein sehr kleiner Wert kann sich in den Berechnungen mit 0 gleichgesetzt.  Wenn dies geschieht, klicken Sie dann eine Kopie der aufrufenden **Geography** Instanz zurückgegeben.  
  
 Wenn eine **Zeichenfolge** Parameter an die Methode übergeben wird, dann erfolgt eine Konvertierung zu einem **"float"** oder löst eine `ArgumentException`.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geography-instance"></a>A. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 für eine eindimensionale geography-Instanz  
 Im folgenden Beispiel wird eine leere Instanz von `GeometryCollection` zurückgegeben:  
  
 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(-1).ToString();
``` 
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geography-instance"></a>B. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 für eine zweidimensionale geography-Instanz  
 Das folgende Beispiel gibt eine `CurvePolygon` Instanz mit einem negativen Puffer:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Aufrufen von BufferWithCurves() mit einem Parameterwert < 0 zur Rückgabe einer leeren GeometryCollection  
 Das folgende Beispiel zeigt, was geschieht, wenn die *Abstand* Parameter-2 entspricht:  
  
 ```sql
 DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Dies **wählen** -Anweisung zurückgibt`GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Aufrufen von BufferWithCurves() mit einem Parameterwert = 0  
 Das folgende Beispiel gibt eine Kopie der aufrufenden **Geography** Instanz:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Aufrufen von BufferWithCurves() mit einem sehr kleinen Parameterwert ungleich 0  
 Das folgende Beispiel gibt auch eine Kopie der aufrufenden **Geography** Instanz:  

 ```sql
 DECLARE @g geography = 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @distance float = 1e-20;  
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Aufrufen von BufferWithCurves() mit einem Parameterwert > 0  
 Das folgende Beispiel gibt eine `CurvePolygon` Instanz:  

 ```sql
 DECLARE @g geography= 'LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
### <a name="g-passing-a-valid-string-parameter"></a>G. Übergeben eines gültigen Zeichenfolgenparameters  
 Im folgende Beispiel gibt denselben Wert zurück `CurvePolygon` Instanz fest, wie bereits erwähnt, jedoch ein Zeichenfolgenparameter an die Methode übergeben wird:  

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
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [BufferWithCurves &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/bufferwithcurves-geometry-data-type.md)  
  
  
