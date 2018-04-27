---
title: Masseneinfügungstask | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.bulkinserttask.f1
- sql13.dts.designer.bulkinserttask.connection.f1
- sql13.dts.designer.bulkinserttask.general.f1
- sql13.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3d5d2ac1ee71fa67ee426c6e9beba05d78fd06a1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="bulk-insert-task"></a>Masseneinfügungstask
  Der Masseneinfügungstask stellt eine effektive Möglichkeit zum Kopieren großer Datenmengen in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle oder -Sicht bereit. Angenommen, Ihr Unternehmen verwaltet eine Produktliste mit einer Million Zeilen auf einem Großrechner. Das E-Commerce-System des Unternehmens verwendet jedoch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Auffüllen von Webseiten. Sie müssen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Produkttabelle jede Nacht mit der Hauptproduktliste vom Großrechner aktualisieren. Dazu speichern Sie die Produktliste in einem Format mit Tabstopp-Trennzeichen und kopieren mit dem Masseneinfügungstask die Daten direkt in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle.  
  
 Damit die Daten schnell kopiert werden, können für Daten keine Transformationen ausgeführt werden, während sie von der Quelldatei in die Tabelle oder Sicht verschoben werden.  
  
## <a name="usage-considerations"></a>Überlegungen zur Verwendung  
 Beachten Sie Folgendes, bevor Sie den Masseneinfügungstask verwenden:  
  
-   Der Masseneinfügungstask kann Daten nur von einer Textdatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle oder -Sicht übertragen. Um mit dem Masseneinfügungstask Daten von anderen Datenbank-Managementsystemen (DBMS, Database Management System) zu übertragen, müssen Sie die Daten von der Quelle in eine Textdatei exportieren und anschließend die Daten aus der Textdatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle oder -Sicht importieren.  
  
-   Das Ziel muss eine Tabelle oder Sicht in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank sein. Falls die Zieltabelle oder -sicht bereits Daten enthält, werden die neuen Daten an die vorhandenen Daten angefügt, wenn der Masseneinfügungstask ausgeführt wird. Wenn Sie die Daten ersetzen möchten, führen Sie einen Task SQL ausführen aus, der eine DELETE- oder TRUNCATE-Anweisung ausführt, bevor Sie den Masseneinfügungstask starten. Weitere Informationen finden Sie unter [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md).  
  
-   Sie können eine Formatdatei für das Masseneinfügungstask-Objekt verwenden. Wenn die Formatdatei über das Hilfsprogramm **bcp** erstellt wurde, können Sie deren Pfad für den Masseneinfügungstask angeben. Der Masseneinfügungstask unterstützt XML- und Nicht-XML-Formatdateien. Weitere Informationen zu Formatdateien finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   Nur Mitglieder der festen Serverrolle sysadmin können ein Paket ausführen, das einen Masseneinfügungstask enthält.  
  
## <a name="bulk-insert-task-with-transactions"></a>Masseneinfügungstasks für Transaktionen  
 Wenn keine Batchgröße festgelegt ist, wird der gesamte Massenkopiervorgang als eine einzige Transaktion behandelt. Die Batchgröße **0** gibt an, dass die Daten in einem einzigen Batch eingefügt werden. Wenn eine Batchgröße festgelegt ist, stellt jeder Batch eine Transaktion dar, für die nach Beendigung des Batches ein Commit ausgeführt wird.  
  
 Das Verhalten des Masseneinfügungstasks in Verbindung mit Transaktionen hängt davon ab, ob der Task an der Pakettransaktion teilnimmt. Wenn der Masseneinfügungstask nicht an der Pakettransaktion teilnimmt, wird für jeden fehlerfreien Batch als eine Einheit ein Commit ausgeführt, bevor der nächste Batch verarbeitet wird. Wenn der Masseneinfügungstask an der Pakettransaktion teilnimmt, verbleiben fehlerfreie Batches nach Abschluss des Tasks in der Transaktion. Diese Batches unterliegen dem Commit- oder Rollbackvorgang des Pakets.  
  
 Bei einem Fehler beim Masseneinfügungstask wird für erfolgreich geladene Batches nicht automatisch ein Rollback ausgeführt; die erfolgreiche Ausführung eines Tasks bedeutet nicht, dass für die Batches automatisch ein Commit ausgeführt wird. Commit- und Rollbackvorgänge erfolgen nur als Reaktion auf Paket- und Workflow-Eigenschaftseinstellungen.  
  
## <a name="source-and-destination"></a>Quelle und Ziel  
 Beachten Sie Folgendes, wenn Sie den Speicherort der Quelltextdatei angeben:  
  
-   Der Server muss die Berechtigung für den Zugriff auf die Datei und die Zieldatenbank besitzen.  
  
-   Der Server führt den Masseneinfügungstask aus. Deshalb muss jede Formatdatei, die vom Task verwendet wird, auf dem Server gespeichert sein.  
  
-   Die Quelldatei, die vom Masseneinfügungstask geladen wird, kann auf demselben Server wie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank, in die Daten eingefügt werden, oder auf einem Remoteserver gespeichert sein. Falls sich die Datei auf einem Remoteserver befindet, müssen Sie den Dateinamen mithilfe des UNC-Namens (Universal Naming Convention) im Pfad angeben.  
  
## <a name="performance-optimization"></a>Leistungsoptimierung  
 Beachten Sie bei der Optimierung der Leistung Folgendes:  
  
-   Wenn sich die Textdatei auf demselben Computer wie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank befindet, in die Daten eingefügt werden, erfolgt der Kopiervorgang sogar noch schneller, weil die Daten nicht im Netzwerk verschoben werden.  
  
-   Der Masseneinfügungstask protokolliert keine Zeilen, die Fehler verursachen. Um diese Informationen aufzuzeichnen, können Sie mit den Fehlerausgaben von Datenflusskomponenten Zeilen, die Fehler verursachen, in einer Ausnahmedatei aufzeichnen.  
  
## <a name="custom-log-entries-available-on-the-bulk-insert-task"></a>Verfügbare benutzerdefinierte Protokolleinträge für den Masseneinfügungstask  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Masseneinfügungstask aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**BulkInsertTaskBegin**|Zeigt den Beginn der Masseneinfügung an.|  
|**BulkInsertTaskEnd**|Zeigt die Fertigstellung der Masseneinfügung an.|  
|**BulkInsertTaskInfos**|Enthält beschreibende Informationen zum Task.|  
  
## <a name="bulk-insert-task-configuration"></a>Konfiguration des Masseneinfügungstasks  
 Es gibt folgende Möglichkeiten, um den Masseneinfügungstask zu konfigurieren:  
  
-   Geben Sie den OLE DB-Verbindungs-Manager zum Herstellen der Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zieldatenbank und der Tabelle oder Sicht an, in die Daten eingefügt werden. Der Masseneinfügungstask unterstützt nur OLE DB-Verbindungen mit der Zieldatenbank.  
  
-   Geben Sie den Dateiverbindungs-Manager oder den Verbindungs-Manager für Flatfiles für den Zugriff auf die Quelldatei an. Der Masseneinfügungstask verwendet den Verbindungs-Manager nur für den Speicherort der Quelldatei. Der Task ignoriert andere Optionen, die Sie im Verbindungs-Manager-Editor auswählen.  
  
-   Definieren Sie das vom Masseneinfügungstask verwendete Format, indem Sie eine Formatdatei verwenden oder die Spalten- und Zeilentrennzeichen der Quelldaten definieren. Falls Sie eine Formatdatei verwenden, geben Sie den Dateiverbindungs-Manager für den Zugriff auf die Formatdatei an.  
  
-   Geben Sie Aktionen an, die für die Zieltabelle oder -sicht beim Einfügen der Daten durch den Task ausgeführt werden sollen. Beispielsweise, ob Einschränkungen überprüft, IDENTITY INSERT aktiviert, NULL-Werte beibehalten, Trigger ausgelöst werden sollen oder ob die Tabelle gesperrt werden soll.  
  
-   Stellen Sie Informationen zum einzufügenden Datenbatch bereit, wie z. B. die Batchgröße, die erste und letzte Zeile aus der einzufügenden Datei, die Anzahl von INSERT-Fehlern, nach der der Task das Einfügen von Zeilen beendet, sowie die Namen der zu sortierenden Spalten.  
  
 Wenn der Masseneinfügungstask für den Zugriff auf die Quelldatei einen Verbindungs-Manager für Flatfiles verwendet, verwendet der Task nicht das im Verbindungs-Manager für Flatfiles angegebene Format. Stattdessen verwendet der Masseneinfügungstask entweder das in einer Formatdatei angegebene Format oder die Werte der Eigenschaften RowDelimiter und ColumnDelimiter des Tasks.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>Programmgesteuerte Konfiguation des Masseneinfügungstasks  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Technischer Artikel [Möglicherweise wird bei UAC-fähigen Systemen der Fehler "Die SSIS-Masseneinfügung kann zum Einfügen von Daten nicht vorbereitet werden" angezeigt](http://go.microsoft.com/fwlink/?LinkId=233693)auf support.microsoft.com.  
  
-   Technischer Artikel [The Data Loading Performance Guide (Leistungsleitfaden für das Laden von Daten)](http://go.microsoft.com/fwlink/?LinkId=233700)auf msdn.microsoft.com  
  
-   Technischer Artikel [Using SQL Server Integration Services to Bulk Load Data](http://go.microsoft.com/fwlink/?LinkId=233701)(Verwenden von SQL Server Integration Services für das Massenladen von Daten) auf simple-talk.com.  
  
## <a name="bulk-insert-task-editor-connection-page"></a>Masseneinfügungstask-Editor (Seite Verbindung)
  Mithilfe der Seite **Verbindung** im Dialogfeld **Masseneinfügungstask-Editor** können Sie die Quelle und das Ziel des Masseneinfügevorgangs und das zu verwendende Format angeben.  
  
 Informationen zum Arbeiten mit Masseneinfügungen finden Sie unter [Masseneinfügungstask](../../integration-services/control-flow/bulk-insert-task.md) und [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
### <a name="options"></a>Tastatur  
 **Verbindung**  
 Wählen Sie einen OLE DB-Verbindungs-Manager in der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um eine neue Verbindung zu erstellen.  
  
 **Verwandte Themen:** [OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
 **DestinationTable**  
 Geben Sie den Namen der Zieltabelle oder Zielsicht ein, oder wählen Sie aus der Liste eine Tabelle oder Sicht aus.  
  
 **Format**  
 Wählen Sie die Quelle des Formats für die Masseneinfügung aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|value|Description|  
|-----------|-----------------|  
|**Use File**|Wählen Sie eine Datei mit Formatspezifikationen aus. Nach Auswahl dieser Option wird die dynamische Option **FormatFile**angezeigt.|  
|**Specify**|Geben Sie das Format an. Nach Auswahl dieser Option werden die dynamischen Optionen **RowDelimiter** und **ColumnDelimiter**angezeigt.|  
  
 **Zuletzt geöffnete Dateien**  
 Wählen Sie einen Datei- oder Flatfileverbindungs-Manager in der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um eine neue Verbindung zu erstellen.  
  
 Der Speicherort ist relativ zum SQL Server-Datenbankmodul, das im Verbindungs-Manager für diesen Task angegeben wurde. Das SQL Server-Datenbankmodul muss auf die Textdatei zugreifen können, und zwar entweder auf einer lokalen Festplatte des Servers oder über eine Freigabe oder einem SQL Server zugeordneten Laufwerk. Auf die Datei wird nicht von der SSIS-Laufzeit zugegriffen.  
  
 Wenn Sie auf die Quelldatei mithilfe eines Flatfileverbindungs-Managers zugreifen, verwendet der Masseneinfügungstask nicht das im Flatfileverbindungs-Manager angegebene Format. Stattdessen verwendet der Masseneinfügungstask entweder das in einer Formatdatei angegebene Format oder die Werte der Eigenschaften RowDelimiter und ColumnDelimiter des Tasks.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md) (Dateiverbindungs-Manager), [File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md) (Verbindungs-Manager für Flatfiles) 
  
 **Tabellen aktualisieren**  
 Aktualisieren Sie die Liste der Tabellen und Sichten.  
  
### <a name="format-dynamic-options"></a>Format (dynamische Optionen)  
  
#### <a name="format--use-file"></a>Format = Use File  
 **FormatFile**  
 Geben Sie den Pfad der Formatdatei ein, oder klicken Sie auf die Schaltfläche mit den drei Punkten ( **…** ), um nach der Formatdatei zu suchen.  
  
#### <a name="format--specify"></a>Format = Specify  
 **RowDelimiter**  
 Geben Sie das Zeilentrennzeichen in der Quelldatei an. Der Standardwert ist **{CR}{LF}**.  
  
 **ColumnDelimiter**  
 Geben Sie das Spaltentrennzeichen in der Quelldatei an. Der Standardwert ist **Tabstopp**.  
  
## <a name="bulk-insert-task-editor-general-page"></a>Masseneinfügungstask-Editor (Seite Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Masseneinfügungstask-Editor** können Sie einen Namen und eine Beschreibung für den Masseneinfügungstask angeben.  
  
### <a name="options"></a>Tastatur  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Masseneinfügungstask an. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung des Masseneinfügungstasks ein.  
 
## <a name="bulk-insert-task-editor-options-page"></a>Masseneinfügungstask-Editor (Seite Optionen)
  Auf der Seite **Optionen** des Dialogfelds **Masseneinfügungstask-Editor** können Sie Eigenschaften für den Masseneinfügungsvorgang festlegen. Durch den Masseneinfügungstask werden große Datenmengen in eine Tabelle oder Sicht von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kopiert.  
  
 Weitere Informationen zum Arbeiten mit Masseneinfügungen finden Sie unter [Masseneinfügungstask](../../integration-services/control-flow/bulk-insert-task.md) und [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
### <a name="options"></a>Tastatur  
 **CodePage**  
 Geben Sie die Codepage für die in der Datendatei enthaltenen Daten an.  
  
 **DataFileType**  
 Geben Sie den Wert für den Datentyp an, der beim Ladevorgang verwendet werden soll.  
  
 **BatchSize**  
 Geben Sie die Anzahl der Zeilen in einem Batch an. Der Standardwert ist die gesamte Datendatei. Wenn Sie **BatchSize** auf null festlegen, werden die Daten in einem Batch geladen.  
  
 **LastRow**  
 Geben Sie die letzte zu kopierende Zeile an.  
  
 **FirstRow**  
 Geben Sie die erste zu kopierende Zeile an.  
  
 **Optionen**  
 |Begriff|Definition|  
|----------|----------------|  
|**Check-Einschränkungen**|Wählen Sie diese Option aus, um die Einschränkungen für Tabelle und Spalte zu überprüfen.|  
|**NULL-Werte beibehalten**|Wählen Sie diese Option aus, um NULL-Werte während des Masseneinfügungsvorgangs beizubehalten, statt für leere Spalten Standardwerte einzufügen.|  
|**IDENTITY_INSERT aktivieren**|Wählen Sie diese Option aus, um vorhandene Werte in eine Identitätsspalte einzufügen.|  
|**Tabellensperre**|Wählen Sie diese Option aus, um die Tabelle während des Masseneinfügungsvorgangs zu sperren.|  
|**Trigger auslösen**|Wählen Sie diese Option aus, um das Einfügen, Aktualisieren oder Löschen von Triggern für die Tabelle auszulösen.|  
  
 **SortedData**  
 Geben Sie die ORDER BY-Klausel in der BULK INSERT-Anweisung an. Der Name der angegebenen Spalte muss eine gültige Spalte in der Zieltabelle sein. Der Standardwert ist **false**. Das bedeutet, dass die Daten nicht durch eine ORDER BY-Klausel sortiert werden.  
  
 **MaxErrors**  
 Geben Sie an, wie viele Fehler maximal auftreten müssen, bevor der Masseneinfügungsvorgang abgebrochen wird. Durch den Wert 0 wird gekennzeichnet, dass eine unendliche Anzahl von Fehlern zulässig ist.  
  
> [!NOTE]  
>  Jede Zeile, die beim Massenladevorgang nicht importiert werden kann, zählt als ein Fehler.  
  
