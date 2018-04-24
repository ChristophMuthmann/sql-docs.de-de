---
title: STCurveN (geometry-Datentyp) | Microsoft-Dokumentation
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
- STCurveN method (geometry)
ms.assetid: 64adf1a1-3a41-41fb-b7d1-44390c3e4ea9
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7248f0ba7ea967dde4bc1f5eb6ddb52dc823ef1e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stcurven-geometry-data-type"></a>STCurveN (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt die von einer Instanz von **geometry** angegebene Kurve zurück, bei der es sich um eine **LineString**, **CircularString**, **CompoundCurve**oder **MultiLineString**handelt.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STCurveN ( curve_index )  
```  
  
## <a name="arguments"></a>Argumente  
 *curve_index*  
 Ein **int** -Ausdruck zwischen 1 und der Anzahl der Kurven in der **geometry** -Instanz.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geometry**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="exceptions"></a>Ausnahmen  
 Wenn *curve_index* < 1 ist, wird der Fehler `ArgumentOutOfRangeException` ausgelöst.  
  
## <a name="remarks"></a>Remarks  
 **NULL** wird in folgenden Fällen zurückgegeben:  
  
-   Die **geometry** -Instanz ist deklariert, aber nicht instanziiert.  
  
-   Die **geometry** -Instanz ist leer.  
  
-   *curve_index* überschreitet die Anzahl der Kurven in der **geometry** -Instanz.  
  
-   Bei der **geometry** -Instanz handelt es sich um einen **Point**, **MultiPoint**, ein **Polygon**, **CurvePolygon**oder **MultiPolygon**  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-stcurven-on-a-circularstring-instance"></a>A. Verwenden von STCurveN() in einer CircularString-Instanz  
 Im folgenden Beispiel wird die zweite Kurve in einer Instanz von `CircularString` zurückgegeben:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Im weiter oben in diesem Thema angegebenen Beispiel wird Folgendes zurückgegeben:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve-instance-with-one-circularstring-instance"></a>B. Verwenden von STCurveN() in einer CompoundCurve-Instanz mit einer CircularString-Instanz  
 Im folgenden Beispiel wird die zweite Kurve in einer Instanz von `CompoundCurve` zurückgegeben:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE(CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Im weiter oben in diesem Thema angegebenen Beispiel wird Folgendes zurückgegeben:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-instance-with-three-circularstring-instances"></a>C. Verwenden von STCurveN() in einer CompoundCurve-Instanz mit drei CircularString-Instanzen  
 Im folgenden Beispiel wird eine Instanz von `CompoundCurve` , die drei separate Instanzen von `CircularString` kombiniert, in der gleichen Kurvensequenz wie im vorherigen Beispiel zurückgegeben:  
  
```
 DECLARE @g geometry = 'COMPOUNDCURVE (CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246), CIRCULARSTRING(3 6.3246, 0 7, -3 6.3246), CIRCULARSTRING(-3 6.3246, -1 2.1082, 0 0))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Im weiter oben in diesem Thema angegebenen Beispiel wird Folgendes zurückgegeben:  
  
 `CIRCULARSTRING (3 6.3246, 0 7, -3 6.3246)`  
  
 Die Ergebnisse sind für die vorherigen drei Beispiele gleich. Unabhängig vom WKT (Well-known Text)-Format, das bei der Eingabe der gleichen Kurvensequenz verwendet wird, die von `STCurveN()` zurückgegebenen Ergebnisse sind bei Verwendung einer `CompoundCurve` -Instanz gleich.  
  
### <a name="d-validating-the-parameter-before-calling-stcurven"></a>D. Überprüfen des Parameters vor Aufruf von STCurveN()  
 Im folgenden Beispiel wird gezeigt, wie die Gültigkeit von `@n` vor dem Aufruf der `STCurveN()`-Methode sichergestellt wird:  
  
```
 DECLARE @g geometry;  
 DECLARE @n int;  
 SET @n = 3;  
 SET @g = geometry::Parse('CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
 ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [STNumCurves &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

