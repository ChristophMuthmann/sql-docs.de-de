---
title: EditMode-Eigenschaft | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d64f1ea25b8febe0ca9c474f76642cf1f74a9302
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="editmode-property"></a>EditMode-Eigenschaft
Gibt den Bearbeitungsstatus des aktuellen Datensatzes an.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) Wert.  
  
## <a name="remarks"></a>Hinweise  
 ADO verwaltet einen Bearbeitungspuffer mit dem aktuellen Datensatz verknüpft sind. Diese Eigenschaft gibt an, ob Änderungen an diesen Puffer vorgenommen wurden, oder ob ein neuer Datensatz erstellt wurde. Verwenden der **EditMode** Eigenschaft, um den Bearbeitungsstatus des aktuellen Datensatzes zu bestimmen. Sie können für ausstehende Änderungen testen, wenn ein Bearbeitungsprozess unterbrochen wurde und zu bestimmen, ob Sie benötigen die [Update](../../../ado/reference/ado-api/update-method.md) oder [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methode.  
  
 In *sofortupdatemodus* der **EditMode** Eigenschaft wird auf zurückgesetzt **AdEditNone** nach einem erfolgreichen Aufruf von der **aktualisieren** Methode wird aufgerufen . Wenn bei einem Aufruf [löschen](../../../ado/reference/ado-api/delete-method-ado-recordset.md) erfolgreich löscht keine Datensätze in der Datenquelle (z. B. aufgrund von Verletzungen der referentiellen Integrität), die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) verbleibt jedoch in den Bearbeitungsmodus (**EditMode** = **AdEditInProgress**). Aus diesem Grund **CancelUpdate** muss aufgerufen werden, bevor Sie fortfahren, aus dem aktuellen Datensatz (z. B. mit [verschieben](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), oder [schließen](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 In *Update Batchmodus* (in dem der Anbieter speichert mehrere Änderungen und schreibt Sie sie in der zugrunde liegenden Datenquelle aus, nur bei Aufruf der [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode), den Wert von der **EditMode**  -Eigenschaft geändert wird, wenn der erste Vorgang ausgeführt wird und er nicht, durch einen Aufruf zurückgesetzt wird der **Update** Methode. Nachfolgende-Vorgänge bleiben unverändert, den Wert der **EditMode** -Eigenschaft, auch wenn andere Vorgänge ausgeführt werden. Z. B. wenn der erste Vorgang besteht darin, einen neuen Datensatz hinzufügen und die zweite nimmt Änderungen an einer vorhandenen aufzuzeichnen, die Eigenschaft des **EditMode** weiterhin **AdEditAdd**. Die **EditMode** Eigenschaft wird nicht zurückgesetzt, um **AdEditNone** erst nach dem Aufruf von **UpdateBatch**. Um zu bestimmen, welche Vorgänge ausgeführt wurden, legen Sie die [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft [AdFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) , damit nur Datensätze mit ausstehenden Änderungen sichtbar werden, und überprüfen Sie die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) Eigenschaft jedes Datensatzes zu bestimmen, welche Änderungen an den Daten vorgenommen wurden.  
  
> [!NOTE]
>  **EditMode** kann einen gültigen Wert zurückgeben, nur dann, wenn ein aktueller Datensatz vorhanden ist. **EditMode** gibt einen Fehler zurück, wenn [BOF oder EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) ist "true", oder wenn der aktuelle Datensatz gelöscht wurde.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CursorType LockType und EditMode Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType LockType und EditMode Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew-Methode (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete-Methode (ADO-Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate-Methode (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update-Methode](../../../ado/reference/ado-api/update-method.md)
