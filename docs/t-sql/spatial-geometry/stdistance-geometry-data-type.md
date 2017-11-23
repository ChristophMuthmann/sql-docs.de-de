---
title: STDistance (Geometry-Datentyp) | Microsoft Docs
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
- STDistance_TSQL
- STDistance (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STDistance (geometry Data Type)
ms.assetid: ac815bc7-5342-4cc4-af40-c80a1c4c8b68
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ab98a6ec1465154a6af27ba29ee41025bedc62b9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stdistance-geometry-data-type"></a>STDistance (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die kürzeste Entfernung zwischen einem Punkt in einer **geometry** -Instanz und einem Punkt in einer anderen **geometry** -Instanz zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STDistance ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geometry*  
 Eine andere **geometry** -Instanz, von der aus die Entfernung zur Instanz, in der `STDistance()` aufgerufen wird, gemessen werden soll. Wenn *other_geometry* eine leere Menge ist, gibt `STDistance()` NULL zurück.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **"float"**  
  
 CLR-Rückgabetyp: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 `STDistance()`immer null zurück, wenn das spatial Reference IDs (SRIDs) auf, der die **Geometrie** -Instanzen nicht übereinstimmen.  
  
## <a name="examples"></a>Beispiele  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 2 0, 2 2, 0 2, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POINT(10 10)', 0);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
