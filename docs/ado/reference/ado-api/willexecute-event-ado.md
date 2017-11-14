---
title: WillExecute-Ereignis (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 63062a2b16cc423c1188aef4302f5b0f8b1e0677
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="willexecute-event-ado"></a>WillExecute-Ereignis (ADO)
Die **WillExecute** Ereignis wird aufgerufen, kurz bevor ein ausstehenden Befehls für eine Verbindung ausgeführt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parameter  
 *Quelle*  
 Ein **Zeichenfolge** , einen SQL-Befehl oder eine gespeicherte Prozedurnamens enthält.  
  
 *CursorType*  
 Ein [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) , enthält den Typ des Cursors für die **Recordset** , wird geöffnet. Mit diesem Parameter können Sie den Cursor auf einen beliebigen Typ während Ändern einer **Recordset**[Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) Vorgang. *CursorType* werden für alle anderen Vorgänge ignoriert.  
  
 *LockType*  
 Ein [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) , enthält den Typ der Sperre für die **Recordset** , wird geöffnet. Mit diesem Parameter können Sie die Sperre ändern, auf einen beliebigen Typ während einer **RecordsetOpen** Vorgang. *LockType* werden für alle anderen Vorgänge ignoriert.  
  
 *Optionen*  
 Ein **lange** Wert, der Optionen, die verwendet werden kann angibt, führen Sie den Befehl aus, oder öffnen Sie die **Recordset**.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert, der möglicherweise **AdStatusCantDeny** oder **AdStatusOK** Wenn dieses Ereignis aufgerufen wird. Ist er **AdStatusCantDeny**, dieses Ereignis kann nicht der Abbruch des ausstehenden Vorgangs anzufordern.  
  
 *pCommand*  
 Die [Befehl Object (ADO)](../../../ado/reference/ado-api/command-object-ado.md) -Objekt für den dieser ereignisbenachrichtigung gilt.  
  
 *pCommand*  
 Die [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt für den dieser ereignisbenachrichtigung gilt.  
  
 *pConnection*  
 Die [Verbindung Object (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt für den dieser ereignisbenachrichtigung gilt.  
  
## <a name="remarks"></a>Hinweise  
 Ein **WillExecute** Ereignis kann auftreten, weil eine Verbindung besteht.  [Execute-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [Execute-Methode (ADO-Befehl)](../../../ado/reference/ado-api/execute-method-ado-command.md), oder [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode der *pConnection* sollte der Parameter enthält immer einen gültigen Verweis auf eine **Verbindung** Objekt. Wenn das Ereignis aufgrund von **Connection.Execute**, *pCommand* und *pCommand* Parameter festgelegt **nichts**. Wenn das Ereignis aufgrund von **Recordset.Open**, die *pCommand* Parameter verweist die **Recordset** Objekt und die *pCommand* Parametersatz auf **nichts**. Wenn das Ereignis aufgrund von **Recordset.Open**, die *pCommand* Parameter verweist die **Befehl** Objekt und die *pCommand* Parametersatz auf **nichts**.  
  
 **WillExecute** können Sie zum Überprüfen und ändern die ausstehenden Execution-Parameter. Dieses Ereignis kann eine Anforderung zurückgeben, dass der ausstehende Befehl abgebrochen werden.  
  
> [!NOTE]
>  Wenn für die ursprüngliche Datenquelle einen **Befehl** ist ein Datenstrom, der gemäß der [CommandStream-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) -Eigenschaft, um eine neue Zeichenfolge zuweisen der **WillExecute** *Quelle* Änderung die Quelle des Parameters der **Befehl**. Die **CommandStream** Eigenschaft wird gelöscht und die [CommandText-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft wird mit der Quelle aktualisiert werden. Der ursprüngliche Stream gemäß **CommandStream** veröffentlicht und kann nicht zugegriffen werden.  
  
 Der Dialekt der neuen Quellzeichenfolge weicht von der ursprünglichen Einstellung für die [Dialect-Eigenschaft](../../../ado/reference/ado-api/dialect-property.md) Eigenschaft (die zugestimmt haben, um die **CommandStream**), durch Festlegen der richtigen Dialekt angegeben werden die **Dialekt** Eigenschaft des Befehlsobjekts verweist *pCommand*.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignisse Modell (VC++-Beispiel)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

