---
title: Assistent zum Verwalten von Partitionen (F1-Hilfe) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: partitions
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-partition
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.swb.managepartition.createjob.f1
- sql13.swb.managepartition.progress.f1
- sql13.swb.managepartition.getstart.f1
- sql13.swb.managepartition.selectswitchtables.f1
- sql13.swb.managepartition.stagingtable.f1
- sql13.swb.managepartition.switchin.f1
- sql13.swb.managepartition.switchout.f1
- sql13.swb.managepartition.partitionaction.f1
- sql13.swb.managepartition.summary.f1
- sql13.swb.managepartition.selectoutput.f1
helpviewer_keywords: wizards [SQL Server Management Studio] See Manage Partition Wizard
ms.assetid: e2478d26-dea4-428d-98c5-aad2d2a30da8
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 25be7d99d07300731a9395b096f316faef973eef
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="manage-partition-wizard-f1-help"></a>Assistent zum Verwalten von Partitionen (F1-Hilfe)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mit dem **Assistenten zum Verwalten von Partitionen** können Sie vorhandene partitionierte Tabellen durch Partitionswechsel oder Implementierung eines Szenarios mit gleitendem Fenster verwalten und ändern. Dieser Assistent vereinfacht die Verwaltung von Partitionen und die Migration von Daten in die und aus den Tabellen.  
  
### <a name="to-start-the-manage-partition-wizard"></a>So starten Sie den Assistenten zum Verwalten von Partitionen  
  
-   Wählen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die Datenbank aus, klicken Sie mit der rechten Maustaste auf die Tabelle, für die Sie Partitionen erstellen möchten, zeigen Sie auf **Speicher**, und klicken Sie anschließend auf **Partition verwalten**.  
  
     **Note** Wenn **Partition verwalten** nicht verfügbar ist, haben Sie möglicherweise eine Tabelle ohne Partitionen ausgewählt. Klicken Sie im Untermenü **Speicher** auf **Partition erstellen** , und erstellen Sie mit dem **Assistenten zum Erstellen von Partitionen** Partitionen in der Tabelle.  
  
 Allgemeine Informationen zu Partitionen und Indizes finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Dieser Abschnitt stellt die Informationen bereit, die zum Verwalten, Ändern und Implementieren von Partitionen mit dem **Assistenten zum Verwalten von Partitionen** erforderlich sind.  
  
##  <a name="Top"></a> In diesem Abschnitt  
 Die folgenden Abschnitte stellen Hilfe für die Seiten des **Assistenten zum Verwalten von Partitionen**bereit.  
  
 [Assistent zum Verwalten von Partitionen (Seite 'Partitionsaktion auswählen')](#SelectPartitionAction)  
  
 [Assistent zum Verwalten von Partitionen (Seite "Einfügen")](#SwitchIn)  
  
 [Assistent zum Verwalten von Partitionen (Seite "Auslagern")](#SwitchOut)  
  
 [Assistent zum Verwalten von Partitionen (Seite 'Stagingtabellenoptionen auswählen')](#StagingTableOptions)  
  
 [Assistent zum Verwalten von Partitionen (Seite 'Ausgabeoption auswählen')](#OutputOption)  
  
 [Assistent zum Verwalten von Partitionen (Seite 'Neuer Auftragszeitplan')](#NewJob)  
  
 [Assistent zum Verwalten von Partitionen (Seite 'Zusammenfassung')](#Summary)  
  
 [Assistent zum Verwalten von Partitionen (Seite 'Status')](#Progress)  
  
##  <a name="SelectPartitionAction"></a> Partitionsaktion auswählen (Seite)  
 Auf der Seite **Partitionsaktion auswählen** können Sie die Aktion auswählen, die Sie für die Partition ausführen möchten.  
  
### <a name="create-a-staging-table"></a>Erstellen einer Stagingtabelle  
 Der Partitionswechsel ist ein gängiger Partitionstask, wenn Sie über eine partitionierte Tabelle verfügen, in die bzw. aus der Sie regelmäßig Daten migrieren. Beispiel: Sie verfügen über eine partitionierte Tabelle, in der aktuelle vierteljährliche Daten gespeichert sind, und müssen zum Ende jedes Quartals alte Daten auslagern und neue Daten einfügen.  
  
 Mithilfe des Assistenten können Sie die Stagingtabelle mit der gleichen Partitionsspalte, Tabelle und Spaltenstruktur sowie Indizes entwerfen. Die neue Tabelle wird in der Dateigruppe gespeichert, in der sich auch die Quellpartition befindet.  
  
 Wählen Sie **Stagingtabelle für den Partitionswechsel erstellen**, um eine Stagingtabelle zum Einfügen und Auslagern von Partitionsdaten zu erstellen.  
  
### <a name="sliding-window-scenario"></a>Szenario mit gleitendem Fenster  
 Um die Partitionen in einem flexiblen Fenster zu verwalten, wählen Sie **Partitionierte Daten in einem Szenario mit gleitendem Fenster verwalten**.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Stagingtabelle für den Partitionswechsel erstellen**  
 Erstellt eine Stagingtabelle für die Daten, die Sie aus der vorhandenen partitionierten Tabelle auslagern bzw. darin einfügen.  
  
 **Partition auslagern**  
 Stellt Optionen beim Entfernen einer Partition aus der Tabelle bereit.  
  
 **Partition einfügen**  
 Stellt Optionen beim Hinzufügen einer Partition zur Tabelle bereit.  
  
 **Partitionierte Daten in einem Szenario mit gleitendem Fenster verwalten**  
 Fügt eine leere Partition an die vorhandene Tabelle an, die zum Einfügen und Auslagern von Daten verwendet werden kann. Der Assistent unterstützt derzeit das Einfügen in die letzte Partition und das Auslagern aus der ersten Partition.  
  
 ![Pfeilsymbol, das mit dem Link „Zurück zum Anfang“ verwendet wird](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [In diesem Abschnitt](#Top)  
  
##  <a name="SwitchIn"></a> Partitionseinfügeoptionen auswählen (Seite)  
 Auf der Seite **Partitionseinfügeoptionen auswählen** können Sie die Stagingtabelle erstellen, die Sie in die partitionierte Tabelle einfügen.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Alle Partitionen anzeigen**  
 Wählen Sie diese Option zum Anzeigen aller Partitionen aus, einschließlich der Partitionen, die sich gegenwärtig in der partitionierten Tabelle befinden.  
  
 **Partitionsschema**  
 Zeigt den Partitionsnamen, **Linke Begrenzung**, **Rechte Begrenzung**, **Dateigruppe**und **Zeilenanzahl** der Partitionen an, die Sie ausgewählt haben.  
  
 **Einzufügende Tabelle**  
 Wählen Sie die Stagingtabelle aus, die die Partition enthält, die Sie der partitionierten Tabelle hinzufügen möchten. Sie müssen diese Stagingtabelle erstellen, bevor Sie Partitionen mit dem Assistenten zum **Verwalten von Partitionen**einfügen können.  
  
 ![Pfeilsymbol, das mit dem Link „Zurück zum Anfang“ verwendet wird](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [In diesem Abschnitt](#Top)  
  
##  <a name="SwitchOut"></a> Partitionsauslagerungsoptionen auswählen (Seite)  
 Auf der Seite **Partitionsauslagerungsoptionen auswählen** können Sie die Partition und die Stagingtabelle für die partitionierten Daten auswählen, die aus der partitionierten Tabelle ausgelagert werden.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Partitionsschema**  
 Zeigt den Partitionsnamen, **Linke Begrenzung**, **Rechte Begrenzung**, **Dateigruppe**und **Zeilenanzahl** der Partitionen an, die Sie ausgewählt haben.  
  
 **Tabelle auslagern**  
 Wählen Sie eine neue oder vorhandene Tabelle aus, in die Sie die Daten auslagern.  
  
 **Neu**  
 Geben Sie einen Namen für die neue Stagingtabelle ein, die zum Auslagern der Partition aus der aktuellen Quelltabelle verwendet werden soll.  
  
 **Vorhanden**  
 Wählen Sie die vorhandene Stagingtabelle aus, die zum Auslagern der Partition aus der aktuellen Quelltabelle verwendet werden soll. Wenn die vorhandene Tabelle Daten enthält, werden diese mit den Daten überschrieben, die Sie auslagern.  
  
 ![Pfeilsymbol, das mit dem Link „Zurück zum Anfang“ verwendet wird](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [In diesem Abschnitt](#Top)  
  
##  <a name="StagingTableOptions"></a> Stagingtabellenoptionen auswählen (Seite)  
 Auf der Seite **Stagingtabellenoptionen auswählen** können Sie die Stagingtabelle erstellen, die zum Verschieben der partitionierten Daten verwendet werden soll.  
  
 Stagingtabellen müssen sich in der gleichen Dateigruppe der ausgewählten Partition befinden, in der sich auch die Quelltabelle befindet. Der Entwurf der Stagingtabelle muss dem der Quell- und der Zieltabelle entsprechen.  
  
 Sie können auch in der Stagingtabelle die gleichen Indizes erstellen, die in der Quellpartition vorhanden ist. Die Stagingtabelle enthält automatisch eine Einschränkung auf Grundlage der Elemente der Quellpartition. Diese Einschränkung wird i. d. R. aus dem Begrenzungswert der Quellpartition generiert.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Stagingtabellenname**  
 Erstellen Sie einen Namen für die Stagingtabelle, oder übernehmen Sie den im Eingabefeld angezeigten Standardnamen.  
  
 **Partition wechseln**  
 Wählen Sie die Quellpartition aus, die Sie aus der aktuellen Tabelle auslagern möchten.  
  
 **Neuer Begrenzungswert**  
 Wählen Sie den gewünschten Begrenzungswert für die Partition in der Stagingtabelle aus, oder geben Sie einen Begrenzungswert ein.  
  
 **Dateigruppe**  
 Wählen Sie eine Dateigruppe für die neue Tabelle aus.  
  
 ![Pfeilsymbol, das mit dem Link „Zurück zum Anfang“ verwendet wird](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [In diesem Abschnitt](#Top)  
  
##  <a name="OutputOption"></a> Ausgabeoption auswählen (Seite)  
 Geben Sie auf der Seite **Ausgabeoption auswählen** an, wie Sie die Änderungen für Ihre Partitionen abschließen möchten.  
  
### <a name="create-script"></a>Erstellen von Skripts  
 Bei Abschluss des Assistenten wird im Abfrage-Editor ein Skript zum Ändern der Partitionen in der Tabelle erstellt. Wählen Sie **Skript erstellen** aus, wenn Sie das Skript überprüfen möchten, und führen Sie das Skript dann manuell aus.  
  
 **Skript in Datei schreiben**  
 Generiert das Skript in einer SQL-Datei. Geben Sie entweder **Unicode** oder **ANSI-Text**an. Klicken Sie auf **Durchsuchen**, um einen Namen und einen Speicherort für die Datei anzugeben.  
  
 **Skript in Zwischenablage schreiben**  
 Speichert das Skript in die Zwischenablage.  
  
 **Skript in Fenster "Neue Abfrage" schreiben**  
 Generiert das Skript in einem Abfrage-Editor-Fenster. Wenn kein Editor-Fenster geöffnet ist, wird ein neues Editor-Fenster als Skriptziel geöffnet.  
  
### <a name="run-immediately"></a>Sofort ausführen  
 **Run immediately**  
 Wenn Sie auf **Weiter** oder **Fertig stellen**klicken, schließt der Assistent die Änderungen an den Partitionen ab.  
  
### <a name="schedule"></a>Zeitplan  
 Wählen Sie diese Option aus, um die Tabellenpartitionen zu einem geplanten Datum und einer geplanten Uhrzeit zu ändern.  
  
 **Zeitplan ändern**  
 Hiermit wird das Dialogfeld **Neuer Auftragszeitplan** geöffnet, in dem Sie die Eigenschaften des geplanten Auftrags auswählen, ändern oder anzeigen können.  
  
 ![Pfeilsymbol, das mit dem Link „Zurück zum Anfang“ verwendet wird](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [In diesem Abschnitt](#Top)  
  
##  <a name="NewJob"></a> Neuer Auftragszeitplan (Seite)  
 Verwenden Sie die Seite **Neuer Auftragszeitplan** , um die Eigenschaften des Zeitplans anzuzeigen und zu ändern.  
  
### <a name="options"></a>Optionen  
 Wählen Sie den Typ des gewünschten Zeitplans für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag aus.  
  
 **Name**  
 Geben Sie einen neuen Namen für den Zeitplan ein.  
  
 **Aufträge im Zeitplan**  
 Zeigen Sie die vorhandenen Aufträge an, die den Zeitplan verwenden.  
  
 **Zeitplantyp**  
 Wählen Sie den Zeitplantyp aus.  
  
 **Aktiviert**  
 Aktivieren oder deaktivieren Sie den Zeitplan.  
  
### <a name="recurring-schedule-types-options"></a>Zeitplantypoptionen für wiederkehrende Aufträge  
 Wählen Sie die Häufigkeit des geplanten Auftrags aus.  
  
 **Tritt auf**  
 Wählen Sie das Intervall aus, nach dem der Zeitplan wiederholt wird.  
  
 **Wiederholen alle**  
 Wählen Sie die Anzahl der Tage oder Wochen aus, die zwischen der wiederholten Ausführung des Zeitplans liegen. Bei monatlichen Zeitplänen ist diese Option nicht verfügbar.  
  
 **Montag**  
 Legt fest, dass der Auftrag an einem Montag ausgeführt wird. Nur bei wöchentlichen Zeitplänen verfügbar.  
  
 **Dienstag**  
 Legt fest, dass der Auftrag an einem Dienstag ausgeführt wird. Nur bei wöchentlichen Zeitplänen verfügbar.  
  
 **Mittwoch**  
 Legt fest, dass der Auftrag an einem Mittwoch ausgeführt wird. Nur bei wöchentlichen Zeitplänen verfügbar.  
  
 **Donnerstag**  
 Legt fest, dass der Auftrag an einem Donnerstag ausgeführt wird Nur bei wöchentlichen Zeitplänen verfügbar.  
  
 **Freitag**  
 Legt fest, dass der Auftrag an einem Freitag ausgeführt wird Nur bei wöchentlichen Zeitplänen verfügbar.  
  
 **Samstag**  
 Legt fest, dass der Auftrag an einem Samstag ausgeführt wird Nur bei wöchentlichen Zeitplänen verfügbar.  
  
 **Sonntag**  
 Legt fest, dass der Auftrag an einem Sonntag ausgeführt wird Nur bei wöchentlichen Zeitplänen verfügbar.  
  
 **Day**  
 Wählen Sie den Tag des Monats aus, an dem der Zeitplan ausgeführt werden soll. Nur bei monatlichen Zeitplänen verfügbar.  
  
 **alle**  
 Wählen Sie die Anzahl der Monate aus, die zwischen wiederholten Ausführungen des Zeitplans liegen sollen. Nur bei monatlichen Zeitplänen verfügbar.  
  
 **Am**  
 Geben Sie einen Zeitplan für den Wochentag einer bestimmten Woche des Monats an. Nur bei monatlichen Zeitplänen verfügbar.  
  
 **Einmalig um**  
 Legen Sie die Uhrzeit für einen täglich auszuführenden Auftrag fest.  
  
 **Alle**  
 Legt die Anzahl von Stunden und Minuten zwischen den Ausführungen fest.  
  
 **Startdatum**  
 Legt fest, ab welchem Datum dieser Zeitplan gültig ist.  
  
 **Enddatum**  
 Legen Sie fest, ab welchem Datum der Zeitplan nicht mehr gültig ist.  
  
 **Kein Enddatum**  
 Geben Sie an, dass der Zeitplan für unbestimmte Zeit gültig bleibt.  
  
### <a name="one-time-schedule-types-options"></a>Zeitplantypoptionen für einmalige Aufträge  
 Wenn ein Zeitplan nur einmalig ausgeführt werden soll, müssen Sie ein Datum und eine Uhrzeit in der Zukunft auswählen.  
  
 **Datum**  
 Wählen Sie das Datum aus, an dem der Auftrag ausgeführt wird.  
  
 **Zeit**  
 Wählen Sie die Uhrzeit aus, zu der der Auftrag ausgeführt wird.  
  
 ![Pfeilsymbol, das mit dem Link „Zurück zum Anfang“ verwendet wird](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [In diesem Abschnitt](#Top)  
  
##  <a name="Summary"></a> Seite "Zusammenfassung"  
 Mithilfe der Seite **Zusammenfassung** können Sie die Optionen überprüfen, die Sie auf den vorherigen Seiten ausgewählt haben.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Überprüfen Sie Ihre Auswahl**  
 Zeigt die auf den einzelnen Seiten des Assistenten getroffene Auswahl an. Klicken Sie auf einen Knoten, um diesen zu erweitern und die ausgewählten Optionen anzuzeigen.  
  
 ![Pfeilsymbol, das mit dem Link „Zurück zum Anfang“ verwendet wird](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [In diesem Abschnitt](#Top)  
  
##  <a name="Progress"></a> Status (Seite)  
 Auf der Seite **Status** können Sie Statusinformationen zu den Aktionen im **Assistenten zum Verwalten von Partitionen**anzeigen. Je nach den im Assistenten ausgewählten Optionen enthält die Seite **Status** eine oder mehrere Aktionen. Im oberen Feld werden der Gesamtstatus des Assistenten und die Anzahl der empfangenen Status-, Fehler- und Warnmeldungen angezeigt.  
  
### <a name="options"></a>Optionen  
 **Details**  
 Stellt für jede vom Assistenten ausgeführte Aktion Informationen zur Aktion, zum Status und zu den zurückgegebenen Meldungen bereit.  
  
 **Aktion**  
 Gibt den Typ und den Namen jeder Aktion an.  
  
 **Status**  
 Gibt an, ob für die Aktion des Assistenten insgesamt der Wert **Erfolg** oder der Wert **Fehler**zurückgegeben wurde.  
  
 **MessageBox**  
 Stellt alle vom Prozess zurückgegebenen Fehler- oder Warnmeldungen bereit.  
  
 **Beenden**  
 Beendet die Aktion des Assistenten.  
  
 **Bericht**  
 Dient zum Erstellen eines Berichts mit den Ergebnissen des **Assistenten zum Verwalten von Partitionen**. Folgende Optionen sind verfügbar:  
  
-   **Bericht anzeigen**  
  
-   **Bericht in Datei speichern**  
  
-   **Bericht in Zwischenablage kopieren**  
  
-   **Bericht als E-Mail senden**  
  
 **Bericht anzeigen**  
 Öffnet das Dialogfeld **Bericht anzeigen** . Dieses Dialogfeld enthält einen Textbericht zum Status des **Assistenten zum Verwalten von Partitionen**.  
  
 **Schließen**  
 Schließen Sie den Assistenten.  
  
 ![Pfeilsymbol, das mit dem Link „Zurück zum Anfang“ verwendet wird](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [In diesem Abschnitt](#Top)  
  
## <a name="see-also"></a>Siehe auch  
 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  
