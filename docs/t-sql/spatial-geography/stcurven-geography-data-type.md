---
title: STCurveN (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d33b8e6752ac8aca3bc6846a4558af4830373081
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stcurven-geography-data-type"></a>STCurveN (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Kurve zurück, die von einer Instanz von **geography** angegeben wurde und eine **LineString**, **CircularString**oder **CompoundCurve**ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STCurveN( n )  
```  
  
## <a name="arguments"></a>Argumente  
 *n*  
 Ein **int** -Ausdruck zwischen 1 und der Anzahl der Kurven in der **geography** -Instanz.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geography**  
  
 CLR-Rückgabetyp: **SqlGeography**  
  
## <a name="exceptions"></a>Ausnahmen  
 Wenn n < 1 ein **ArgumentOutOfRangeException** ausgelöst wird.  
  
## <a name="remarks"></a>Hinweise  
 **NULL** wird zurückgegeben, wenn die folgenden Kriterien erfüllt sind.  
  
-   Die **geography** -Instanz wird deklariert, aber nicht instanziiert  
  
-   Die **geography** -Instanz ist leer.  
  
-   n überschreitet die Anzahl der Kurven in der **Geography** Instanz (siehe [STNumCurves &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)  
  
-   Die Dimension für die **Geography** Instanz entspricht nicht (finden Sie unter [STDimension &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
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
  
 `STCurveN()`Gibt die gleichen Ergebnisse unabhängig vom Format (WELL-Known Text), das verwendet wird.  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. Testen auf Gültigkeit vor dem Aufrufen von STCurve()  
 Im folgende Beispiel wird gezeigt, wie Sie sicher, dass  *n*  gültig ist, bevor Sie die Methode von STCurveN() aufrufen:  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für Geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
