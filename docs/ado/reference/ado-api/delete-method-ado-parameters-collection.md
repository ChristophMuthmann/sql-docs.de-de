---
title: Delete-Methode (ADO-Parameters-Auflistung) | Microsoft Docs
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
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5b7aff01cf3bb0dd34c53986a586aeae7b499a6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="delete-method-ado-parameters-collection"></a>Delete-Methode (ADO-Parameters-Auflistung)
Löscht ein Objekt aus der [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parameter  
 *Index*  
 Ein **Zeichenfolge** Wert, der den Namen des zu löschenden Objekts oder des Objekts Ordnungsposition (Index) in der Auflistung enthält.  
  
## <a name="remarks"></a>Hinweise  
 Mithilfe der **löschen** Methode in einer Auflistung können Sie eines der Objekte in der Auflistung zu entfernen. Diese Methode ist nur auf die **Parameter** Auflistung von einem [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt. Verwenden Sie die [Parameter](../../../ado/reference/ado-api/parameter-object.md) des Objekts [Namen](../../../ado/reference/ado-api/name-property-ado.md) Eigenschaft oder der Auflistungsindex beim Aufrufen der **löschen** Methode – Objektvariable ist kein gültiges Argument.  
  
## <a name="applies-to"></a>Gilt für  
 [Parameters-Collection (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Delete-Methode (ADO Fields-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete-Methode (ADO-Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord-Methode (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
