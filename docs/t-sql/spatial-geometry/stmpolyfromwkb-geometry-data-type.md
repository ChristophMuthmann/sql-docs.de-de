---
title: STMPolyFromWKB (Geometry-Datentyp) | Microsoft Docs
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
- STMPolyFromWKB (geometry Data Type)
- STMPolyFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPolyFromWKB (geometry Data Type)
ms.assetid: cac25868-08ef-46fc-9c3d-a15e43794a7a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c36780e823c67469b72cdaebda8e2e877daaee8d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="stmpolyfromwkb-geometry-data-type"></a>STMPolyFromWKB (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **GeometryMultiPolygon** Instanz aus einer Open Geospatial Consortium (OGC) Well-Known Binary (WKB)-Darstellung.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STMPolyFromWKB ( 'WKB_multipolygon' , SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *WKB_multipolygon*  
 Ist die WKB-Darstellung der **GeometryMultiPolygon** Instanz, die Sie zurückgeben möchten. *WKB_multipolygon* ist ein **varbinary(max)** Ausdruck.  
  
 *SRID*  
 Ist ein **Int** Ausdruck darstellt, die räumliche verweisen ID (SRID), der die **GeometryMultiPolygon** Instanz, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
 OGC-Typ: **MultiPolygon**  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STMPolyFromWKB()` zum Erstellen einer `geometry` Instanz:  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPolyFromWKB(0x0106000000020000000103000000010000000400000000000000000014400000000000001440000000000000244000000000000014400000000000002440000000000000244000000000000014400000000000001440010300000001000000050000000000000000002440000000000000244000000000000059400000000000002440000000000000694000000000000069400000000000003E400000000000003E4000000000000024400000000000002440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statische geometry-Methoden des OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

