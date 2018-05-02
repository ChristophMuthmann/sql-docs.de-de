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
ms.openlocfilehash: a931ddb3cf3229970de4b301e18002484acbaf53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>Tutorial: Erstellen von Skripts für Objekte in SQL Server Management Studio
In diesem Tutorial erfahren Sie, wie Sie T-SQL-Skripts (Transact-SQL) für verschiedene Objekte in SQL Server Management Studio erstellen können.  Dabei wird die Skripterstellung für die folgenden Objekte beschrieben: 

> [!div class="checklist"]
> * Abfragen beim Ausführen von Aktionen auf der grafischen Benutzeroberfläche
> * Datenbanken (mithilfe der beiden Methoden „Script Database As“ (Skript für Datenbank erstellen als) und „Skript generieren“)
> * Tabellen
> * Gespeicherte Prozeduren
> * Erweiterte Ereignisse

In diesem Tutorial haben Sie erfahren, dass Sie für jedes Objekt im **Objekt-Explorer** ein Skript erstellen können, indem Sie mit der rechten Maustaste darauf klicken und anschließend die Option **Script Object As** (Skript für Objekt als) auswählen. 


## <a name="prerequisites"></a>Voraussetzungen
Zur Durchführung dieses Tutorials benötigen Sie SQL Server Management Studio, Zugriff auf einen SQL-Server und eine AdventureWorks-Datenbank. 

- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Installieren Sie die [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Laden Sie die [AdventureWorks 2016-Beispieldatenbank](https://github.com/Microsoft/sql-server-samples/releases) herunter. Anweisungen zum Wiederherstellen von Datenbanken in SSMS finden Sie hier: [Restoring a Database (Wiederherstellen einer Datenbank)](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 


## <a name="script-queries-from-gui"></a>Erstellen von Skripts für Abfragen über die grafische Benutzeroberfläche
Beim Ausführen einer Aufgabe über die grafische Benutzeroberfläche in SSMS können Sie gleichzeitig den zugehörigen T-SQL-Code generieren. In den folgenden Beispielen wird dies anhand der Sicherung einer Datenbank und der Verkleinerung eines Transaktionsprotokolls demonstriert.  Die gleichen Schritte lassen sich auf jede Aktion anwenden, die über die grafische Benutzeroberfläche ausgeführt wird. 

### <a name="script-t-sql-when-backing-up-a-database"></a>Erstellen von T-SQL-Skripts beim Sichern einer Datenbank
1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken** .
3. Klicken Sie mit der rechten Maustaste auf die **AdventureWorks 2016**-Datenbank, dann auf **Aufgaben** > **Sichern**:

    ![Sichern der Datenbank](media/scripting-ssms/backupdb.png)

4. Konfigurieren Sie die Sicherung auf die gewünschte Weise. In diesem Tutorial werden die Standardeinstellungen beibehalten. Wenn Sie jedoch in diesem Fenster Änderungen vornehmen, werden diese auch im Skript übernommen. 
5. Wählen Sie die Option **Skript** > **Script Action to New Query Window** (Skript für Aktion in neuem Abfragefenster erstellen) aus:
 
    ![Skript für Datenbanksicherung](media/scripting-ssms/scriptdbbackup.PNG)
6. Sehen Sie sich den T-SQL-Code im Abfragefenster an: 

    ![Skript für Datenbanksicherung](media/scripting-ssms/dbbackupscript.PNG)
7. Klicken Sie auf **Ausführen**, um die Abfrage auszuführen, um die Datenbank über T-SQL zu sichern. 


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>Erstellen von T-SQL-Skripts beim Verkleinern des Transaktionsprotokolls
1. Klicken Sie mit der rechten Maustaste auf die **AdventureWorks2016**-Datenbank, und rufen Sie anschließend **Aufgaben** > **Verkleinern** > **Dateien** auf:

     ![Verkleinern von Dateien](media/scripting-ssms/shrinkfiles.png)

2. Wählen Sie aus der Dropdownliste **Dateityp** den Eintrag **Protokoll** aus:

    ![Verkleinern des Transaktionsprotokolls](media/scripting-ssms/shrinktlog.png)

3. Klicken Sie zuerst auf die Option **Skript** und anschließend auf **Script Action to Clipboard** (Skript für Aktion in Zwischenablage erstellen):

    ![Skript in Zwischenablage schreiben](media/scripting-ssms/scriptactiontoclipboard.png)

4. Öffnen Sie über **Neue Abfrage** ein Fenster, und fügen Sie das Skript durch Rechtsklicken und **Einfügen** ein:

    ![Einfügen des Skripts](media/scripting-ssms/paste.png)
5. Klicken Sie auf **Ausführen**, um die Abfrage auszuführen und das Transaktionsprotokoll zu schließen. 


## <a name="script-databases"></a>Erstellen von Skripts für Datenbanken
Im folgenden Abschnitt erfahren Sie, wie Sie mit den Optionen **Script Database As** (Skript für Datenbank erstellen als) und **Skripts generieren** Skripts für eine Datenbank erstellen.  Mithilfe der Option **Script Database As** (Skript für Datenbank erstellen als) werden die Datenbank und die zugehörigen Konfigurationsoptionen neu erstellt. Mithilfe der Option **Skripts generieren** können Sie jeweils Skripts für das Schema und die Daten erstellen. In diesem Abschnitt erstellen Sie zwei neue Datenbanken: *AdventureWorks2016a* wird mithilfe der Option **Script As** (Skripterstellung als) erstellt, und *AdventureWorks2016b* wird mithilfe der Option **Skripts generieren** erstellt. 


### <a name="script-database-using-script-option"></a>Erstellen eines Skripts für eine Datenbank mit der Option „Script Database As“ (Skript für Datenbank erstellen als)
1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken** .
3. Klicken Sie mit der rechten Maustaste auf die **AdventureWorks2016**-Datenbank, wählen Sie dann **Script Database As** > **Create To** > **Neues Abfragefenster** (Skript für Datenbank erstellen als > Erstellen in) aus:

    ![Erstellen eines Skripts für eine Datenbank](media/scripting-ssms/scriptdb.png)

4. Sehen Sie sich die Datenbankerstellungsabfrage im Fenster an: 

    ![Erstelltes Skript für Datenbank](media/scripting-ssms/scriptedoutdb.png)
    - Mit dieser Option wird nur ein Skript für die Datenbank-Konfigurationsoptionen erstellt.
5. Klicken Sie auf **STRG+F**, um das Dialogfeld **Suchen** zu öffnen. Klicken Sie auf den Pfeil nach unten, und wählen Sie die Option **Ersetzen** aus. Geben Sie oben in der **Suchzeile** *AdventureWorks2016* ein, und geben Sie unten unter **Ersetzen** *AdventureWorks2016a* ein. 
6. Wählen Sie **Alle ersetzen** aus, um alle Instanzen von *AdventureWorks2016* durch *AdventureWorks2016a* zu ersetzen. 

    ![Suchen und Ersetzen](media/scripting-ssms/findandreplace.png)

1. Wählen Sie **Ausführen** aus, um die Abfrage auszuführen, und erstellen Sie Ihre neue *AdventureWorks2016a*-Datenbank. 

### <a name="script-database-using-generate-scripts-option"></a>Erstellen eines Skripts für eine Datenbank mit der Option „Skripts generieren“
1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken** .
3. Klicken Sie mit der rechten Maustaste auf die **AdventureWorks2016**-Datenbank, und rufen Sie anschließend **Aufgaben** > **Skripts erstellen** auf:

    ![Generieren von Skripts für eine Datenbank](media/scripting-ssms/generatescriptsfordb.png)

4. Die Seite **Einführung** wird nun angezeigt. Klicken Sie auf **Weiter**, um die Seite **Objekte auswählen** zu öffnen. Sie haben die Möglichkeit, die gesamte Datenbank oder nur bestimmte Objekte in der Datenbank auszuwählen. Wählen Sie die Option **Skripterstellung für gesamte Datenbank und alle Datenbankobjekte** aus. 
 
    ![Generieren von Skripts für Objekte](media/scripting-ssms/scriptobjects.png)
 
5. Klicken Sie auf **Weiter**, um die Seite **Skripterstellungsoptionen festlegen** zu öffnen. Auf dieser Seite können Sie konfigurieren, wo die Skripts gespeichert werden, sowie zusätzliche erweiterte Optionen. 

    A. Wählen Sie die Option **In neuem Abfragefenster speichern** aus. 

    B. Wählen Sie **Erweitert** aus, um zu überprüfen, ob folgende Optionen festgelegt sind: 

      - **Skripterstellung für Statistiken** muss auf *Skripterstellung für Statistiken* festgelegt sein.
      - **Datentypen, für die ein Skript erstellt wird** muss auf *Nur Schema* festgelegt sein.
      - **Skripterstellung für Indizes** muss auf *True* festgelegt sein.

   ![Erstellen von Skripts für Objekte](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > Sie haben die Möglichkeit, für die Datenbank Skripts für die Daten zu erstellen, indem Sie für die Option **Datentypen, für die ein Skript erstellt wird** *Schema und Daten* auswählen. Für große Datenbanken ist diese Vorgehensweise jedoch nicht ideal, da diese mehr Speicherplatz benötigt als SSMS zuordnen kann. Für kleine Datenbanken ist das in Ordnung, wenn Sie jedoch Daten für größere Datenbanken verschieben möchten, sollten Sie den [Import/Export-Assistenten](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) verwenden.



1. Klicken Sie auf **OK** und anschließend auf **Weiter**. 
2. Klicken Sie auf der Seite **Zusammenfassung** auf **Weiter**, klicken Sie erneut auf **Weiter**, um das Skript für ein **Neue Abfrage**-Fenster zu generieren.  
3. Klicken Sie auf **STRG+F**, um das Dialogfeld **Suchen** zu öffnen. Klicken Sie auf den Pfeil nach unten, und wählen Sie die Option **Ersetzen** aus. Geben Sie oben in der **Suchzeile** *AdventureWorks2016* ein, und geben Sie unten unter **Ersetzen** *AdventureWorks2016b* ein. 
    A. Wählen Sie **Alle ersetzen** aus, um alle Instanzen von *AdventureWorks2016* durch *AdventureWorks2016b* zu ersetzen. 

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)
7. Wählen Sie **Ausführen** aus, um die Abfrage auszuführen, und erstellen Sie Ihre neue *AdventureWorks2016b*-Datenbank. 
 
## <a name="script-tables"></a>Erstellen von Skripts für Tabellen
In diesem Abschnitt wird beschrieben, wie Sie Skripts für Datenbanktabellen erstellen. Mithilfe dieser Option können Sie entweder die Tabelle erstellen oder die Tabelle löschen und neu erstellen. Sie können diese Option auch verwenden, um ein Skript für den T-SQL-Code zu erstellen, der im Zusammenhang mit der Bearbeitung der Tabelle steht, also z.B. um etwas einzufügen oder ein Update dafür auszuführen. In diesem Abschnitt löschen Sie eine Tabelle und erstellen diese dann neu. 

1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken**.
3. Erweitern Sie den Datenbankknoten **AdventureWorks**. 
4. Erweitern Sie den Knoten **Tabellen**.
5. Klicken Sie mit der rechten Maustaste auf **dbo.ErrorLog**, dann auf **Skript für Tabelle als** > **Drop und Create to** > **Neues Abfrage-Editor-Fenster** (Löschen und neu erstellen in):
    
    ![Skripttabelle](media/scripting-ssms/scripttable.png)

6. Klicken Sie auf **Ausführen**, um die Abfrage auszuführen. Dadurch wird die Tabelle *Errorlog* gelöscht und wieder erstellt. 

    >[!NOTE]
    > Die *Errorlog*-Tabelle in der AdventureWorks2016-Datenbank ist standardmäßig leer, es gehen also beim Löschen der Tabelle keine Daten verloren. Dieselbe Vorgehensweise führt jedoch bei einer Tabelle mit Daten zu Datenverlust. 
 
## <a name="script-stored-procedures"></a>Erstellen von Skripts für gespeicherte Prozeduren
In diesem Abschnitt erfahren Sie, wie Sie eine gespeicherte Prozedur löschen und neu erstellen.  

1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Datenbanken**.
3. Erweitern Sie den Knoten **Programmierbarkeit**. 
4. Erweitern Sie den Knoten **Gespeicherte Prozedur**.
5. Klicken Sie mit der rechten Maustaste auf die gespeicherte Prozedur **dbo.uspGetBillOfMaterials**, dann auf **Skript für gespeicherte Prozeduren als** > **Löschen und neu erstellen in** > **Neues Abfragefenster**:
    
    ![Erstellen von Skripts für gespeicherte Prozeduren](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>Erstellen von Skripts für erweiterte Ereignisse
In diesem Abschnitt wird beschrieben, wie Sie ein Skript für [erweiterte Ereignisse](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events) erstellen. 

1. Stellen Sie eine Verbindung mit Ihrem SQL Server her.
2. Erweitern Sie den Knoten **Verwaltung**.
3. Erweitern Sie den Knoten **Erweiterte Ereignisse**.
4. Erweitern Sie den Knoten **Sitzungen**.
5. Klicken Sie mit der rechten Maustaste auf eine Sitzung und anschließend mit der linken auf **Script Session As** (Skript für Sitzung erstellen als) und dann auf **Neues Abfrage-Editor-Fenster**:

    ![Skript für erweiterte Ereignisse](media/scripting-ssms/scriptxevents.png) 
6. Ändern Sie unter **Neues Abfragefenster** den neuen Namen der Sitzung von *system_health* in *system_health2*, und klicken Sie auf **Ausführen**, um die Abfrage auszuführen. 

    A. Klicken Sie mit der rechten Maustaste im **Objekt-Explorer** auf **Sitzungen**, und dann auf **Aktualisieren**, um Ihre neue erweiterte Ereignissitzung anzuzeigen. Ein grünes Symbol neben der Sitzung besagt, dass die Sitzung ausgeführt wird. Ein rotes Symbol bedeutet, dass die Sitzung angehalten wurde. 

    ![Neues XEvent](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > Sie können die Sitzung starten, indem Sie mit der rechten Maustaste darauf klicken und **Start** (Starten) auswählen. Da es sich jedoch hier um eine Kopie der bereits ausgeführten Sitzung *system_health* handelt, kann dieser Schritt übersprungen werden. Sie können die Kopie der erweiterten Ereignissitzung löschen, indem Sie mit der rechten Maustaste darauf klicken, und **Löschen** auswählen. 

## <a name="next-steps"></a>Nächste Schritte
Im nächsten Artikel werden die ersten Schritte mit bereits vorhandenen T-SQL-Vorlagen in SSMS beschrieben. 

Für weitere Informationen zum nächsten Artikel blättern:
> [!div class="nextstepaction"]
> [Nächste Schritte](templates-ssms.md)


