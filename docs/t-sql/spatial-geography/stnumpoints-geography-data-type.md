---
title: STNumPoints (geography-Datentyp) | Microsoft-Dokumentation
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
- STNumPoints (geography Data Type)
- STNumPoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints method
ms.assetid: 25ff7ad1-ba5f-4cfb-816a-59255ac1591d
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4b26ee90a53bf5331761ff6fc3d15bdfd52d561
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Gesamtzahl von Punkten aller Abbildungen in einer **geography** -Instanz zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rückgabetyp: **int**  
  
 CLR-Rückgabetyp: **SqlInt32**  
  
## <a name="remarks"></a>Remarks  
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
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658),( -122.348 47.658, -121.56 48.12, -122.358 47.653))'  
 SELECT @g.STNumPoints();
 ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
