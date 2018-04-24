---
title: Clear-Methode (ADO) | Microsoft Docs
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
- Errors::raw_Clear
- Errors::Clear
helpviewer_keywords:
- Clear method [ADO]
ms.assetid: 0a61ba7a-20b8-426a-91a0-9040e7c5a98a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1e19263664607c1237d00b17523b492d4be013d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="clear-method-ado"></a>Clear-Methode (ADO)
Entfernt alle der [Fehler](../../../ado/reference/ado-api/error-object.md) Objekte aus der [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Errors.Clear  
```  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **deaktivieren** Methode für die [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung So entfernen Sie alle vorhandenen [Fehler](../../../ado/reference/ado-api/error-object.md) Objekte aus der Auflistung. Wenn ein Fehler auftritt, löscht ADO automatisch die **Fehler** Auflistung und füllt ihn mit **Fehler** Objekte basierend auf dem neuen Fehler.  
  
 Einige Eigenschaften und Methoden zurück Warnungen, die als **Fehler** Objekte in der **Fehler** Auflistung jedoch die Ausführung des Programms nicht angehalten werden. Vor dem Aufrufen der [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), oder [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methoden auf einen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt; die [Öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) Methode auf eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt; oder legen Sie die [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft auf eine **Recordset** -Objekt, rufen Sie die **deaktivieren**Methode für die **Fehler** Auflistung. Auf diese Weise erfahren Sie die [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft von der **Fehler** zurückgegebene Auflistung zur Prüfung auf Warnungen.  
  
## <a name="applies-to"></a>Gilt für  
 [Errors-Collection (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Führen Sie abzufragen und Clear-Methoden-Beispiel (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Führen Sie abzufragen und Clear-Methoden-Beispiel (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Führen Sie Requery und deaktivieren Sie die Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CancelBatch-Methode (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Delete-Methode (ADO Fields-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete-Methode (ADO-Parameters-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete-Methode (ADO-Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Filter-Eigenschaft](../../../ado/reference/ado-api/filter-property.md)   
 [Resync-Methode](../../../ado/reference/ado-api/resync-method.md)   
 [UpdateBatch-Methode](../../../ado/reference/ado-api/updatebatch-method.md)
