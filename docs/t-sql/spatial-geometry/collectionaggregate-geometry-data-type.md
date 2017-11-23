---
title: CollectionAggregate (Geometry-Datentyp) | Microsoft Docs
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
dev_langs: TSQL
helpviewer_keywords: CollectionAggregate method (geometry)
ms.assetid: b7c85d59-c841-4b7f-9d46-8b4b7f2a3afe
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44f6131f572c509c43fd671dee7f0331e73fb441
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="collectionaggregate-geometry-data-type"></a>CollectionAggregate (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Erstellt eine **GeometryCollection** -Instanz aus einem Satz von **geometry** -Typen.
  
## <a name="syntax"></a>Syntax  
  
```  
  
CollectionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Argumente  
 *geometry_operand*  
 Eine Tabellenspalte vom Typ **geometry** , die einen Satz von **geometry** -Objekten darstellt, die in der **GeometryCollection** -Instanz aufgelistet werden sollen.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
## <a name="exceptions"></a>Ausnahmen  
 Löst eine `FormatException` aus, wenn ungültige Eingabewerte vorhanden sind. Finden Sie unter [STIsValid &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt **null** zurück, wenn die Eingabe leer ist oder andere SRIDs aufweist. Finden Sie unter [Spatial Reference Identifiers &#40; SRIDs &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 Diese Methode ignoriert **null** -Eingaben.  
  
> [!NOTE]  
>  Diese Methode gibt **null** zurück, wenn alle eingegebenen Werte **null**sind.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `GeometryCollection` -Instanz mit einem `CurvePolygon` und einem `Polygon`zurückgegeben.  
  
 ```
 -- Setup table variable for CollectionAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform CollectionAggregate on @Geom.shape column  
 SELECT geometry::CollectionAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte statische geometry-Methoden](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

