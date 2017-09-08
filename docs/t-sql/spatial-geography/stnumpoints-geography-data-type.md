---
title: STNumPoints (Geography-Datentyp) | Microsoft Docs
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
- STNumPoints (geography Data Type)
- STNumPoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints method
ms.assetid: 25ff7ad1-ba5f-4cfb-816a-59255ac1591d
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 803e631cb1e0250ebedd28a97afe4e20476396cf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Gesamtzahl von Punkten aller Abbildungen in einer **geography** -Instanz zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Int**  
  
 CLR-Rückgabetyp: **SqlInt32**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode zählt die Punkte in der Beschreibung einer **geography** -Instanz. Doppelte Punkte werden gezählt, verbundene Punkte zwischen Segmenten allerdings nur einmal. Wenn diese Instanz eine Auflistung ist, gibt diese Methode die Gesamtzahl der Punkte in der Auflistung zurück.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-retrieving-the-total-number-of-points-in-a-linestring"></a>A. Abrufen der Gesamtzahl der Punkte in einem LineString  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und `STNumPoints()` verwendet, um festzustellen, wie viele Punkte in der Beschreibung der Instanz verwendet wurden.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STNumPoints();  
```  
  
### <a name="b-retrieving-the-total-number-of-points-in-a-geometrycollection"></a>B. Abrufen der Gesamtzahl der Punkte in einer GeometryCollection  
 Im folgenden Beispiel wird eine Summe der Punkte für alle Elemente in der `GeometryCollection`zurückgegeben.  
  
```  
DECLARE @g geography = 'GEOMETRYCOLLECTION(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)  
    ,CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.STNumPoints();  
```  
  
### <a name="c-returning-the-number-of-points-in-a-compoundcurve"></a>C. Zurückgeben der Anzahl der Punkte in einer CompoundCurve  
 Im folgenden Beispiel wird die Anzahl der Punkte in einer CompoundCurve-Instanz zurückgegeben. Die Abfrage gibt 5 statt 6 zurück, da der verbundene Punkt zwischen den Segmenten von STNumPoints() nur einmal gezählt wird.  
  
 `DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658),( -122.348 47.658, -121.56 48.12, -122.358 47.653))'`  
  
 `SELECT @g.STNumPoints();`  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für Geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
