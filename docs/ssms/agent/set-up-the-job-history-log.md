---
title: Einrichten des Auftragsverlaufsprotokolls | Microsoft-Dokumentation
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
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82d09693143af337c03a54e653f029fb50710a17
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
In diesem Thema wird beschrieben, wie Sie das Auftragsverlaufsprotokoll des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents einrichten.  
  
-   **Vorbereitungen:**  [Sicherheit](#Security)  
  
-   **Einrichten des Auftragsverlaufsprotokolls mit:** [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Sicherheit  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
**So richten Sie das Auftragsverlaufsprotokoll ein**  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Wählen Sie im Dialogfeld **Eigenschaften des SQL Server-Agents** die Seite **Verlauf** aus.  
  
4.  Nehmen Sie für die folgenden Optionen die gewünschten Einstellungen vor:  
  
    1.  Aktivieren Sie die Option **Größe des Auftragsverlaufsprotokolls beschränken**, und geben Sie dann die maximale Anzahl von Zeilen für das Auftragsverlaufsprotokoll sowie die maximale Anzahl von Zeilen je Auftrag ein.  
  
    2.  Aktivieren Sie die Option **Agentverlauf automatisch entfernen**, und geben Sie den Zeitraum an, nach dem ältere Verlaufsdaten aus dem Protokoll gelöscht werden.  
  
## <a name="see-also"></a>Siehe auch  
[Implementieren von Aufträgen](../../ssms/agent/implement-jobs.md)  
[Überwachen der Auftragsaktivität](../../ssms/agent/monitor-job-activity.md)  
[Erstellen von Aufträgen](../../ssms/agent/create-jobs.md)  
  

