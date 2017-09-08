---
title: Null (Geometry-Datentyp) | Microsoft Docs
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
- Null (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geometry Data Type)
ms.assetid: 67a4b019-9091-4443-85cc-f4836d0cb509
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a7585bc509c4e19a08144109dee56ea30502005d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="null-geometry-data-type"></a>Null (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Eine schreibgeschützte Eigenschaft, die eine NULL-Instanz des **geometry** -Typs bereitstellt.
  
## <a name="syntax"></a>Syntax  
  
```  
  
Null  
```  
  
## <a name="arguments"></a>Argumente  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Typ: **Geometrie**  
  
 CLR-Typ: **SqlGeometry**  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine NULL- `geometry` -Instanz abgerufen.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte statische Geometry-Methoden](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


