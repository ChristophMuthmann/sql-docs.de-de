---
title: STIsSimple (Geometry-Datentyp) | Microsoft Docs
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
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 52c407fb89544ef7857ffd5ac3dae00a9c4e233c
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="stissimple-geometry-data-type"></a>STIsSimple (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt 1 zurück, wenn eine **geometry** -Instanz nach der Definition des Open Geospatial Consortium (OGC) einfach ist. Gibt 0 zurück, wenn eine **geometry** -Instanz nicht einfach ist.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STIsSimple ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Um als einfach zu gelten, muss eine **geometry** -Instanz alle nachfolgenden Anforderungen erfüllen:  
  
-   Keine Abbildung der Instanz darf sich selbst außer an den Endpunkten schneiden.  
  
-   Keine zwei Abbildungen einer Instanz dürfen sich an einem Punkt schneiden, der nicht auf den Umrisslinien dieser beiden Abbildungen liegt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine nicht einfache `LineString` -Instanz erstellt, die sich selbst schneidet. Anschließend wird `STIsSimple()` verwendet, um zu überprüfen, ob die `LineString` -Instanz einfach ist.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

