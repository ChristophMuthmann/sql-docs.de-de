---
title: "&#196;ndern der Rollen zwischen prim&#228;rem und sekund&#228;rem Protokollversandserver (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Protokollversand [SQL Server], Rollenänderungen"
  - "Sekundäre Datendateien [SQL Server], Rollenänderung zwischen"
  - "Primäre Datenbanken [SQL Server]"
  - "Erste Rollenänderung [SQL Server]"
  - "Protokollversand [SQL Server-Agent], Failover"
  - "Failover [SQL Server], Protokollversand"
ms.assetid: 2d7cc40a-47e8-4419-9b2b-7c69f700e806
caps.latest.revision: 20
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 20
---
# &#196;ndern der Rollen zwischen prim&#228;rem und sekund&#228;rem Protokollversandserver (SQL Server)
  Nachdem Sie für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Protokollversandkonfiguration ein Failover zu einem sekundären Server ausgeführt haben, können Sie die sekundäre Datenbank so konfigurieren, dass sie als primäre Datenbank fungiert. Anschließend können Sie primäre und sekundäre Datenbanken je nach Bedarf austauschen.  
  
## Ausführen der ersten Rollenänderung  
 Bei erstmaligem Failover zu einer sekundären Datenbank und einer anschließenden Konfiguration als neuer primärer Datenbank müssen Sie mehrere Schritte ausführen. Nachdem Sie diese anfänglichen Schritte ausgeführt haben, können Sie die Rollen zwischen der primären und sekundären Datenbank problemlos wechseln.  
  
1.  Führen Sie ein manuelles Failover von der primären Datenbank zu einer sekundären Datenbank aus. Sichern Sie das aktive Transaktionsprotokoll auf dem primären Server mit NORECOVERY. Weitere Informationen finden Sie unter [Failover zu einer sekundären Datenbank für den Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md).  
  
2.  Deaktivieren Sie den Protokollversand-Sicherungsauftrag auf dem ursprünglichen primären Server, und kopieren Sie die Aufträge auf den ursprünglichen sekundären Server, um sie dort wiederherzustellen.  
  
3.  Konfigurieren Sie für die sekundäre Datenbank (die neue primäre Datenbank) den Protokollversand mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Weitere Informationen finden Sie unter [Konfigurieren des Protokollversands &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md). Berücksichtigen Sie folgende Punkte:  
  
    1.  Verwenden Sie dieselbe Freigabe zum Erstellen von Sicherungen, die Sie für den ursprünglichen primären Server erstellt haben.  
  
    2.  Geben Sie beim Hinzufügen der sekundären Datenbank im Dialogfeld **Einstellungen für die sekundäre Datenbank** im Feld **Sekundäre Datenbank** den Namen der ursprünglichen primären Datenbank ein.  
  
    3.  Wählen Sie im Dialogfeld **Einstellungen für die sekundäre Datenbank** die Option **Nein, die sekundäre Datenbank ist initialisiert**aus.  
  
4.  Wenn für die frühere Protokollversandkonfiguration die Protokollversandüberwachung aktiviert war, konfigurieren Sie die Protokollversandüberwachung neu, sodass die neue Protokollversandkonfiguration überwacht wird.  Führen Sie die folgenden Befehle aus, und ersetzen Sie *database_name* durch den Namen Ihrer Datenbank:  
  
    1.  **Auf dem neuen primären Server**  
  
         Führen Sie die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen aus:  
  
        ```  
        -- Statement to execute on the new primary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_secondary_database @secondary_database = N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
    2.  **Auf dem neuen sekundären Server**  
  
         Führen Sie die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen aus:  
  
        ```  
        -- Statement to execute on the new secondary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_primary_database @database=N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
## Tauschen der Rollen  
 Nachdem Sie die oben aufgeführten Schritte für den erstmaligen Rollenwechsel ausgeführt haben, können Sie die Rollen zwischen der primären und der sekundären Datenbank mithilfe der im folgenden Abschnitt beschriebenen Schritte tauschen. Führen Sie für einen Rollenwechsel die folgenden allgemeinen Schritte aus:  
  
1.  Schalten Sie die sekundäre Datenbank online. Sichern Sie das Transaktionsprotokoll auf dem primären Server mit NORECOVERY.  
  
2.  Deaktivieren Sie den Protokollversand-Sicherungsauftrag auf dem ursprünglichen primären Server, und kopieren Sie die Aufträge auf den ursprünglichen sekundären Server, um sie dort wiederherzustellen.  
  
3.  Aktivieren Sie den Protokollversand-Sicherungsauftrag auf dem sekundären Server (dem neuen primären Server), und kopieren Sie die Aufträge auf den primären Server (den neuen sekundären Server), um sie dort wiederherzustellen.  
  
> [!IMPORTANT]  
>  Wenn sich der Wechsel zwischen sekundärer und primärer Datenbank für Benutzer und Anwendungen so reibungslos wie möglich gestalten soll, müssen Sie ggf. einige oder alle Metadaten für die Datenbank, wie z. B. Anmeldenamen und Aufträge, auf der neuen primären Serverinstanz neu erstellen. Weitere Informationen finden Sie unter [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Failover zu einer sekundären Datenbank für den Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Verwaltung von Anmeldenamen und Aufträgen nach einem Rollenwechsel &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## Siehe auch  
 [Protokollversandtabellen und gespeicherte Prozeduren](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  