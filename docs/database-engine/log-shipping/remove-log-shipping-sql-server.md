---
title: "Entfernen des Protokollversands (SQL Server) | Microsoft Docs"
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
  - "Protokollversand [SQL Server], entfernen"
  - "Entfernen des Protokollversands"
  - "Löschen des Protokollversands"
ms.assetid: 859373db-c744-4a4b-8479-45163f61e8cb
caps.latest.revision: 18
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 18
---
# Entfernen des Protokollversands (SQL Server)
  In diesem Thema wird beschrieben, wie der Protokollversand in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]entfernt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So entfernen Sie den Protokollversand mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die gespeicherten Prozeduren für den Protokollversand erfordern die Mitgliedschaft in der festen Serverrolle **sysadmin**.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So entfernen Sie den Protokollversand  
  
1.  Stellen Sie eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, die derzeit als primärer Server für den Protokollversand verwendet wird, und erweitern Sie diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf die primäre Datenbank für den Protokollversand, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie unter **Seite auswählen**auf **Transaktionsprotokollversand**.  
  
4.  Entfernen Sie das Kontrollkästchen vor **Diese Datenbank als primäre Datenbank in einer Protokollversandkonfiguration aktivieren** .  
  
5.  Klicken Sie auf **OK** , um den Protokollversand aus dieser primären Datenbank zu entfernen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So entfernen Sie den Protokollversand  
  
1.  Führen Sie auf dem primären Server für den Protokollversand [sp_delete_log_shipping_primary_secondary](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql.md) aus, um die Informationen zur sekundären Datenbank vom primären Server zu löschen.  
  
2.  Führen Sie auf dem sekundären Server für den Protokollversand [sp_delete_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md) aus, um die sekundäre Datenbank zu löschen.  
  
    > [!NOTE]  
    >  Falls keine anderen sekundären Datenbanken mit der gleichen sekundären ID vorhanden sind, wird **sp_delete_log_shipping_secondary_primary** von **sp_delete_log_shipping_secondary_database** aufgerufen und löscht den Eintrag für die sekundäre ID sowie die Kopier- und Wiederherstellungsaufträge.  
  
3.  Führen Sie auf dem primären Server für den Protokollversand **sp_delete_log_shipping_primary_database** aus, um die Informationen zur Protokollversandkonfiguration vom primären Server zu löschen. Dadurch wird auch der Sicherungsauftrag gelöscht.  
  
4.  Deaktivieren Sie auf dem primären Server für den Protokollversand den Sicherungsauftrag. Weitere Informationen finden Sie unter [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md).  
  
5.  Deaktivieren Sie auf dem sekundären Server für den Protokollversand den Kopier- und Wiederherstellungsauftrag.  
  
6.  Wenn Sie die sekundäre Datenbank für den Protokollversand nicht mehr verwenden, können Sie sie auch vom sekundären Server löschen.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Aktualisieren des Protokollversands auf SQL Server 2016 &#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Konfigurieren des Protokollversands &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
-   [Hinzufügen einer sekundären Datenbank zu einer Protokollversandkonfiguration &#40;SQL Server&#41;](../../database-engine/log-shipping/add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [Entfernen einer sekundären Datenbank aus einer Protokollversandkonfiguration &#40;SQL Server&#41;](../../database-engine/log-shipping/remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [Überwachen des Protokollversands &#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
-   [Failover zu einer sekundären Datenbank für den Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Deaktivieren oder Aktivieren eines Auftrags](../../ssms/agent/disable-or-enable-a-job.md)  
  
## Siehe auch  
 [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Protokollversandtabellen und gespeicherte Prozeduren](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  