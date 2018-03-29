---
title: Anzeigen oder Ändern von Aufträgen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 216e985b79e70553919d27912de86bd0c20752bc
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="view-or-modify-jobs"></a>Anzeigen oder Ändern von Aufträgen
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Jeden Auftrag, den Sie erstellt haben, können Sie anzeigen. Nachdem Sie einen Auftrag ausgeführt haben, können Sie auch den Auftragsverlauf anzeigen. Auf diese Weise erfahren Sie, wann der Auftrag ausgeführt wurde, den Status des Auftrags insgesamt sowie den Status jedes Auftragsschritts. Sie sehen, ob bei dem Auftrag in der Vergangenheit jemals ein Fehler aufgetreten ist, wann der Auftrag zuletzt erfolgreich ausgeführt wurde sowie welche Ausgabe bei jeder Ausführung des Auftrags erstellt wurde. Mitglieder der festen Serverrolle **sysadmin** können jeden Auftrag anzeigen oder ändern, unabhängig vom Besitzer.  
  
> [!NOTE]  
> Ein Auftrag muss mindestens einmal ausgeführt worden sein, damit ein Auftragsverlauf vorhanden ist. Sie können die Gesamtgröße des Auftragsverlaufsprotokolls und die Größe pro Auftrag begrenzen.  
  
Schließlich können Sie einen Auftrag an neue Anforderungen anpassen. Sie können Folgendes ändern:  
  
-   Benachrichtigungsoptionen  
  
-   Zeitpläne  
  
-   Auftragsschritte  
  
-   Besitz  
  
-   Auftragskategorie  
  
-   Zielserver (ausschließlich bei Multiserveraufträgen)  
  
Wenn Sie Änderungen an Multiserveraufträgen vornehmen, müssen Sie die Änderungen der Downloadliste bereitstellen, damit die Zielserver den aktualisierten Auftrag herunterladen können. Um sicherzustellen, dass die Zielserver über die aktuellsten Auftragsdefinitionen verfügen, führen Sie nach dem Aktualisieren des Multiserverauftrags wie folgt eine INSERT-Anweisung aus:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Weitere Informationen finden Sie unter [sp_purge_jobhistory (Transact-SQL)](http://msdn.microsoft.com/en-us/237f9bad-636d-4262-9bfb-66c034a43e88).  
  
Mitglieder der festen Serverrolle **sysadmin** können die Definition oder den Verlauf jedes Auftrags anzeigen und können jeden Auftrag ändern.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Beschreibung**|**Thema**|  
|Beschreibt, wie [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträge angezeigt werden.|[Anzeigen eines Auftrags](../../ssms/agent/view-a-job.md)|  
|Beschreibt, wie das Auftragsverlaufsprotokoll des [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents angezeigt wird.|[Anzeigen des Auftragsverlaufs](../../ssms/agent/view-the-job-history.md)|  
|Beschreibt, wie der Inhalt des Auftragsverlaufsprotokolls des [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents gelöscht wird.|[Löschen des Auftragsverlaufsprotokolls](../../ssms/agent/clear-the-job-history-log.md)|  
|Beschreibt, wie Größenbeschränkungen für Auftragsverlaufsprotokolle des [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents festgelegt werden.|[Resize the Job History Log](../../ssms/agent/resize-the-job-history-log.md)|  
|Beschreibt, wie die Eigenschaften von [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträgen geändert werden.|[Ändern eines Auftrags](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[sysjobhistory](http://msdn.microsoft.com/en-us/1b1fcdbb-2af2-45e6-bf3f-e8279432ce13)  
  
