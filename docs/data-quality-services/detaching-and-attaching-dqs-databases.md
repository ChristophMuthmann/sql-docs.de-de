---
title: "Trennen und Anf&#252;gen von DQS-Datenbanken | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 830e33bc-dd15-4f8e-a4ac-d8634b78fe45
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Trennen und Anf&#252;gen von DQS-Datenbanken
  In diesem Thema wird beschrieben, wie DQS-Datenbanken getrennt und angefügt werden.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Limitations"></a> Einschränkungen  
 Eine Liste der Einschränkungen, finden Sie unter [Datenbank trennen und Anfügen & #40; SQL Server & #41;](../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Stellen Sie sicher, dass in DQS keine Aktivitäten oder Prozesse ausgeführt werden. Dies kann mithilfe des Bildschirms **Aktivitätsüberwachung** überprüft werden. Weitere Informationen zum Verwenden dieses Bildschirms finden Sie unter [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md).  
  
-   Stellen Sie sicher, dass keine Benutzer beim [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]angemeldet sind.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Das Windows-Benutzerkonto muss Mitglied der festen Serverrolle db_owner in der SQL Server-Instanz sein, damit DQS-Datenbanken getrennt werden können.  
  
-   Das Windows-Benutzerkonto muss über die Berechtigung CREATE DATABASE, CREATE ANY DATABASE oder ALTER ANY DATABASE verfügen, damit eine Datenbank angefügt werden kann.  
  
-   Sie müssen über die Rolle „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um ausgeführte Aktivitäten abzubrechen oder ausgeführte Prozesse in DQS anzuhalten.  
  
##  <a name="Detach"></a> Trennen von DQS-Datenbanken  
 Wenn Sie eine DQS-Datenbank unter Verwendung von SQL Server Management Studio trennen, verbleiben die getrennten Dateien auf dem Computer und können erneut an dieselbe SQL Server-Instanz angefügt oder auf einen anderen Server verschoben und dort angefügt werden. Die DQS-Datenbankdateien stehen in der Regel am folgenden Speicherort auf Ihrem Computer Data Quality Services: C:\Program Files\Microsoft SQL Server\MSSQL13.*\< Instanzname >*\MSSQL\DATA.  
  
1.  Starten Sie Microsoft SQL Server Management Studio, und stellen Sie eine Verbindung mit der entsprechenden SQL Server-Instanz her.  
  
2.  Erweitern Sie im Objekt-Explorer den Knoten **Datenbanken** .  
  
3.  Mit der rechten Maustaste die **DQS_MAIN** Datenbank, zeigen Sie auf **Aufgaben**, und klicken Sie dann auf **trennen**. Das Dialogfeld **Datenbank trennen** wird angezeigt.  
  
4.  Wählen Sie das Kontrollkästchen unter der **Löschen** Spalte, und klicken Sie auf **OK** zum Trennen der Datenbank DQS_MAIN.  
  
5.  Wiederholen Sie Schritt 3 und 4 für die DQS_PROJECTS- und DQS_STAGING_DATA-Datenbank, um sie zu trennen.  
  
 DQS-Datenbanken können auch unter Verwendung der Transact-SQL-Anweisungen mit der gespeicherten Prozedur sp_detach_db getrennt werden. Weitere Informationen zum Trennen von Datenbanken mithilfe von Transact-SQL-Anweisungen finden Sie unter [mit Transact-SQL](../relational-databases/databases/detach-a-database.md#TsqlProcedure) in [Trennen einer Datenbank](../relational-databases/databases/detach-a-database.md).  
  
##  <a name="Attach"></a> Anfügen von DQS-Datenbanken  
 In den folgenden Anweisungen wird erläutert, wie Sie eine DQS-Datenbank an dieselbe SQL Server-Instanz (von der sie getrennt wurde) oder an eine andere SQL Server-Instanz anfügen, auf der [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] installiert wurde.  
  
1.  Starten Sie Microsoft SQL Server Management Studio, und stellen Sie eine Verbindung mit der entsprechenden SQL Server-Instanz her.  
  
2.  Im Objekt-Explorer mit der rechten Maustaste **Datenbanken**, und klicken Sie dann auf **Anfügen**. Das Dialogfeld **Datenbanken anfügen** wird angezeigt.  
  
3.  Klicken Sie auf **Hinzufügen**, um die anzufügende Datenbank anzugeben. Das Dialogfeld **Datenbankdateien suchen** wird angezeigt.  
  
4.  Wählen Sie das Laufwerk aus, auf dem die Datenbank gespeichert ist, und erweitern Sie die Verzeichnisstruktur, um die MDF-Datei der Datenbank zu suchen und auszuwählen. Beispiel für die DQS_MAIN-Datenbank:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\DQS_MAIN.mdf  
    ```  
  
5.  Die **Datenbankdetails** (unten) zeigt die Namen der Dateien, die angefügt werden. Um zu überprüfen, oder ändern den Pfadnamen einer Datei, klicken Sie auf die **Durchsuchen** Schaltfläche (...).  
  
6.  Klicken Sie auf **OK** zum Anfügen der Datenbank DQS_MAIN.  
  
7.  Wiederholen Sie Schritt 2 bis 6 für die DQS_PROJECTS- und DQS_STAGING_DATA-Datenbank, um sie anzufügen.  
  
8.  Sie müssen zusätzlich die Transact-SQL-Anweisungen im nächsten Schritt ausführen, nachdem die DQS_MAIN-Datenbank wiederhergestellt wurde. Andernfalls wird eine Fehlermeldung angezeigt, sobald Sie versuchen, über die Data Quality-Clientanwendung eine Verbindung mit dem Data Quality-Server herzustellen, und es kann keine Verbindung hergestellt werden. Schritt 9 und 10 müssen jedoch nicht ausgeführt werden, wenn Sie gerade die DQS_PROJECTS- oder DQS_STAGING_DATA-Datenbank und nicht die DQS_MAIN-Datenbank angefügt haben.  
  
     Führen Sie die Transact-SQL-Anweisungen im Objekt-Explorer auf dem Server, und klicken Sie dann auf **neue Abfrage**.  
  
9. Geben Sie im Fenster Abfrage-Editor die folgenden SQL-Anweisungen ein:  
  
    ```  
    ALTER DATABASE [DQS_MAIN] SET TRUSTWORTHY ON;  
    EXEC sp_configure 'clr enabled', 1;  
    RECONFIGURE WITH OVERRIDE  
    ALTER DATABASE [DQS_MAIN] SET ENABLE_BROKER  
    ALTER AUTHORIZATION ON DATABASE::[DQS_MAIN] TO [##MS_dqs_db_owner_login##]  
    ALTER AUTHORIZATION ON DATABASE::[DQS_PROJECTS] TO [##MS_dqs_db_owner_login##]  
  
    ```  
  
10. Drücken Sie F5, um die Anweisungen auszuführen. Überprüfen Sie im Ergebnisbereich, ob die Anweisungen erfolgreich ausgeführt wurden. Die folgende Meldung wird angezeigt: `Configuration option 'clr enabled' changed from 1 to 1. Run the RECONFIGURE statement to install.`  
  
11. Stellen Sie über den Data Quality-Client eine Verbindung mit dem Data Quality-Server her, um zu überprüfen, ob erfolgreich eine Verbindung hergestellt werden kann.  
  
 Sie können DQS-Datenbanken auch mithilfe der Transact-SQL-Anweisungen anfügen. Weitere Informationen zum Anfügen von Datenbanken mithilfe von Transact-SQL-Anweisungen finden Sie unter [mit Transact-SQL](../relational-databases/databases/attach-a-database.md#TsqlProcedure) in [Anfügen einer Datenbank](../relational-databases/databases/attach-a-database.md).  
  
## Siehe auch  
 [Verwalten von DQS-Datenbanken](../data-quality-services/manage-dqs-databases.md)  
  
  