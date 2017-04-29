---
title: "Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database backups [SQL Server], recovery models
- recovery [SQL Server], recovery model
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], switching
- recovery models [SQL Server], viewing
- database restores [SQL Server], recovery models
- modifying database recovery models
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d848c756eee54184aa10b5553779d0ebf1807366
ms.lasthandoff: 04/11/2017

---
# <a name="view-or-change-the-recovery-model-of-a-database-sql-server"></a>Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird die Vorgehensweise zum Anzeigen oder Ändern der Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]beschrieben. 
  
  Ein *Wiederherstellungsmodell* ist eine Datenbankeigenschaft, die steuert, wie Transaktionen protokolliert werden, ob das Transaktionsprotokoll gesichert werden muss (und kann) und welche Arten von Wiederherstellungsvorgängen verfügbar sind. Es stehen drei Wiederherstellungsmodelle zur Verfügung: einfach, vollständig und massenprotokolliert. Für eine Datenbank wird im Allgemeinen das vollständige oder das einfache Wiederherstellungsmodell verwendet. Eine Datenbank kann jederzeit auf ein anderes Wiederherstellungsmodell umgestellt werden. Die **model** -Datenbank legt das Standardwiederherstellungsmodell der neuen Datenbanken fest.  
  
  Eine ausführlichere Erläuterung zu [Wiederherstellungsmodellen](https://msdn.microsoft.com/library/ms189275.aspx)finden Sie im Artikel [SQL Server-Wiederherstellungsmodelle](https://www.mssqltips.com/sqlservertutorial/2/sql-server-recovery-models/) , der von den Leuten bei [MSSQLTips!](https://www.mssqltips.com/)bereitgestellt wird.
  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  

-   [Back up the transaction log](https://msdn.microsoft.com/library/ms179478.aspx) **before** switching from the [full recovery or bulk-logged recovery model](https://msdn.microsoft.com/library/ms189275.aspx).  
  
-   Beim massenprotokollierten Modell ist keine Zeitpunktwiederherstellung möglich. Wenn Sie Transaktionen im massenprotokollierten Wiederherstellungsmodell ausführen, für die eine Wiederherstellung des Transaktionsprotokolls erforderlich ist, besteht die Gefahr eines Datenverlusts. Um die Wiederherstellbarkeit von Daten im Notfall zu maximieren, wechseln Sie nur unter folgenden Bedingungen zum massenprotokollierten Wiederherstellungsmodell:  
  
    -   Benutzer sind in der Datenbank derzeit nicht zulässig.  
  
    -   Alle während der Massenverarbeitung vorgenommenen Änderungen sind wiederherstellbar, ohne dass dazu eine Protokollsicherung erstellt werden muss, z. B. durch erneute Ausführung der Massenprozesse.  
  
     Wenn Sie beide Bedingungen erfüllen, besteht während der Wiederherstellung eines Transaktionsprotokolls, das unter dem massenprotokollierten Wiederherstellungsmodell gesichert wurde, keine Gefahr eines Datenverlusts.  
  
**Hinweis!** Wenn Sie während eines Massenvorgangs zum vollständigen Wiederherstellungsmodell wechseln, ändert sich die Protokollierung für Massenvorgänge von der minimalen Protokollierung in die vollständige Protokollierung und umgekehrt.  
  
###  <a name="Security"></a> Erforderliche Berechtigungen  
   Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-recovery-model"></a>So zeigen Sie das Wiederherstellungsmodell an oder ändern es  
  
1.  Stellen Sie eine Verbindung mit der entsprechenden Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und klicken Sie danach im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie je nach Datenbank eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken** , und wählen Sie eine Systemdatenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Datenbankeigenschaften** wird geöffnet.  
  
4.  Klicken Sie auf der Seite **Seite auswählen** auf **Optionen**.  
  
5.  Das aktuelle Wiederherstellungsmodell wird im Listenfeld **Wiederherstellungsmodell** angezeigt.  
  
6.  Sie können auch zum Wechseln des Wiederherstellungsmodells eine andere Modellliste auswählen. Die Auswahlmöglichkeiten sind **Vollständig**, **Massenprotokolliert**oder **Einfach**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-view-the-recovery-model"></a>So zeigen Sie das Wiederherstellungsmodell an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie die [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht abgefragt werden muss, um mehr über das Wiederherstellungsmodell der **model** -Datenbank zu erfahren.  
  
```tsql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### <a name="to-change-the-recovery-model"></a>So ändern Sie das Wiederherstellungsmodell  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie Sie das Wiederherstellungsmodell in der `model` -Datenbank in `FULL` mithilfe der `SET RECOVERY` -Option der [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) -Anweisung ändern können.  
  
```tsql  
USE master ;  
ALTER DATABASE model SET RECOVERY FULL ;  
```  
  
##  <a name="FollowUp"></a> Empfehlungen: Nach dem Ändern des Wiederherstellungsmodells  
  
-   **Nach dem Umschalten zwischen dem vollständigen und massenprotokollierten Wiederherstellungsmodell**  
  
    -   Wechseln Sie nach der Ausführung der Massenvorgänge sofort wieder zum vollständigen Wiederherstellungsmodus.  
  
    -   Sichern Sie das Protokoll erneut, nachdem Sie vom massenprotokollierten Wiederherstellungsmodell zurück zum vollständigen Wiederherstellungsmodell gewechselt sind.  
  
        >**HINWEIS:** Ihre Sicherungsstrategie ändert sich nicht. Führen Sie weiterhin regelmäßige Datenbanksicherungen, Protokollsicherungen und differenzielle Sicherungen aus.  
  
-   **Nach dem Umschalten vom einfachen Wiederherstellungsmodell**  
  
    -   Erstellen Sie sofort nach der Umstellung auf das vollständige Wiederherstellungsmodell bzw. das massenprotokollierte Wiederherstellungsmodell eine vollständige oder eine differenzielle Datenbanksicherung, um die Protokollkette zu starten.  
  
        >**HINWEIS:** Die Umstellung auf das vollständige oder das massenprotokollierte Wiederherstellungsmodell wird erst nach der ersten Datensicherung wirksam.  
  
    -   Planen Sie regelmäßige Protokollsicherungen, und aktualisieren Sie dementsprechend Ihren Wiederherstellungsplan.  
  
        > **WICHTIG!** Sichern Sie Ihre Protokolle! Wenn Sie das Transaktionsprotokoll nicht oft genug sichern, kann das Protokoll so stark vergrößert werden, bis kein Speicherplatz mehr verfügbar ist.  
  
-   **Nach dem Umschalten zum einfachen Wiederherstellungsmodell**  
  
    -   Unterbrechen Sie alle geplanten Aufträge, um das Transaktionsprotokoll zu sichern.  
  
    -   Stellen Sie sicher, dass regelmäßige Datenbanksicherungen stattfinden. Datenbanksicherungen müssen regelmäßig durchgeführt werden, damit Ihre Daten geschützt sind und der inaktive Teil des Transaktionsprotokolls abgeschnitten werden kann.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Erstellen eines Auftrags](http://msdn.microsoft.com/library/b35af2b6-6594-40d1-9861-4d5dd906048c)  
  
-   [Deaktivieren oder Aktivieren eines Auftrags](http://msdn.microsoft.com/library/5041261f-0c32-4d4a-8bee-59a6c16200dd)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Datenbankwartungspläne](http://msdn.microsoft.com/library/ms187658.aspx) (in der [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] -Onlinedokumentation)  
  
## <a name="see-also"></a>Siehe auch  
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  

