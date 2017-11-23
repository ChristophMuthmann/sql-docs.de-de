---
title: InstanceOf (Geography-Datentyp) | Microsoft Docs
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
- InstanceOf
- InstanceOf_TSQL
dev_langs: TSQL
helpviewer_keywords: InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa35fb390b51699d4291a51efaea373129273365
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="instanceof-geography-data-type"></a>InstanceOf (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Testet, ob die **Geography** Instanz ist identisch mit den angegebenen Typ.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.InstanceOf ( 'geography_type')  
```  
  
## <a name="arguments"></a>Argumente  
 *geography_type*  
 Ist ein **nvarchar(4000)** Zeichenfolge, die Angabe einer 16 Datentypen, die verfügbar gemacht werden, der **Geography** Typhierarchie.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Gibt 1 zurück, wenn der Typ des eine **Geography** Instanz ist identisch mit den angegebenen Typ, oder wenn der angegebene Typ ein Vorgänger des Instanztyps ist, andernfalls 0.  
  
 Diese **geography** -Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
 Die Eingabe für die Methode muss einen der folgenden sein: Geometry, Punkt, Curve, LineString, CircularString, Surface, Polygon, CurvePolygon, **GeometryCollection**, **MultiSurface**,  **MultiPolygon, MultiCurve, MultiLineString**, **MultiPoint**, oder **FullGlobe**.  
  
 Diese Methode löst eine `ArgumentException` aus, wenn andere Zeichenfolgen als die genannten für die Eingabe verwendet werden.  
  
 Diese Methode ist nicht exakt.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt eine `MultiPoint` -Instanz `InstanceOf()` um festzustellen, ob die Instanz ist eine `GeometryCollection`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
