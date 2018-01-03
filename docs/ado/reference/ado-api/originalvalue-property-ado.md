---
title: OriginalValue-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Field20::OriginalValue
helpviewer_keywords: OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70e33fcec6571a845ee81a393e5f267cc945de5d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="originalvalue-property-ado"></a>OriginalValue-Eigenschaft (ADO)
Gibt den Wert einer [Feld](../../../ado/reference/ado-api/field-object.md) , die im Datensatz vorhanden waren, bevor Änderungen vorgenommen wurden.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Variant** Wert, der den Wert eines Felds vor jeder Änderung darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **OriginalValue** -Eigenschaft zum Zurückgeben von des ursprünglichen Feldwert für ein Feld aus dem aktuellen Datensatz.  
  
 In *sofortupdatemodus* (in dem der Anbieter schreibt Änderungen in der zugrunde liegenden Datenquelle nach dem Aufruf der [aktualisieren](../../../ado/reference/ado-api/update-method.md) Methode), wird die **OriginalValue** Eigenschaft gibt der Wert des Felds, das vor dem Änderungen vorhanden waren (d. h., seit dem letzten **Update** Methodenaufruf). Dies entspricht dem Wert, der [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methode verwendet zum Ersetzen der [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft.  
  
 In *Update Batchmodus* (in dem der Anbieter speichert mehrere Änderungen und schreibt Sie sie in der zugrunde liegenden Datenquelle aus, nur bei Aufruf der [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode), wird die **OriginalValue** -Eigenschaft zurück, den Wert des Felds, das vor dem Änderungen vorhanden waren (d. h., seit dem letzten **UpdateBatch** Methodenaufruf). Dies entspricht dem Wert, der [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methode verwendet zum Ersetzen der **Wert** Eigenschaft. Bei Verwendung dieser Eigenschaft mit dem [OriginalValue](../../../ado/reference/ado-api/underlyingvalue-property.md) -Eigenschaft, können Sie Konflikte von BatchUpdates beheben.  
  
## <a name="record"></a>Aufzeichnung (Record)  
 Für [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekte, die **OriginalValue** -Eigenschaft wird für Felder hinzugefügt, bevor Sie leer sein [Update](../../../ado/reference/ado-api/update-method.md) aufgerufen wird.  
  
## <a name="applies-to"></a>Gilt für  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OriginalValue und OriginalValue Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue und OriginalValue Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue-Eigenschaft](../../../ado/reference/ado-api/underlyingvalue-property.md)
