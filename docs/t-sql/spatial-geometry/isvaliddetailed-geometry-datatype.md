---
title: IsValidDetailed (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: IsValidDetailed geometry
ms.assetid: 5a31e88a-ad7b-4ef7-b773-e2571f1cb3aa
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55ede35d26ce9f7de1655e076f1aeaad40642218
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="isvaliddetailed-geometry-datatype"></a>IsValidDetailed (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt eine Meldung zurück, die Informationen zur Identifizierung von Problemen mit einem räumlichen Objekt enthält, das nicht gültig ist. Wenn das Objekt nicht gültig ist, wird nur der erste Fehler zurückgegeben. Wenn das Objekt gültig ist, wird der Wert 24400 zurückgegeben.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **nvarchar(max)**  
  
 CLR-Rückgabetyp: **Zeichenfolge**  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Tabelle enthält mögliche Rückgabewerte:  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|24400|Gültig|  
|24401|Ungültig, die Ursache ist unbekannt.|  
|24402|Ungültig, weil der Punkt {0} ein isolierter Punkt ist, der für diesen Objekttyp ungültig ist.|  
|24403|Ungültig, weil sich ein Polygonkantenpaar überlappt.|  
|24404|Ungültig, weil eine Überschneidung des Polygonrings {0} mit sich selbst oder einem anderen Ring vorliegt.|  
|24405|Ungültig, weil eine Überschneidung eines Polygonrings mit sich selbst oder einem anderen Ring vorliegt.|  
|24406|Ungültig, weil die Kurve {0} zu einem Punkt degeneriert wird.|  
|24407|Ungültig, weil auf eine Linie an Punkt \ {1\} {0} Polygon-Ring reduziert.|  
|24408|Ungültig, weil der Polygonring {0} nicht geschlossen ist.|  
|24409|Ungültig, weil sich ein Teil des Polygonrings {0} im Inneren eines Polygons befindet.|  
|24410|Ungültig, weil der Ring {0} der erste Ring in einem Polygon, aber nicht dessen äußerer Ring ist.|  
|24411|Ungültig, weil der Ring {0} außerhalb der äußere Ring \ {1\} des zugehörigen Polygons liegt.|  
|24412|Ungültig, weil das Innere eines Vielecks, das mit Ringe {0} und \ {1\} nicht verbunden ist.|  
|24413|Ungültig aufgrund von zwei überlappenden Kanten in Kurve {0}.|  
|24414|Ist ungültig, da sich eine Kante der Kurve {0} eine Kante der Kurve \ {1\} überschneidet.|  
|24415|Ungültig, weil ein Polygon über eine ungültige Ringstruktur verfügt.|  
|24416|Ungültig, weil in Kurve {0} die Kante, die an Punkt beginnt, \ {1\} eine Linie oder ein degenerierter Bogen mit entgegengesetzten Endpunkten ist.|  
  
## <a name="examples"></a>Beispiele  
 Ein ungültiges räumliches Objekt im folgende Beispiel wird veranschaulicht, wie die **IsValidDetailed()** -Methoden Verhalten.  
  
```sql  
DECLARE @p GEOMETRY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24404: Not valid because polygon ring (1) intersects itself or some other ring.  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

