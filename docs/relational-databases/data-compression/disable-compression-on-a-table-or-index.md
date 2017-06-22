---
title: "So deaktivieren Sie die Komprimierung für eine Tabelle oder einen Index | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-compression
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data compression [SQL Server], disabling
ms.assetid: bda1e452-397b-4757-82a4-181217361589
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 342baf08233852778ca7caaf5a528d0362490de6
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="disable-compression-on-a-table-or-index"></a>Deaktivieren der Komprimierung für eine Tabelle oder einen Index
  In diesem Thema wird beschrieben, wie die Komprimierung für eine Tabelle oder einen Index in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]deaktiviert wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So deaktivieren Sie die Komprimierung für eine Tabelle oder einen Index mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn die Tabelle ein Heap ist, erfolgt der Neuerstellungsvorgang für den ONLINE-Modus mit einem einzelnen Thread. Verwenden Sie den OFFLINE-Modus für einen Multithreaded-Neuerstellungsvorgang von Heaps. Weitere Informationen zur Datenkomprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
-   Mit der gespeicherten Prozedur [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) können Sie einschätzen, wie sich eine Änderung des Komprimierungsstatus auf eine Tabelle, einen Index oder eine Partition auswirkt.  
  
-   Sie können die Komprimierungseinstellung einer einzelnen Partition nicht ändern, wenn die Tabelle nicht ausgerichtete Indizes aufweist.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle oder den Index.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-disable-compression-on-a-table"></a>So deaktivieren Sie die Komprimierung für eine Tabelle  
  
1.  Erweitern Sie in Objekt-Explorer die Datenbank, die die Tabelle enthält, für die Sie die Komprimierung deaktivieren möchten, und erweitern Sie dann den Ordner **Tabellen** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Tabelle oder den Index, für die bzw. den Sie die Komprimierung deaktivieren möchten, zeigen Sie auf **Speicher** , und wählen Sie **Komprimierung verwalten…**aus.  
  
3.  Um die Komprimierung für einen Index zu deaktivieren, erweitern Sie die Tabelle, die den Index enthält, und dann erweitern Sie den Ordner **Indizes** .  
  
4.  Klicken Sie auf der Seite **Willkommen** des Datenkomprimierungs-Assistenten auf **Weiter**.  
  
5.  Wählen Sie auf der Seite **Komprimierungstyp auswählen** für Komprimierungstyp **Keiner** aus, damit die Einstellung für alle Partitionen des Index gilt, für den Sie die Komprimierung deaktivieren möchten. Klicken Sie auf **Weiter**, wenn Sie fertig sind.  
  
     Die folgenden Optionen sind auf der Seite **Komprimierungstyp auswählen** verfügbar:  
  
     **Gleichen Komprimierungstyp für alle Partitionen verwenden** (Kontrollkästchen)  
     Wählen Sie diese Option aus, um für alle Partitionen die gleiche Komprimierungseinstellung zu konfigurieren. Damit werden das Auswahlfeld aktiviert und die Spalte **Komprimierungstyp** im Raster deaktiviert. Wenn das Kontrollkästchen aktiviert ist, enthält die nebenstehende Liste die Optionen **Keiner**, **Zeile**und **Seite**.  
  
     **Partitionsnummer**  
     Listet jede Partition in der Tabelle bzw. im Index auf. Diese Spalte ist schreibgeschützt.  
  
     **Komprimierungstyp**  
     Wählen Sie die Komprimierungsoption für jede Partition aus. Nicht verfügbar, wenn **Gleichen Komprimierungstyp für alle Partitionen verwenden** ausgewählt ist. Listenoptionen sind **Keiner**, **Zeile**und **Seite**.  
  
     **Grenze**  
     Zeigt die Partitionsbegrenzung an. Diese Spalte ist schreibgeschützt.  
  
     **Zeilenanzahl**  
     Zeigt die Anzahl von Zeilen in dieser Partition an. Diese Spalte ist schreibgeschützt.  
  
     **Aktueller Speicherplatz**  
     Zeigt den aktuell von dieser Partition belegten Speicherplatz in Megabytes (MB) an. Diese Spalte ist schreibgeschützt.  
  
     **Angeforderter komprimierter Speicherplatz**  
     Nachdem Sie auf **Berechnen**geklickt haben, wird in dieser Spalte die geschätzte Größe der einzelnen Partitionen nach der Komprimierung angezeigt. Dabei wird die in der Spalte **Komprimierungstyp** angegebene Einstellung zugrunde gelegt. Diese Spalte ist schreibgeschützt.  
  
     **Berechnen**  
     Klicken Sie auf diese Option, um die Größe der einzelnen Partitionen nach der Komprimierung auf Grundlage der in der Spalte **Komprimierungstyp** angegebenen Einstellung zu schätzen.  
  
6.  Geben Sie auf der Seite **Ausgabeoption auswählen** an, wie Sie diese Aufgabe fertig stellen möchten. Wählen Sie **Skript erstellen** aus, um ein auf den vorherigen Seiten im Assistenten basierendes SQL-Skript zu erstellen. Wählen Sie **Sofort ausführen** aus, um die neue partitionierte Tabelle zu erstellen, nachdem Sie alle verbleibenden Seiten im Assistenten vervollständigt haben. Wählen Sie **Zeitplan** aus, um die neue partitionierte Tabelle zu einer vorher bestimmten Zeit für die Zukunft zu erstellen.  
  
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
  
7.  Erweitern Sie auf der Seite **Zusammenfassung überprüfen** unter **Überprüfen Sie Ihre Auswahl**alle verfügbaren Optionen, um zu überprüfen, ob alle Partitionseinstellungen richtig sind. Klicken Sie auf **Fertig stellen**, wenn alle Einstellungen richtig sind.  
  
8.  Auf der Seite **Status des Komprimierungsassistenten** können Sie Statusinformationen zu den Aktionen des Assistenten zum Erstellen von Partitionen überwachen. Je nach den im Assistenten ausgewählten Optionen enthält diese Seite eine oder mehrere Aktionen. Im oberen Feld werden der Gesamtstatus des Assistenten und die Anzahl der empfangenen Status-, Fehler- und Warnmeldungen angezeigt.  
  
     Die folgenden Optionen sind auf der Seite **Status des Komprimierungsassistenten** verfügbar:  
  
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
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-disable-compression-on-a-table"></a>So deaktivieren Sie die Komprimierung für eine Tabelle  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Person.Person REBUILD PARTITION = ALL  
    WITH (DATA_COMPRESSION = NONE);  
    GO  
    ```  
  
#### <a name="to-disable-compression-on-an-index"></a>So deaktivieren Sie die Komprimierung für einen Index  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER INDEX AK_Person_rowguid ON Person.Person REBUILD PARTITION = ALL WITH (DATA_COMPRESSION = NONE);  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) und [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
  
