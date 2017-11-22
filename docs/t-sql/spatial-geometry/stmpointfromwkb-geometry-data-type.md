---
title: STMPointFromWKB (Geometry-Datentyp) | Microsoft Docs
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
- STMPointFromWKB (geometry Data Type)
- STMPointFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STMPointFromWKB (geometry Data Type)
ms.assetid: 01d4117f-01a0-4bc3-8762-7382a1cdbd6c
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 68010590f352feb605aec069ba9237cf86ec901a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stmpointfromwkb-geometry-data-type"></a>STMPointFromWKB (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **GeometryMultiPoint** Instanz aus einer Open Geospatial Consortium (OGC) Well-Known Binary (WKB)-Darstellung.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STMPointFromWKB ( 'WKB_multipoint' , SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *WKB_multipoint*  
 Ist die WKB-Darstellung der **GeometryMultiPoint** Instanz, die Sie zurückgeben möchten. *WKB_multipoint* ist ein **varbinary(max)** Ausdruck.  
  
 *SRID*  
 Ist ein **Int** Ausdruck darstellt, die räumliche verweisen ID (SRID), der die **GeometryMultiPoint** Instanz, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
 OGC-Typ: **MultiPoint**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode löst eine **FormatException** aus, wenn die Eingabe nicht korrekt formatiert ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STMPointFromWKB()` zum Erstellen einer `geometry` Instanz.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPointFromWKB(0x010400000002000000010100000000000000000059400000000000005940010100000000000000000069400000000000006940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statische geometry-Methoden des OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

