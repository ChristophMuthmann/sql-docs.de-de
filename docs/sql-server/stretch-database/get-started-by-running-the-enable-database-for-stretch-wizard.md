---
title: "Erste Schritte durch Ausf&#252;hren des Assistenten zum Aktivieren von Stretch f&#252;r eine Datenbank | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "08/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
f1_keywords: 
  - "sql13.swb.stretchwizard.f1"
  - "sql13.swb.stretchwizard.createdatabasecredentials.f1"
  - "sql13.swb.stretchwizard.selectdatabasetables.f1"
  - "sql13.swb.stretchwizard.validatesqlserver.f1"
  - "sql13.swb.stretchwizard.selectazuredeployment.f1"
  - "sql13.swb.stretchwizard.configureazuredeployment.f1"
  - "sql13.swb.stretchwizard.Summary.f1"
  - "sql13.swb.stretchwizard.Results.f1"
  - "sql13.swb.stretchwizard.introduction.f1"
helpviewer_keywords: 
  - "Stretch-Datenbank-Assistent"
  - "Assistent zum Aktivieren von Stretch für eine Datenbank"
ms.assetid: 855dd9fc-f80c-4dbc-bf46-55a9736bfe15
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Erste Schritte durch Ausf&#252;hren des Assistenten zum Aktivieren von Stretch f&#252;r eine Datenbank
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 Um eine Datenbank für Stretch-Datenbank zu konfigurieren, führen Sie den Assistenten zum Aktivieren von Stretch für eine Datenbank aus.  In diesem Thema werden die im Assistenten einzugebenden Informationen und zu treffenden Entscheidungen beschrieben.  
  
 Weitere Informationen zu Stretch-Datenbank finden Sie unter [Stretch Database](../../sql-server/stretch-database/stretch-database.md). 
 
 >   [!NOTE] Wenn Sie Stretch-Datenbank später deaktivieren, sollten Sie daran denken, dass durch die Deaktivierung von Stretch-Datenbank für eine Tabelle oder Datenbank das Remoteobjekt nicht gelöscht wird. Wenn Sie die Remotetabelle oder Remotedatenbank löschen möchten, müssen Sie sie mithilfe des Azure-Verwaltungsportals löschen. Die Remoteobjekte erzeugen weiterhin Azure-Kosten, bis Sie die Objekte manuell löschen. 
  
## Starten des Assistenten  
  
1.  Wählen Sie in SQL Server Management Studio im Objekt-Explorer die Datenbank, für die Sie Stretch aktivieren möchten.  
  
2.  Klicken Sie mit der rechten Maustaste, wählen Sie **Aufgaben**, **Stretch** und dann **Aktivieren** aus, um den Assistenten zu starten.  
  
##  <a name="Intro"></a> Einführung  
 Überprüfen Sie den Zweck des Assistenten und die Voraussetzungen.  
 
 Folgende wichtige Voraussetzungen müssen erfüllt sein.
 -   Sie müssen Administrator sein, um Datenbankeinstellungen ändern zu können.
 -   Sie müssen über ein Microsoft Azure-Abonnement verfügen.
 -   Ihre SQL Server-Instanz muss mit dem Azure-Remoteserver kommunizieren können.
  
 ![Introduction page of Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-1.png "Introduction page of Stretch Database wizard")  
  
##  <a name="Tables"></a> Tabellen auswählen  
 Wählen Sie die Tabellen aus, die Sie für Stretch aktivieren möchten.  
 
Oben in der sortierten Liste werden Tabellen mit einer Vielzahl von Zeilen angezeigt. Bevor der Assistent die Tabellenliste anzeigt, analysiert er die Tabellen, um Datentypen zu ermitteln, die derzeit von der Stretch-Datenbank nicht unterstützt werden. 
  
 ![Select tables page of Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-2.png "Select tables page of Stretch Database wizard")  
  
|Column|Beschreibung|  
|------------|-----------------|  
|(kein Titel)|Aktivieren Sie das Kontrollkästchen in dieser Spalte, um die ausgewählte Tabelle für Stretch zu aktivieren.|  
|**Name**|Gibt den Namen der Tabelle in der Datenbank an.|  
|(kein Titel)|Ein Symbol in dieser Spalte kann auf eine Warnung hinweisen, die Sie nicht daran hindert, die ausgewählte Tabelle für Stretch zu aktivieren. Es kann auch auf ein blockierendes Problem hinweisen, die verhindert, dass Sie die ausgewählte Tabelle für Stretch aktivieren können – z.B. weil die Tabelle einen nicht unterstützten Datentyp verwendet. Zeigen Sie auf das Symbol, um weitere Informationen in einer QuickInfo anzuzeigen. Weitere Informationen finden Sie unter [Einschränkungen für Stretch-Datenbank](../../sql-server/stretch-database/limitations-for-stretch-database.md).|  
|**Gestreckt**|Gibt an, ob die Tabelle bereits für Stretch aktiviert ist.|  
|**Migrieren**|Sie können eine vollständige Tabelle migrieren (**Gesamte Tabelle**) oder einen Filter für eine vorhandene Spalte in der Tabelle angeben. Wenn Sie eine andere Filterfunktion verwenden möchten, um zu migrierende Zeilen auszuwählen, führen Sie nach dem Schließen des Assistenten die Anweisung ALTER TABLE aus, um die Filterfunktion anzugeben. Weitere Informationen zur Filterfunktion finden Sie unter [Auswählen zu migrierender Zeilen mithilfe einer Filterfunktion (Stretch-Datenbank)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Informationen zum Anwenden der Funktion finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) oder [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).|  
|**Zeilen**|Gibt die Zeilenanzahl in der Tabelle an.|  
|**Größe (KB)**|Gibt die Größe der Tabelle in KB an.|  
  
## Optionales Angeben eines Zeilenfilters  
 Wenn Sie zum Auswählen zu migrierender Zeilen eine Filterfunktion verwenden möchten, führen Sie auf der Seite **Tabellen auswählen** die folgenden Schritte aus.  
  
1.  Klicken Sie in der Liste **Wählen Sie die Tabellen aus, die Sie strecken möchten.** in der Zeile für die Tabelle auf **Gesamte Tabelle**. Das Dialogfeld **Wählen Sie die zu streckenden Zeilen aus.** wird geöffnet.  
  
     ![Define a date-based filter predicate](../../sql-server/stretch-database/media/stretch-wizard-2a.png "Define a date-based filter predicate")  
  
2.  Wählen Sie im Dialogfeld **Wählen Sie die zu streckenden Zeilen aus.** die Option **Zeilen auswählen**.  
  
3.  Geben Sie im Feld **Namensfeld** einen Namen für die Filterfunktion an.  
  
4.  Wählen Sie für die **Where**-Klausel eine Spalte aus der Tabelle und einen Operator aus, und geben Sie einen Wert an.  
  
5.  Klicken Sie auf **Überprüfen**, um die Funktion zu testen. Wenn die Funktion Ergebnisse aus der Tabelle zurückgibt, also zu migrierende Zeilen vorhanden sind, die die Bedingung erfüllen, meldet der Test **Erfolg**.  

    >   [!NOTE] Das Textfeld, das die Filterabfrage anzeigt, ist schreibgeschützt. Sie können die Abfrage im Textfeld nicht bearbeiten.
  
6.  Klicken Sie auf „Fertig“, um zur Seite **Tabellen auswählen** zurückzukehren.  

Die Filterfunktion wird in SQL Server erst erstellt, wenn Sie den Assistenten beenden. Bis dahin können Sie zur Seite **Tabellen auswählen** zurückkehren, um die Filterfunktion zu ändern oder umzubenennen.

![Select Tables page after defining a filter predicate](../../sql-server/stretch-database/media/stretch-wizard-2b.png "Select Tables page after defining a filter predicate")

Wenn Sie zum Auswählen zu migrierender Zeilen eine andere Art von Filterfunktion verwenden möchten, führen Sie einen der folgenden Schritte aus.  
  
-   Beenden Sie den Assistenten, und führen Sie die ALTER TABLE-Anweisung aus, um Stretch für die Tabelle zu aktivieren und eine Filterfunktion anzugeben. Weitere Informationen finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
-   Führen Sie die ALTER TABLE-Anweisung aus, um eine Filterfunktion anzugeben, nachdem Sie den Assistenten beendet haben. Die erforderlichen Schritte finden Sie unter [Hinzufügen einer Filterfunktion nach Ausführen des Assistenten](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz).  
  
##  <a name="Configure"></a> Konfigurieren von Azure  
  
1.  Melden Sie sich mit einem Microsoft-Konto bei Azure an.  
  
     ![Sign in to Azure - Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-3.png "Sign in to Azure - Stretch Database wizard")  
  
2.  Wählen Sie das für Stretch-Datenbank zu verwendende vorhandene Azure-Abonnement aus. 

>   [!NOTE] Zum Aktivieren von Stretch für eine Datenbank benötigen Sie Administratorrechte für das verwendete Abonnement. Der Stretch-Datenbank-Assistent zeigt nur Abonnements an, für die der Benutzer über Administratorrechte verfügt.
  
3.  Wählen Sie die für Stretch-Datenbank zu verwendende Azure-Region aus.
    -   Wenn Sie einen neuen Server erstellen, wird der Server in dieser Region erstellt.  
    -   Wenn in der ausgewählten Region Server vorhanden sind, führt der Assistent diese auf, nachdem Sie **Vorhandener Server** ausgewählt haben.
  
     Zum Minimieren der Wartezeit wählen Sie die Azure-Region aus, in der sich Ihr SQL Server befindet. Weitere Informationen zu Regionen finden Sie unter [Azure-Regionen](https://azure.microsoft.com/regions/).  
  
4.  Geben Sie an, ob Sie einen vorhandenen Server verwenden oder einen neuen Azure-Server erstellen möchten.  
  
     Wenn der Active Directory-Dienst auf Ihrem SQL Server mit Azure Active Directory verbunden ist, können Sie optional ein Verbunddienstkonto verwenden, damit SQL Server mit dem Azure-Remoteserver kommunizieren kann. Weitere Informationen zu den Anforderungen für diese Option finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md).  
  
    -   **Erstellen eines neuen Servers**  
  
        1.  Erstellen Sie einen Anmeldenamen und ein Kennwort für den Serveradministrator.  
  
        2.  Verwenden Sie optional ein Verbunddienstkonto, damit SQL Server mit dem Azure-Remoteserver kommunizieren kann.  
  
         ![Create new Azure server - Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-4.png "Create new Azure server - Stretch Database wizard")  
  
    -   **Vorhandener Server**  
  
        1.  Wählen Sie den vorhandenen Azure-Server aus.  
  
        2.  Wählen Sie die Authentifizierungsmethode aus.  
  
            -   Wenn Sie **SQL Server-Authentifizierung** auswählen, geben Sie den Administratorbenutzernamen und das zugehörige Kennwort ein.  
  
            -   Wählen Sie eine **integrierte Active Directory-Authentifizierung** zum Verwenden eines Verbunddienstkontos aus, damit SQL Server mit dem Azure-Remoteserver kommunizieren kann. Wenn der ausgewählte Server nicht in Azure Active Directory integriert ist, wird diese Option nicht angezeigt.
  
         ![Select existing Azure server - Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-5.png "Select existing Azure server - Stretch Database wizard")  
  
##  <a name="Credentials"></a> Sichern der Anmeldeinformationen  
 Sie benötigen einen Datenbank-Hauptschlüssel zum Sichern der Anmeldeinformationen, die Stretch-Datenbank für die Verbindung mit der Remotedatenbank verwendet.  
  
 Wenn der Datenbank-Hauptschlüssel bereits vorhanden ist, geben Sie das zugehörige Kennwort ein.  
  
 ![Secure credentials page of the Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-6b.PNG "Secure credentials page of the Stretch Database wizard")  
  
 Wenn kein Hauptschlüssel für die Datenbank vorhanden ist, geben Sie ein sicheres Kennwort ein, um einen Datenbank-Hauptschlüssel zu erstellen.  
  
 ![Secure credentials page of the Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-6.png "Secure credentials page of the Stretch Database wizard")  
  
 Weitere Informationen zum Datenbank-Hauptschlüssel finden Sie unter [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) und [Erstellen eines Datenbank-Hauptschlüssels](../../relational-databases/security/encryption/create-a-database-master-key.md). Weitere Informationen zu den Anmeldeinformationen, die der Assistent erstellt, finden Sie unter[CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
##  <a name="Network"></a> Auswählen der IP-Adresse  
 Verwenden Sie den IP-Adressbereich des Subnetzes (empfohlen) oder die öffentliche IP-Adresse Ihrer SQL Server-Instanz, um eine Firewallregel in Azure zu erstellen, durch die SQL Server mit dem Azure-Remoteserver kommunizieren kann.  
  
 Die IP-Adressen, die Sie auf dieser Seite bereitstellen, teilen dem Azure-Server mit, dass er von SQL Server initiierte, eingehende Daten, Abfragen und Verwaltungsvorgänge die Azure-Firewall passieren lassen soll. Der Assistent ändert nichts an den Firewalleinstellungen auf dem SQL Server.  
  
 ![Select IP address page of the Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-7.png "Select IP address page of the Stretch Database wizard")  
  
##  <a name="Summary"></a> Zusammenfassung  
 Überprüfen Sie die im Assistenten eingegebenen Werte und ausgewählten Optionen sowie die geschätzten Kosten in Azure. Wählen Sie dann **Fertig stellen** aus, um Stretch zu aktivieren.  
  
 ![Summary page of the Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-8.png "Summary page of the Stretch Database wizard")  
  
##  <a name="Results"></a> Ergebnisse  
 Überprüfen Sie die Ergebnisse.  
  
 Informationen zum Überwachen des Status der Datenmigration finden Sie unter [Überwachung und Problembehandlung bei der Datenmigration &#40;Stretch-Datenbank&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
 ![Results page of the Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-9.PNG "Results page of the Stretch Database wizard")  
  
##  <a name="KnownIssues"></a> Problembehandlung für den Assistenten  
 **Fehler beim Stretch-Datenbank-Assistenten.**  
 Wenn Stretch-Datenbank noch nicht auf Serverebene aktiviert ist und Sie den Assistenten ohne die Systemadministratorberechtigungen zum Aktivieren des Assistenten ausführen, tritt ein Fehler auf. Bitten Sie den Systemadministrator, Stretch-Datenbank auf der lokalen Serverinstanz zu aktivieren, und führen Sie den Assistenten dann erneut aus. Weitere Informationen finden Sie unter [Prerequisite: Permission to enable Stretch Database on the server](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md#EnableTSQLServer).  
  
## Nächste Schritte  
 Aktivieren Sie zusätzliche Tabellen für Stretch-Datenbank. Überwachen Sie die Datenmigration, und verwalten Sie für Stretch aktivierte Datenbanken und Tabellen.  
  
-   Aktivieren zusätzlicher Tabellen mithilfe des Artikels[Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) .  
  
-   [Überwachung und Problembehandlung bei der Datenmigration &#40;Stretch-Datenbank&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) zum Anzeigen des Status der Datenmigration.  
  
-   [Anhalten und Fortsetzen der Datenmigration &#40;Stretch-Datenbank&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Verwalten und Problembehandlung von Stretch-Datenbank](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Sichern von Stretch-aktivierten Datenbanken](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Restore Stretch-enabled databases (Wiederherstellen von für die Streckung aktivierten Datenbanken)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## Siehe auch  
 [Aktivieren von Stretch-Datenbank für eine Datenbank](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  