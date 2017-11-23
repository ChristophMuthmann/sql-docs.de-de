---
title: CancelBatch-Methode (ADO) | Microsoft Docs
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
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords: CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b5dc5cc6d3047c7dc0804c42c7e8efcc80b64054
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="cancelbatch-method-ado"></a>CancelBatch-Methode (ADO)
Bricht einen ausstehenden BatchUpdate ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parameter  
 *AffectRecords*  
 Optional. Ein [AffectEnum](../../../ado/reference/ado-api/affectenum.md) Wert, der angibt, wie viele Datensätze die **CancelBatch** Methode wirkt sich auf.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **CancelBatch** Methode, um alle ausstehenden Updates in "Abbrechen" eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) im Batchmodus-Update. Wenn die **Recordset** befindet sich im sofortupdatemodus Aufrufen **CancelBatch** ohne **AdAffectCurrent** wird ein Fehler generiert.  
  
 Wenn Sie den aktuellen Datensatz bearbeiten oder ein neues Datensatzes beim Aufrufen hinzufügen **CancelBatch**, ADO-ruft zunächst die [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methode, um eine "Abbrechen" zwischengespeicherte Änderungen. Danach alle ausstehenden Änderungen in der **Recordset** abgebrochen werden.  
  
 Möglicherweise ist der aktuelle Datensatz Maskierungsstufe nach einer **CancelBatch** aufzurufen, insbesondere dann, wenn Sie gerade einen neuen Datensatz hinzugefügt wurden. Aus diesem Grund ist es unerlässlich, legen Sie die Position des aktuellen Datensatzes an einem bekannten Speicherort in der **Recordset** nach der **CancelBatch** aufrufen. Beispielsweise rufen Sie die [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) Methode.  
  
 Schlägt der Versuch zum Abbrechen von ausstehenden Updates aufgrund eines Konflikts mit dem zugrunde liegenden Daten (z. B., wenn ein Datensatz von einem anderen Benutzer gelöscht wurde), gibt der Anbieter Warnungen, um die [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung jedoch lässt sich nicht anhalten Ausführung des Programms. Ein Laufzeitfehler tritt nur dann, wenn auf den angeforderten Datensätzen Konflikte bestehen. Verwenden der [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft (**AdFilterAffectedRecords**) und die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) Eigenschaft, um Datensätze mit Konflikten zu suchen.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBatch und CancelBatch-Methoden (Beispiel) (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch und CancelBatch Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel-Methode (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel-Methode (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelUpdate-Methode (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate-Methode (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear-Methode (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType-Eigenschaft (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch-Methode](../../../ado/reference/ado-api/updatebatch-method.md)
