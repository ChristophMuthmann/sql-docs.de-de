---
title: STCurveN (geography-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff45e4e7b678df70d67c7d53a4640c3fea382d59
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stcurven-geography-data-type"></a>STCurveN (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Kurve zurück, die von einer Instanz von **geography** angegeben wurde und eine **LineString**, **CircularString**oder **CompoundCurve**ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>Argumente  
 *n*  
 Ein **int** -Ausdruck zwischen 1 und der Anzahl der Kurven in der **geography** -Instanz.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="exceptions"></a>Ausnahmen  
 **ArgumentOutOfRangeException** wird ausgelöst, wenn n < 1 ist.  
  
## <a name="remarks"></a>Remarks  
 **NULL** wird zurückgegeben, wenn die folgenden Kriterien erfüllt sind.  
  
-   Die **geography** -Instanz wird deklariert, aber nicht instanziiert  
  
-   Die **geography** -Instanz ist leer.  
  
-   n überschreitet die Anzahl der Kurven in der **geography**-Instanz (siehe [STNumCurves &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md))  
  
-   Die Dimension für die **geography**-Instanz entspricht nicht gleich (siehe [STDimension &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. Verwenden von STCurveN() für einen CircularString  
 Im folgenden Beispiel wird die zweite Kurve in einer Instanz von **CircularString** zurückgegeben:  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Die Rückgabe des Beispiels lautet wie folgt.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. Verwenden von STCurveN() für eine CompoundCurve  
 Im folgenden Beispiel wird die zweite Kurve in einer Instanz von **CompoundCurve** zurückgegeben:  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Die Rückgabe des Beispiels lautet wie folgt.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. Verwenden von STCurveN() für eine CompoundCurve mit drei CircularStrings  
 Im folgenden Beispiel wird eine Instanz von **CompoundCurve** , die drei separate Instanzen von **CircularString** kombiniert, in der gleichen Kurvensequenz wie im vorherigen Beispiel zurückgegeben:  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 Die Rückgabe des Beispiels lautet wie folgt.  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()` gibt unabhängig vom verwendeten WKT-Format (Well-Known Text) die gleichen Ergebnisse zurück.  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. Testen auf Gültigkeit vor dem Aufrufen von STCurve()  
 Im folgenden Beispiel wird gezeigt, wie Sie sicherstellen, dass *n* gültig ist, bevor Sie die Methode STCurve() aufrufen:  
  
```
 DECLARE @g geography;  
 DECLARE @n int;  
 SET @n = 2;  
 SET @g = geography::Parse('LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
  ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
