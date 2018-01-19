---
title: STGeomCollFromText (Geometry-Datentyp) | Microsoft Docs
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
- STGeomCollFromText_TSQL
- STGeomCollFromText (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STGeomCollFromText (geometry Data Type)
ms.assetid: 19e757b3-cb2e-4852-87b9-40a815ab707e
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18232e3995a555e46f4556b576351c766aa163e8
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="stgeomcollfromtext-geometry-data-type"></a>STGeomCollFromText (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt eine **geometry** -Instanz aus einer Darstellung des Typs Open Geospatial Consortium (OGC) Well-Known Text (WKT) zurück, die um alle von der Instanz getragenen Z (Höhe)- und M (Measure)-Werte erweitert wurde.
  
## <a name="syntax"></a>Syntax  
  
```  
  
STGeomCollFromText ( 'geometrycollection_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumente  
 *geometrycollection_tagged_text*  
 Die WKT-Darstellung der Instanz von **geometry** , die zurückgegeben werden soll. *geometry_tagged_text* ist ein **nvarchar(max)** -Ausdruck.  
  
 *SRID*  
 Ein **int** -Ausdruck, der die SRID (Spatial Reference ID) der **geometry** -Instanz darstellt, die Sie zurückgeben möchten.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
 Der OGC-Typ der **geometry** -Instanz, die von `STGeomCollFromText()` zurückgegeben wird, wird auf die entsprechende WKT-Eingabe festgelegt.  
  
 Diese Methode löst eine Ausnahme aus, wenn die Eingabe nicht gültig ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STGeomCollFromText()` verwendet, um eine geometry-Instanz zu erstellen.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION ( POLYGON((5 5, 10 5, 10 10, 5 5)), POINT(10 10) )', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statische geometry-Methoden des OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

