---
title: STIsValid (Geometry-Datentyp) | Microsoft Docs
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
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 436cab211eceff9eb286b4e44e90aa3f64b9d03c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt true zurück, wenn eine **geometry** -Instanz basierend auf ihrem Open Geospatial-Konsortium (OGC)-Typ wohlgeformt ist. Gibt false zurück, wenn eine **geometry** -Instanz nicht wohlgeformt ist.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Die OGC-Typ, der eine **Geometrie** Instanz kann bestimmt werden, durch den Aufruf [STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erzeugt nur gültige **Geometrie** Instanzen, erlaubt aber für die Speicherung und Abruf Ungültiger Instanzen. Eine gültige Instanz, die die gleiche Punktmenge wie eine ungültige Instanz darstellt, kann mithilfe der `MakeValid()` -Methode abgerufen werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `geometry` -Instanz erstellt und `STIsValid()` verwendet, um zu überprüfen, ob die Instanz gültig ist.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [STGeometryType &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [OGC-Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

