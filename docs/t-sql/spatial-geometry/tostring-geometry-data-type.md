---
title: ToString (Geometry-Datentyp) | Microsoft Docs
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
- ToString (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString (geometry Data Type)
ms.assetid: 2e55fa98-aa22-4baa-a516-7c233a33e212
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ffe70ad712605222a66dc12ba7af4e330dc12c9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="tostring-geometry-data-type"></a>ToString (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die Open Geospatial Consortium (OGC) Well-Known Text (WKT)-Darstellung einer geometry-Instanz zurück, die um alle von der Instanz getragenen Z (Höhe)- und M (Measure)-Werte erweitert ist.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **nvarchar(max)**  
  
 CLR-Rückgabetyp: **SqlString**  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode gibt die Zeichenfolge "NULL" zurück, wenn sie für NULL-Instanzen aufgerufen wird.  
  
 Bei Instanzen, die nicht NULL sind, entspricht diese Methode der Verwendung von `AsTextZM().`.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine `LineString` -Instanz erstellt und mithilfe von `ToString()` eine Textbeschreibung der Instanz abgerufen.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Siehe auch  
 [STAsText &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)   
 [Erweiterte Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  


