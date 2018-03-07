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
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1178b0287c167666216b090a87c6c9dd645622f7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
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
  
  
