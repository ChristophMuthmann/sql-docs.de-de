---
title: "Statistikaktualisierung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-statistics"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Aktualisieren von Statistiken"
  - "Statistiken [SQL Server], aktualisieren"
ms.assetid: 4b97c0b4-03ff-4cfb-9c3f-3b33290b7a2c
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Statistikaktualisierung
  Sie können Abfrageoptimierungsstatistiken für eine Tabelle oder indizierte Sicht in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]aktualisieren. Standardmäßig nimmt der Abfrageoptimierer erforderliche Updates der Statistiken automatisch vor, um den Abfrageplan zu verbessern. In einigen Fällen können Sie die Abfrageleistung mit UPDATE STATISTICS oder der gespeicherten Prozedur `sp_updatestats` verbessern, um Statistiken häufiger zu aktualisieren, als von der Standardeinstellung vorgegeben.  
  
 Durch das Update von Statistiken wird sichergestellt, dass Abfragen anhand aktueller Statistiken kompiliert werden. Dies führt jedoch dazu, dass Abfragen neu kompiliert werden. Es empfiehlt sich, Statistiken nicht zu oft zu aktualisieren und die Vorteile optimierter Abfragepläne gegen den Zeitaufwand für die Neukompilierung von Abfragen abzuwägen. Die Entscheidung hängt von der verwendeten Anwendung ab. UPDATE STATISTICS-Vorgänge können mithilfe von tempdb die Stichprobenzeilen zum Erstellen von Statistiken sortieren.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So aktualisieren Sie ein Statistikobjekt mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Bei der Verwendung von UPDATE STATISTICS oder beim Vornehmen von Änderungen mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ist für die Tabelle oder Sicht die ALTER-Berechtigung erforderlich. Wenn Sie `sp_updatestats` verwenden, ist die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der Besitz der Datenbank (**dbo**) erforderlich.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So aktualisieren Sie ein Statistikobjekt  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um die Datenbank zu erweitern, in der Sie die Statistik aktualisieren möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, in der Sie die Statistik aktualisieren möchten.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Statistik** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Statistikobjekt, das Sie aktualisieren möchten, und wählen Sie **Eigenschaften**.  
  
6.  Aktivieren Sie im Dialogfeld **Statistikeigenschaften –***statistics_name* das Kontrollkästchen **Statistiken für diese Spalten aktualisieren** und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So aktualisieren Sie ein bestimmtes Statistikobjekt  
  
1.  Stellen Sie im Objekt-Explorer ** **eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example updates the statistics for the AK_SalesOrderDetail_rowguid index of the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;   
    GO  
    ```  
  
#### So aktualisieren Sie alle Statistiken in einer Tabelle  
  
1.  Stellen Sie im Objekt-Explorer ** **eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all indexes on the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail;   
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md).  
  
#### So aktualisieren Sie alle Statistiken in einer Datenbank  
  
1.  Stellen Sie im Objekt-Explorer ** **eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all tables in the database.   
    EXEC sp_updatestats;  
    ```  
  
 Weitere Informationen finden Sie unter [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md).  
  
  