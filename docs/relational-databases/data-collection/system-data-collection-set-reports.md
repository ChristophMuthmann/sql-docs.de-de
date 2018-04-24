---
title: Berichte der Systemdaten-Sammlungssätze | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: data-collection
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data collector [SQL Server], server activity
- server activity [SQL Server]
- reports [SQL Server], data collection
- reports [SQL Server], disk usage
- collection sets [SQL Server], reports
- data collector [SQL Server], reports
- reports [SQL Server], query statistics
- query statistics reports [SQL Server]
- disk usage reports [SQL Server]
ms.assetid: 0b126b8d-4fe7-443d-8a9a-c266350181e5
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a7edb1ffcbc2a1679bdae6f01ff0fed50562704
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="system-data-collection-set-reports"></a>Berichte der Systemdaten-Sammlungssätze
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Datensammler stellt einen Verlaufsbericht für jeden der Systemdaten-Sammlungssätze bereit. Jeder der folgenden Berichte verwendet Daten, die im Verwaltungs-Data Warehouse gespeichert werden:  
  
-   [Zusammenfassung der Datenträgerverwendung](#Disk)  
  
-   [Abfragestatistik - Verlauf](#Query)  
  
-   [Serveraktivität - Verlauf](#Server)  
  
 Sie können diese Berichte verwenden, um Informationen zum Überwachen der Systemkapazität und zur Behandlung von Problemen mit der Systemleistung abzurufen.  
  
##  <a name="Disk"></a> Bericht über die Zusammenfassung der Datenträgerverwendung  
 Der Bericht über die Zusammenfassung der Datenträgerverwendung enthält Daten über die Speicherplatzverwendung aller Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die in den Berichten bereitgestellten Daten werden unter Verwendung des Sammlungssatzes für die Datenträgerverwendung ermittelt, der den generischen T-SQL-Abfragensammlertyp verwendet.  
  
 Sie können auf den Bericht über die Zusammenfassung der Datenträgerverwendung vom Objekt-Explorer aus zugreifen. Erweitern Sie den Ordner **Verwaltung** , klicken Sie mit der rechten Maustaste auf **Datensammlung**, zeigen Sie auf **Berichte**und anschließend auf **Verwaltungs-Data Warehouse**, und klicken Sie auf **Zusammenfassung der Datenträgerverwendung**, um den Bericht anzuzeigen. Weitere Informationen finden Sie unter [Anzeigen eines Sammlungssatzberichts &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="disk-usage-collection-set-report"></a>Bericht über den Sammlungssatz für Datenträgerverwendung  
 Der Bericht über den Sammlungssatz für Datenträgerverwendung enthält eine Übersicht über den Speicherplatz, der für alle Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet wird, sowie die Vergrößerungstrends der Daten- und Protokolldateien für die einzelnen Datenbanken.  
  
-   In der Zusammenfassungstabelle werden die anfängliche Größe (in Megabytes) und die aktuelle Größe aller Datenbanken angezeigt, die auf dem Server installiert sind, den der Datensammler überwacht.  
  
-   Der Trend und die Informationen zur durchschnittlichen Vergrößerung werden grafisch und numerisch für Daten- und Protokolldateien dargestellt.  
  
#### <a name="disk-usage-collection-set---database-databasename-subreport"></a>Unterbericht "Sammlungssatz für Datenträgerverwendung – Datenbank: <Datenbankname>"  
 Der Unterbericht „Sammlungssatz für Datenträgerverwendung – Datenbank: *<Datenbankname>*“ wird angezeigt, wenn Sie auf eine Trendlinie für eine bestimmte Datenbank oder Protokolldatei in der Zusammenfassungstabelle des Berichts über den Sammlungssatz für Datenträgerverwendung klicken. Dieser Bericht liefert eine grafische Darstellung der Vergrößerungstrends bei der Speicherplatzverwendung während des Berichtzeitraums. Die Datenträgerverwendung ist nach verwendetem Speicher, Datenspeicherplatz, nicht zugeordnetem Speicher sowie dem Indexspeicher für Datendateien und dem verwendeten und nicht verwendeten Speicherplatz für Protokolldateien gegliedert.  
  
 In der Tabelle unter dem Diagramm sind Datensammlungszeiten und zugehörige Nutzungsdaten aufgeführt.  
  
#### <a name="disk-usage-for-database-databasename-subreport"></a>Unterbericht "Datenträgerverwendung für Datenbank: <Datenbankname>"  
 Der Unterbericht **Datenträgerverwendung für Datenbank:***<Datenbankname>* wird angezeigt, wenn Sie in der Zusammenfassungstabelle des Berichts zum Sammlungssatz für die Datenträgerverwendung auf einen Datenbanknamen klicken. Dieser Bericht liefert eine numerische und grafische Aufschlüsselung der Speicherplatzverwendung durch die Daten- und Transaktionsprotokolldateien der Datenbank. Die Speicherplatzverwendung für Datendateien wird als Prozentsatz angegeben, kategorisiert nach dem prozentualen Anteil, der den Indexseiten, dem nicht zugeordneten Speicherplatz, den Datenseiten und dem nicht verwendeten Speicherplatz zugeordnet ist. Diese Kategorien sind folgendermaßen definiert:  
  
|Kategorie|Definition|  
|--------------|----------------|  
|Index|Der verwendete Speicherplatz für Indexseiten|  
|Nicht zugeordnet|Der für die Datenbank verfügbare Speicherplatz, der jedoch noch keinem Objekt zugeordnet wurde|  
|data|Der von Datenseiten verwendete Speicherplatz|  
|Nicht verwendet|Der Speicherplatz, der mindestens einem Objekt zugeordnet, jedoch noch nicht verwendet wurde|  
  
 Die Speicherplatzverwendung für die Transaktionsprotokolldatei ist als verwendeter und nicht verwendeter Speicherplatz kategorisiert.  
  
 Automatische Vergrößerungs- und Verkleinerungsereignisse werden für Daten- und Protokolldateien aufgeführt, wenn diese Ereignisse in der Datenbank stattgefunden haben. Im Bericht werden die Startzeit und Dauer jedes Ereignisses sowie die resultierende Änderung der Dateigröße angezeigt.  
  
 Der von jeder Datendatei in der Datenbank verwendete Speicherplatz wird aufgeführt. Reservierter Speicherplatz ist die Menge von verwendetem Speicherplatz plus dem Speicherplatz, der der Datei zugeordnet, jedoch noch nicht verwendet wurde. Verwendeter Speicherplatz ist der tatsächlich von der Datei momentan verwendete Speicherplatz, ohne den zugeordneten Speicherplatz.  
  
##  <a name="Query"></a> Bericht "Abfragestatistik - Verlauf"  
 Der Bericht Abfragestatistik - Verlauf enthält Statistiken zur Abfrageausführung. Die Daten in diesem Bericht werden unter Verwendung des Sammlungssatzes für die Abfragestatistik ermittelt, der den Abfrageaktivitäts-Sammlertyp verwendet.  
  
 Sie können auf den Bericht Abfragestatistik - Verlauf über den Objekt-Explorer zugreifen. Erweitern Sie den Ordner **Verwaltung** , klicken Sie mit der rechten Maustaste auf **Datensammlung**, zeigen Sie auf **Berichte**und anschließend auf **Verwaltungs-Data Warehouse**, und klicken Sie auf **Abfragestatistik – Verlauf**, um den Bericht anzuzeigen. Weitere Informationen finden Sie unter [Anzeigen eines Sammlungssatzberichts &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="selecting-data-to-include-in-the-report"></a>Auswählen von Daten zum Einschließen in den Bericht  
 Der Bericht enthält Statistiken zur Abfrageausführung für den gesamten Zeitraum der Datensammlung. Sie können durch die Datensammlungszeitachse auf zwei Arten navigieren, um ein Datensegment zur Ansicht auszuwählen.  
  
 **Zeitachsensteuerelement und Navigationsschaltflächen**  
  
 Verwenden Sie das Zeitachsensteuerelement und die Navigationsschaltflächen, um durch die Zeitachse zu navigieren oder einen Datumsbereich auszuwählen. Über die Pfeilschaltflächen können Sie nach links bzw. nach rechts blättern und sich so rückwärts bzw. vorwärts durch die Zeitachse bewegen. In der Standardeinstellung navigieren Sie mit den Pfeilschaltflächen in 4-Stunden-Schritten durch die Zeitachse. Mit den Lupenschaltflächen können Sie diesen Zeitschritt auf einen der folgenden Werte vergrößern oder verkleinern: 15 Minuten, 1 Stunde, 4 Stunden, 12 Stunden oder 24 Stunden. Der aktuell ausgewählte Zeitbereich wird durch den hervorgehobenen Teil der Zeitachse dargestellt und im Text unter der Zeitachse angezeigt. Diese Werte, sowie die Daten im Bericht, werden immer aktualisiert, wenn Sie auf die Zeitachse klicken oder die Navigationsschaltflächen verwenden.  
  
 **Schaltfläche "Kalender"**  
  
 Verwenden Sie die Schaltfläche Kalender, um das Startdatum, die Startzeit und die Dauer der Daten anzugeben, über die ein Bericht erstellt werden soll.  
  
#### <a name="query-statistics-history-report"></a>Bericht "Abfragestatistik - Verlauf"  
 Im Diagramm Erste Abfragen nach CPU gesamt werden die relativen Aufwendungen für jede Abfrage für den ausgewählten Zeitbereich auf der Basis der CPU-Gesamtnutzung dargestellt. Zum Anzeigen einer anderen Sicht der relativen Aufwendungen für jede Abfrage klicken Sie auf einen der Links unter dem Diagramm: **Dauer**, **E/A gesamt**, **Physische Lesevorgänge**oder **Logische Schreibvorgänge**.  
  
 In der Tabelle unter dem Diagramm werden weitere Abfragedaten bereitgestellt. Sie enthält den Text für jede grafisch dargestellte Abfrage zusammen mit ausführlichen statistischen Informationen. Beachten Sie, dass die Diagrammbalken aktive Links sind, ebenso wie die einzelnen Abfragen in der Tabelle. Durch Klicken auf einen aktiven Link wird der Unterbericht Abfragedetails für die Abfrage geöffnet.  
  
#### <a name="query-details-subreport"></a>Unterbericht "Abfragedetails"  
 Der Unterbericht Abfragedetails enthält den gesamten Abfragetext. Der Link **Abfragetext bearbeiten** wird neben der Abfrage angezeigt. Sie können auf diesen Link klicken, um die Abfrage im Abfrage-Editor zu öffnen. In der Tabelle unter der Abfrage wird die Abfrageausführungsstatistik angezeigt, z. B. die durchschnittliche Dauer pro Abfrageausführung.  
  
 Ein Diagramm von Abfrageplänen und die durchschnittliche Dauer pro Ausführung werden angezeigt. Sie können eine andere Ansicht der relativen Kosten für jeden Abfrageplan abrufen, indem Sie auf einen der folgenden Hyperlinks unterhalb des Diagramms klicken: **Dauer**, **Physische Lesevorgänge**oder **Logische Schreibvorgänge**. Die Diagrammlinie ist aktiv, und Sie können auf jeden Punkt klicken, um den Unterbericht Abfrageplandetails zu öffnen.  
  
 In der Tabelle unter dem Diagramm werden die ersten zehn Abfragepläne auf Grundlage der CPU-Verwendung pro Ausführung angezeigt. Jede Nummer in der Spalte **Plan #** ist ein aktiver Link, auf den Sie klicken können, um den Unterbericht „Abfrageplandetails“ zu öffnen.  
  
#### <a name="query-plan-details-subreport"></a>Unterbericht "Abfrageplandetails"  
 In diesem Bericht werden Informationen für einen Abfrageplan angezeigt. Der Bericht erlaubt Ihnen nicht nur, die Abfrage zu bearbeiten und Ausführungsstatistiken anzuzeigen, sondern er liefert auch ausführliche Informationen über den Abfrageplan. Über den Link **Grafischen Abfrageausführungsplan anzeigen** wird eine grafische Darstellung des Ausführungsplans für die aktuelle Abfrage geöffnet.  
  
## <a name="server-activity-history-report"></a>Bericht "Serveraktivität - Verlauf"  
 Der Bericht Serveraktivität - Verlauf enthält Daten zu Ressourcenverbrauch und Serveraktivität für den Server und für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die Daten in diesem Bericht werden vom Sammlungssatz für die Serveraktivität gesammelt, der den generischen T-SQL-Abfragesammlertyp und den Leistungsindikatoren-Sammlertyp verwendet.  
  
 Sie können auf den Bericht Serveraktivität - Verlauf über den Objekt-Explorer zugreifen. Erweitern Sie den Ordner **Verwaltung** , klicken Sie mit der rechten Maustaste auf **Datensammlung**, zeigen Sie auf **Berichte**und anschließend auf **Verwaltungs-Data Warehouse**, und klicken Sie auf **Serveraktivität – Verlauf**, um den Bericht anzuzeigen. Weitere Informationen finden Sie unter [Anzeigen eines Sammlungssatzberichts &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="selecting-data-to-include-in-the-report"></a>Auswählen von Daten zum Einschließen in den Bericht  
 Der Bericht enthält die Serveraktivität für den gesamten Zeitraum der Datensammlung. Sie können durch die Datensammlungszeitachse auf zwei Arten navigieren, um ein Datensegment zur Ansicht auszuwählen.  
  
 **Zeitachsensteuerelement und Navigationsschaltflächen**  
  
 Verwenden Sie das Zeitachsensteuerelement und die Navigationsschaltflächen, um durch die Zeitachse zu navigieren oder einen Datumsbereich auszuwählen. Über die Pfeilschaltflächen können Sie nach links bzw. nach rechts blättern und sich so rückwärts bzw. vorwärts durch die Zeitachse bewegen. In der Standardeinstellung navigieren Sie mit den Pfeilschaltflächen in 4-Stunden-Schritten durch die Zeitachse. Mit den Lupenschaltflächen können Sie diesen Zeitschritt auf einen der folgenden Werte vergrößern oder verkleinern: 15 Minuten, 1 Stunde, 4 Stunden, 12 Stunden oder 24 Stunden. Der aktuell ausgewählte Zeitbereich wird durch den hervorgehobenen Teil der Zeitachse dargestellt und im Text unter der Zeitachse angezeigt. Diese Werte, sowie die Daten im Bericht, werden immer aktualisiert, wenn Sie auf die Zeitachse klicken oder die Navigationsschaltflächen verwenden.  
  
 **Schaltfläche "Kalender"**  
  
 Verwenden Sie die Schaltfläche Kalender, um das Startdatum, die Startzeit und die Dauer der Daten anzugeben, über die ein Bericht erstellt werden soll.  
  
###  <a name="Server"></a> Bericht "Serveraktivität - Verlauf"  
 Der Bericht Serveraktivität - Verlauf zeigt die anfängliche Ansicht der Serveraktivität für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und das Hostbetriebssystem an.  
  
 In der folgenden Tabelle werden die Diagramme beschrieben, mit denen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Aktivität und Systemaktivität im Bericht und in den ausführlichen Unterberichten, die über die Diagramme aufrufbar sind, grafisch dargestellt werden.  
  
|Diagramm|Berichtsbeschreibung|  
|-----------|------------------------|  
|% CPU|Diese Unterberichte werden aufgerufen, indem Sie auf einen beliebigen Punkt auf den Diagrammlinien für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder das System im Diagramm % CPU klicken.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : Der Bericht „Abfragestatistik – Verlauf“ enthält ein Diagramm der aufwändigsten Abfragen in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In einer Tabelle unter dem Diagramm werden die Abfragen aufgelistet. Sie enthält außerdem statistische Daten für jede Abfrage. Sie können auf eine Abfrage klicken, um weitere Details abzurufen.<br /><br /> **System**: Der Bericht „System-CPU-Verwendung“ enthält ein Diagramm mit dem Prozentsatz der CPU-Zeit pro Prozessor sowie statistische Daten für jeden Prozess im Tabellenformat.|  
|Speicherauslastung|Diese Unterberichte werden aufgerufen, indem Sie auf einen beliebigen Punkt auf den Diagrammlinien für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder das System im Diagramm Speicherauslastung klicken.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : Der Bericht „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Speicherauslastung“ enthält Diagramme für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozessspeichernutzung, für Arbeitsspeicher-Leistungsindikatoren, für die interne Arbeitsspeichernutzung nach Typ und eine Tabelle mit Daten zur durchschnittlichen Arbeitsspeichernutzung nach Komponententyp.<br /><br /> **System**: Der Bericht „Systemspeicherverwendung“ enthält Diagramme für die Speicherauslastung, Zwischenspeicher- und Seiten-Trefferquoten und eine Tabelle mit Informationen über den Arbeitssatz und die privaten Bytes für jeden Prozess.|  
|Datenträger-E/A-Nutzung|Diese Unterberichte werden aufgerufen, indem Sie auf einen beliebigen Punkt auf den Diagrammlinien für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder das System im Diagramm Datenträger-E/A-Verwendung klicken.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : Der Bericht „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenträger-E/A-Verwendung“ enthält Diagramme für die Antwortzeit und die Übertragungsrate des Datenträgers. Eine zusätzliche Tabelle bietet Statistiken virtueller Dateien anhand von Datenträger, Datenbank und Datei.<br /><br /> **System**: Der Bericht „Systemdatenträgerverwendung“ enthält Diagramme für die Antwortzeit des Datenträgers, die durchschnittliche Warteschlangenlänge des Datenträgers, die Übertragungsrate des Datenträgers und eine Tabelle mit Informationen über Schreib- und Lesezugriffe für jeden Prozess.|  
|Netzwerkauslastung|Es sind keine weiteren Berichte verfügbar.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Wartevorgänge|Das Diagramm für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Wartevorgänge zeigt Wartevorgänge in den Threads, die ausgeführt wurden, nach Kategorie an. Sie können auf einen ausführlichen Bericht zugreifen, indem Sie auf ein beliebiges Segment im Diagramm klicken. Neben der grafischen Darstellung von Statistikdaten zu den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Wartevorgängen während eines engeren Zeitrahmens liefert dieser Bericht Informationen über Wartevorgangskategorien im Tabellenformat. Für jede Kategorie, z. B. CPU und deren Unterkategorien, zeigt die Tabelle die Anzahl der Wartevorgänge, die Wartezeit und den Prozentsatz der Gesamtwartezeit an.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Aktivität|Verschiedene Aspekte der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Aktivität sind über das Diagramm zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Aktivität abrufbar. Sie können folgende Berichte durch Klicken auf einen Punkt auf der Diagrammlinie SQL-Kompilierungen/Sekunde abrufen:<br /><br /> <br /><br /> Verbindungen und Sitzungen<br /><br /> Anforderungen<br /><br /> Plancache-Trefferquote<br /><br /> tempdb-Eigenschaften|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Anzeigen eines Sammlungssatzberichts &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  
