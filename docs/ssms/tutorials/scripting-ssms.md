---
Title: 'Tutorial: Script Objects in SQL Server Management Studio'
description: Tutorial zur Erstellung von Skripts für Objekte in SSMS
keywords: SQL Server, SSMS, SQL Server Management Studio, Skripts, Skripterstellung
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: 2ee56bc26c22f91af7bf156ea967c19b61eab881
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>Tutorial: Erstellen von Skripts für Objekte in SQL Server Management Studio
In diesem Tutorial erfahren Sie, wie Sie T-SQL-Skripts (Transact-SQL) für verschiedene Objekte in SQL Server Management Studio erstellen können.  Dabei wird die Skripterstellung für die folgenden Objekte beschrieben: 
 - Abfragen beim Ausführen von Aktionen auf der grafischen Benutzeroberfläche
 - Datenbanken (mithilfe der beiden Methoden „Script Database As“ (Skript für Datenbank erstellen als) und „Skript generieren“)
 - Tabellen
 - Gespeicherte Prozeduren
 - Erweiterte Ereignisse

In diesem Tutorial haben Sie erfahren, dass Sie für jedes Objekt im **Objekt-Explorer** ein Skript erstellen können, indem Sie mit der rechten Maustaste darauf klicken und anschließend die Option **Script Object As** (Skript für Objekt als) auswählen. 


## <a name="prerequisites"></a>Voraussetzungen
Zur Durchführung dieses Tutorials benötigen Sie SQL Server Management Studio, Zugriff auf einen SQL-Server und eine AdventureWorks-Datenbank. 

- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Installieren Sie die [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Laden Sie eine [AdventureWorks-Beispieldatenbank](https://github.com/Microsoft/sql-server-samples/releases) herunter. 
    - Anweisungen zum Wiederherstellen von Datenbanken in SSMS finden Sie unter [Restoring a Database (Wiederherstellen einer Datenbank)](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 


## <a name="script-queries-from-gui"></a>Erstellen von Skripts für Abfragen über die grafische Benutzeroberfläche
Beim Ausführen einer Aufgabe über die grafische Benutzeroberfläche in SSMS können Sie gleichzeitig den zugehörigen T-SQL-Code generieren. In den folgenden Beispielen wird dies anhand der Sicherung einer Datenbank und der Verkleinerung eines Transaktionsprotokolls demonstriert.  Die gleichen Schritte lassen sich auf jede Aktion anwenden, die über die grafische Benutzeroberfläche ausgeführt wird. 

### <a name="scriptt-sql-when-backing-up-a-database"></a>Erstellen von T-SQL-Skripts beim Sichern einer Datenbank
1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken** .
3. Klicken Sie mit der rechten Maustaste auf die Datenbank, und rufen Sie anschließend **Aufgaben** > **Back Up...** (Sichern) auf:

    ![Sichern der Datenbank](media/scripting-ssms/backupdb.png)

4. Konfigurieren Sie die Sicherung auf die gewünschte Weise. In diesem Tutorial werden die Standardeinstellungen beibehalten. Wenn Sie jedoch in diesem Fenster Änderungen vornehmen, werden diese auch im Skript übernommen. 
5. Rufen Sie die Option **Skript** > **Script Action to New Query Window** (Skript für Aktion in neuem Abfragefenster erstellen) auf:
 
    ![Skript für Datenbanksicherung](media/scripting-ssms/scriptdbbackup.PNG)
6. Sehen Sie sich den T-SQL-Code im Abfragefenster an: 

    ![Skript für Datenbanksicherung](media/scripting-ssms/dbbackupscript.PNG)


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>Erstellen von T-SQL-Skripts beim Verkleinern des Transaktionsprotokolls
1. Klicken Sie mit der rechten Maustaste auf die Datenbank, und rufen Sie anschließend **Aufgaben** > **Verkleinern** > **Dateien** auf:

     ![Verkleinern von Dateien](media/scripting-ssms/shrinkfiles.png)

2. Wählen Sie aus der Dropdownliste **Dateityp** den Eintrag **Protokoll** aus:

    ![Verkleinern des Transaktionsprotokolls](media/scripting-ssms/shrinktlog.png)

3. Klicken Sie zuerst auf die Option **Skript** und anschließend auf **Script Action to Clipboard** (Skript für Aktion in Zwischenablage erstellen):

    ![Skript in Zwischenablage schreiben](media/scripting-ssms/scriptactiontoclipboard.png)

4. Öffnen Sie über **Neue Abfrage** ein Fenster, und fügen Sie das Skript durch Rechtsklicken und Anklicken der Option **Einfügen** ein:

    ![Einfügen des Skripts](media/scripting-ssms/paste.png)


## <a name="script-databases"></a>Erstellen von Skripts für Datenbanken
Im folgenden Abschnitt erfahren Sie, wie Sie mit den Optionen **Script Database As** (Skript für Datenbank erstellen als) und **Skripts generieren** Skripts für eine Datenbank erstellen.  Mithilfe der Option **Script Database As** (Skript für Datenbank erstellen als) werden die Datenbank und die zugehörigen Konfigurationsoptionen neu erstellt. Durch die Option **Skripts generieren** werden für alle Datenbankobjekte Skripts erstellt, nicht aber für die Daten. Wenn Sie auch für die Daten Skripts erstellen möchten, müssen Sie den [Import/Export-Assistenten](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/start-the-sql-server-import-and-export-wizard) verwenden.  


### <a name="script-database-using-script-option"></a>Erstellen eines Skripts für eine Datenbank mit der Option „Script Database As“ (Skript für Datenbank erstellen als)
1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken** .
3. Klicken Sie mit der rechten Maustaste zuerst auf die Datenbank und anschließend mit der linken auf **Script Database As** (Skript für Datenbank erstellen als):

    ![Erstellen eines Skripts für eine Datenbank](media/scripting-ssms/scriptdb.png)

4. Sehen Sie sich die Datenbankerstellungsabfrage im Fenster an: 

    ![Erstelltes Skript für Datenbank](media/scripting-ssms/scriptedoutdb.png)
    - Mit dieser Option wird nur ein Skript für die Datenbank-Konfigurationsoptionen erstellt.  

### <a name="script-database-using-generate-scripts-option"></a>Erstellen eines Skripts für eine Datenbank mit der Option „Skripts generieren“
1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken** .
3. Klicken Sie mit der rechten Maustaste auf die Datenbank, und rufen Sie anschließend **Aufgaben** > **Skripts generieren** auf:

    ![Generieren von Skripts für eine Datenbank](media/scripting-ssms/generatescriptsfordb.png)

4. Klicken Sie auf **Weiter**. Nun können Sie entweder ein Skript für die gesamte Datenbank oder für bestimmte Datenbankobjekte erstellen: 
 
    ![Generieren von Skripts für Objekte](media/scripting-ssms/scriptobjects.png)
 
5. Wählen Sie **Weiter**aus. Auf diesem Bildschirm können Sie den Speicherort für das Skript festlegen. 
    - Außerdem haben Sie die Möglichkeit, erweiterte Optionen durch einen Klick auf **Erweitert** zu konfigurieren:

    ![Erweiterte Skriptoptionen](media/scripting-ssms/advancedscripts.png)

6. Klicken Sie anschließend solange auf **Weiter**, bis die Skripts erstellt werden und die Schaltfläche **Fertig stellen** angezeigt wird. Das Datenbankskript befindet sich an dem Speicherort, der in Schritt 5 festgelegt wurde. 
    - Dadurch wird ein Skript für das Schema und für die verschiedenen Objekte innerhalb der Datenbank erstellt, jedoch nicht für die Daten. 
 
## <a name="script-tables"></a>Erstellen von Skripts für Tabellen
In diesem Abschnitt wird beschrieben, wie Sie Skripts für Datenbanktabellen erstellen.

1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken**.
3. Erweitern Sie den Datenbankknoten **AdventureWorks**. 
4. Erweitern Sie den Knoten **Tabellen**.
5. Klicken Sie zuerst mit der rechten Maustaste auf die Tabelle, für die Sie ein Skript erstellen möchten, und anschließend mit der linken auf **Script Table as** (Skript für Tabelle erstellen als):
    - Nun stehen mehrere Optionen zur Auswahl. Beispielsweise können Sie eine Tabelle erstellen oder Daten in diese einfügen: 
    
    ![Skripttabelle](media/scripting-ssms/scripttable.png)
 
## <a name="script-stored-procedures"></a>Erstellen von Skripts für gespeicherte Prozeduren
In diesem Abschnitt wird beschrieben, wie Sie ein Skript für eine gespeicherte Prozedur erstellen. 

1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken**.
3. Erweitern Sie den Knoten **Programmierbarkeit**. 
4. Erweitern Sie den Knoten **Gespeicherte Prozedur**.
5. Klicken Sie mit der rechten Maustaste auf eine gespeicherte Prozedur und anschließend mit der linken auf **Script Stored Procedure As** (Skript für gespeicherte Prozedur erstellen als):
    
    ![Erstellen von Skripts für gespeicherte Prozeduren](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>Erstellen von Skripts für erweiterte Ereignisse
In diesem Abschnitt wird beschrieben, wie Sie ein Skript für [erweiterte Ereignisse](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events) erstellen. 

1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Verwaltung**.
3. Erweitern Sie den Knoten **Erweiterte Ereignisse**.
4. Erweitern Sie den Knoten **Sitzungen**.
5. Klicken Sie mit der rechten Maustaste auf eine Sitzung und anschließend mit der linken auf **Script Session As** (Skript für Sitzung erstellen als):

    ![Skript für erweiterte Ereignisse](media/scripting-ssms/scriptxevents.png) 

## <a name="next-steps"></a>Nächste Schritte
Im nächsten Artikel werden die ersten Schritte mit bereits vorhandenen SSMS-Vorlagen beschrieben. 

Für weitere Informationen zum nächsten Artikel blättern
> [!div class="nextstepaction"]
> [Schaltfläche „Nächste Schritte“](templates-ssms.md)


