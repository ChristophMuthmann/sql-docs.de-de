---
title: M (Geometry-Datentyp) | Microsoft Docs
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
- M (geometry Data Type)
- M_TSQL
dev_langs: TSQL
helpviewer_keywords: M (geometry Data Type)
ms.assetid: 443ae2ea-739b-41ef-96cc-ac5dfd65e10b
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e1e51e478e2929f5c458568ceaae1966990ef95
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="m-geometry-data-type"></a>M (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Der **M** (Measure)-Wert der **geometry** -Instanz. Die Semantik des Measurewerts ist benutzerdefiniert.  

## <a name="syntax"></a>Syntax  
  
```  
  
.M  
```  
  
## <a name="arguments"></a>Argumente  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Typ: **"float"**  
  
 CLR-Typ: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieser Eigenschaft ist NULL, wenn die **geometry** -Instanz kein **Point**ist. Sie ist außerdem NULL für jede **Point** -Instanz, für die sie nicht festgelegt ist.  
  
 Diese Eigenschaft ist schreibgeschützt.  
  
 **M** -Werte werden in Berechnungen der Bibliothek nicht verwendet und werden nicht in Bibliotheksberechnungen einbezogen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `Point` -Instanz mit Z (Höhe)- und M (Measure)-Werten erstellt und `M` verwendet, um den M-Wert der Instanz abzurufen.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM &#40;geometry-Datentyp&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  

