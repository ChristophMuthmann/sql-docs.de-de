---
title: CancelUpdate-Methode (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a85b135d743b356f5e4f5bd28e6bb2f2bb1eec0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="cancelupdate-method-ado"></a>CancelUpdate-Methode (ADO)
Bricht alle Änderungen an der aktuellen oder neue Zeile ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt, oder die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einer [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) -Objekt, vor dem Aufruf der [Update ](../../../ado/reference/ado-api/update-method.md) Methode.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="recordset"></a>Recordset  
 Verwenden der **CancelUpdate** -Methode Abbrechen von Änderungen an der aktuellen Zeile oder eine neu hinzugefügte Zeile zu verwerfen. Änderungen an der aktuellen Zeile oder eine neue Zeile kann nicht abgebrochen werden, nach dem Aufruf der **Update** -Methode, es sei denn, die Änderungen entweder Teil einer Transaktion sind, die Sie mit Rollback können die [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) -Methode oder teilweise von einem BatchUpdate. Sie können bei einem BatchUpdate Abbrechen der **aktualisieren** mit der **CancelUpdate** oder [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methode.  
  
 Wenn Sie eine neue Zeile, beim Aufrufen Hinzufügen der **CancelUpdate** -Methode, zur aktiven Zeile wird die Zeile, die vor dem aktuellen wurde die [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) aufrufen.  
  
 Wenn Sie im Bearbeitungsmodus befindet und Sie den aktuellen Datensatz verschoben werden soll (z. B. mithilfe der [verschieben](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), oder [schließen](../../../ado/reference/ado-api/close-method-ado.md) Methoden), können Sie ** CancelUpdate** , alle ausstehenden Änderungen abzubrechen. Möglicherweise müssen Sie dies tun, wenn das Update erfolgreich an die Datenquelle bereitgestellt werden, nicht möglich. Beispielsweise ein Verbindungsversuch löschen, ein Fehler auftritt, aufgrund von Verletzungen der referentiellen Integrität auslassen, werden die **Recordset** im Bearbeitungsmodus nach einem Aufruf von [löschen](../../../ado/reference/ado-api/delete-method-ado-recordset.md).  
  
## <a name="record"></a>Aufzeichnung (Record)  
 Die **CancelUpdate** -Methode bricht alle ausstehenden Einfüge- oder Löschvorgänge [Feld](../../../ado/reference/ado-api/field-object.md) Objekte aufweist, und bricht ausstehende Updates vorhandener Felder ab und stellt diese in ihre ursprünglichen Werte wieder her. Die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) Eigenschaft aller Felder in der **Felder** Sammlungssatz zu **AdFieldOK**.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Fields-Auflistung (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Update- und CancelUpdate Methoden Beispiel (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update- und CancelUpdate Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew-Methode (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel-Methode (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel-Methode (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch-Methode (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate-Methode (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode-Eigenschaft](../../../ado/reference/ado-api/editmode-property.md)   
 [Update-Methode](../../../ado/reference/ado-api/update-method.md)

