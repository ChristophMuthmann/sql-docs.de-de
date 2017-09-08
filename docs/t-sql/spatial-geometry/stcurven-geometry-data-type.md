---
title: STCurveN (Geometry-Datentyp) | Microsoft Docs
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
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd5b459bfa271d98844d30455e4e1a9e03d0e2cd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stcurven-geometry-data-type"></a>STCurveN (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt die von einer Instanz von **geometry** angegebene Kurve zurück, bei der es sich um eine **LineString**, **CircularString**, **CompoundCurve**oder **MultiLineString**handelt.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>Argumente  
 *curve_index*  
 Ein **int** -Ausdruck zwischen 1 und der Anzahl der Kurven in der **geometry** -Instanz.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="exceptions"></a>Ausnahmen  
 Wenn *Curve_index* < 1 ein `ArgumentOutOfRangeException` ausgelöst wird.  
  
## <a name="remarks"></a>Hinweise  
 **NULL** wird in folgenden Fällen zurückgegeben:  
  
-   Die **geometry** -Instanz ist deklariert, aber nicht instanziiert.  
  
-   Die **geometry** -Instanz ist leer.  
  
-   *curve_index* überschreitet die Anzahl der Kurven in der **geometry** -Instanz.  
  
-   Bei der **geometry** -Instanz handelt es sich um einen **Point**, **MultiPoint**, ein **Polygon**, **CurvePolygon**oder **MultiPolygon**  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>A. Verwenden von STCurveN() in einer CircularString-Instanz  
 Im folgenden Beispiel wird die zweite Kurve in einer Instanz von `CircularString` zurückgegeben:  
  
 `DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 Im weiter oben in diesem Thema angegebenen Beispiel wird Folgendes zurückgegeben:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. Verwenden von STCurveN() in einer CompoundCurve-Instanz mit einer CircularString-Instanz  
 Im folgenden Beispiel wird die zweite Kurve in einer Instanz von `CompoundCurve` zurückgegeben:  
  
 `DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 Im weiter oben in diesem Thema angegebenen Beispiel wird Folgendes zurückgegeben:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. Verwenden von STCurveN() in einer CompoundCurve-Instanz mit drei CircularString-Instanzen  
 Im folgenden Beispiel wird eine Instanz von `CompoundCurve` , die drei separate Instanzen von `CircularString` kombiniert, in der gleichen Kurvensequenz wie im vorherigen Beispiel zurückgegeben:  
  
 `DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';`  
  
 `SELECT @g.STCurveN(2).ToString();`  
  
 Im weiter oben in diesem Thema angegebenen Beispiel wird Folgendes zurückgegeben:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 Die Ergebnisse sind für die vorherigen drei Beispiele gleich. Unabhängig vom WKT (Well-known Text)-Format, das bei der Eingabe der gleichen Kurvensequenz verwendet wird, die von `STCurveN()` zurückgegebenen Ergebnisse sind bei Verwendung einer `CompoundCurve` -Instanz gleich.  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. Überprüfen des Parameters vor Aufruf von STCurveN()  
 Im folgenden Beispiel wird gezeigt, wie die Gültigkeit von `@n` vor dem Aufruf der `STCurveN()`-Methode sichergestellt wird:  
  
 `DECLARE @g geometry;`  
  
 `DECLARE @n int;`  
  
 `SET @n = 3;`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');`  
  
 `IF @n >= 1 AND @n <= @g.STNumCurves()`  
  
 `BEGIN`  
  
 `SELECT @g.STCurveN(@n).ToString();`  
  
 `END`  
  
## <a name="see-also"></a>Siehe auch  
 [STNumCurves &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [OGC-Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


