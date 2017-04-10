---
title: "Anhalten oder Fortsetzen einer Datenbank-Spiegelungssitzung (SQL Server) | Microsoft Docs"
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
  - "Fortsetzen der Datenbankspiegelung"
  - "Datenbankspiegelung [SQL Server], Sitzungen"
  - "Datenbankspiegelung [SQL Server], anhalten"
  - "Datenbankspiegelung [SQL Server], fortsetzen"
  - "Anhalten der Datenbankspiegelung"
ms.assetid: 05ede3b4-6abe-4442-abb7-9f5aee1d6bc0
caps.latest.revision: 34
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 34
---
# Anhalten oder Fortsetzen einer Datenbank-Spiegelungssitzung (SQL Server)
  In diesem Thema wird beschrieben, wie Sie eine Datenbankspiegelung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]anhalten oder fortsetzen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So ReplaceThisText mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Anhalten oder Fortsetzen der Datenbankspiegelung](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 Eine Datenbank-Spiegelungssitzung kann jederzeit angehalten werden. Dadurch kann die Leistung bei Engpässen ggf. verbessert werden, und anschließend können Sie die angehaltene Sitzung jederzeit fortsetzen.  
  
> [!CAUTION]  
>  Nach einem erzwungenen Dienst, wenn der ursprüngliche Prinzipalserver die Verbindung wiederherstellt, wird die Spiegelung angehalten. Das Fortsetzen der Spiegelung in dieser Situation könnte auf dem ursprünglichen Prinzipalserver zu Datenverlust führen. Informationen zum Verwalten des potenziellen Datenverlusts finden Sie unter [Rollenwechsel während einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Eine Datenbank-Spiegelungssitzung können Sie auf der Seite **Spiegelung** der Datenbankeigenschaften anhalten bzw. fortsetzen.  
  
#### So halten Sie eine Datenbankspiegelung an bzw. setzen sie fort  
  
1.  Stellen Sie während einer Datenbank-Spiegelungssitzung eine Verbindung mit der Prinzipalserverinstanz her, und klicken Sie im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie die Datenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, wählen Sie **Tasks** aus, und klicken Sie anschließend auf **Spiegeln**. Dadurch wird die Seite **Spiegelung** im Dialogfeld **Datenbankeigenschaften** geöffnet.  
  
4.  Klicken Sie zum Anhalten der Sitzung auf **Anhalten**.  
  
     Wenn Sie in der Bestätigungsaufforderung auf **Ja**klicken, wird die Sitzung angehalten und die Schaltfläche erhält die Bezeichnung **Fortsetzen**.  
  
     Weitere Informationen über die Auswirkung des Anhaltens einer Sitzung finden Sie unter [Anhalten und Fortsetzen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md).  
  
5.  Klicken Sie zum Fortsetzen der Sitzung auf **Fortsetzen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So halten Sie die Datenbankspiegelung an  
  
1.  Stellen Sie für einen der Partner eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Führen Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aus:  
  
     ALTER DATABASE *Datenbankname* SET PARTNER SUSPEND  
  
     wobei *Datenbankname* für die gespiegelte Datenbank steht, deren Sitzung Sie anhalten möchten.  
  
     Im folgenden Beispiel wird die Beispieldatenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] angehalten.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER SUSPEND;  
    ```  
  
##### So setzen Sie die Datenbankspiegelung fort  
  
1.  Stellen Sie für einen der Partner eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Führen Sie die folgende Transact-SQL-Anweisung aus:  
  
     ALTER DATABASE *Datenbankname* SET PARTNER RESUME  
  
     wobei *Datenbankname* für die gespiegelte Datenbank steht, deren Sitzung Sie fortsetzen möchten.  
  
     Im folgenden Beispiel wird die Beispieldatenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] angehalten.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER RESUME;  
    ```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Anhalten oder Fortsetzen der Datenbankspiegelung  
  
-   **Nach dem Anhalten der Datenbankspiegelung**  
  
     Treffen Sie auf der primären Datenbank entsprechende Vorkehrungen, um ein Überlaufen des Transaktionsprotokolls zu verhindern. Weitere Informationen finden Sie im [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
-   **Nach dem Fortsetzen der Datenbankspiegelung**  
  
     Durch das Fortsetzen einer Datenbankspiegelung wird die Spiegeldatenbank in den SYNCHRONIZING-Status gesetzt. Ist die Sicherheitsstufe auf FULL festgelegt, holt der Spiegel den aktuellen Verarbeitungsstand des Prinzipals auf, und die Spiegeldatenbank geht in den SYNCHRONIZED-Status über. Zu diesem Zeitpunkt ist das Ausführen eines Failovers möglich. Ist der Zeuge vorhanden und auf ON festgelegt, ist ein automatisches Failover möglich. Bei Abwesenheit eines Zeugen ist ein manuelles Failover möglich.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
## Siehe auch  
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  