---
title: Verwenden des Wartungsplanungs-Assistenten | Microsoft-Dokumentation
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.maintwiz.integrity.f1
- sql13.ag.maintwiz.order.f1
- sql13.ag.maintwiz.report.f1
- sql13.ag.maintwiz.updatestats.f1
- sql13.ag.maintwiz.indexdefrag.f1
- sql13.ag.maintwiz.progress.f1
- sql13.ag.maintwiz.maintcleanup.f1
- sql13.ag.maintwiz.backupfull.f1
- sql13.ag.maintwiz.task.f1
- sql13.ag.maintwiz.server.f1
- sql13.ag.maintwiz.shrinkdb.f1
- sql13.ag.maintwiz.execagentjob.f1
- sql13.ag.maintwiz.summary.f1
- sql13.ag.maintwiz.welcome.f1
- sql13.ag.maintwiz.planprop.f1
- sql13.ag.maintwiz.reindex.f1
- sql13.ag.maintwiz.histcleanup.f1
- sql13.ag.maintwiz.backuplog.f1
- sql13.ag.maintwiz.backupdiff.f1
helpviewer_keywords:
- Maintenance Plan Wizard
- Database Maintenance Plan Wizard
- Database Maintenance Plan Wizard, starting
ms.assetid: db65c726-9892-480c-873b-3af29afcee44
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 21c05a6f8d841bc32cbcebd0830042c8b17c2421
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="use-the-maintenance-plan-wizard"></a>Verwenden des Wartungsplanungs-Assistenten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie einen Einzelserver- oder Multiserver-Wartungsplan mithilfe des Wartungsplanungs-Assistenten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] erstellen. Der Wartungsplanungs-Assistent erstellt einen Wartungsplan, den der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent regelmäßig ausführen kann. Dies ermöglicht es Ihnen, verschiedene Aufgaben für die Datenbankverwaltung in bestimmten Intervallen auszuführen, z. B. Sicherungen, Datenbankintegritätsprüfungen oder Datenbankstatistikupdates.  
    
 
##  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie einen Multiserver-Wartungsplan erstellen möchten, müssen Sie eine Multiserverumgebung mit einem Masterserver und mindestens einem Zielserver konfigurieren. Sie müssen Multiserver-Wartungspläne auf dem Masterserver erstellen und warten. Sie können Pläne auf Zielservern anzeigen.   

-   Mitglieder der **db_ssisadmin** -Rolle und der **dc_admin** -Rolle können ihre Berechtigungen möglicherweise auf **sysadmin**erhöhen. Diese Ausweitung von Berechtigungen ist möglich, da diese Rollen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete ändern können. Diese Pakete können von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des **sysadmin** -Sicherheitskontexts des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ausgeführt werden. 

Konfigurieren Sie als Schutz vor dieser Ausweitung von Berechtigungen beim Ausführen von Wartungsplänen, Datensammlungssätzen und anderen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen Aufträge des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents, die Pakete ausführen, für die Verwendung eines Proxykontos mit eingeschränkten Berechtigungen, oder fügen Sie der **db_ssisadmin** -Rolle und der **dc_admin** -Rolle nur **sysadmin** -Mitglieder hinzu.  

##  <a name="Prerequisite"></a> Voraussetzungen 
Sie müssen [Agent XPs (Serverkonfigurationsoption)](../../database-engine/configure-windows/agent-xps-server-configuration-option.md)aktivieren.
  
  
##  <a name="Permissions"></a> Berechtigungen  
 Sie müssen Mitglied der festen Serverrolle **sysadmin** sein, um Wartungspläne erstellen oder verwalten zu können. Im Objekt-Explorer wird der **Wartungspläne** -Knoten nur für Benutzer angezeigt, die Mitglied der festen Serverrolle **sysadmin** sind.  
  
##  <a name="SSMSProcedure"></a> Verwenden des Wartungsplanungs-Assistenten  
  
**Starten des Assistenten** 

  
1.  Erweitern Sie den Server, auf dem Sie den Verwaltungsplan erstellen möchten.  
  
2.  Erweitern Sie den Ordner **Verwaltung** .  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Wartungspläne** , und wählen Sie **Wartungsplanungs-Assistent**aus.  
  
4.  Klicken Sie auf der Seite **SQL Server Wartungsplanungs-Assistent** auf **Weiter**.  
  
5.  Auf der Seite **Planeigenschaften auswählen** :  
  
    1.  Geben Sie im Feld **Name** den Namen des Wartungsplans ein, den Sie erstellen möchten.  
  
    2.  Geben Sie im Feld **Beschreibung** eine kurze Beschreibung des Wartungsplans ein.  
  
    3.  Geben Sie in der Liste **Ausführen als** die Anmeldeinformationen an, die der Microsoft SQL Server-Agent beim Ausführen des Wartungsplans verwendet.  
  
    4.  Wählen Sie **Getrennte Zeitpläne für jede Aufgabe** oder **Einzelner Zeitplan für den gesamten Plan oder kein Zeitplan** aus, um den Wiederholungszeitplan für den Wartungsplan anzugeben.  
  
        > **HINWEIS:** Wenn Sie **Getrennte Zeitpläne für jede Aufgabe**auswählen, müssen Sie die Schritte unter **e** für jede Aufgabe im Wartungsplan ausführen.  
  
    5.  Wenn Sie unter **Zeitplan**die Option **Einzelner Zeitplan für den gesamten Plan oder kein Zeitplan**ausgewählt haben, klicken Sie auf **Ändern**.  
  
        1.  Geben Sie im Dialogfeld **Neuer Auftragszeitplan** im Feld **Name** den Namen des Auftragszeitplans ein.  
  
        2.  Wählen Sie in der Liste **Zeitplantyp** den Zeitplantyp aus:  
  
            -   **Automatisch starten, wenn der SQL Server-Agent startet**  
  
            -   **Starten, wenn sich die CPUs im Leerlauf befinden**  
  
            -   **Wiederholt**. Dies ist die Standardauswahl.  
  
            -   **Einmal**  
  
        3.  Aktivieren oder deaktivieren Sie das Kontrollkästchen **Aktiviert** , um den Zeitplan zu aktivieren oder zu deaktivieren.  
  
        4.  Wenn Sie **Wiederholt**auswählen:  
  
            1.  Geben Sie unter **Häufigkeit**in der Liste **Tritt auf** die Häufigkeit des Vorkommens an:  
  
                -   Wenn Sie im Dialogfeld **Wiederholen alle**die Option **Täglich** auswählen, geben Sie ein, wie oft der Auftragszeitplan wiederholt wird (in Tagen).  
  
                -   Wenn Sie im Dialogfeld **Wiederholen alle**die Option **Wöchentlich** auswählen, geben Sie ein, wie oft der Auftragszeitplan wiederholt wird (in Wochen). Wählen Sie die Tage der Woche aus, an denen der Auftragszeitplan ausgeführt wird.  
  
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
  
    6.  Klicken Sie auf **Weiter**.  
  
6.  Auf der Seite **Zielserver auswählen** können Sie die Server auswählen, auf denen der Wartungsplan ausgeführt werden soll. Diese Seite wird nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen angezeigt, die als Masterserver konfiguriert sind.  
  
    > **HINWEIS:** Wenn Sie einen Multiserver-Wartungsplan erstellen möchten, muss eine Multiserverumgebung mit einem Masterserver und mindestens einem Zielserver konfiguriert sein, und der lokale Server sollte als Masterserver konfiguriert sein. In Multiserverumgebungen werden auf dieser Seite der **(local)** -Masterserver und alle entsprechenden Zielserver angezeigt.  
  
7.  Wählen Sie auf der Seite **Wartungstasks auswählen** die Wartungstasks aus, die Sie dem Plan hinzufügen möchten. Klicken Sie anschließend auf **Weiter**.  
  
    > **HINWEIS:** Die hier ausgewählten Tasks bestimmen, auf welchen Seiten Sie nach der Seite **Wartungstaskreihenfolge auswählen** Einstellungen vornehmen müssen.  
  
8.  Klicken Sie auf der Seite **Wartungstaskreihenfolge auswählen** einen Task aus, und klicken Sie auf **Nach oben** oder **Nach unten** , um die Ausführungsreihenfolge zu ändern. Klicken Sie auf **Weiter**, wenn Sie fertig bzw. mit der aktuellen Taskreihenfolge zufrieden sind.  
  
    > **HINWEIS:** Wenn Sie zuvor auf der Seite **Planeigenschaften auswählen** die Option **Getrennte Zeitpläne für jede Aufgabe** ausgewählt haben, können Sie die Reihenfolge der Wartungstasks auf dieser Seite nicht ändern.  
  
## <a name="define-database-check-integrity-checkdb"></a>'Datenbankintegrität überprüfen' definieren (CHECKDB)  
  
 Wählen Sie auf der Seite **Task 'Datenbankintegrität überprüfen' definieren** die Datenbanken aus, in denen die Zuordnung und die strukturelle Integrität von Benutzer- und Systemtabellen sowie Indizes überprüft werden sollen. Dieser Task stellt durch die Ausführung der `DBCC CHECKDB`[!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung sicher, dass etwaige Integritätsprobleme in der Datenbank gemeldet werden und später vom Systemadministrator oder Datenbankbesitzer behoben werden können. Weitere Informationen finden Sie unter [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)Klicken Sie abschließend auf **Weiter**.  
  
Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
 Liste**Datenbanken**   
 Gibt die Datenbanken an, die von dieser Aufgabe betroffen sind.  
  
 -  **Alle Datenbanken**  
  
Generiert einen Wartungsplan, der diesen Task für alle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken außer **tempdb**ausführt.  
  
**Systemdatenbanken**  
  
  - Generiert einen Wartungsplan, der diesen Task für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemdatenbanken außer **tempdb** und vom Benutzer erstellten Datenbanken ausführt.  
  
 **Alle Benutzerdatenbanken (außer 'master', 'model', 'msdb', 'tempdb')**  
  
 - Generiert einen Wartungsplan, der diesen Task für alle vom Benutzer erstellten Datenbanken ausführt. Für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemdatenbanken werden keine Wartungstasks ausgeführt.  
  
 **Diese Datenbanken**  
  
  - Generiert einen Wartungsplan, der diesen Task nur für die ausgewählten Datenbanken ausführt. Wenn diese Option ausgewählt wird, muss mindestens eine Datenbank in der Liste ausgewählt werden.  
  
Kontrollkästchen**Indizes einschließen**   
 - Überprüft die Integrität aller Indexseiten und der Tabellendatenseiten.  
  
**Nur physisch**  
 - Begrenzt die Überprüfung der Integrität der physischen Struktur der Seite, der Datensatzheader und der Zuordnungskonsistenz der Datenbank. Das Verwenden dieser Option verkürzt möglicherweise die Ausführungszeit von DBCC CHECKDB für große Datenbanken. Sie wird daher für die häufige Verwendung in Produktionssystemen empfohlen.  
  
**Tablock**  
 - Bewirkt, dass DBCC CHECKDB Sperren erhält, statt eine interne Datenbankmomentaufnahme zu verwenden. Dies schließt eine kurzfristige exklusive Sperre (X) für die Datenbank ein. Durch diese Option wird DBCC CHECKDB schneller in einer stark ausgelasteten Datenbank ausgeführt, allerdings verringert sich während der Ausführung von DBCC CHECKDB die in der Datenbank verfügbare Parallelität.  
  
## <a name="define-database-shrink-tasks"></a>Definieren von Tasks zum Verkleinern der Datenbank  
  
1.  Erstellen Sie auf der Seite **Task 'Datenbank verkleinern' definieren** einen Task, der versucht, die Größe der ausgewählten Datenbanken mithilfe der `DBCC SHRINKDATABASE` -Anweisung mit der `NOTRUNCATE` - oder `TRUNCATEONLY` -Option zu reduzieren. Weitere Informationen finden Sie unter [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md). Klicken Sie anschließend auf **Weiter**.  
  
    > **WARNUNG!** Daten, die zum Verkleinern einer Datei verschobenen werden, können an jede verfügbare Position in der Datei verteilt werden. Dies führt zur Indexfragmentierung und kann die Leistung von Abfragen, die einen Bereich des Indexes suchen, verlangsamen. Zur Vermeidung von Fragmentierung sollten die Dateiindizes nach der Verkleinerung neu erstellt werden.  
  
     Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     Liste**Datenbanken**   
     Gibt die Datenbanken an, die von dieser Aufgabe betroffen sind. Weitere Informationen zu den verfügbaren Optionen in dieser Liste finden Sie weiter oben in Schritt 9.  
  
     Feld**Datenbank verkleinern, wenn sie folgende Größe überschreitet**   
     Gibt die Größe in Megabytes an, die zur Ausführung des Tasks führt.  
  
     Feld**Menge des freien Speicherplatzes nach dem Verkleinern**   
     Beendet das Verkleinern, wenn der freie Speicherplatz in der Datenbankdatei diesen Wert (in Prozent) erreicht.  
  
     **Freigegebenen Speicherplatz in Datenbankdateien belassen**  
     Die Datenbank wird in aufeinander folgenden Seiten komprimiert. Dabei werden jedoch weder die Seiten neu zugeordnet noch die Datenbankdateien verkleinert. Verwenden Sie diese Option, wenn Sie erwarten, dass die Datenbank wieder wächst, und Sie den Speicher nicht neu zuordnen möchten. Bei Auswahl dieser Option werden die Datenbankdateien nicht so stark wie möglich verkleinert. Dabei wird die NOTRUNCATE-Option verwendet.  
  
     **Freigegebenen Speicherplatz an Betriebssystem zurückgeben**  
     Die Datenbank wird in aufeinander folgenden Seiten komprimiert und die Seiten werden wieder für das Betriebssystem freigegeben und können für andere Programme verwendet werden. Dabei wird die TRUNCATEONLY-Option verwendet. Dies ist die Standardeinstellung.  
  
## <a name="define-the-index-tasks"></a>Definieren der Indextasks  
  
1.  Wählen Sie auf der Seite **Task „Index neu organisieren“ definieren** die Server aus, auf denen Indexseiten in eine effizientere Suchreihenfolge gebracht werden sollen. Für diesen Task wird die `ALTER INDEX … REORGANIZE`-Anweisung verwendet. Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md). Klicken Sie anschließend auf **Weiter**.  
  
     Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     Liste**Datenbanken**   
     Gibt die Datenbanken an, die von dieser Aufgabe betroffen sind. Weitere Informationen zu den verfügbaren Optionen in dieser Liste finden Sie weiter oben in Schritt 9.  
  
     Liste**Objekt**   
     Begrenzt die Liste **Auswahl** auf die Anzeige von Tabellen und/oder Sichten. Diese Liste ist nur verfügbar, wenn in der obigen Liste **Datenbanken** eine einzelne Datenbank ausgewählt wurde.  
  
     Liste**Auswahl**   
     Gibt die Tabellen oder Indizes an, auf die sich dieser Task auswirkt. Nicht verfügbar, wenn im Objektfeld der Eintrag **Tabellen und Sichten** ausgewählt ist.  
  
     Kontrollkästchen**Große Objekte komprimieren**   
     Hebt die Speicherplatzzuordnung für Tabellen und Sichten nach Möglichkeit auf. Diese Option verwendet `ALTER INDEX … LOB_COMPACTION = ON`.  
  
2.  Wählen Sie auf der Seite **Task „Index neu erstellen“ definieren** die Datenbanken aus, in denen mehrere Indizes neu erstellt werden sollen. Für diesen Task wird die `ALTER INDEX … REBUILD PARTITION`-Anweisung verwendet. Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).) Klicken Sie anschließend auf **Weiter**.  
  
     Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     Liste**Datenbanken**   
     Gibt die Datenbanken an, die von dieser Aufgabe betroffen sind. Weitere Informationen zu den verfügbaren Optionen in dieser Liste finden Sie weiter oben in Schritt 9.  
  
     Liste**Objekt**   
     Begrenzt die Liste **Auswahl** auf die Anzeige von Tabellen und/oder Sichten. Diese Liste ist nur verfügbar, wenn in der obigen Liste **Datenbanken** eine einzelne Datenbank ausgewählt wurde.  
  
     Liste**Auswahl**   
     Gibt die Tabellen oder Indizes an, auf die sich dieser Task auswirkt. Nicht verfügbar, wenn im Objektfeld der Eintrag **Tabellen und Sichten** ausgewählt ist.  
  
     Bereich**Optionen für freien Speicherplatz**   
     Enthält Optionen, mit denen ein Füllfaktor auf Indizes und Tabellen angewendet werden kann.  
  
     **Freier Standardspeicherplatz pro Seite**  
     Organisiert die Seiten mit der standardmäßigen freien Speicherplatzmenge neu. Dadurch werden die Indizes für die Tabellen in der Datenbank gelöscht, und sie werden mit dem Füllfaktor, der beim Erstellen der Indizes angegeben wurde, neu erstellt. Dies ist die Standardeinstellung.  
  
     Feld**Freien Speicherplatz pro Seite ändern in**   
     Löscht die Indizes für die Tabellen in der Datenbank und erstellt sie mit einem neuen, automatisch berechneten Füllfaktor neu. Auf diese Weise wird der angegebene freie Speicherplatz auf den Indexseiten reserviert. Ein höherer Prozentsatz bedeutet, dass mehr freier Speicherplatz auf den Indexseiten reserviert wird und der Index entsprechend wachsen kann. Die gültigen Werte sind 0 bis 100. Verwendet die `FILLFACTOR` -Option.  
  
     Bereich**Erweiterte Optionen**   
     Enthält zusätzliche Optionen zum Sortieren von Indizes und Neuindizieren.  
  
     Kontrollkästchen**Ergebnisse in 'tempdb' sortieren**   
     Legt mithilfe der `SORT_IN_TEMPDB` -Option fest, wo die während der Indexerstellung generierten Zwischenergebnisse der Sortierung temporär gespeichert werden. Wenn ein Sortiervorgang nicht erforderlich ist oder im Arbeitsspeicher ausgeführt werden kann, wird die `SORT_IN_TEMPDB` -Option ignoriert.  
  
     Kontrollkästchen**Index mit Leerstellen auffüllen**   
     Verwendet die `PAD_INDEX` -Option.  
  
     Kontrollkästchen**Index online während Neuindizierung**   
     Verwendet die `ONLINE` -Option, die es Benutzern ermöglicht, während Indexvorgängen auf die zugrunde liegenden Tabellen- oder gruppierten Indexdaten und alle zugehörigen nicht gruppierten Indizes zuzugreifen. Bei Auswahl dieser Option werden zusätzliche Optionen zum Neuerstellen von Indizes aktiviert, die keine Onlineneuerstellungen zulassen: **Indizes nicht neu erstellen** und **Indizes offline neu erstellen**.  
  
     Die Auswahl dieser Option aktiviert auch „Mit niedriger Priorität“, das die `WAIT_AT_LOW_PRIORITY` -Option verwendet. Der Onlineneuerstellungsvorgang für den Index wartet auf Sperren mit niedriger Priorität ( `MAX_DURATION` Minuten) und ermöglicht die weitere Ausführung anderer Vorgänge, während der Onlineerstellungsvorgang für den Index wartet.  
  
    > **HINWEIS:** Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]verfügbar. Weitere Informationen finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
     Kontrollkästchen**MAXDOP**   
     Überschreibt die Konfigurationsoption "Max. Grad an Parallelität" von sp_configure für DBCC CHECKDB. Weitere Informationen finden Sie unter [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).  
  
#### <a name="define-the-update-statistics-task"></a>Definieren des Tasks "Statistiken aktualisieren"  
  
1.  Geben Sie auf der Seite **Task 'Statistiken aktualisieren' definieren** die Datenbanken an, in denen Tabellen- und Indexstatistiken aktualisiert werden sollen. Für diesen Task wird die `UPDATE STATISTICS`-Anweisung verwendet. Weitere Informationen finden Sie unter [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md). Klicken Sie zum Abschluss auf **Weiter**.  
  
     Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     Liste**Datenbanken**   
     Gibt die Datenbanken an, die von dieser Aufgabe betroffen sind. Weitere Informationen zu den verfügbaren Optionen in dieser Liste finden Sie weiter oben in Schritt 9.  
  
     Liste**Objekt**   
     Begrenzt die Liste **Auswahl** auf die Anzeige von Tabellen und/oder Sichten. Diese Liste ist nur verfügbar, wenn in der obigen Liste **Datenbanken** eine einzelne Datenbank ausgewählt wurde.  
  
     Liste**Auswahl**   
     Gibt die Tabellen oder Indizes an, auf die sich dieser Task auswirkt. Nicht verfügbar, wenn im Objektfeld der Eintrag **Tabellen und Sichten** ausgewählt ist.  
  
     **Alle vorhandenen Statistiken**  
     Aktualisiert alle Statistiken für Spalten und für Indizes.  
  
     **Nur Spaltenstatistiken**  
     Aktualisiert nur Spaltenstatistiken. Verwendet die `WITH COLUMNS` -Option.  
  
     **Nur Indexstatistiken**  
     Aktualisiert nur Indexstatistiken. Verwendet die `WITH INDEX` -Option.  
  
     **Scantyp**  
     Der Typ des Scanvorgangs, der zum Zusammenstellen von aktualisierten Statistiken verwendet wird.  
  
     **Vollständiger Scan**  
     Liest zum Zusammenstellen der Statistiken alle Zeilen in der Tabelle oder Sicht.  
  
     **Stichprobe von**  
     Gibt den prozentualen Anteil der Tabelle oder der indizierten Sicht an bzw. die Anzahl der Zeilen, für die die Stichprobe vorgenommen werden soll, wenn Statistiken für größere Tabellen oder Sichten gesammelt werden.  
  
#### <a name="define-the-history-cleanup-task"></a>Definieren des Tasks "Verlaufscleanup"  
  
1.  Geben Sie auf der Seite **Task 'Verlaufscleanup' definieren** die Datenbanken an, in denen der alte Taskverlauf verworfen werden soll. Dieser Task entfernt Verlaufsinformationen mithilfe der Anweisungen `EXEC sp_purge_jobhistory`, `EXEC sp_maintplan_delete_log`und `EXEC sp_delete_backuphistory` aus den **msdb** -Tabellen. Klicken Sie auf **Weiter**, wenn Sie fertig sind.  
  
     Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     **Wählen Sie die zu löschenden Verlaufsdaten aus**  
     Wählen Sie den zu löschenden Typ von Taskdaten aus.  
  
     **Sicherungs- und Wiederherstellungsverlauf**  
     Das Beibehalten von Datensätzen, in denen festgehalten ist, wann Sicherungen erstellt wurden, kann für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Erstellen eines Wiederherstellungsplans hilfreich sein, wenn Sie eine Datenbank wiederherstellen möchten. Die Beibehaltungsdauer muss mindestens dem Intervall entsprechen, in dem vollständige Datenbanksicherungen erstellt werden.  
  
     **Auftragsverlauf des SQL Server-Agents**  
     Dieser Verlauf kann Ihnen bei der Problembehandlung fehlgeschlagener Aufträge bzw. der Ermittlung der Ursache von Datenbankaktionen helfen.  
  
     **Wartungsplanverlauf**  
     Dieser Verlauf kann Ihnen bei der Problembehandlung fehlgeschlagener Wartungsplanaufträge bzw. der Ermittlung der Ursache von Datenbankaktionen helfen.  
  
     **Verlaufsdaten entfernen, die älter sind als**  
     Geben Sie das Alter an, in dem Elemente gelöscht werden sollen. Sie können **Stunde(n)**, **Tag(e)**, **Woche(n)** (Standardeinstellung), **Monat(e)**oder **Jahr(e)**angeben.  
  
#### <a name="define-the-execute-agent-job-task"></a>Definieren des Tasks zum Ausführen von Agentaufträgen  
  
1.  Wählen Sie auf der Seite **Task 'Agentauftrag ausführen' definieren** unter **Verfügbare Aufträge des SQL Server-Agents**die auszuführenden Aufträge aus. Diese Option ist nicht verfügbar, wenn Sie keine SQL-Agentaufträge besitzen. Für diesen Task wird die `EXEC sp_start_job`-Anweisung verwendet. Weitere Informationen finden Sie unter [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md). Klicken Sie zum Abschluss auf **Weiter**.  
  
#### <a name="define-backup-tasks"></a>Definieren von Sicherungstasks  
  
1.  Wählen Sie auf der Seite **Task 'Datenbank sichern (vollständig)' definieren** die Datenbanken aus, für die eine vollständige Sicherung ausgeführt werden soll. Für diesen Task wird die `BACKUP DATABASE`-Anweisung verwendet. Weitere Informationen finden Sie unter [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md). Klicken Sie auf **Weiter**, wenn Sie fertig sind.  
  
     Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     Liste**Sicherungstyp**   
     Zeigt den Typ der Sicherung an, die ausgeführt werden soll. Dieses Feld ist schreibgeschützt.  
  
     Liste**Datenbanken**   
     Gibt die Datenbanken an, die von dieser Aufgabe betroffen sind. Weitere Informationen zu den verfügbaren Optionen in dieser Liste finden Sie weiter oben in Schritt 9.  
  
     **Sicherungskomponente**  
     Wählen Sie **Datenbank** aus, um die gesamte Datenbank zu sichern. Wählen Sie **Datei und Dateigruppen** aus, um nur einen Teil der Datenbank zu sichern. Bei Auswahl dieser Option müssen Sie die Datei bzw. Dateigruppe angeben. Wenn im Feld **Datenbanken** mehrere Datenbanken ausgewählt wurden, geben Sie für die **Sicherungskomponenten** nur **Datenbanken**an. Erstellen Sie einen Task für jede Datenbank, um Datei- oder Dateigruppensicherungen auszuführen. Diese Optionen sind nur verfügbar, wenn in der obigen Liste **Datenbanken** eine einzelne Datenbank ausgewählt wurde.  
  
     Kontrollkästchen**Sicherungssatz läuft ab**   
     Gibt an, wann der Sicherungssatz für diese Sicherung überschrieben werden kann. Wählen Sie **Nach** aus, und geben Sie die Anzahl von Tagen ein, nach der der Satz ablaufen soll, oder wählen Sie **Am** aus, und geben Sie ein Ablaufdatum ein. Diese Option ist deaktiviert, wenn **URL** als Sicherungsziel ausgewählt ist.  
  
     **Sichern auf**  
     Gibt das Medium an, auf dem die Datenbank gesichert wird. Wählen Sie **Datenträger**, **Band**oder **URL**aus. Es stehen nur Bandmedien zur Verfügung, die an den Computer mit der Datenbank angeschlossen sind.  
  
     **Datenbanken in einer oder in mehreren Dateien sichern**  
     Klicken Sie auf **Hinzufügen** , um das Dialogfeld **Sicherungsziel auswählen** zu öffnen. Diese Option ist deaktiviert, wenn Sie URL als Sicherungsziel ausgewählt haben.  
  
     Klicken Sie auf **Entfernen** , wenn eine Datei aus dem Feld entfernt werden soll.  
  
     Klicken Sie auf **Inhalt** , um den Dateiheader zu lesen und den aktuellen Sicherungsinhalt der Datei anzuzeigen.  
  
     Dialogfeld**Sicherungsziel auswählen**   
     Wählen Sie die Datei, das Bandlaufwerk oder das Sicherungsmedium für das Sicherungsziel aus. Diese Option ist deaktiviert, wenn Sie URL als Sicherungsziel ausgewählt haben.  
  
     Liste**Wenn Sicherungsdateien vorhanden sind**   
     Gibt an, wie vorhandene Sicherungen zu behandeln sind. Wählen Sie **Anfügen** aus, wenn neue Sicherungen in der Datei bzw. auf dem Band nach den vorhandenen Sicherungen eingefügt werden sollen. Wählen Sie **Überschreiben** aus, wenn der alte Inhalt einer Datei oder eines Bands mit der neuen Sicherung überschrieben werden soll.  
  
     **Für jede Datenbank eine Sicherungsdatei erstellen**  
     Erstellt eine Sicherungsdatei an dem im Feld für den Ordner angegebenen Speicherort. Für jede ausgewählte Datenbank wird eine Datei erstellt. Diese Option ist deaktiviert, wenn Sie URL als Sicherungsziel ausgewählt haben.  
  
     Kontrollkästchen**Unterverzeichnis für jede Datenbank erstellen**   
     Erstellt im angegebenen Datenträgerverzeichnis ein Unterverzeichnis, das die Datenbanksicherung für jede im Rahmen des Wartungsplans gesicherte Datenbank enthält.  
  
    > **WICHTIG!** Das Unterverzeichnis erbt Berechtigungen vom übergeordneten Verzeichnis. Schränken Sie die Berechtigungen ein, um einen nicht autorisierten Zugriff zu verhindern.  
  
     Feld**Ordner**   
     Gibt den Ordner an, in dem die automatisch erstellten Datenbankdateien gespeichert werden sollen. Diese Option ist deaktiviert, wenn Sie URL als Sicherungsziel ausgewählt haben.  
  
     **SQL-Anmeldeinformationen**  
     Wählen Sie SQL-Anmeldeinformationen aus, die zur Authentifizierung beim Windows Azure-Speicher verwendet werden sollen. Wenn Sie über keine vorhandenen geeigneten SQL-Anmeldeinformationen verfügen, klicken Sie auf die Schaltfläche **Erstellen** , um neue SQL-Anmeldeinformationen zu erstellen.  
  
    > **WICHTIG!** Das Dialogfeld, das beim Klicken auf **Erstellen** geöffnet wird, erfordert ein Verwaltungszertifikat oder das Veröffentlichungsprofil für das Abonnement. Wenn Sie keinen Zugriff auf das Verwaltungszertifikat oder Veröffentlichungsprofil haben, können Sie SQL-Anmeldeinformationen erstellen, indem Sie den Namen des Speicherkontos und die Informationen zum Zugriffsschlüssel mithilfe von Transact-SQL oder SQL Server Management Studio angeben. Der Beispielcode im Thema [Erstellen von Anmeldeinformationen](../../relational-databases/backup-restore/sql-server-backup-to-url.md#credential) veranschaulicht das Erstellen von Anmeldeinformationen mithilfe von Transact-SQL. Alternativ können Sie auf der Datenbankmodulinstanz in SQL Server Management Studio mit der rechten Maustaste auf **Sicherheit**klicken und **Neu**sowie **Anmeldeinformationen**auswählen. Geben Sie im Feld **Identität** den Namen des Speicherkontos und im Feld **Kennwort** den Zugriffsschlüssel an.  
  
     **Azure-Speichercontainer**  
     Geben Sie den Namen des Windows Azure-Speichercontainers an.  
  
     **URL-Präfix:**  
     Wird automatisch entsprechend den Speicherkontoinformationen, die in den SQL-Anmeldeinformationen gespeichert sind, und dem Namen des Azure-Speichercontainers generiert. Es wird empfohlen, die Informationen in diesem Feld nur zu bearbeiten, wenn Sie eine Domäne mit einem anderen Format als **\<Speicherkonto.blob.core.windows.net** verwenden.  
  
     Feld**Sicherungsdateierweiterung**   
     Gibt die Dateierweiterung an, die für Sicherungsdateien verwendet wird. Der Standardwert lautet BAK.  
  
     Kontrollkästchen**Sicherungsintegrität überprüfen**   
     Überprüft, ob der Sicherungssatz vollständig ist und alle Volumes lesbar sind.  
  
     Kontrollkästchen**Prüfsumme bilden**   
     Prüft jede Seite auf Prüfsumme und zerrissene Seiten (wenn aktiviert und verfügbar) und generiert eine Prüfsumme für die gesamte Sicherung.  
  
     Kontrollkästchen**Bei Fehler fortsetzen**   
     BACKUP wird auch dann fortgesetzt, wenn Fehler auftreten, z. B. ungültige Prüfsummen oder zerrissene Seiten.  
  
     **Verschlüsseln der Sicherung**  
     Um eine verschlüsselte Sicherung zu erstellen, aktivieren Sie das Kontrollkästchen **Sicherung verschlüsseln** . Wählen Sie einen Verschlüsselungsalgorithmus für den Verschlüsselungsschritt aus, und geben Sie ein Zertifikat oder einen asymmetrischen Schlüssel aus der Liste der vorhandenen Zertifikate und asymmetrischen Schlüssel an. Folgende Algorithmen stehen für die Verschlüsselung zur Verfügung:  
  
    -   AES 128  
  
    -   AES 192  
  
    -   AES 256  
  
    -   Triple DES  
  
     Die Verschlüsselungsoption ist deaktiviert, wenn Sie ausgewählt haben, dass die Sicherung an einen vorhandenen Sicherungssatz angefügt werden soll.  
  
     Es ist ratsam, das Zertifikat bzw. die Schlüssel zu sichern und an einem anderen Speicherort als dem der verschlüsselten Sicherung zu speichern.  
  
     Es werden nur Schlüssel aus der erweiterbaren Schlüsselverwaltung (Extensible Key Management, EKM) unterstützt.  
  
     Kontrollkästchen**Blockgröße** , Liste  
  
     Legt die physische Blockgröße in Bytes fest. Diese Option hat i. d. R. dann Auswirkungen auf die Leistung, wenn auf Bandmedien, RAID-Arrays oder SAN geschrieben wird.  
  
     Kontrollkästchen**Maximale Übertragungsgröße** , Liste  
  
     Gibt die größte zu verwendende Übertragungseinheit zwischen SQL Server und dem Sicherungsmedium in Byte an.  
  
     Liste**Sicherungskomprimierung festlegen**    
     Wählen Sie in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (oder höher) einen der folgenden Werte für die [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md) aus:  
  
    |||  
    |-|-|  
    |**Standardservereinstellungen verwenden**|Klicken Sie hier, um die Standardeinstellung auf Serverebene zu verwenden. Diese Standardeinstellung wird durch die Serverkonfigurationsoption **Komprimierungsstandard für Sicherung** festgelegt. Informationen zum Anzeigen der aktuellen Einstellung dieser Option finden Sie unter [Anzeigen oder Konfigurieren der Serverkonfigurationsoption „Standardeinstellung für die Sicherungskomprimierung“](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
    |**Sicherung komprimieren**|Klicken Sie hier, um die Sicherung unabhängig von der Standardeinstellung auf Serverebene zu komprimieren.<br /><br /> **\*\* Wichtig \*\*** Standardmäßig steigt die CPU-Nutzung durch die Komprimierung erheblich, und die bei der Komprimierung zusätzlich verbrauchten CPU-Ressourcen können sich negativ auf gleichzeitige Vorgänge auswirken. Daher ist es u. U. sinnvoll, in einer Sitzung, bei der die CPU-Nutzung durch die Ressourcenkontrolle eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen. Weitere Informationen finden Sie unter [Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen.|  
    |**Sicherung nicht komprimieren**|Klicken Sie hier, um unabhängig von der Standardeinstellung auf Serverebene eine nicht komprimierte Sicherung zu erstellen.|  
  
2.  Wählen Sie auf der Seite **Task 'Datenbank sichern (differenziell)' definieren** die Datenbanken aus, für die eine Teilsicherung ausgeführt werden soll. Weitere Informationen zu den verfügbaren Optionen auf dieser Seite finden Sie in der Definitionsliste in Schritt 16 oben. Für diesen Task wird die `BACKUP DATABASE … WITH DIFFERENTIAL`-Anweisung verwendet. Weitere Informationen finden Sie unter [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  Klicken Sie auf **Weiter**, wenn Sie fertig sind.  
  
3.  Wählen Sie auf der Seite **Task 'Datenbank sichern (Transaktionsprotokoll)' definieren** die Datenbanken aus, in denen eine Sicherung für ein Transaktionsprotokoll ausgeführt werden soll. Weitere Informationen zu den verfügbaren Optionen auf dieser Seite finden Sie in der Definitionsliste in Schritt 16 oben. Für diesen Task wird die `BACKUP LOG`-Anweisung verwendet. Weitere Informationen finden Sie unter [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md). Klicken Sie auf **Weiter**, wenn Sie fertig sind.  
  
#### <a name="define-maintenance-cleanup-tasks"></a>Definieren von Wartungscleanuptasks  
  
1.  Geben Sie auf der Seite **Task 'Wartungscleanup' definieren** die Dateitypen an, die im Rahmen des Wartungsplans gelöscht werden sollen (einschließlich Textberichte, die durch Wartungspläne erstellt wurden, sowie Datenbanksicherungsdateien). Für diesen Task wird die `EXEC xp_delete_file` -Anweisung verwendet. Klicken Sie auf **Weiter**, wenn Sie fertig sind.  
  
    > **WICHTIG!** Dateien in den Unterordnern des angegebenen Verzeichnisses werden von diesem Task nicht automatisch gelöscht. Mit dieser Sicherheitsmaßnahme wird die Möglichkeit eines bösartigen Angriffs, bei dem der Task Wartungscleanup zum Löschen von Dateien verwendet wird, reduziert. Wenn Sie Dateien in Unterordnern auf oberster Ebene löschen möchten, müssen Sie **Unterordner auf oberster Ebene einschließen**auswählen.  
  
     Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     **Dateien folgenden Typs löschen**  
     Geben Sie den zu löschenden Dateityp an.  
  
     **Sicherungsdateien**  
     Löscht Sicherungsdateien von Datenbanken.  
  
     **Textberichte für Wartungsplan**  
     Löscht Textberichte über zuvor ausgeführte Wartungspläne.  
  
     **Dateispeicherort**  
     Geben Sie den Pfad der zu löschenden Dateien an.  
  
     **Bestimmte Datei löschen**  
     Löscht die im Textfeld **Dateiname** angegebene Datei.  
  
     **Ordner durchsuchen und Dateien anhand einer Erweiterung löschen**  
     Löscht alle Dateien mit der angegebenen Erweiterung im angegebenen Ordner. Mithilfe dieser Option können Sie mehrere Dateien gleichzeitig löschen, z. B. alle Sicherungsdateien mit der Erweiterung BAK im ausgewählten Ordner Tuesday.  
  
     Feld**Ordner**   
     Pfad und Name des Ordners, in dem die zu löschenden Dateien enthalten sind.  
  
     Feld**Dateierweiterung**   
     Geben Sie die Dateierweiterung der zu löschenden Dateien an. Um mehrere Dateien gleichzeitig zu löschen, z. B. alle Sicherungsdateien mit der Erweiterung .bak im Ordner Tuesday, geben Sie .bak an.  
  
     Kontrollkästchen**Unterordner auf oberster Ebene einschließen**   
     Löscht Dateien mit der für **Dateierweiterung** angegebenen Erweiterung aus den Unterordnern der obersten Ebene unter dem in **Ordner**angegebenen Ordner.  
  
     Kontrollkästchen**Dateien anhand ihres Alters zur Tasklaufzeit löschen**   
     Geben Sie das Mindestalter der zu löschenden Dateien an, indem Sie im Feld **Dateien löschen, die älter sind als** eine Zahl und eine Zeiteinheit festlegen.  
  
     **Dateien löschen, die älter sind als**  
     Geben Sie das Mindestalter der zu löschenden Dateien an, indem Sie eine Zahl und eine Zeiteinheit (**Stunde**, **Tag**, **Woche**, **Monat**oder **Jahr**) angeben. Dateien, die älter sind als der angegebene Zeitrahmen, werden gelöscht.  
  
#### <a name="select-report-options"></a>Berichtsoptionen auswählen  
  
1.  Aktivieren Sie auf der Seite **Berichtsoptionen auswählen** Optionen zum Speichern oder Verteilen eines Berichts der Wartungsplanaktionen. Für diesen Task wird die `EXEC sp_notify_operator`-Anweisung verwendet. Weitere Informationen finden Sie unter [sp_notify_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-notify-operator-transact-sql.md). Klicken Sie zum Abschluss auf **Weiter**.  
  
     Die folgenden Optionen sind auf dieser Seite verfügbar.  
  
     Kontrollkästchen**Bericht in eine Textdatei schreiben**   
     Speichert den Bericht in einer Datei.  
  
     Feld**Speicherort des Ordners**   
     Geben Sie den Speicherort der Berichtsdatei an.  
  
     Kontrollkästchen**Bericht als E-Mail senden**   
     Sendet eine E-Mail, wenn ein Task fehlschlägt. Zur Verwendung dieses Tasks muss Datenbank-E-Mail aktiviert und korrekt mit MSDB als Mailhost-Datenbank und einem [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentoperator mit einer gültigen E-Mail-Adresse konfiguriert sein.  
  
     **Agentoperator**  
     Gibt den Empfänger der E-Mail an.  
  
     **Mailprofil**  
     Gibt das Profil an, das den Absender der E-Mail definiert.  
  
#### <a name="complete-the-wizard"></a>Assistenten abschließen  
  
1.  Überprüfen Sie auf der Seite **Assistenten abschließen** die auf den vorherigen Seiten ausgewählten Optionen, und klicken Sie auf **Fertig stellen**.  
  
2.  Auf der Seite **Status des Wartungsplanungs-Assistenten** können Sie Statusinformationen zu den vom Assistenten ausgeführten Aktionen überwachen. Je nach den im Assistenten ausgewählten Optionen enthält diese Seite eine oder mehrere Aktionen. Im oberen Feld werden der Gesamtstatus des Assistenten und die Anzahl der empfangenen Status-, Fehler- und Warnmeldungen angezeigt.  
  
     Die folgenden Optionen sind auf der Seite **Status des Wartungsplanungs-Assistenten** verfügbar:  
  
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
  
  

