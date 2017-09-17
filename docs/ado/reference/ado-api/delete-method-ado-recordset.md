---
title: Delete-Methode (ADO-Recordset) | Microsoft Docs
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
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7555de66879f0caa75c72196c30c5a7ec3611249
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="delete-method-ado-recordset"></a>Delete-Methode (ADO-Recordset)
Löscht den aktuellen Datensatz oder eine Gruppe von Datensätzen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>Parameter  
 *AffectRecords*  
 Ein [AffectEnum](../../../ado/reference/ado-api/affectenum.md) Wert, der bestimmt, wie viele Datensätze die **löschen** Methode wirkt sich auf. Der Standardwert ist **AdAffectCurrent**.  
  
> [!NOTE]
>  **AdAffectAll** und **AdAffectAllChapters** sind keine gültigen Argumente, **löschen**.  
  
## <a name="remarks"></a>Hinweise  
 Mithilfe der **löschen** Methode kennzeichnet den aktuellen Datensatz oder eine Gruppe von Datensätzen in einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt zum Löschen. Wenn die **Recordset** Objekt kann keine Datensätze löschen, ein Fehler auftritt. Wenn Sie sich im sofortupdatemodus sind, werden Löschvorgänge sofort in der Datenbank. Wenn ein Datensatz (aufgrund der Datenbank Verletzungen der Integrität, z. B.) wurde erfolgreich gelöscht werden kann, der Datensatz bleibt im Bearbeitungsmodus nach dem Aufruf von [Update](../../../ado/reference/ado-api/update-method.md). Dies bedeutet, dass Sie das Update mit "Abbrechen" müssen [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) vor dem Verschieben aus dem aktuellen Datensatz (z. B. mit [schließen](../../../ado/reference/ado-api/close-method-ado.md), [verschieben](../../../ado/reference/ado-api/move-method-ado.md), oder [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Wenn Sie im Batchmodus Update ausgeführt werden, die Datensätze werden zum Löschen aus dem Cache markiert und das eigentliche löschen erfolgt beim Aufrufen der [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode. Verwenden der [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft, um die gelöschten Datensätze anzuzeigen.  
  
 Abrufen von Feldwerten aus dem gelöschten Datensatz generiert einen Fehler. Nach dem Löschen des aktuellen Datensatzes, bleibt der gelöschte Datensatz aktuell, bis Sie zu einem anderen Datensatz wechseln. Nachdem Sie verschieben Weg von den gelöschten Datensatz nicht mehr darauf zugreifen können.  
  
 Wenn Sie Löschvorgänge in einer Transaktion schachteln, können Sie wiederherstellen, gelöschte Datensätze mit den [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) Methode. Wenn Sie im Batchmodus Update ausgeführt werden, können Sie Abbrechen, eine ausstehende Löschung oder eine Gruppe von ausstehenden Löschvorgängen mit dem [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methode.  
  
 Schlägt der Versuch zum Löschen von Datensätzen aufgrund eines Konflikts mit dem zugrunde liegenden Daten (z. B. ein Datensatz wurde bereits gelöscht von einem anderen Benutzer), der Anbieter gibt Warnungen, um die [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung jedoch nicht das Programm angehalten wurde die Ausführung. Ein Laufzeitfehler tritt nur dann, wenn auf den angeforderten Datensätzen Konflikte bestehen.  
  
 Wenn die [eindeutige Tabelle](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) dynamische Eigenschaft festgelegt ist, und die **Recordset** ist das Ergebnis der Ausführung einer JOIN-Operation für mehrere Tabellen, die **löschen** Methode wird nur gelöscht werden. Zeilen aus der Tabelle mit dem Namen der [eindeutige Tabelle](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Löschen von Methodenbeispiel (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete Methodenbeispiel (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Löschen Sie die (VC++-Methodenbeispiel)](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete-Methode (ADO Fields-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete-Methode (ADO-Parameters-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord-Methode (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

