---
title: Status-Eigenschaft (ADO-Feld) | Microsoft Docs
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
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65acf492f0364b26fa6a12240fbbd49c7d1dfed3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="status-property-ado-field"></a>Status-Eigenschaft (ADO-Feld)
Gibt den Status einer [Feld](../../../ado/reference/ado-api/field-object.md) Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) Wert. Der Standardwert ist **AdFieldOK**.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="record-field-status"></a>Datensatzstatus-Feld  
 Änderungen an den Wert der eine **Feld** Objekt in der Fields-Auflistung, der eine [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt werden zwischengespeichert, bis des Objekts [Update](../../../ado/reference/ado-api/update-method.md) Methode wird aufgerufen. An diesem Punkt wird die Änderung an der Wert des Felds einen Fehler verursacht, löst OLE DB-Fehler **DB_E_ERRORSOCCURRED** (2147749409). Die Status-Eigenschaft aller der **Feld** Objekte in der **Felder** -Auflistung, die den Fehler verursacht hat, enthält einen Wert aus der [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) , beschreibt die Ursache des das Problem.  
  
 Zur Verbesserung der Leistung, hinzufügen und Löschen von der [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Sammlungen von der **Datensatz** Objekt werden zwischengespeichert, bis die **Update** -Methode aufgerufen wird, und klicken Sie dann die Änderungen werden in einem Batch optimistische Update vorgenommen werden. Wenn die **Update** -Methode nicht aufgerufen wird, der Server wird nicht aktualisiert. Wenn Fehler bei Updates, und klicken Sie dann ein OLE DB-Anbieter-Fehler (DB_E_ERRORSOCCURRED) zurückgegeben wird und die **Status** Eigenschaft gibt den kombinierten Werten des Statuscodes Vorgang und Fehler an. Beispielsweise **AdFieldPendingInsert OR AdFieldPermissionDenied**. Die **Status** Eigenschaft für die einzelnen **Feld** können verwendet werden, um zu bestimmen, warum die **Feld** wurde nicht hinzugefügt, geändert oder gelöscht.  
  
 Viele Arten von Problemen beim Hinzufügen, ändern oder Löschen einer **Feld** gemeldet werden, über die **Status** Eigenschaft. Wenn der Benutzer löscht beispielsweise eine **Feld**, wird er zum Löschen von markiert die **Felder** Auflistung. Wenn die nachfolgenden **Update** gibt einen Fehler zurück, da der Benutzer versucht, zu löschen einer **Feld** für die sie sind nicht berechtigt, die **Feld** müssen eine ** Status** von **AdFieldPermissionDenied OR AdFieldPendingDelete**. Aufrufen der [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methoden Wiederherstellungen ursprüngliche Werte und legt die **Status** auf **AdFieldOK**.  
  
 Auf ähnliche Weise die **Update** Methode möglicherweise einen Fehler zurück, da ein neues **Feld** hinzugefügt und einen Ungültiger Wert angegeben wurde. In diesem Fall die neue **Feld** werden in der **Felder** Auflistung und haben den Status des **AdFieldPendingInsert** und vielleicht **AdFieldCantCreate** (abhängig von Ihrem Anbieter). Sie können einen geeigneten Wert angeben, für die neue **Feld** , und rufen Sie **Update** erneut aus.  
  
## <a name="recordset-field-status"></a>Feldstatus Recordset  
 Änderungen an den Wert des eine **Feld** Objekt in der Fields-Auflistung, der entweder eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) werden zwischengespeichert, bis des Objekts [Update](../../../ado/reference/ado-api/update-method.md) -Methode aufgerufen wird. An diesem Punkt wird die Änderung an der Wert des Felds einen Fehler verursacht, löst OLE DB-Fehler **DB_E_ERRORSOCCURRED** (2147749409). Die Status-Eigenschaft aller der **Feld** Objekte in der **Felder** -Auflistung, die den Fehler verursacht hat, enthält einen Wert aus der [FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md) , beschreibt die Ursache des das Problem.  
  
## <a name="applies-to"></a>Gilt für  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel der Status-Eigenschaft (Feld) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Status-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/status-property-example-vc.md)   

