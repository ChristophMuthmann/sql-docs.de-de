---
title: STTouches (Geometry-Datentyp) | Microsoft Docs
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
- STTouches (geometry Data Type)
- STTouches_TSQL
dev_langs: TSQL
helpviewer_keywords: STTouches (geometry Data Type)
ms.assetid: af3650b4-26da-4600-9cc2-1be71dd76a14
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46f877bba6e70110f34662bf3110dcd7128d468e
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="sttouches-geometry-data-type"></a>STTouches (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt 1 zurück, wenn eine **geometry** -Instanz eine andere **geometry** -Instanz räumlich berührt. Andernfalls wird 0 zurückgegeben.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STTouches ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumente  
 *other_geometry*  
 Eine andere **geometry** -Instanz zum Vergleich mit der Instanz, in der `STTouches()` aufgerufen wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Zwei **geometry** -Instanzen berühren sich, wenn sich ihre Punktmengen, jedoch nicht ihre Innenbereiche überschneiden.  
  
 Diese Methode gibt immer NULL zurück, wenn die SRIDs (Spatial Reference IDs) der **geometry** -Instanzen nicht übereinstimmen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `STTouches()` verwendet, um zwei `geometry` -Instanzen daraufhin zu überprüfen, ob sie sich berühren.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STTouches(@h);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

