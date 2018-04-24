---
title: Auftragsaktivitäten anzeigen | Microsoft-Dokumentation
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
- viewing job activity
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- displaying job activity
ms.assetid: 5c284e5e-7775-435d-ac49-f3f12a27ddc7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 43c9857e4579e1d72434fe14db513daa5fee0492
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-job-activity"></a>Auftragsaktivitäten anzeigen
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie den Laufzeitstatus von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträgen in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]anzeigen können.  
  
Wenn der [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst startet, wird eine neue Sitzung erstellt und die **sysjobactivity** -Tabelle in der **msdb** -Datenbank wird mit allen vorhandenen definierten Aufträgen aufgefüllt. In dieser Tabelle werden die aktuelle Auftragsaktivität und der aktuelle Auftragsstatus aufgezeichnet. Mithilfe des Auftragsaktivitätsmonitors im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent können Sie den aktuellen Status von Aufträgen anzeigen. Falls der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst unerwartet beendet wird, ersehen Sie aus der **sysjobactivity** -Tabelle, welche Aufträge ausgeführt wurden, als der Dienst beendet wurde.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So zeigen Sie die Auftragsaktivität an mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-job-activity"></a>So zeigen Sie die Auftragsaktivität an  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Auftragsaktivitätsmonitor** , und klicken Sie dann auf **Auftragsaktivitäten anzeigen**.  
  
4.  Im **Auftragsaktivitätsmonitor**können Sie Details zu jedem Auftrag anzeigen, der für diesen Server definiert ist.  
  
5.  Klicken Sie mit der rechten Maustaste auf einen Auftrag. Nun können Sie den Auftrag starten, beenden, aktivieren oder deaktivieren, löschen, dessen Status im Auftragsaktivitätsmonitor aktualisieren oder dessen Verlauf oder Eigenschaften anzeigen.  Um mehrere Aufträge zu starten, beenden, aktivieren, deaktivieren oder aktualisieren, wählen Sie mehrere Zeilen im Auftragsaktivitätsmonitor aus, und klicken Sie mit der rechten Maustaste auf die Auswahl.  
  
6.  Klicken Sie auf **Aktualisieren**, um den Auftragsaktivitätsmonitor zu aktualisieren. Um weniger Zeilen anzuzeigen, klicken Sie auf **Filter** , und geben Sie Filterparameter ein.  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-view-job-activity"></a>So zeigen Sie die Auftragsaktivität an  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- lists activity for all jobs that the current user has permission to view.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobactivity ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_help_jobactivity (Transact-SQL)](http://msdn.microsoft.com/en-us/d344864f-b4d3-46b1-8933-b81dec71f511).  
  
