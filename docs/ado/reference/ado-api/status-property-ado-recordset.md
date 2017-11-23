---
title: Status-Eigenschaft (ADO-Recordset) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords: Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0005de0669a2dd68622c2e81c9f7b3be2f912da1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="status-property-ado-recordset"></a>Status-Eigenschaft (ADO-Recordset)
Gibt den Status des aktuellen Datensatzes in Bezug auf BatchUpdates oder andere Massenvorgänge an.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine Summe für eine oder mehrere [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) Werte.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Status** Eigenschaft, um festzustellen, welche Änderungen ausstehen für Datensätze, die während des BatchUpdates geändert. Können Sie auch die **Status** Eigenschaft zum Anzeigen des Status von Datensätzen, bei denen bei Massenvorgängen, z. B. beim Aufrufen der [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), oder [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methoden auf einen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt, oder legen Sie die [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft auf einen **Recordset** -Objekts in ein Array von Lesezeichen. Mit dieser Eigenschaft können Sie bestimmen, wie ein bestimmter Datensatz ist fehlgeschlagen, und lösen Sie ihn entsprechend.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel der Status-Eigenschaft (Recordset) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status-Eigenschaft – Beispiel (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
