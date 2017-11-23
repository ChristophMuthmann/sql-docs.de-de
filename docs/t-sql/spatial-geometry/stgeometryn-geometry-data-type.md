---
title: STGeometryN (Geometry-Datentyp) | Microsoft Docs
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
- STGeometryN_TSQL
- STGeometryN (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STGeometryN (geometry Data Type)
ms.assetid: 348c7047-3442-4590-8879-fe841e79058c
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69f43fb4bb718c62426adf155d45711fcab20906
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stgeometryn-geometry-data-type"></a>STGeometryN (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die angegebene Geometry-Instanz in eine **geometrieauflistung**.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STGeometryN ( expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein **Int** -Ausdruck zwischen 1 und die Anzahl der **Geometrie** -Instanzen lautet in der **Geometrycollection**.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt **null** ist der Parameter größer als das Ergebnis der `STNumGeometries()` und löst eine **ArgumentOutOfRangeException** Wenn die *Ausdruck* -Parameter ist kleiner als 1.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt eine `MultiPoint``geometry collection` und verwendet `STGeometryN()` finden Sie die zweite `geometry` Instanz der Sammlung.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

