---
title: Umgang mit fehlerhaften Updates | Microsoft Docs
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
helpviewer_keywords: updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
caps.latest.revision: "3"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e2be023b954040c1c539063c1e1a3d1cf67931ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dealing-with-failed-updates"></a>Umgang mit fehlerhaften Updates
Wenn ein Update mit Fehlern abgeschlossen ist, hängt wie Sie die Fehler beheben von der Art und Schweregrad der Fehler und die Logik Ihrer Anwendung. Wenn die Datenbank für andere Benutzer freigegeben werden, ist ein typische Fehler jedoch, dass eine andere Person Feld ändert, bevor Sie ausführen. Diese Art des Fehlers ist einen Konflikt bezeichnet. ADO erkennt diese Situation und meldet einen Fehler.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Update-Fehler vorhanden sind, werden sie in eine Fehlerbehandlungsroutine aufgefangen werden. Filtern Sie das Recordset mit der Konstante vorliegt, sodass nur die in Konflikt stehenden Zeilen angezeigt werden. In diesem Beispiel wird die Fehlerbehebung Strategie ist lediglich zum Drucken des Autors vor- und Nachnamen Namen (Au_fname und Au_lname).  
  
 Der Code Benachrichtigung des Benutzers an den Updatekonflikt sieht wie folgt:  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Batchmodus](../../../ado/guide/data/batch-mode.md)
