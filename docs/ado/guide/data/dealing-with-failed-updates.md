---
title: Umgang mit fehlerhaften Updates | Microsoft Docs
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
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3ca859e2e8d7a4948a1fb38567500c44daff4ba
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
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
