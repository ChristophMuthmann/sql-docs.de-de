---
title: GetSchemaObject-Methode (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01142e27e03cd85dcdd59e92737ee46a3bb4cf09
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="getschemaobject-method-ado-md"></a>GetSchemaObject-Methode (ADO MD)
Ruft ein Objekt der ADO MD-Schema ([Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [Hierarchie](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md), oder [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md)) von seiner [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *ObjType*  
 Ein [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) Wert, der Art eines Schemaobjekts (Dimension, Hierarchie, Ebene oder Member) abzurufenden angibt.  
  
 *UniqueName*  
 Ein **Zeichenfolge** angeben der **UniqueName** Eigenschaftswert des abzurufenden Objekts.  
  
## <a name="remarks"></a>Hinweise  
 **GetSchemaObject** ruft Objekte, die mit ihren eindeutigen Namen, entsprechend den Angaben von der **UniqueName** Eigenschaft. Die Namen der übergeordneten Objekte müssen nicht bekannt sein, und übergeordneten Auflistungen müssen nicht aufgefüllt werden, um ein Objekt abzurufen.  
  
## <a name="applies-to"></a>Gilt für  
 [CubeDef-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CubeDef-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
