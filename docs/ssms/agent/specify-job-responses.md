---
title: Angeben von Auftragsantworten | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], responses
- SQL Server Agent jobs, responses
- actions [SQL Server Agent jobs]
- responding to jobs
ms.assetid: 050242e1-9b79-4ade-91a9-580707b9d2d9
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d2970e6ba2c2c3bc34436752beb7fa72834786c7
ms.lasthandoff: 04/11/2017

---
# <a name="specify-job-responses"></a>Angeben von Auftragsantworten
Auftragsantworten geben Aktionen an, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Dienst nach Abschluss eines Auftrags ausführt. Sie stellen sicher, dass Datenbankadministratoren wissen, wann Aufträge fertig gestellt sind und wie oft diese ausgeführt werden. Zu den typischen Auftragsantworten gehören folgende:  
  
-   Benachrichtigen des Operators per E-Mail, Pager oder **NET SEND** -Nachricht.  
  
    Verwenden Sie eine dieser Auftragsantworten vor allem dann, wenn der Operator weitere Schritte ausführen muss. Wenn beispielsweise ein Sicherungsauftrag erfolgreich ausgeführt wurde, muss der Operator darüber informiert werden, um das Sicherungsband entfernen zu können und an einem sicheren Standort aufbewahren zu lassen.  
  
-   Schreiben einer Ereignismeldung in das Windows-Anwendungsprotokoll.  
  
    Diese Art der Antwort können Sie nur bei fehlgeschlagenen Aufträgen verwenden.  
  
-   Automatisches Löschen des Auftrags.  
  
    Verwenden Sie diese Auftragsantwort, wenn Sie sicher sind, dass Sie diesen Auftrag nicht erneut ausführen müssen.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|**Description**|**Thema**|  
|Beschreibt, wie ein Operator über den Auftragsstatus benachrichtigt wird.|[Benachrichtigen eines Operators über den Auftragsstatus](../../ssms/agent/notify-an-operator-of-job-status.md)|  
|Beschreibt, wie der Auftragsstatus in das Windows-Anwendungsprotokoll ausgegeben wird.|[Write the Job Status to the Windows Application Log](../../ssms/agent/write-the-job-status-to-the-windows-application-log.md)|  
  
## <a name="see-also"></a>Siehe auch  
[Überwachen und Reagieren auf Ereignisse](../../ssms/agent/monitor-and-respond-to-events.md)  
  

