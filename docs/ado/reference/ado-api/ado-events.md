---
title: ADO-Ereignisse | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO]
- ADO, events
ms.assetid: 0ded5ad9-8f83-4224-95af-38512783b972
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 59492bb63fd11aa1c60b3c45daed5a7431475cd9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ado-events"></a>ADO-Ereignisse
|||  
|-|-|  
|[BeginTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Wird aufgerufen, nachdem die **BeginTrans** Vorgang.|  
|[CommitTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Wird aufgerufen, nachdem die **CommitTrans** Vorgang.|  
|[ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Wird aufgerufen, nachdem eine Verbindung gestartet wird.|  
|[Trennen](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|Wird aufgerufen, nachdem eine Verbindung beendet.|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Wird aufgerufen, wenn der Versuch zum Verschieben einer Zeile nach dem Ende der **Recordset**.|  
|[ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|Wird aufgerufen, nachdem ein Befehl beendet wurde.|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Wird aufgerufen, nachdem alle Datensätze in einer langen asynchronen Operation in abgerufen wurden die **Recordset**.|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|Wird aufgerufen, in regelmäßigen Abständen während eines längeren asynchronen Vorgangs gemeldet wird, wie viele Zeilen in derzeit abgerufen wurden die **Recordset**.|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Wird aufgerufen, nachdem der Wert aus einem oder mehreren **Feld** Objekte wurde geändert.|  
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|Wird aufgerufen, sobald eine Warnung, während auftritt eine **ConnectionEvent** Vorgang.|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Wird aufgerufen, nachdem die aktuelle Position in der **Recordset** ändert.|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Wird aufgerufen, nachdem einem oder mehreren Datensätzen ändern.|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Wird aufgerufen, nachdem die **Recordset** hat sich geändert.|  
|[RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|Wird aufgerufen, nachdem die **RollbackTrans** Vorgang.|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Wird aufgerufen, bevor Sie ein ausstehender Vorgang ändert sich den Wert einer oder mehrerer **Feld** Objekte in der **Recordset**.|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Aufgerufen, bevor Sie einem oder mehreren Datensätzen (Zeilen) in der **Recordset** ändern.|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Wird aufgerufen, bevor Sie ein ausstehender Vorgang ändert die **Recordset**.|  
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md)|Wird aufgerufen, bevor eine Verbindung gestartet wird.|  
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md)|Wird aufgerufen, kurz bevor ein ausstehenden Befehls für diese Verbindung führt und gibt dem Benutzer die Möglichkeit zum Überprüfen und ändern die ausstehenden Execution-Parameter.|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Die **WillMove** Ereignis wird aufgerufen, *vor* ein ausstehender Vorgang ändert die aktuelle Position in der **Recordset**.|  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-API-Referenz](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO-Auflistungen](../../../ado/reference/ado-api/ado-collections.md)   
 [Dynamische Eigenschaften von ADO.NET](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO--Enumerationskonstanten](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Anhang B: ADO-Fehler](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Behandlung von Ereignissen für ADO](../../../ado/guide/data/handling-ado-events.md)   
 [ADO-Methoden](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO-Objektmodell](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO-Objekte und Schnittstellen](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Eigenschaften von ADO.NET](../../../ado/reference/ado-api/ado-properties.md)

