---
title: Delete-Methode (ADO Fields-Auflistung) | Microsoft Docs
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
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 731a9fd24b1961b918efffba2f26e49a9cc782b8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="delete-method-ado-fields-collection"></a>Delete-Methode (ADO Fields-Auflistung)
Löscht ein Objekt aus der [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parameter  
 *Feld*  
 Ein **Variant** , der festlegt, die [Feld](../../../ado/reference/ado-api/field-object.md) zu löschende Objekt. Dieser Parameter kann den Namen des der **Feld** Objekt oder die Ordnungsposition der **Feld** Objekt selbst.  
  
## <a name="remarks"></a>Hinweise  
 Aufrufen der **Fields.Delete** -Methode für ein offenes [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) verursacht einen Laufzeitfehler.  
  
## <a name="applies-to"></a>Gilt für  
 [Fields-Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Delete-Methode (ADO-Parameters-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete-Methode (ADO-Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [DeleteRecord-Methode (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
