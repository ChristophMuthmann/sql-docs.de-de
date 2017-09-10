---
title: Long (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Long_TSQL
- Long
dev_langs:
- TSQL
helpviewer_keywords:
- Long method
ms.assetid: bedbeced-70b8-4569-84f3-f86bfb04ce50
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0c69ce921e8aa22d65011a56d47c5cd7b05ad76f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="long-geography-data-type"></a>Long (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Die Längengradeigenschaft der **geography** -Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.Long  
```  
  
## <a name="return-value"></a>Rückgabewert  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Typ: **"float"**  
  
 CLR-Typ: **SqlDouble**  
  
## <a name="remarks"></a>Hinweise  
 Im OpenGIS-Modell lange ist definiert nur auf **Geography** Instanzen aus einem einzelnen Punkt bestehen. Diese Eigenschaft gibt NULL zurück, wenn **geography** -Instanzen mehr als nur einen Punkt enthalten. Diese Eigenschaft exakt und ist schreibgeschützt.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird eine **Point** -Instanz erstellt und der Längengrad des Punkts abgerufen.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Long;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

