---
title: STAsBinary (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- STAsBinary_TSQL
- STAsBinary (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STAsBinary (geometry Data Type)
ms.assetid: 65353777-e3e6-461c-9504-ea4d83312692
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5da53f9a5c9c0262e2d12cae36de477d1e51b391
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stasbinary-geometry-data-type"></a>STAsBinary (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Open Geospatial Consortium (OGC) Well-Known Binary (WKB)-Darstellung einer geometry-Instanz zurück.  
 
## <a name="syntax"></a>Syntax  
  
```  
  
.STAsBinary ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **varbinary(max)**  
  
 CLR-Rückgabetyp: **SqlBytes**  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString` -geometry-Instanz von (0,0) bis (2,3) aus Text erstellt. `STAsBinary()` gibt das Ergebnis in WKB zurück.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
