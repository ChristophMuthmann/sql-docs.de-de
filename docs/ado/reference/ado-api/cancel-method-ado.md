---
title: Cancel-Methode (ADO) | Microsoft Docs
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
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords: Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b0112431262f9b120bb3006c07e077e968f79c7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="cancel-method-ado"></a>Cancel-Methode (ADO)
Bricht die Ausführung eines ausstehenden asynchronen Methodenaufrufs ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **"Abbrechen"** Methode, um die Ausführung eines asynchronen Methodenaufrufs beenden: d. h. eine Methode aufgerufen wird, mit der **AdAsyncConnect**, **AdAsyncExecute**, oder **AdAsyncFetch** Option.  
  
 Die folgende Tabelle zeigt, welche Aufgabe beendet wird, bei der Verwendung der **"Abbrechen"** Methode für einen bestimmten Typ des Objekts.  
  
|Wenn *Objekt* ist ein|Der letzte asynchrone Aufruf dieser Methode wird beendet.|  
|----------------------|-------------------------------------------------------------|  
|[Befehl](../../../ado/reference/ado-api/command-object-ado.md)|[Ausführen](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Verbindung](../../../ado/reference/ado-api/connection-object-ado.md)|[Führen Sie](../../../ado/reference/ado-api/execute-method-ado-connection.md) oder [öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[Datensatz](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md), oder [öffnen](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|[Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Stream](../../../ado/reference/ado-api/stream-object-ado.md)|[Öffnen](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record-Objekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Siehe auch  
 [Cancel-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Cancel-Methode (Beispiel) (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel-Methode (VC++-Beispiel)](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Cancel-Methode (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch-Methode (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate-Methode (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate-Methode (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Execute-Methode (ADO-Befehl)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Open-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open-Methode (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
