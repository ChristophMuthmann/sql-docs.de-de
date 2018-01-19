---
title: STIsRing (Geometry-Datentyp) | Microsoft Docs
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
- STIsRing_TSQL
- STIsRing (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STIsRing (geometry Data Type)
ms.assetid: ea0063be-1c74-4cc4-ac6f-b65321ddfa54
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 47f7878070d87c6d35db0cdec57cab6f326ea8be
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="stisring-geometry-data-type"></a>STIsRing (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt 1 zurück, wenn eine **geometry** -Instanz die folgenden Anforderungen erfüllt:
-   Sie ist eine **LineString** -Instanz.  
-   Sie ist geschlossen.  
-   Sie ist einfach.  
-   Gibt 0 zurück, wenn die **LineString** -Instanz die Anforderungen nicht erfüllt.  

 Für eine **Geometrie** Instanz geschlossen und einfach ist, werden beide [STIsClosed()](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md) und [STIsSimple()](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md) muss 1 zurückgeben, wenn für die Instanz aufgerufen. Um zu bestimmen, den Instanztyp einer **Geometrie**, verwenden Sie [STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STIsRing ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt NULL zurück, wenn die Instanz kein **LineString**ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und `STIsRing()` verwendet, um zu überprüfen, ob die Instanz ein Ring ist.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0, 0 0)', 0);  
SELECT @g.STIsRing();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [STIsClosed &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STGeometryType &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [STIsSimple &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)   
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

