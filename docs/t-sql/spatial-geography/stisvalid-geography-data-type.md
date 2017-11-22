---
title: STIsValid (Geography-Datentyp) | Microsoft Docs
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
dev_langs: TSQL
helpviewer_keywords: STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 035a7edb3f17ac40a19e427d1e80844fbf9e221c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stisvalid-geography-data-type"></a>STIsValid (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt true zurück, wenn eine **geography** -Instanz wohlgeformt ist und anhand des Open Geospatial Consortium (OGC)-Typs als gültiges geography-Objekt erkannt wird. Gibt false zurück, wenn eine **geography** -Instanz nicht wohlgeformt ist. Diese Methode ist exakt.  
  
 Diese geography-Datentypmethode unterstützt Instanzen von **FullGlobe** oder räumliche Instanzen, die größer als eine Hemisphäre sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **Bit**  
  
 CLR-Rückgabetyp: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 Die OGC-Typ, der eine **Geography** Instanz kann bestimmt werden, durch den Aufruf [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erzeugt nur gültige **Geography** Instanzen, erlaubt aber für die Speicherung und Abruf Ungültiger Instanzen. Eine gültige Instanz, die die gleiche Punktmenge wie eine ungültige Instanz darstellt, kann mithilfe der `MakeValid()` -Methode abgerufen werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `geography` -Instanz erstellt und `STIsValid()` verwendet, um zu überprüfen, ob die Instanz gültig ist.  
  
```  
DECLARE @g geography = geography::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 4326);  
SELECT @g.STIsValid();  
DECLARE @g geography  
```  
  
## <a name="see-also"></a>Siehe auch  
 [STGeometryType &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)   
 [MakeValid &#40;geography-Datentyp&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [OGC-Methoden für geography-Instanzen](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
