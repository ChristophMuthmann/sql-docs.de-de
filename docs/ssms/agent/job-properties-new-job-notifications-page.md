---
title: "Auftragseigenschaften – Neuer Auftrag (Seite „Benachrichtigungen“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6508f164910c229f2acee22638dff7d661bf9d04
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="job-properties---new-job-notifications-page"></a>Auftragseigenschaften – Neuer Auftrag (Seite „Benachrichtigungen“)
Auf dieser Seite können Sie die Aktionen für den [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent festlegen, die bei Abschluss des Auftrags auszuführen sind.  
  
## <a name="options"></a>enthalten  
**E-Mail**  
Diese Option wird ausgewählt, um bei Abschluss des Auftrags eine E-Mail zu senden. Nachdem Sie die Option ausgewählt haben, müssen Sie den zu benachrichtigenden Operator und die Bedingung auswählen, durch die die Benachrichtigung ausgelöst wird. Die Bedingungen sind **Bei erfolgreicher Auftragsausführung**, **Bei Auftragsfehler**oder **Beim Abschluss des Auftrags**.  
  
**Page**  
Diese Option wird ausgewählt, um eine E-Mail an den Pager des Operators zu senden, wenn der Auftrag abgeschlossen ist. Nachdem Sie die Option ausgewählt haben, müssen Sie den zu benachrichtigenden Operator und die Bedingung auswählen, durch die die Benachrichtigung ausgelöst wird. Die Bedingungen sind **Bei erfolgreicher Auftragsausführung**, **Bei Auftragsfehler**oder **Beim Abschluss des Auftrags**.  
  
**NET SEND**  
Diese Option wird ausgewählt, um einen Operator bei Abschluss des Auftrags über net send zu benachrichtigen. Nachdem Sie die Option ausgewählt haben, müssen Sie den zu benachrichtigenden Operator und die Bedingung auswählen, durch die die Benachrichtigung ausgelöst wird. Die Bedingungen sind **Bei erfolgreicher Auftragsausführung**, **Bei Auftragsfehler**oder **Beim Abschluss des Auftrags**.  
  
**In das Windows-Anwendungsereignisprotokoll schreiben**  
Diese Option wird ausgewählt, um bei Abschluss des Auftrags einen Eintrag in das Anwendungsereignisprotokoll zu schreiben. Nachdem Sie die Option ausgewählt haben, müssen Sie die Bedingung angeben, durch die veranlasst wird, dass der Eintrag geschrieben wird. Die Bedingungen sind **Bei erfolgreicher Auftragsausführung**, **Bei Auftragsfehler**und **Beim Abschluss des Auftrags**.  
  
**Auftrag automatisch löschen**  
Diese Option wird ausgewählt, um den Auftrag bei Abschluss zu löschen. Nachdem Sie die Option ausgewählt haben, müssen Sie die Bedingung angeben, durch die veranlasst wird, dass der Auftrag gelöscht wird. Die Bedingungen sind **Bei erfolgreicher Auftragsausführung**, **Bei Auftragsfehler**und **Beim Abschluss des Auftrags**.  
  
## <a name="see-also"></a>Siehe auch  
[Implementieren von Aufträgen](../../ssms/agent/implement-jobs.md)  
[Vorgehensweise: Konfigurieren der Verwendung von Datenbank-E-Mail für SQL Server-Agent-Mail (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  

