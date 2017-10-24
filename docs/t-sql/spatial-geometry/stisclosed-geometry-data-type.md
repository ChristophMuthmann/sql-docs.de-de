---
title: STIsClosed (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STIsClosed_TSQL
- STIsClosed (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed (geometry Data Type)
ms.assetid: 14edbb22-df7b-4b8a-b16c-ac477a5d32c1
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1fca12de9a05ff424532fa488fda7a306b8a9c37
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt 1 zurück, wenn die Start- und Endpunkte von der angegebenen **Geometrie** -Instanz gleich sind. Gibt 1 für **Geometrycollection** Typen, wenn alle enthaltenen **Geometrie** -Instanz geschlossen ist. Gibt 0 zurück, wenn die Instanz nicht geschlossen ist.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STIsClosed ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt 0 zurück, wenn alle Abbildung eine **Geometry** Instanz sind Punkte, oder wenn die Instanz leer ist.  
  
 Alle **Polygon** -Instanzen werden als geschlossen betrachtet.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString`-Instanz erstellt und `STIsClosed()` verwendet, um zu überprüfen, ob die `LineString`-Instanz geschlossen ist.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [OGC-Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  


