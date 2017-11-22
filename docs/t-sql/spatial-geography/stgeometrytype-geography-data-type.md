---
title: STGeometryType (Geography-Datentyp) | Microsoft Docs
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
- STGeometryType (geography Data Type)
- STGeometryType_TSQL
dev_langs: TSQL
helpviewer_keywords: STGeometryType method
ms.assetid: 3e169ead-a98e-44af-8d33-fd59a955cae4
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 814958f4cafd98266529e9ee237aaf3375ea6a4b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stgeometrytype-geography-data-type"></a>STGeometryType (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt zurück, die durch dargestellten Open Geospatial Consortium (OGC)-Typnamen eine **Geography** Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STGeometryType ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **nvarchar(4000)**  
  
 CLR-Rückgabetyp: **SqlString**  
  
## <a name="remarks"></a>Hinweise  
 Die OGC-Typnamen, die von zurückgegeben werden können `STGeometryType()` sind **Punkt**, **LineString**, **CircularString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **GeometryCollection**, **MultiPoint**, **MultiLineString**, und **MultiPolygon**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiels wird eine Instanz von `Polygon` erstellt, und mit `STGeometryType()` wird bestätigt, dass es sich um ein Polygon handelt.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
