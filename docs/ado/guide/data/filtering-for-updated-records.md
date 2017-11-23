---
title: "Filtern für Datensätze aktualisiert | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 29539dfd62901a2db41e3d282f615a5ce550cb84
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="filtering-for-updated-records"></a>Filtern nach aktualisierten Datensätzen
Bevor Sie UpdateBatch aufrufen, können Sie Recordset-Filter-Eigenschaft, um nur die Datensätze anzuzeigen, die geändert wurden, seit dem Öffnen des Recordsets oder dem letzten Aufruf von UpdateBatch. Zu diesem Zweck legen Sie Filter auf AdFilterPendingRecords, um zu bestimmen, wie viele Datensätze aktualisiert werden, wie im Codebeispiel im nächsten Abschnitt gezeigt.  
  
## <a name="remarks"></a>Hinweise  
 In diesem Beispiel erweitert das vorherige UpdateBatch Beispiel durch das Recordset filtern, kurz bevor die UpdateBatch aufruft, der Benutzer angezeigt, auf welche Änderungsdatensätze und Möglichkeit zum Abbrechen des Updates (mit der CancelBatch-Methode).  
  
```  
'BeginFilterPend  
    '...  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    objRs1.Filter = adFilterPendingRecords  
  
    MsgBox "There are " & objRs1.RecordCount & " records pending.", _  
            , "Filter Pending"  
  
    ' Cancel the updates  
    objRs1.CancelBatch  
'EndFilterPend  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Batchmodus](../../../ado/guide/data/batch-mode.md)
