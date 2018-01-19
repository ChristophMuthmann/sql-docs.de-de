---
title: STPointN (Geometry-Datentyp) | Microsoft Docs
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
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fb3933aee8f8880b23bb4883753acb85d83ddb1e
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="stpointn-geometry-data-type"></a>STPointN (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt einen festgelegten Punkt in einer **geometry** -Instanz zurück.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein **int** -Ausdruck zwischen 1 und der Anzahl der Punkte in der **geometry** -Instanz.  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Geometrie**  
  
 CLR-Rückgabetyp: **SqlGeometry**  
  
 Open Geospatial Consortium (OGC)-Typ: **Point**  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine **geometry** -Instanz von einem Benutzer erstellt wurde, gibt `STPointN()` den durch *expression* festgelegten Punkt zurück, indem die Punkte in der Reihenfolge sortiert werden, in der sie ursprünglich eingegeben wurden.  
  
 Wenn eine **geometry** -Instanz systemseitig konstruiert wurde, gibt `STPointN()` den durch *expression* festgelegten Punkt zurück, indem alle Punkte in der Reihenfolge sortiert werden, in der sie ausgegeben würden: erst nach Geometrie, dann nach Ring innerhalb der Geometrie (falls zutreffend) und schließlich nach Punkt innerhalb des Rings. Diese Reihenfolge ist deterministisch.  
  
 Wenn diese Methode mit einem geringeren Wert als 1 aufgerufen wird, löst sie eine **ArgumentOutOfRangeException**aus.  
  
 Wenn diese Methode mit einem Wert aufgerufen wird, der die Anzahl der Punkte in der Instanz übersteigt, gibt sie NULL zurück.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und `STPointN()` verwendet, um den zweiten Punkt in der Beschreibung der Instanz abzurufen.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

