---
title: Erstellen partitionierter Tabellen und Indizes | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: partitions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-partition
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.createpartition.progress.f1
- sql13.swb.createpartition.partitioncolumn.f1
- sql13.swb.createpartition.createjob.f1
- sql13.swb.createpartition.finish.f1
- sql13.swb.createpartition.selectoutput.f1
- sql13.swb.createpartition.partitionfunction.f1
- sql13.swb.createpartition.partitionscheme.f1
- sql13.swb.createpartition.getstart.f1
- sql13.swb.createpartition.mappartition.f1
- sql13.swb.createpartition.summary.f1
helpviewer_keywords:
- partitioned indexes [SQL Server], creating
- partition schemes [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], creating
- partition functions [SQL Server]
- partition schemes [SQL Server]
ms.assetid: 7641df10-1921-42a7-ba6e-4cb03b3ba9c8
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: df57d6fa660d806b38deb6730dd2152099873f15
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="create-partitioned-tables-and-indexes"></a>Erstellen partitionierter Tabellen und Indizes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Sie können in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] eine partitionierte Tabelle oder einen Index erstellen. Die Daten in partitionierten Tabellen und Indizes werden horizontal in Einheiten aufgeteilt, die über mehrere Dateigruppen in einer Datenbank verteilt werden können. Die Partitionierung kann bewirken, dass sich große Tabellen und Indizes besser verwalten und skalieren lassen.  
  
 Das Erstellen einer partitionierten Tabelle oder eines Indexes erfolgt in der Regel in vier Teilen:  
  
1.  Erstellen Sie eine Dateigruppe oder Dateigruppen und entsprechende Dateien, die die vom Partitionsschema angegebenen Partitionen enthalten.  
  
2.  Erstellen Sie eine Partitionsfunktion, die die Zeilen einer Tabelle oder eines Indexes Partitionen zuordnet. Dies erfolgt auf Grundlage der Werte einer angegebenen Spalte.  
  
3.  Erstellen Sie ein Partitionsschema, das die Partitionen einer partitionierten Tabelle oder eines partitionierten Indexes den neuen Dateigruppen zuordnet.  
  
4.  Erstellen oder ändern Sie eine Tabelle oder einen Index, und geben Sie das Partitionsschema als Speicherort an.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Security](#Security)  
  
-   **Erstellen einer partitionierten Tabelle oder eines partitionierten Indexes mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Der Bereich einer Partitionsfunktion und eines Schemas ist auf die Datenbank beschränkt, in der er erstellt wurde. Innerhalb der Datenbank befinden sich Partitionsfunktionen in einem von anderen Funktionen abgetrennten Namespace.  
  
-   Wenn beliebige Zeilen innerhalb einer Partitionsfunktion Partitionierungsspalten mit NULL-Werten aufweisen, werden diese Zeilen der am weitesten links stehenden Partition zugeordnet. Jedoch wenn NULL als Begrenzungswert sowie RIGHT angegeben werden, bleibt die am weitesten links stehende Partition leer, und die NULL-Werte werden in der zweiten Partition eingefügt.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Zum Erstellen einer partitionierten Tabelle sind die CREATE TABLE-Berechtigung für die Datenbank und die ALTER-Berechtigung für das Schema erforderlich, in dem die Tabelle erstellt wird. Das Erstellen eines partitionierten Indexes erfordert die ALTER-Berechtigung für die Tabelle oder Sicht, in der der Index erstellt wird. Das Erstellen einer partitionierten Tabelle oder eines partitionierten Indexes erfordert eine der folgenden zusätzlichen Berechtigungen:  
  
-   ALTER ANY DATASPACE-Berechtigung. Diese Berechtigung gilt standardmäßig für Mitglieder der festen Serverrolle **sysadmin** und für Mitglieder der festen Datenbankrollen **db_owner** und **db_ddladmin** .  
  
-   CONTROL- oder ALTER-Berechtigung für die Datenbank, in der die Partitionsfunktion und das Partitionsschema erstellt werden.  
  
-   CONTROL SERVER- oder ALTER ANY DATABASE-Berechtigung für den Server der Datenbank, in der die Partitionsfunktion und das Partitionsschema erstellt werden.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 Führen Sie die Schritte in dieser Prozedur aus, um mindestens eine Dateigruppe, entsprechende Dateien und eine Tabelle zu erstellen. Sie versehen diese Objekte in der nächsten Prozedur mit Verweisen, wenn Sie die partitionierte Tabelle erstellen.  
  
#### <a name="to-create-new-filegroups-for-a-partitioned-table"></a>So erstellen Sie neue Dateigruppen für eine partitionierte Tabelle  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Datenbank, in der Sie eine partitionierte Tabelle erstellen möchten und wählen Sie **Eigenschaften**aus.  
  
2.  Wählen Sie im Dialogfeld **Datenbankeigenschaften –** *database_name* unter **Seite auswählen**die Option **Dateigruppen**aus.  
  
3.  Klicken Sie unter **Zeilen**auf **Hinzufügen**. Geben Sie in der neuen Zeile den Dateigruppennamen ein.  
  
    > [!WARNING]  
    >  Zusätzlich zu der Anzahl der für die Begrenzungswerte angegebenen Dateigruppen müssen Sie beim Erstellen von Partitionen stets über eine weitere Dateigruppe verfügen.  
  
4.  Fügen Sie weiterhin Zeilen hinzu, bis Sie alle Dateigruppen für die partitionierte Tabelle erstellt haben.  
  
5.  Klicken Sie auf **OK**.  
  
6.  Wählen Sie unter **Seite auswählen**die Option **Dateien**aus.  
  
7.  Klicken Sie unter **Zeilen**auf **Hinzufügen**. Geben Sie in der neuen Zeile einen Dateinamen ein, und wählen Sie eine Dateigruppe aus.  
  
8.  Fügen Sie weiter Zeilen hinzu, bis Sie mindestens eine Datei für jede Dateigruppe erstellt haben.  
  
9. Erweitern Sie den Ordner **Tabellen** , und erstellen Sie eine Tabelle. Weitere Informationen finden Sie unter [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/tables/create-tables-database-engine.md). Alternativ können Sie in der nächsten Prozedur eine vorhandene Tabelle angeben.  
  
#### <a name="to-create-a-partitioned-table"></a>So erstellen Sie eine partitionierte Tabelle  
  
1.  Klicken Sie mit der rechten Maustaste auf die Tabelle, die Sie partitionieren möchten, zeigen Sie auf **Speicher**, und klicken Sie dann auf **Partition erstellen**.  
  
2.  Klicken Sie im **Assistent zum Erstellen von Partitionen**auf der Seite **Willkommen beim Assistenten zum Erstellen von Partitionen** auf **Weiter**.  
  
3.  Wählen Sie auf der Seite **Partitionierungsspalte auswählen** im Raster **Verfügbare Partitionierungsspalten** die Spalte aus, an der Sie die Tabelle partitionieren möchten. Im Raster **Verfügbare Partitionierungsspalten** werden nur Spalten mit Datentypen angezeigt, die zum Partitionieren von Daten verwendet werden können. Wenn Sie eine berechnete Spalte als Partitionierungsspalte auswählen, muss die Spalte als persistente berechnete Spalte gekennzeichnet sein.  
  
     Die Auswahlmöglichkeiten, die Ihnen für die Partitionierungsspalte und den Wertebereich zur Verfügung stehen, werden in erster Linie durch das Ausmaß bestimmt, in dem Ihre Daten auf logische Weise gruppiert werden können. So können Sie z. B. die Daten nach Monaten oder Quartalen in logische Gruppierungen aufteilen. Ob die logische Gruppierung für die Verwaltung der Tabellenpartitionen geeignet ist, hängt von den Abfragen ab, die Sie für die Daten ausführen möchten. Als Partitionierungsspalte sind alle Datentypen außer **text**, **ntext**, **image**, **xml**, **timestamp**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, Aliasdatentypen oder CLR-benutzerdefinierten Datentypen, zulässig.  
  
     Die folgenden zusätzlichen Optionen sind auf dieser Seite verfügbar:  
  
     **Diese Tabelle der ausgewählten partitionierten Tabelle zuordnen**  
     Ermöglicht das Auswählen einer partitionierten Tabelle mit verwandten Daten, die über die Partitionierungsspalte mit einer anderen Tabelle verknüpft werden soll. Tabellen mit Partitionen, die über die Partitionierungsspalten verknüpft sind, können i. d. R. effizienter abgefragt werden.  
  
     **Nicht eindeutige Indizes und eindeutige Indizes mit indizierter Partitionsspalte am Speicher ausrichten**  
     Richtet alle Indizes der Tabelle, die mit dem gleichen Partitionsschema partitioniert sind, aneinander aus. Wenn eine Tabelle und ihre Indizes aneinander ausgerichtet sind, können Sie Partitionen effektiver in und aus partitionierten Tabellen verschieben, da die Daten mit dem gleichen Algorithmus partitioniert sind.  
  
     Nach der Auswahl der Partitionierungsspalte und beliebiger anderer Optionen klicken Sie auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Partitionsfunktion auswählen** unter **Partitionsfunktion auswählen**auf **Neue Partitionsfunktion** oder **Vorhandene Partitionsfunktion**. Wenn Sie **Neue Partitionsfunktion**auswählen, geben Sie den Namen der Funktion ein. Wenn Sie **Vorhandene Partitionsfunktion**auswählen, wählen Sie in der Liste den Namen der Funktion aus, die Sie verwenden möchten. Die Option **Vorhandene Partitionsfunktion** ist nicht verfügbar, wenn die Datenbank keine anderen Partitionsfunktionen enthält.  
  
     Nach Fertigstellen dieser Seite klicken Sie auf **Weiter**.  
  
5.  Klicken Sie auf der Seite **Partitionsschema auswählen** unter **Partitionsschema auswählen**auf **Neues Partitionsschema** oder **Vorhandenes Partitionsschema**. Wenn Sie **Neues Partitionsschema**auswählen, geben Sie den Namen des Schemas ein. Wenn Sie **Vorhandenes Partitionsschema**auswählen, wählen Sie in der Liste den Namen des Schemas aus, die Sie verwenden möchten. Die Option **Vorhandenes Partitionsschema** ist nicht verfügbar, wenn die Datenbank keine anderen Partitionsschemas enthält.  
  
     Nach Fertigstellen dieser Seite klicken Sie auf **Weiter**.  
  
6.  Wählen Sie auf der Seite **Partitionen zuordnen** unter **Bereich**entweder **Linke Begrenzung** oder **Rechte Begrenzung** aus, um anzugeben, ob der höchste oder niedrigste umgebende Wert in jeder Dateigruppe enthalten sein soll, die Sie erstellen. Zusätzlich zu der Anzahl der für die Begrenzungswerte angegebenen Dateigruppen müssen Sie beim Erstellen von Partitionen stets eine weitere Dateigruppe eingeben.  
  
     Wählen Sie im Raster **Wählen Sie Dateigruppen aus, und geben Sie Begrenzungswerte an** unter **Dateigruppe**die Dateigruppe aus, in die Sie die Daten partitionieren möchten. Geben Sie unter **Begrenzung**den Begrenzungswert für jede Dateigruppe ein. Wenn der Begrenzungswert leer bleibt, ordnet die Partitionsfunktion die gesamte Tabelle oder den gesamten Index mithilfe eines einzigen Partitionsfunktionsnamens zu.  
  
     Die folgenden zusätzlichen Optionen sind auf dieser Seite verfügbar:  
  
     **Begrenzungen festlegen…**  
     Öffnet das Dialogfeld **Begrenzungswerte festlegen** , um die Begrenzungswerte und Datumsbereiche für die Partitionen auszuwählen. Diese Option ist nur verfügbar, wenn Sie eine Partitionierungsspalte ausgewählt haben, die einen der folgenden Datentypen enthält: **date**, **datetime**, **smalldatetime**, **datetime2**oder **datetimeoffset**.  
  
     **Schätzungsspeicher**  
     Schätzt die Zeilenanzahl sowie den zum Speichern erforderlichen und verfügbaren Speicherplatz für jede für die Partitionen angegebene Dateigruppe. Diese Werte werden im Raster als schreibgeschützte Werte angezeigt.  
  
     Das Dialogfeld **Begrenzungswerte festlegen** berücksichtigt die folgenden zusätzlichen Optionen:  
  
     **Startdatum**  
     Wählt das Anfangsdatum für die Bereichswerte der Partitionen aus.  
  
     **Enddatum**  
     Wählt das Enddatum für die Bereichswerte der Partitionen aus. Wenn Sie auf der Seite **Partitionen zuordnen** die Option **Linke Begrenzung** ausgewählt haben, ist dieses Datum der letzte Wert für alle Dateigruppen/Partition. Wenn Sie auf der Seite **Partitionen zuordnen** die Option **Rechte Begrenzung** wählen, ist dieses Datum der erste Wert in der vorletzten Dateigruppe.  
  
     **Datumsbereich**  
     Wählt die Datumsgranularität bzw. das Bereichswertinkrement für jede Partition aus.  
  
     Nach Fertigstellen dieser Seite klicken Sie auf **Weiter**.  
  
7.  Geben Sie auf der Seite **Ausgabeoption auswählen** an, wie Sie die partitionierte Tabelle fertigstellen möchten. Wählen Sie **Skript erstellen** aus, um ein auf den vorherigen Seiten im Assistenten basierendes SQL-Skript zu erstellen. Wählen Sie **Sofort ausführen** aus, um die neue partitionierte Tabelle zu erstellen, nachdem Sie alle verbleibenden Seiten im Assistenten vervollständigt haben. Wählen Sie **Zeitplan** aus, um die neue partitionierte Tabelle zu einer vorher bestimmten Zeit für die Zukunft zu erstellen.  
  
     Wenn Sie **Skript erstellen**auswählen, sind die folgenden Optionen unter **Skriptoptionen**verfügbar:  
  
     **Skript in Datei schreiben**  
     Generiert das Skript als SQL-Datei. Geben Sie in das Dialogfeld **Dateiname** einen Dateinamen und einen Speicherort ein, oder klicken Sie auf **Durchsuchen** , um das Dialogfeld **Speicherort der Skriptdatei** zu öffnen. Wählen Sie in **Speichern unter** **Unicode-Text** oder **ANSI-Text**aus.  
  
     **Skript in Zwischenablage schreiben**  
     Speichert das Skript in der Zwischenablage.  
  
     **Skript in Fenster "Neue Abfrage" schreiben**  
     Generiert das Skript in einem neuen Abfrage-Editor-Fenster. Dies ist die Standardauswahl.  
  
     Wenn Sie **Zeitplan**auswählen, klicken Sie auf **Zeitplan ändern**.  
  
    1.  Geben Sie im Dialogfeld **Neuer Auftragszeitplan** im Feld **Name** den Namen des Auftragszeitplans ein.  
  
    2.  Wählen Sie in der Liste **Zeitplantyp** den Zeitplantyp aus:  
  
        -   **Automatisch starten, wenn der SQL Server-Agent startet**  
  
        -   **Starten, wenn sich die CPUs im Leerlauf befinden**  
  
        -   **Wiederholt**. Aktivieren Sie diese Option, wenn die neue partitionierte Tabellen regelmäßig mit neuen Informationen aktualisiert wird.  
  
        -   **Einmalige Ausführung**. Dies ist die Standardauswahl.  
  
    3.  Aktivieren oder deaktivieren Sie das Kontrollkästchen **Aktiviert** , um den Zeitplan zu aktivieren oder zu deaktivieren.  
  
    4.  Wenn Sie **Wiederholt**auswählen:  
  
        1.  Geben Sie unter **Häufigkeit**in der Liste **Tritt auf** die Häufigkeit des Vorkommens an:  
  
            -   Wenn Sie im Dialogfeld **Wiederholen alle**die Option **Täglich** auswählen, geben Sie ein, wie oft der Auftragszeitplan wiederholt wird (in Tagen).  
  
            -   Wenn Sie im Dialogfeld **Wiederholen alle**die Option **Wöchentlich** auswählen, geben Sie ein, wie oft der Auftragszeitplan wiederholt wird (in Wochen). Wählen Sie den Tag oder die Tage der Woche aus, an denen der Auftragszeitplan ausgeführt wird.  
  
            -   Wenn Sie **Monatlich**auswählen, wählen Sie **Tag** oder **Am**aus.  
  
                -   Wenn Sie **Tag**auswählen, geben Sie das Datum ein, an dem der Auftragszeitplan ausgeführt wird, und wie oft der Auftragszeitplan wiederholt werden soll (in Monaten). Falls Sie beispielsweise möchten, dass der Auftragszeitplan jeden zweiten Monat am 15. ausgeführt wird, wählen Sie **Tag** aus, und geben Sie in das erste Feld "15" und in das zweite Feld "2" ein. Beachten Sie, dass die größte im zweiten Feld zugelassene Zahl "99" ist.  
  
                -   Wenn Sie **Am**auswählen, geben Sie den spezifischen Tag der Woche im Monat an, an dem der Auftragszeitplan ausgeführt wird, und wie oft der Auftragszeitplan wiederholt werden soll (in Monaten). Falls Sie beispielsweise möchten, dass der Auftragszeitplan jeden zweiten Monat am letzten Wochentag ausgeführt werden soll, wählen Sie **Tag**und in der ersten Liste **Letzter** und in der zweiten Liste **Wochentag** aus, und geben Sie in das letzte Feld "2" ein. Sie können auch **erster**, **zweiter**, **dritter**oder **vierter**sowie bestimmte Wochentage (z.B. Sonntag oder Mittwoch) aus den ersten beiden Listen auswählen. Beachten Sie, dass die größte im letzten Feld zugelassene Zahl "99" ist.  
  
        2.  Geben Sie unter **Häufigkeit pro Tag**an, wie oft der Auftragszeitplan an dem Tag wiederholt werden soll, an dem der Auftragszeitplan ausgeführt wird:  
  
            -   Wenn Sie **Einmalig um**auswählen, geben Sie im Feld **Einmalig um** die spezifische Tageszeit ein, zu der der Auftragszeitplan ausgeführt werden soll. Geben Sie die Stunde, Minute und Sekunde des Tages sowie AM oder PM ein.  
  
            -   Wenn Sie **Alle**auswählen, geben Sie an, wie oft der Auftragszeitplan an dem unter **Häufigkeit**ausgewählten Tag ausgeführt werden soll. Wenn Sie z.B. möchten, dass der Auftragszeitplan am Tag seiner Ausführung alle 2 Stunden wiederholt wird, wählen Sie **Alle**aus, geben in das erste Feld „2“ ein und wählen in der Liste **Stunde(n)** aus. Aus dieser Liste können Sie auch **Minute(n)** und **Sekunde(n)**auswählen. Beachten Sie, dass die größte im ersten Feld zugelassene Zahl "100" ist.  
  
                 Geben Sie im Feld **Start** die Zeit ein, zu der die Ausführung des Auftragszeitplans beginnen soll. Geben Sie im Feld **Ende** die Zeit ein, zu der die Ausführung des Auftragszeitplans enden soll. Geben Sie die Stunde, Minute und Sekunde des Tages sowie AM oder PM ein.  
  
        3.  Geben Sie unter **Dauer**in **Startdatum**das Datum ein, an dem die Ausführung des Auftragszeitplans beginnen soll. Wählen Sie **Enddatum** oder **Kein Enddatum** aus, um anzugeben, wann die Ausführung des Auftragszeitplans beendet werden soll. Wenn Sie **Enddatum**auswählen, geben Sie das Datum ein, an dem die Ausführung des Auftragszeitplans beendet werden soll.  
  
    5.  Wenn Sie **Einmal**auswählen, geben Sie unter **Einmalig**in das Feld **Datum** das Datum ein, an dem der Auftragszeitplan ausgeführt werden soll. Geben Sie im Feld **Uhrzeit** die Zeit ein, zu der der Auftragszeitplan ausgeführt werden soll. Geben Sie die Stunde, Minute und Sekunde des Tages sowie AM oder PM ein.  
  
    6.  Überprüfen Sie unter **Zusammenfassung**im Feld **Beschreibung**, ob alle Auftragszeitplaneinstellungen richtig sind.  
  
    7.  Klicken Sie auf **OK**.  
  
     Nach Fertigstellen dieser Seite klicken Sie auf **Weiter**.  
  
8.  Erweitern Sie auf der Seite **Zusammenfassung der Überprüfung** unter **Überprüfen Sie Ihre Auswahl**alle verfügbaren Optionen, um zu überprüfen, ob alle Partitionseinstellungen richtig sind. Klicken Sie auf **Fertig stellen**, wenn alle Einstellungen richtig sind.  
  
9. Auf der Seite **Status des Assistenten zum Erstellen von Partitionen** können Sie Statusinformationen zu den Aktionen des Assistenten zum Erstellen von Partitionen überwachen. Je nach den im Assistenten ausgewählten Optionen enthält diese Seite eine oder mehrere Aktionen. Im oberen Feld werden der Gesamtstatus des Assistenten und die Anzahl der empfangenen Status-, Fehler- und Warnmeldungen angezeigt.  
  
     Die folgenden Optionen sind auf der Seite **Status des Assistenten zum Erstellen von Partitionen** verfügbar:  
  
     **Details**  
     Stellt für jede vom Assistenten ausgeführte Aktion Informationen zur Aktion, zum Status und zu den zurückgegebenen Meldungen bereit.  
  
     **Aktion**  
     Gibt den Typ und den Namen jeder Aktion an.  
  
     **Status**  
     Gibt an, ob für die Aktion des Assistenten insgesamt der Wert **Erfolg** oder der Wert **Fehler**zurückgegeben wurde.  
  
     **MessageBox**  
     Stellt alle vom Prozess zurückgegebenen Fehler- oder Warnmeldungen bereit.  
  
     **Bericht**  
     Erstellt einen Bericht mit den Ergebnissen des Assistenten zum Erstellen von Partitionen. Die Optionen sind **Bericht anzeigen**, **Bericht in Datei speichern**, **Bericht in Zwischenablage kopieren**und **Bericht als E-Mail senden**.  
  
     **Bericht anzeigen**  
     Öffnet das Dialogfeld **Bericht anzeigen** , das einen Textbericht zum Fortschritt des Assistenten zum Erstellen von Partitionen enthält.  
  
     **Bericht in Datei speichern**  
     Öffnet das Dialogfeld **Bericht speichern unter** .  
  
     **Bericht in Zwischenablage kopieren**  
     Kopiert die Ergebnisse aus dem Statusbericht des Assistenten in die Zwischenablage.  
  
     **Bericht als E-Mail senden**  
     Kopiert die Ergebnisse aus dem Statusbericht des Assistenten in eine E-Mail.  
  
     Nach Abschluss dieser Schritte klicken Sie auf **Schließen**.  
  
 Vom Assistenten zum Erstellen von Partitionen werden die Partitionsfunktion und das -schema erstellt, und anschließend wird die Partitionierung auf die angegebene Tabelle angewendet. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Tabelle und wählen Sie **Eigenschaften**aus, um die Tabellenpartitionierung zu überprüfen. Klicken Sie auf die Seite **Speicherung** . Auf der Seite werden Informationen, beispielsweise der Name der Partitionsfunktion und das -schema sowie die Anzahl an Partitionen, angezeigt.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-partitioned-table"></a>So erstellen Sie eine partitionierte Tabelle  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im Beispiel werden neue Dateigruppen, eine Partitionsfunktion und ein Partitionsschema erstellt. Eine neue Tabelle wird mit dem Partitionsschema erstellt, das als Speicherort angegeben wurde.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Adds four new filegroups to the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test1fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test4fg;   
  
    -- Adds one file for each filegroup.  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test1dat1,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat1.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test1fg;  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test2dat2,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t2dat2.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test3dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t3dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test4dat4,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t4dat4.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test4fg;  
    GO  
    -- Creates a partition function called myRangePF1 that will partition a table into four partitions  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
        AS RANGE LEFT FOR VALUES (1, 100, 1000) ;  
    GO  
    -- Creates a partition scheme called myRangePS1 that applies myRangePF1 to the four filegroups created above  
    CREATE PARTITION SCHEME myRangePS1  
        AS PARTITION myRangePF1  
        TO (test1fg, test2fg, test3fg, test4fg) ;  
    GO  
    -- Creates a partitioned table called PartitionTable that uses myRangePS1 to partition col1  
    CREATE TABLE PartitionTable (col1 int PRIMARY KEY, col2 char(10))  
        ON myRangePS1 (col1) ;  
    GO  
    ```  
  
#### <a name="to-determine-if-a-table-is-partitioned"></a>So bestimmen Sie, ob eine Tabelle partitioniert ist  
  
1.  Die folgende Abfrage gibt mindestens eine Zeile zurück, wenn die `PartitionTable` -Tabelle partitioniert ist. Wenn die Tabelle nicht partitioniert ist, werden keine Zeilen zurückgegeben.  
  
    ```  
    SELECT *   
    FROM sys.tables AS t   
    JOIN sys.indexes AS i   
        ON t.[object_id] = i.[object_id]   
        AND i.[type] IN (0,1)   
    JOIN sys.partition_schemes ps   
        ON i.data_space_id = ps.data_space_id   
    WHERE t.name = 'PartitionTable';   
    GO  
    ```  
  
#### <a name="to-determine-the-boundary-values-for-a-partitioned-table"></a>Sie definieren Sie Begrenzungswerte für eine partitionierte Tabelle  
  
1.  Die folgende Abfrage gibt die Begrenzungswerte für jede Partition in der `PartitionTable` -Tabelle zurück.  
  
    ```  
    SELECT t.name AS TableName, i.name AS IndexName, p.partition_number, p.partition_id, i.data_space_id, f.function_id, f.type_desc, r.boundary_id, r.value AS BoundaryValue   
    FROM sys.tables AS t  
    JOIN sys.indexes AS i  
        ON t.object_id = i.object_id  
    JOIN sys.partitions AS p  
        ON i.object_id = p.object_id AND i.index_id = p.index_id   
    JOIN  sys.partition_schemes AS s   
        ON i.data_space_id = s.data_space_id  
    JOIN sys.partition_functions AS f   
        ON s.function_id = f.function_id  
    LEFT JOIN sys.partition_range_values AS r   
        ON f.function_id = r.function_id and r.boundary_id = p.partition_number  
    WHERE t.name = 'PartitionTable' AND i.type <= 1  
    ORDER BY p.partition_number;  
    ```  
  
#### <a name="to-determine-the-partition-column-for-a-partitioned-table"></a>So definieren Sie die Partitionsspalte für eine partitionierte Tabelle  
  
1.  Die folgende Abfrage gibt den Namen der Partitionierungsspalte für die Tabelle zurück. `PartitionTable`eine partitionierte Tabelle oder einen Index erstellen.  
  
    ```  
    SELECT   
        t.[object_id] AS ObjectID   
        , t.name AS TableName   
        , ic.column_id AS PartitioningColumnID   
        , c.name AS PartitioningColumnName   
    FROM sys.tables AS t   
    JOIN sys.indexes AS i   
        ON t.[object_id] = i.[object_id]   
        AND i.[type] <= 1 -- clustered index or a heap   
    JOIN sys.partition_schemes AS ps   
        ON ps.data_space_id = i.data_space_id   
    JOIN sys.index_columns AS ic   
        ON ic.[object_id] = i.[object_id]   
        AND ic.index_id = i.index_id   
        AND ic.partition_ordinal >= 1 -- because 0 = non-partitioning column   
    JOIN sys.columns AS c   
        ON t.[object_id] = c.[object_id]   
        AND ic.column_id = c.column_id   
    WHERE t.name = 'PartitionTable' ;   
    GO  
    ```  
  
 Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [ALTER DATABASE-Optionen für Dateien und Dateigruppen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
-   [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)  
  
-   [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  
