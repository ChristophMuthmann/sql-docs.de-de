---
title: "Entfernen von veralteten Dateigruppen (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Schrittweise Wiederherstellungen [SQL Server], veraltete Dateigruppen"
  - "Veraltete Dateigruppen"
  - "Wiederherstellen von Dateigruppen [SQL Server]"
  - "Verzögerte Transaktionen"
  - "Dateigruppen [SQL Server], veraltet"
  - "Nicht wiederhergestellte Dateigruppen"
ms.assetid: 055f9c6a-5c18-4942-98e7-ec918f0ff975
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# Entfernen von veralteten Dateigruppen (SQL Server)
  In diesem Thema wird beschrieben, wie veraltete Dateigruppen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]entfernt werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
-   [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So entfernen Sie veraltete Dateigruppen mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Dieses Thema ist nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken relevant, die mehrere Dateien oder Dateigruppen enthalten, und unter dem einfachen Wiederherstellungsmodell nur für schreibgeschützte Dateigruppen.  
  
-   Alle Dateien in einer Dateigruppe erhalten den Status "defunct", wenn eine Offlinedateigruppe entfernt wird.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn eine nicht wiederhergestellte Dateigruppe auch zu keinem späteren Zeitpunkt mehr wiederhergestellt werden soll, können Sie sie als *veraltet* aus der Datenbank entfernen. Die veraltete Dateigruppe kann zu keinem Zeitpunkt in dieser Datenbank wiederhergestellt werden, die zugehörigen Metadaten bleiben jedoch erhalten. Nachdem die Dateigruppe veraltet ist, d. h. außer Kraft gesetzt wurde, kann die Datenbank neu gestartet werden, und durch die Wiederherstellung wird die Datenbank über alle wiederhergestellten Dateigruppen hinweg konsistent.  
  
     Eine Dateigruppe außer Kraft zu setzen, stellt eine Option zum Auflösen verzögerter Transaktionen dar, die durch eine Offline-Dateigruppe ausgelöst wurden, die nicht mehr in der Datenbank enthalten sein soll. Transaktionen, die sich verzögert haben, weil eine Dateigruppe offline ist, befinden sich, nachdem eine Dateigruppe außer Kraft gesetzt wird, nicht mehr im Verzögerungsmodus. Weitere Informationen finden Sie unter [Markierte Transaktionen&#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So entfernen Sie veraltete Dateigruppen  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf die Datenbank, aus der Sie die Datei löschen möchten, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Wählen Sie die Seite **Dateien** aus.  
  
4.  Wählen Sie im Raster **Datenbankdateien** die zu löschende Datei aus, klicken Sie auf **Entfernen**und dann auf **OK**.  
  
5.  Wählen Sie die Seite **Dateigruppen** aus.  
  
6.  Wählen Sie im Raster **Zeilen** die zu löschende Dateigruppe aus, klicken Sie auf **Entfernen**und dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So entfernen Sie veraltete Dateigruppen  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. (**Hinweis:** Bei diesem Beispiel wird vorausgesetzt, dass die Dateien und die Dateigruppen bereits vorhanden sind. Weitere Informationen zum Erstellen dieser Objekte finden Sie in Beispiel B im Thema [ALTER DATABASE-Optionen Datei und Dateigruppe](../Topic/ALTER%20DATABASE%20File%20and%20Filegroup%20Options%20\(Transact-SQL\).md).) Im ersten Beispiel werden die `test1dat3`- und `test1dat4`-Dateien aus der veralteten Dateigruppe unter Verwendung der `ALTER DATABASE`-Anweisung mit der `REMOVE FILE`-Klausel entfernt. Im zweiten Beispiel wird die veraltete Dateigruppe `Test1FG1` mithilfe der `REMOVE FILEGROUP`-Klausel entfernt.  
  
```tsql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat3 ;  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4 ;  
GO  
  
```  
  
```tsql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILEGROUP Test1FG1 ;  
GO  
  
```  
  
## Siehe auch  
 [ALTER DATABASE-Optionen Datei und Dateigruppe &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20File%20and%20Filegroup%20Options%20\(Transact-SQL\).md)   
 [Markierte Transaktionen &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)   
 [Dateiwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Dateiwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Onlinewiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  