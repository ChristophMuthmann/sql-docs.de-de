---
title: AsBinaryZM (Geography-Datentyp) | Microsoft Docs
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
- AsBinaryZM
- AsBinaryZM_TSQL
dev_langs: TSQL
helpviewer_keywords:
- AsBinaryZM, geography
- AsBinaryZM
ms.assetid: 37246adb-814d-4113-9983-4d336de8182c
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f46f38c4a08c9cac11393c044876c2569b412a02
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="asbinaryzm-geography-data-type"></a>AsBinaryZM (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt die Open Geospatial Consortium (OGC) Well-Known Binary (WKB)-Darstellung einer **Geometrie** Instanz getragenen alle **Z** (Höhe) und **M** (Measure) Werte, die von der Instanz getragen werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **varbinary(max)**  
  
 CLR-Rückgabetyp: **SqlBytes**  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
  
```sql  
DECLARE @g1 GEOGRAPHY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Übe &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40; Geography-Datentyp &#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
