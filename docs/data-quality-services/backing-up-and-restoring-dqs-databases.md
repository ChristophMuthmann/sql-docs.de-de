---
title: Sichern und Wiederherstellen von DQS-Datenbanken | Microsoft-Dokumentation
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
ms.assetid: f3091f62-2234-4a80-a615-cf14c2a1da85
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce4be3eaa3722fb75363c84c2af3c955c44395d1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="backing-up-and-restoring-dqs-databases"></a>Sichern und Wiederherstellen von DQS-Datenbanken
  In diesem Thema wird beschrieben, wie die DQS-Datenbanken gesichert und wiederhergestellt werden.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen das Kennwort für den Datenbank-Hauptschlüssel kennen, das Sie während der DQS-Serverinstallation angegeben haben.  
  
-   Stellen Sie sicher, dass in DQS keine Aktivitäten oder Prozesse ausgeführt werden. Dies kann mithilfe des Bildschirms **Aktivitätsüberwachung** überprüft werden. Weitere Informationen zum Verwenden dieses Bildschirms finden Sie unter [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md).  
  
-   Stellen Sie sicher, dass keine Benutzer am DQS-Server angemeldet sind.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Das Windows-Benutzerkonto muss ein Mitglied der festen sysadmin-Serverrolle in der SQL Server-Instanz sein, um die Sicherungs- und Wiederherstellungsvorgänge auszuführen.  
  
-   Sie müssen über die Rolle „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um ausgeführte Aktivitäten abzubrechen oder ausgeführte Prozesse in DQS anzuhalten.  
  
##  <a name="BackupRestore"></a> Sichern und Wiederherstellen von DQS-Datenbanken  
  
1.  Starten Sie Microsoft SQL Server Management Studio, und stellen Sie eine Verbindung mit der entsprechenden SQL Server-Instanz her.  
  
2.  Erweitern Sie im Objekt-Explorer den Knoten **Datenbanken** .  
  
3.  Sichern Sie die DQS_STAGING_DATA-Datenbank. Ausführliche Anweisungen zum Sichern einer SQL Server-Datenbank finden Sie unter [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
4.  Sichern Sie die DQS_PROJECTS-Datenbank.  
  
5.  Sichern Sie die DQS_MAIN-Datenbank.  
  
6.  Trennen Sie die Verbindung mit der aktuellen Instanz von SQL Server, und stellen Sie eine Verbindung mit der SQL Server-Instanz her, auf der Sie diese Datenbanken wiederherstellen möchten.  
  
7.  Stellen Sie die DQS_MAIN-Datenbank wieder her. Ausführliche Anweisungen zum Wiederherstellen einer SQL Server-Datenbank finden Sie unter [Wiederherstellen einer Datenbanksicherung (SQL Server Management Studio)](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).  
  
8.  Stellen Sie die DQS_PROJECTS-Datenbank wieder her.  
  
9. Stellen Sie die DQS_STAGING_DATA-Datenbank wieder her.  
  
10. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Server, und klicken Sie dann auf **Neue Abfrage**.  
  
11. Kopieren Sie im Fenster des Abfrage-Editors die folgenden SQL-Anweisungen, und ersetzen Sie *\<KENNWORT>* durch das Kennwort, das Sie während der DQS-Installation für den Datenbank-Hauptschlüssel angegeben haben:  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    EXECUTE [internal_core].[RestoreDQDatabases] '<PASSWORD>'  
    GO  
  
    ```  
  
12. Drücken Sie F5, um die Anweisungen auszuführen. Überprüfen Sie im Bereich **Ergebnisse** , ob die Anweisungen erfolgreich ausgeführt wurden.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von DQS-Datenbanken](../data-quality-services/manage-dqs-databases.md)  
  
  
