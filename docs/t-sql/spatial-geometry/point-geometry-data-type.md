---
title: Point (Geometry-Datentyp) | Microsoft Docs
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
- Point
- Point_TSQL
dev_langs: TSQL
helpviewer_keywords: Point (geometry Data Type)
ms.assetid: 7a2e593a-4d4c-4214-b0c5-02d1ac46bc66
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2632d18c1073ebda8b6aef9fac862b63b3f03405
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="point-geometry-data-type"></a>Point (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Erstellt eine **geometry** -Instanz, die mit ihren X- und Y-Werten sowie dem SRID (Spatial Reference ID) eine **Point** -Instanz darstellt.
  
## <a name="syntax"></a>Syntax  
  
```  
  
Point ( X, Y, SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *X*  
 Ein **float** -Ausdruck, der die X-Koordinate der zu erstellenden **Point** -Instanz angibt.  
  
 *J*  
 Ein **float** -Ausdruck, der die Y-Koordinate der zu erstellenden **Point** -Instanz angibt.  
  
 *SRID*  
 Ein **int** -Ausdruck, der die SRID (Spatial Reference ID) der **geometry** -Instanz darstellt, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `Point()` verwendet, um eine `geometry` -Instanz zu erstellen.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Point(1, 10, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte statische geometry-Methoden](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

