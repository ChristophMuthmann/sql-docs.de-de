---
title: STSrid (Geometry-Datentyp) | Microsoft Docs
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
f1_keywords:
- STSrid (geometry Data Type)
- STSrid_TSQL
dev_langs: TSQL
helpviewer_keywords: STSrid (geometry Data Type)
ms.assetid: 5e0de983-a0fe-48b7-9e08-30588d7271e2
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70780c6378940904345853e21a022e92e5598c20
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stsrid-geometry-data-type"></a>STSrid (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid** ist eine ganze Zahl, die die SRID (Spatial Reference Identifier) der Instanz darstellt.  
  
Diese Eigenschaft kann geändert werden.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STSrid  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Typ: **Int**  
  
 CLR-Typ: **SqlInt32**  
  
## <a name="examples"></a>Beispiele  
 Im ersten Beispiel wird eine **geometry** -Instanz mit dem SRID-Wert 13 erstellt und `STSrid` verwendet, um die SRID zu bestätigen.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 13);  
SELECT @g.STSrid;  
```  
  
 Im zweiten Beispiel wird `STSrid` verwendet, um die SRID-Wert der Instanz auf 23 zu ändern und dann den geänderten SRID-Wert zu bestätigen.  
  
```  
SET @g.STSrid = 23;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [STX &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

