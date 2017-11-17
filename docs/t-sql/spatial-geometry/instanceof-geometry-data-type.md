---
title: InstanceOf (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
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
- InstanceOf (geometry Data Type)
ms.assetid: fdea1248-29a4-4bab-a60d-a1b359b5e109
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a7106339cc346cbd49b3cbfc3905ea3a2a941c15
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="instanceof-geometry-data-type"></a>InstanceOf (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Eine Methode, die testet die **Geometrie** Instanz ist identisch mit den angegebenen Typ. Gibt 1 zurück, wenn der Typ des eine **Geometrie** Instanz ist identisch mit den angegebenen Typ, oder wenn der angegebene Typ ein Vorgänger des Instanztyps ist, andernfalls 0.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.InstanceOf (geometry_type )  
```  
  
## <a name="arguments"></a>Argumente  
 *geometry_type*  
 Ist ein **nvarchar(4000)** Zeichenfolge angeben, einen von 15 Typen, die verfügbar gemacht werden, der **Geometrie** Typhierarchie.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Die Eingabe für die Methode muss einen der folgenden sein: **Geometrie**, **Punkt**, **Kurve**, **LineString**,  **CircularString**, **CompoundCurve**, **Oberfläche**, **Polygon**, **CurvePolygon**, **GeometryCollection**, **MultiSurface**, **MultiPolygon**, **MultiCurve**, **MultiLineString**, und **MultiPoint**. Diese Methode löst eine **ArgumentException** anderen Zeichenfolgen für die Eingabe verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `MultiPoint`-Instanz erstellt und `InstanceOf()` verwendet, um zu überprüfen, ob die Instanz eine `GeometryCollection` ist.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


