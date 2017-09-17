---
title: UpdateBatch-Methode | Microsoft Docs
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
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57c85b6ed83792e2e489eb91dab59bd0da598939
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updatebatch-method"></a>UpdateBatch-Methode
Schreibt alle ausstehenden BatchUpdates auf den Datenträger an.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parameter  
 *AffectRecords*  
 Optional. Ein [AffectEnum](../../../ado/reference/ado-api/affectenum.md) Wert, der angibt, wie viele Datensätze die **UpdateBatch** Methode wirkt sich auf.  
  
 *PreserveStatus*  
 Optional. Ein **booleschen** Wert, der angibt, und zwar unabhängig davon, ob lokale geändert wird, durch die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) -Eigenschaft muss ein Commit ausgeführt wurde. Wenn dieser Wert, um festgelegt wird **"true"**, **Status** Eigenschaft jedes Datensatzes bleibt unverändert, nachdem das Update abgeschlossen ist.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **UpdateBatch** Methode beim Ändern einer **Recordset** Objekt im Batchaktualisierungsmodus übertragen Sie alle Änderungen, die einer **Recordset** Objekt der zugrunde liegenden Datenbank.  
  
 Wenn die **Recordset** Objekt unterstützt BatchUpdates, mehrere Änderungen an einem oder mehreren Datensätzen können zwischengespeichert werden, lokal, bis Sie rufen die **UpdateBatch** Methode. Wenn Sie den aktuellen Datensatz bearbeiten oder Hinzufügen eines neuen Datensatzes beim Aufrufen der **UpdateBatch** Methode, ADO wird automatisch aufgerufen haben die [Update](../../../ado/reference/ado-api/update-method.md) Methode, um alle ausstehenden Änderungen in den aktuellen Datensatz vor dem Speichern die Übertragung von der zusammengefasste Änderungen an den Anbieter. Sie sollten Batchaktualisierung mit einem Keyset oder static-Cursor verwenden.  
  
> [!NOTE]
>  Angeben von **AdAffectGroup** wie der Wert für diesen Parameter zu einem Fehler führt, wenn es keine Datensätze angezeigt, in der aktuellen werden **Recordset** (z. B. einen Filter für die keine Datensätze entsprechen).  
  
 Schlägt der Versuch zum Übertragen von Änderungen für einige oder alle Datensätze aufgrund eines Konflikts mit dem zugrunde liegenden Daten (z. B. ein Datensatz wurde bereits gelöscht von einem anderen Benutzer), der Anbieter gibt Warnungen, um die [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung und ein zur Laufzeit Fehler tritt auf. Verwenden der [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft (**AdFilterAffectedRecords**) und die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) Eigenschaft, um Datensätze mit Konflikten zu suchen.  
  
 Um alle ausstehenden BatchUpdates "Abbrechen", verwenden die [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methode.  
  
 Wenn die [eindeutige Tabelle](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) und [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) dynamischen Eigenschaften werden festgelegt, und die **Recordset** ist das Ergebnis der Ausführung einer JOIN-Operation für mehrere Tabellen, die Ausführung der **UpdateBatch** Methode wird implizit gefolgt von der [Resync](../../../ado/reference/ado-api/resync-method.md) -Methode, abhängig von den Einstellungen der der [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) Eigenschaft.  
  
 Die Reihenfolge an, unter denen die einzelnen Updates eines Batches, für die Datenquelle ausgeführt werden, ist nicht notwendigerweise die Reihenfolge, in dem sie auf dem lokalen ausgeführt wurden, identisch **Recordset**. Aktualisierungsreihenfolge ist abhängig von den Anbieter. Berücksichtigen Sie dies beim Schreiben von Updates, die miteinander, z. B. foreign Key-Einschränkungen auf eine INSERT- oder Update verknüpft sind.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBatch und CancelBatch-Methoden (Beispiel) (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch und CancelBatch Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch-Methode (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear-Methode (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType-Eigenschaft (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update-Methode](../../../ado/reference/ado-api/update-method.md)

