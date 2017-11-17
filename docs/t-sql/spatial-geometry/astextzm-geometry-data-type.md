---
title: AsTextZM (Geometry-Datentyp) | Microsoft Docs
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
- AsTextZM_TSQL
- AsTextZM
- AsTextZM (geometry Data Type)
- AsTextZM_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM (geometry Data Type)
ms.assetid: 08ac8aa0-aff7-4b22-87e0-1a1d55dcbc04
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 91f77bd684d79bbef2530307aa65fc0d92b91c5e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="astextzm-geometry-data-type"></a>AsTextZM (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die Open Geospatial Consortium (OGC) Well-Known Text (WKT)-Darstellung einer Geometry-Instanz alle getragenen **Z** (Höhe) und **M** (Measure)-Werte, die von der Instanz getragen werden.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **nvarchar(max)**  
  
 CLR-Rückgabetyp: **SqlChars**  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `Point` -Instanz mit dem Wert **Z** (Höhe)- und **M** (Measure) erstellt. `STAsText()`Wählt die WKT-Werte (1, 2). `AsTextZM()` wählt identische WKT-Werte und gibt auch die Werte für **Z** und **M**, und gibt (1, 2, 3, 4).  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Übe &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  


