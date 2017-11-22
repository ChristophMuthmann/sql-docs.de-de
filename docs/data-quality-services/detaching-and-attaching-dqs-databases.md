---
title: "Trennen und Anfügen von DQS-Datenbanken | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 830e33bc-dd15-4f8e-a4ac-d8634b78fe45
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87883705cb8af3f2e5d1d9cc8bb457ec94773441
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="detaching-and-attaching-dqs-databases"></a>Trennen und Anfügen von DQS-Datenbanken
  In diesem Thema wird beschrieben, wie DQS-Datenbanken getrennt und angefügt werden.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Limitations"></a> Einschränkungen  
 Eine Liste der Einschränkungen finden Sie unter [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md)getrennt wird.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Stellen Sie sicher, dass in DQS keine Aktivitäten oder Prozesse ausgeführt werden. Dies kann mithilfe des Bildschirms **Aktivitätsüberwachung** überprüft werden. Weitere Informationen zum Verwenden dieses Bildschirms finden Sie unter [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md).  
  
-   Stellen Sie sicher, dass keine Benutzer beim [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]angemeldet sind.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Das Windows-Benutzerkonto muss Mitglied der festen Serverrolle db_owner in der SQL Server-Instanz sein, damit DQS-Datenbanken getrennt werden können.  
  
-   Das Windows-Benutzerkonto muss über die Berechtigung CREATE DATABASE, CREATE ANY DATABASE oder ALTER ANY DATABASE verfügen, damit eine Datenbank angefügt werden kann.  
  
-   Sie müssen über die Rolle „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um ausgeführte Aktivitäten abzubrechen oder ausgeführte Prozesse in DQS anzuhalten.  
  
##  <a name="Detach"></a> Trennen von DQS-Datenbanken  
 Wenn Sie eine DQS-Datenbank unter Verwendung von SQL Server Management Studio trennen, verbleiben die getrennten Dateien auf dem Computer und können erneut an dieselbe SQL Server-Instanz angefügt oder auf einen anderen Server verschoben und dort angefügt werden. Die DQS-Datenbankdateien befinden sich auf dem Data Quality Services-Computer normalerweise im folgenden Ordner: C:\Programme\Microsoft SQL Server\MSSQL13.*<Instanzname>*\MSSQL\DATA.  
  
1.  Starten Sie Microsoft SQL Server Management Studio, und stellen Sie eine Verbindung mit der entsprechenden SQL Server-Instanz her.  
  
2.  Erweitern Sie im Objekt-Explorer den Knoten **Datenbanken** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die **DQS_MAIN** -Datenbank, zeigen Sie auf **Tasks**, und klicken Sie dann auf **Trennen**. Das Dialogfeld **Datenbank trennen** wird angezeigt.  
  
4.  Aktivieren Sie das Kontrollkästchen unter der Spalte **Löschen** , und klicken Sie auf **OK** , um die DQS_MAIN-Datenbank zu trennen.  
  
5.  Wiederholen Sie Schritt 3 und 4 für die DQS_PROJECTS- und DQS_STAGING_DATA-Datenbank, um sie zu trennen.  
  
 DQS-Datenbanken können auch unter Verwendung der Transact-SQL-Anweisungen mit der gespeicherten Prozedur sp_detach_db getrennt werden. Weitere Informationen zum Trennen von Datenbanken mithilfe von Transact-SQL-Anweisungen finden Sie unter [Using Transact-SQL](../relational-databases/databases/detach-a-database.md#TsqlProcedure) in [Detach a Database](../relational-databases/databases/detach-a-database.md).  
  
##  <a name="Attach"></a> Anfügen von DQS-Datenbanken  
 In den folgenden Anweisungen wird erläutert, wie Sie eine DQS-Datenbank an dieselbe SQL Server-Instanz (von der sie getrennt wurde) oder an eine andere SQL Server-Instanz anfügen, auf der [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] installiert wurde.  
  
1.  Starten Sie Microsoft SQL Server Management Studio, und stellen Sie eine Verbindung mit der entsprechenden SQL Server-Instanz her.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **Datenbanken**, und klicken Sie dann auf **Anfügen**. Das Dialogfeld **Datenbanken anfügen** wird angezeigt.  
  
3.  Klicken Sie auf **Hinzufügen**, um die anzufügende Datenbank anzugeben. Das Dialogfeld **Datenbankdateien suchen** wird angezeigt.  
  
4.  Wählen Sie das Laufwerk aus, auf dem die Datenbank gespeichert ist, und erweitern Sie die Verzeichnisstruktur, um die MDF-Datei der Datenbank zu suchen und auszuwählen. Beispiel für die DQS_MAIN-Datenbank:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\DQS_MAIN.mdf  
    ```  
  
5.  Im (unteren) Bereich **Datenbankdetails** werden die Namen der anzufügenden Dateien angezeigt. Um den Pfadnamen einer Datei zu überprüfen bzw. zu ändern, klicken Sie auf die Schaltfläche **Durchsuchen** (…).  
  
6.  Klicken Sie auf **OK** , um die DQS_MAIN-Datenbank anzufügen.  
  
7.  Wiederholen Sie Schritt 2 bis 6 für die DQS_PROJECTS- und DQS_STAGING_DATA-Datenbank, um sie anzufügen.  
  
8.  Sie müssen zusätzlich die Transact-SQL-Anweisungen im nächsten Schritt ausführen, nachdem die DQS_MAIN-Datenbank wiederhergestellt wurde. Andernfalls wird eine Fehlermeldung angezeigt, sobald Sie versuchen, über die Data Quality-Clientanwendung eine Verbindung mit dem Data Quality-Server herzustellen, und es kann keine Verbindung hergestellt werden. Schritt 9 und 10 müssen jedoch nicht ausgeführt werden, wenn Sie gerade die DQS_PROJECTS- oder DQS_STAGING_DATA-Datenbank und nicht die DQS_MAIN-Datenbank angefügt haben.  
  
     Um die Transact-SQL-Anweisungen auszuführen, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Server, und klicken Sie dann auf **Neue Abfrage**.  
  
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
  
 Sie können DQS-Datenbanken auch mithilfe der Transact-SQL-Anweisungen anfügen. Weitere Informationen zum Anfügen von Datenbanken mithilfe von Transact-SQL-Anweisungen finden Sie unter [Using Transact-SQL](../relational-databases/databases/attach-a-database.md#TsqlProcedure) in [Attach a Database](../relational-databases/databases/attach-a-database.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von DQS-Datenbanken](../data-quality-services/manage-dqs-databases.md)  
  
  
