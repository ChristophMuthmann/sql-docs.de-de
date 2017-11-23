---
title: IsValidDetailed (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- IsValidDetailed_TSQL
- IsValidDetailed
dev_langs: TSQL
helpviewer_keywords: IsValidDetailed geography
ms.assetid: f5f0b753-c825-43ce-987d-98655d8d8702
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be983f785ef54523f27366d73e329b3b0517e9b3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="isvaliddetailed-geography-data-type"></a>IsValidDetailed (geography-Datentyp)
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
  
```tsql  
DECLARE @p GEOGRAPHY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24409: Not valid because some portion of polygon ring (1) lies in the interior of a polygon.  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
