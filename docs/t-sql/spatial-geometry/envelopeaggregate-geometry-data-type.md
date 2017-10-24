---
title: EnvelopeAggregate (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geometry)
ms.assetid: c4c15abe-0fe9-441d-9d42-6572e264869c
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f6bf9a42f6d41973f2abed3377c5a311271e106f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="envelopeaggregate-geometry-data-type"></a>EnvelopeAggregate (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt für einen angegebenen Satz von **geometry** -Objekten einen Begrenzungsrahmen zurück.
  
## <a name="syntax"></a>Syntax  
  
```  
  
EnvelopeAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Argumente  
 *geometry_operand*  
 Eine Tabellenspalte vom Typ **geometry** , die den Satz von **geometry** -Objekten darstellt.  
  
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
 Im folgenden Beispiel wird ein Begrenzungsrahmen für einen Satz von Objekten in der Variablenspalte einer Tabelle zurückgegeben.  
  
 ```
 -- Setup table variable for EnvelopeAggregate example 
DECLARE @Geom TABLE 
( 
shape geometry, 
shapeType nvarchar(50) 
) 
INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'), 
('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle'); 
-- Perform EnvelopeAggregate on @Geom.shape column 
SELECT geometry::EnvelopeAggregate(shape).ToString() 
FROM @Geom;
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte statische Geometry-Methoden](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


