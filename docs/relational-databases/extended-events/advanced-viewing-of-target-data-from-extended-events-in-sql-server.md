---
title: Erweiterte Ansicht von Zieldaten aus erweiterten Ereignissen in SQL Server | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/04/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b2e839d7-1872-46d9-b7b7-6dcb3984829f
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b92d37d2ae439f9d1ce10da56dff0582e5e32f77
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="advanced-viewing-of-target-data-from-extended-events-in-sql-server"></a>Erweiterte Ansicht von Zieldaten aus erweiterten Ereignissen in SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Dieser Artikel veranschaulicht, wie Sie die erweiterten Funktionen von SQL Server Management Studio (SSMS.exe) verwenden können, um die Zieldaten aus erweiterten Ereignissen sehr detailliert anzuzeigen. Der Artikel erläutert Folgendes:


- Öffnen und Anzeigen der Zieldaten auf verschiedene Weise.
- Exportieren der Zieldaten in verschiedene Formate mithilfe des speziellen Menüs bzw. der Symbolleiste für erweiterte Ereignisse.
- Bearbeiten der Daten in der Anzeige oder vor dem Export.



### <a name="prerequisites"></a>Voraussetzungen

In diesem Artikel wird davon ausgegangen, dass Sie wissen, wie Sie eine Ereignissitzung erstellen und starten. Die Erstellung einer Ereignissitzung wird in folgendem Artikel demonstriert:

[Schnellstart: Erweiterte Ereignisse in SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)


In diesem Artikel wird ebenfalls davon ausgegangen, dass Sie eine möglichst aktuelle monatliche Version von SSMS installiert haben. Hier finden Sie Hilfe zur Installation:

- [SQL Server Management Studio (SSMS) herunterladen](http://msdn.microsoft.com/library/mt238290.aspx)



### <a name="differences-with-azure-sql-database"></a>Unterschiede zu Azure SQL-Datenbank


Die Implementierung und die Funktionen der erweiterten Ereignisse in den beiden Produkten Microsoft SQL Server und Azure SQL-Datenbank sind sich in vielerlei Hinsicht sehr ähnlich. Es gibt jedoch einige Unterschiede, die die SSMS-Benutzeroberfläche betreffen.


- In SQL-Datenbank darf das Ziel package0.event_file keine Datei auf dem lokalen Laufwerk sein. Stattdessen muss ein Azure Storage-Container verwendet werden. Wenn Sie also eine Verbindung mit SQL-Datenbank hergestellt haben, fragt die SSMS-Benutzeroberfläche nach einem Speichercontainer, nicht nach einem lokalen Pfad und Dateinamen.


- Wenn das Kontrollkästchen **Livedaten anzeigen** in der SSMS-Benutzeroberfläche deaktiviert ist, liegt dies daran, dass diese Funktion für SQL-Datenbank nicht verfügbar ist.


- Einige Ereignisse werden mit SQL Server installiert. Im Knoten **Sitzungen** sehen Sie **AlwaysOn_health** sowie einige weitere. Diese Ereignisse werden bei einer Verbindung mit SQL-Datenbank nicht angezeigt, weil sie für SQL-Datenbank nicht existieren.


Der vorliegende Artikel behandelt die Perspektive von SQL Server. In diesem Artikel wird das Ziel event_target verwendet – einer der Bereiche, in dem Unterschiede bestehen. In diesem Artikel werden ansonsten nur wichtige oder nicht offensichtliche Unterschiede erläutert.


Eine Dokumentation der erweiterten Ereignissen, die nur für Azure SQL-Datenbank gelten, finden Sie hier:

- [Erweiterte Ereignisse in Azure SQL-Datenbank](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)



## <a name="a-general-options"></a>A. Allgemeine Optionen


Im Allgemeinen erfolgt der Zugriff auf die erweiterten Optionen mit einer der folgenden Methoden:


- Das reguläre Menü **Datei** > **Öffnen** > **Datei**.
- Rechtsklick im **Objekt-Explorer** unter **Verwaltung** > **Erweiterte Ereignisse**.
- Das spezielle Menü **Erweiterte Ereignisse**und die spezielle Symbolleiste für erweiterte Ereignisse.
- Rechtsklick in den Bereich im Registerkartenformat, in dem die Zieldaten angezeigt werden.



## <a name="b-bring-target-data-into-ssms-for-display"></a>B. Einfügen von Zieldaten zur Anzeige in SSMS


Es gibt verschiedene Möglichkeiten event_file-Zieldaten in die SSMS-Benutzeroberfläche einzufügen. Wenn Sie ein event_file-Ziel angeben, legen Sie den Dateipfad und den Namen für das Ziel fest:

- Die Dateinamenerweiterung lautet .XEL.


- Jedes Mal, wenn die Ereignissitzung gestartet wird, bettet das System eine große Ganzzahl in einen neuen Dateinamen ein, sodass der Dateiname eindeutig ist und sich von dem Dateinamen einer zuvor ausgeführten Ereignissitzung unterscheidet.
  - *Beispiel:* Checkpoint_Begins_ES_0_131103935140400000.xel


- Die Inhalte einer XEL-Datei liegen nicht im Nur-Text-Format vor, das mit dem Text-Editor angezeigt werden kann.
  - Wenn Sie möchten, können Sie über das Menü **Datei** > **Öffnen** > **Dateien für erweiterte Ereignisse zusammenführen**mehrere XEL-Dateien aneinanderfügen.



SSMS kann Daten aus jedem Ziel anzeigen. Die Ansichten unterscheiden sich jedoch für die verschiedenen Ziele:

- *event_file:* Daten aus einem event_file-Ziel werden gut lesbar angezeigt und bieten viele Funktionen.


- *ring_buffer:* Daten aus einem Ringpufferziel werden als unformatiertes XML angezeigt.


- Bei anderen Zielen liegt die Lesbarkeit der Anzeige zwischen event_file und ring_buffer.
  - Beispiele für andere Ziele: event_counter, histogram und pair_matching.


- *etw_classic_sync_target:* SSMS kann Daten für den Zieltyp etw_classic_sync_target nicht anzeigen.



### <a name="b1-open-xel-with-menu-file--open--file"></a>B.1 Öffnen einer .XEL-Datei über das Menü „Datei“ > „Öffnen“ > „Datei“


Sie können eine einzelne .XEL-Datei über das Standardmenü **Datei** > **Öffnen** > **Datei**öffnen.

Sie können auch eine .XEL-Datei per Drag & Drop auf die Registerkartenleiste in der SSMS-Benutzeroberfläche ziehen.



### <a name="b2-view-target-data"></a>B.2 Anzeigen von Zieldaten


Die Option **Zieldaten anzeigen** zeigt die Daten an, die bisher erfasst wurden.


Im Bereich **Objekt-Explorer** können Sie die Knoten erweitern und dann mit der rechten Maustaste auf folgende Optionen klicken:

- **Verwaltung** > **Erweiterte Ereignisse** > **Sitzungen** > *[Ihre_Sitzung]* > *[Ihr_Zielknoten]* > **Zieldaten anzeigen**.


Die Zieldaten werden in SSMS in einem Bereich im Registerkartenformat angezeigt. Dies wird im folgenden Screenshot gezeigt.


![Ihr Ziel > Zieldaten anzeigen](../../relational-databases/extended-events/media/xevents-ssms-ui20-viewtargetdata.png)


> [!NOTE] 
> **Zieldaten anzeigen** zeigt die *kumulierten Daten aus mehreren .XEL-Dateien* der angegebenen Ereignissitzung an. Jeder **Start**-**Stopp** -Zyklus erstellt eine Datei mit einer von einem späteren Zeitpunkt abgeleiteten Ganzzahl im Namen. Der Stammname ist jedoch für alle Dateien gleich.



#### <a name="b3-watch-live-data"></a>B.3 Anzeigen von Livedaten


Wenn Ihre Ereignissitzung aktiv ist, können Sie die Ereignisdaten in Echtzeit anzeigen, so wie sie vom Ziel empfangen werden.


- **Verwaltung** > **Erweiterte Ereignisse** > **Sitzungen** > *[Ihre_Sitzung]* > **Livedaten anzeigen**.


![Ihre Sitzung > Livedaten anzeigen](../../relational-databases/extended-events/media/xevents-ssms-ui55-watchlivedata.png)


Die Datenanzeige wird in einem von Ihnen angegebenen Intervall aktualisiert. Siehe **Maximale Verteilungslatenzzeit** unter:

- **Erweiterte Ereignisse** > **Sitzungen** > *[Ihre_Sitzung]* > **Eigenschaften** > **Erweitert** > **Maximale Verteilungslatenzzeit**



### <a name="b4-view-xel-with-sysfnxefiletargetreadfile-function"></a>B.4 Anzeigen von .XEL mit der sys.fn_xe_file_target_read_file-Funktion


Für die Batchverarbeitung kann die folgende Systemfunktion die Datensätze in einer .XEL-Datei im XML-Format generieren:

- [sys.fn\_xe\_file\_target\_read\_file](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)



## <a name="c-export-the-target-data"></a>C. Exportieren der Zieldaten


Wenn die Zieldaten in SSMS vorhanden sind, können Sie die Daten mit folgenden Schritten in verschiedene Formate exportieren:


1. Setzen Sie den Fokus auf die Datenanzeige.
    - Es werden eine neue Symbolleiste und ein neues Menüelement für erweiterte Ereignisse angezeigt.

    ![Exportieren der angezeigten Daten: Erweiterte Ereignisse > Exportieren nach > (CSV- oder XEL-Datei oder eine Tabelle)](../../relational-databases/extended-events/media/xevents-ssms-ui75-menuextevent-exportto-xel.png)

2. Klicken Sie auf das neue Menüelement **Erweiterte Ereignisse**.
3. Klicken Sie auf **Exportieren nach**, und wählen Sie ein Format aus.



## <a name="d-manipulate-data-in-the-display"></a>D. Bearbeiten von Daten in der Anzeige


Die SSMS-Benutzeroberfläche bietet verschiedene Möglichkeiten zum Bearbeiten der Daten – weit mehr als nur die reine Anzeige der Daten.



### <a name="d1-context-menus-in-the-data-display"></a>D.1 Kontextmenüs in der Datenanzeige


Verschiedene Stellen in der Datenanzeige bieten verschiedene Kontextmenüs, wenn Sie mit der rechten Maustaste klicken.



#### <a name="d11-right-click-a-data-cell"></a>D.1.1 Rechtsklick auf eine Datenzelle


Der folgende Screenshot zeigt das Kontextmenü, das geöffnet wird, wenn Sie mit der rechten Maustaste auf eine Zelle in der Datenanzeige klicken. Der Screenshot zeigt auch die Erweiterung des Menüelements **Kopieren** .


![Rechtsklick auf eine Zelle in der Datenanzeige](../../relational-databases/extended-events/media/xevents-ssms-ui25-rightclickcell.png)



#### <a name="d12-right-click-a-column-header"></a>D.1.2 Rechtsklick auf eine Spaltenüberschrift


Der folgende Screenshot zeigt das Kontextmenü nach einem Rechtsklick auf die Spaltenüberschrift **Zeitstempel** .


![Rechtsklick auf eine Spaltenüberschrift in der Datenanzeige plus Detailanzeige](../../relational-databases/extended-events/media/xevents-ssms-ui40-toolbar.png)


Der obige Screenshot zeigt auch die spezielle Symbolleiste für erweiterte Ereignisse. Da die Schaltfläche „Details“ nicht abgeblendet dargestellt wird, ist die Schaltfläche aktiv. Aus diesem Grund zeigt die Abbildung auch die Registerkarte **Details** , und die Detailanzeige ist als zweiter Bereich der Datenanzeige vorhanden.



### <a name="d2-choose-columns-merge-columns"></a>D.2 Auswählen und Zusammenführen von Spalten


Mit der Option **Spalten auswählen** können Sie steuern, welche Datenspalten angezeigt werden und welche nicht. Sie finden das Menüelement **Spalten auswählen** an verschiedenen Stellen:

- Im Menü **Erweiterte Ereignisse** .
- Auf der Symbolleiste für erweiterte Ereignisse.
- Im Kontextmenü einer Überschrift in der Datenanzeige.


Wenn Sie auf **Spalten auswählen**klicken, wird das gleichnamige Dialogfeld angezeigt.


![Dialogfeld „Spalten auswählen“ mit Optionen „Spalten zusammenführen“](../../relational-databases/extended-events/media/xevents-ssms-ui35-choosecolumns.png)



#### <a name="d21-merge-columns"></a>D.2.1 Zusammenführen von Spalten


Das Dialogfeld **Spalten auswählen** bietet einen Bereich, in dem Sie zu folgenden Zwecken mehrere Spalten zu einer zusammenführen können:

- Anzeige
- Exportieren



### <a name="d3-filters"></a>D.3 Filter


Im Bereich der erweiterten Ereignisse gibt es zwei Hauptarten von Filtern, die Sie angeben können:

- *Filter vor Erfassen der Zieldaten:* Diese Filter reduzieren die Datenmenge, die vom Ereignismodul an Ihr Ziel gesendet werden.

- *Filter nach Erfassen der Zieldaten* : Diese Filter können Sie in der SSMS-Benutzeroberfläche auswählen, um einige Zieldatensätze von der Anzeige auszuschließen.


Folgende SSMS-Anzeigefilter stehen zur Verfügung:

- Ein Filter für den *Zeitraum* , der die Spalte **Zeitstempel** untersucht.
- Ein Filter für *Spaltenwerte* .


Die Beziehung zwischen dem Zeitfilter und dem Spaltenfilter ist ein boolesches*AND*.


![Filter für Zeitraum und Spalten im Dialogfeld „Filter“](../../relational-databases/extended-events/media/xevents-ssms-ui45-filters.png)



### <a name="d4-grouping-and-aggregation"></a>D.4 Gruppierung und Aggregation


Die Gruppierung von Zeilen durch Abgleichen von Werten in einer bestimmten Spalte ist der erste Schritt für eine zusammenfassende Aggregation von Daten.



#### <a name="d41-grouping"></a>D.4.1 Gruppierung


Mit der Schaltfläche **Gruppierung** auf der Symbolleiste der erweiterten Ereignisse starten Sie ein Dialogfeld, in dem Sie die angezeigten Daten nach einer bestimmten Spalte gruppieren können. Der nächste Screenshot zeigt ein Dialogfeld, das zum Gruppieren nach der Spalte *Name* verwendet wird.

![Symbolleiste > Schaltfläche „Gruppierung“, dann Dialogfeld „Gruppierung“](../../relational-databases/extended-events/media/xevents-ssms-ui53-grouping.png)

Nachdem die Gruppierung durchgeführt wurde, ändert sich die Anzeige, wie in der nächsten Abbildung veranschaulicht.

![Neue Anzeige nach Gruppierung](../../relational-databases/extended-events/media/xevents-ssms-ui54-grouped.png)



#### <a name="d42-aggregation"></a>D.4.2 Aggregation


Nachdem die angezeigten Daten gruppiert wurden, können Sie damit fortfahren, Daten in anderen Spalten zu aggregieren.  Der nächste Screenshot zeigt die gruppierten Daten, die nach *Anzahl*aggregiert werden.

![Symbolleiste > Schaltfläche „Aggregation“, dann Dialogfeld „Aggregation“](../../relational-databases/extended-events/media/xevents-ssms-ui51-aggregdialogcount.png)

Nachdem die Aggregation durchgeführt wurde, ändert sich die Anzeige, wie in der nächsten Abbildung veranschaulicht.

![Symbolleiste > Schaltfläche „Aggregation“, dann Dialogfeld „Aggregation“](../../relational-databases/extended-events/media/xevents-ssms-ui52-aggregnewdisplay.png)



### <a name="d5-view-run-time-query-plan"></a>D.5 Anzeigen des Runtimeabfrageplans


Das Ereignis **query_post_execution_showplan** ermöglicht Ihnen die Anzeige des tatsächlichen Abfrageplans in der SSMS-Benutzeroberfläche. Wenn der Bereich **Details** angezeigt wird, können Sie auf der Registerkarte **Abfrageplan** ein Diagramm des Abfrageplans sehen. Indem Sie die Maus über einen Knoten im Abfrageplan bewegen, können Sie eine Liste der Eigenschaftennamen und der zugehörigen Werte für den Knoten anzeigen.


![Abfrageplan mit Eigenschaftenliste für einen Knoten](../../relational-databases/extended-events/media/xevents-ssms-ui60-showplangraph.png)


