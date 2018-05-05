---
title: Updatemethode | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c0a5cd4e12848ecdec7c3c5168b6106dd95215c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="update-method"></a>Update-Methode
Speichert alle Änderungen an der aktuellen Zeile ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt, oder die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parameter  
 *Fields*  
 Optional. Ein **Variant** , einen einzelnen Namen darstellt, oder ein **Variant** Array, das darstellt, Namen oder die Ordnungsposition des Felds oder der Felder, die Sie ändern möchten.  
  
 *Werte*  
 Optional. Ein **Variant** , die einen einzelnen Wert darstellt, oder ein **Variant** Array, das Werte für das Feld oder Felder im neuen Datensatz darstellt.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="recordset"></a>Recordset  
 Verwenden der **Update** Methode, um die Änderungen zu speichern, Sie nehmen Sie an den aktuellen Datensatz des, eine **Recordset** Objekt seit dem Aufrufen der [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) Methode oder seit ändern alle Feldwerte in einer vorhandenen Datensatz. Die **Recordset** Objekt muss Updates unterstützen.  
  
 Führen Sie eine der folgenden Aktionen aus, um Feldwerte festzulegen:  
  
-   Werte zuweisen einer [Feld](../../../ado/reference/ado-api/field-object.md) des Objekts [Wert](../../../ado/reference/ado-api/value-property-ado.md) -Eigenschaft, und rufen die **Update** Methode.  
  
-   Übergeben Sie einen Feldnamen und einen Wert als Argumente mit den **Update** aufrufen.  
  
-   Übergibt ein Array von Feldnamen und ein Array von Werten mit der **Update** aufrufen.  
  
 Wenn Sie Arrays von Feldern und Werten verwenden, muss eine gleiche Anzahl von Elementen in beiden Arrays sein. Die Reihenfolge der Feldnamen muss ebenfalls die Reihenfolge der Feldwerte entsprechen. Wenn die Anzahl und Reihenfolge der Felder und Werte nicht übereinstimmen, tritt ein Fehler auf.  
  
 Wenn die **Recordset** Objekt unterstützt BatchUpdates, mehrere Änderungen an einem oder mehreren Datensätzen können zwischengespeichert werden, lokal, bis Sie rufen die [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode. Wenn Sie den aktuellen Datensatz bearbeiten oder Hinzufügen eines neuen Datensatzes beim Aufrufen der **UpdateBatch** Methode, ADO wird automatisch aufgerufen haben die **Update** Methode, um alle ausstehenden Änderungen in den aktuellen Datensatz vor dem Speichern die Übertragung von der zusammengefasste Änderungen an den Anbieter.  
  
 Wenn Sie aus dem Datensatz verschieben Sie hinzufügen oder bearbeiten Sie vor dem Aufruf der **Update** , ADO wird automatisch-Methodenaufruf **Update** um die Änderungen zu speichern. Rufen Sie die [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methode, wenn Sie "Abbrechen" Alle Änderungen an den aktuellen Datensatz oder einen neu hinzugefügten Datensatz verwerfen möchten.  
  
 Der aktuelle Datensatz bleibt der aktuelle nach dem Aufruf der **Update** Methode.  
  
## <a name="record"></a>Aufzeichnung (Record)  
 Die **Update** Methode schließt Hinzufügungen, löschungen und Aktualisierungen von Feldern in der [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einem **Datensatz** Objekt.  
  
 Z. B. Felder, die gelöscht werden, mit der **löschen** verbleiben in der Auflistung jedoch Methode sofort zum Löschen markiert sind. Die **Update** -Methode muss aufgerufen werden, um diese Felder aus der Auflistung des Anbieters tatsächlich zu löschen.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Fields-Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Update- und CancelUpdate Methoden Beispiel (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update- und CancelUpdate Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew-Methode (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate-Methode (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode-Eigenschaft](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch-Methode](../../../ado/reference/ado-api/updatebatch-method.md)
