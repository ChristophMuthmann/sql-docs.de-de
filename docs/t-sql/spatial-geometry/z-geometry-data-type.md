---
title: Z (Geometry-Datentyp) | Microsoft Docs
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
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs: TSQL
helpviewer_keywords: Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60ca49605233bcdc374341c7d481cc12b03328c5
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="z-geometry-data-type"></a>Z (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Der Z-Wert (Höhe) der Instanz. Die Semantik des Höhenwerts ist benutzerdefiniert.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.Z  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Typ: **"float"**  
  
 CLR-Typ: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieser Eigenschaft ist NULL, wenn die geometry-Instanz kein Punkt ist. Sie ist außerdem NULL für jede **Point** -Instanz, für die sie nicht festgelegt ist.  
  
 Diese Eigenschaft ist schreibgeschützt.  
  
 Z-Koordinaten werden in Berechnungen der Bibliothek nicht verwendet und werden nicht in Bibliotheksberechnungen einbezogen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `Point` -Instanz mit Z (Höhe)- und M (Measure)-Werten erstellt und `Z` verwendet, um den Z-Wert der Instanz abzurufen.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Übe &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [Erweiterte Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

