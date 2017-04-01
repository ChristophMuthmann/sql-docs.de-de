---
title: "Masseneinf&#252;gungstask | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.bulkinserttask.f1"
helpviewer_keywords: 
  - "Masseneinfügungstask"
  - "Kopieren von Daten [Integration Services]"
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Masseneinf&#252;gungstask
  Der Masseneinfügungstask stellt eine effektive Möglichkeit zum Kopieren großer Datenmengen in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle oder -Sicht bereit. Angenommen, Ihr Unternehmen verwaltet eine Produktliste mit einer Million Zeilen auf einem Großrechner. Das E-Commerce-System des Unternehmens verwendet jedoch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Auffüllen von Webseiten. Sie müssen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Produkttabelle jede Nacht mit der Hauptproduktliste vom Großrechner aktualisieren. Dazu speichern Sie die Produktliste in einem Format mit Tabstopp-Trennzeichen und kopieren mit dem Masseneinfügungstask die Daten direkt in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle.  
  
 Damit die Daten schnell kopiert werden, können für Daten keine Transformationen ausgeführt werden, während sie von der Quelldatei in die Tabelle oder Sicht verschoben werden.  
  
## Überlegungen zur Verwendung  
 Beachten Sie Folgendes, bevor Sie den Masseneinfügungstask verwenden:  
  
-   Der Masseneinfügungstask kann Daten nur von einer Textdatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle oder -Sicht übertragen. Um mit dem Masseneinfügungstask Daten von anderen Datenbank-Managementsystemen (DBMS, Database Management System) zu übertragen, müssen Sie die Daten von der Quelle in eine Textdatei exportieren und anschließend die Daten aus der Textdatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle oder -Sicht importieren.  
  
-   Das Ziel muss eine Tabelle oder Sicht in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank sein. Falls die Zieltabelle oder -sicht bereits Daten enthält, werden die neuen Daten an die vorhandenen Daten angefügt, wenn der Masseneinfügungstask ausgeführt wird. Wenn Sie die Daten ersetzen möchten, führen Sie einen Task SQL ausführen aus, der eine DELETE- oder TRUNCATE-Anweisung ausführt, bevor Sie den Masseneinfügungstask starten. Weitere Informationen finden Sie unter [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md).  
  
-   Sie können eine Formatdatei für das Masseneinfügungstask-Objekt verwenden. Wenn die Formatdatei über das Hilfsprogramm **bcp** erstellt wurde, können Sie deren Pfad für den Masseneinfügungstask angeben. Der Masseneinfügungstask unterstützt XML- und Nicht-XML-Formatdateien. Weitere Informationen zu Formatdateien finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   Nur Mitglieder der festen Serverrolle sysadmin können ein Paket ausführen, das einen Masseneinfügungstask enthält.  
  
## Masseneinfügungstasks für Transaktionen  
 Wenn keine Batchgröße festgelegt ist, wird der gesamte Massenkopiervorgang als eine einzige Transaktion behandelt. Die Batchgröße **0** gibt an, dass die Daten in einem einzigen Batch eingefügt werden. Wenn eine Batchgröße festgelegt ist, stellt jeder Batch eine Transaktion dar, für die nach Beendigung des Batches ein Commit ausgeführt wird.  
  
 Das Verhalten des Masseneinfügungstasks in Verbindung mit Transaktionen hängt davon ab, ob der Task an der Pakettransaktion teilnimmt. Wenn der Masseneinfügungstask nicht an der Pakettransaktion teilnimmt, wird für jeden fehlerfreien Batch als eine Einheit ein Commit ausgeführt, bevor der nächste Batch verarbeitet wird. Wenn der Masseneinfügungstask an der Pakettransaktion teilnimmt, verbleiben fehlerfreie Batches nach Abschluss des Tasks in der Transaktion. Diese Batches unterliegen dem Commit- oder Rollbackvorgang des Pakets.  
  
 Bei einem Fehler beim Masseneinfügungstask wird für erfolgreich geladene Batches nicht automatisch ein Rollback ausgeführt; die erfolgreiche Ausführung eines Tasks bedeutet nicht, dass für die Batches automatisch ein Commit ausgeführt wird. Commit- und Rollbackvorgänge erfolgen nur als Reaktion auf Paket- und Workflow-Eigenschaftseinstellungen.  
  
## Quelle und Ziel  
 Beachten Sie Folgendes, wenn Sie den Speicherort der Quelltextdatei angeben:  
  
-   Der Server muss die Berechtigung für den Zugriff auf die Datei und die Zieldatenbank besitzen.  
  
-   Der Server führt den Masseneinfügungstask aus. Deshalb muss jede Formatdatei, die vom Task verwendet wird, auf dem Server gespeichert sein.  
  
-   Die Quelldatei, die vom Masseneinfügungstask geladen wird, kann auf demselben Server wie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank, in die Daten eingefügt werden, oder auf einem Remoteserver gespeichert sein. Falls sich die Datei auf einem Remoteserver befindet, müssen Sie den Dateinamen mithilfe des UNC-Namens (Universal Naming Convention) im Pfad angeben.  
  
## Leistungsoptimierung  
 Beachten Sie bei der Optimierung der Leistung Folgendes:  
  
-   Wenn sich die Textdatei auf demselben Computer wie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank befindet, in die Daten eingefügt werden, erfolgt der Kopiervorgang sogar noch schneller, weil die Daten nicht im Netzwerk verschoben werden.  
  
-   Der Masseneinfügungstask protokolliert keine Zeilen, die Fehler verursachen. Um diese Informationen aufzuzeichnen, können Sie mit den Fehlerausgaben von Datenflusskomponenten Zeilen, die Fehler verursachen, in einer Ausnahmedatei aufzeichnen.  
  
## Verfügbare benutzerdefinierte Protokolleinträge für den Masseneinfügungstask  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Masseneinfügungstask aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) und [Benutzerdefinierte Meldungen für die Protokollierung](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**BulkInsertTaskBegin**|Zeigt den Beginn der Masseneinfügung an.|  
|**BulkInsertTaskEnd**|Zeigt die Fertigstellung der Masseneinfügung an.|  
|**BulkInsertTaskInfos**|Enthält beschreibende Informationen zum Task.|  
  
## Konfiguration des Masseneinfügungstasks  
 Es gibt folgende Möglichkeiten, um den Masseneinfügungstask zu konfigurieren:  
  
-   Geben Sie den OLE DB-Verbindungs-Manager zum Herstellen der Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zieldatenbank und der Tabelle oder Sicht an, in die Daten eingefügt werden. Der Masseneinfügungstask unterstützt nur OLE DB-Verbindungen mit der Zieldatenbank.  
  
-   Geben Sie den Dateiverbindungs-Manager oder den Verbindungs-Manager für Flatfiles für den Zugriff auf die Quelldatei an. Der Masseneinfügungstask verwendet den Verbindungs-Manager nur für den Speicherort der Quelldatei. Der Task ignoriert andere Optionen, die Sie im Verbindungs-Manager-Editor auswählen.  
  
-   Definieren Sie das vom Masseneinfügungstask verwendete Format, indem Sie eine Formatdatei verwenden oder die Spalten- und Zeilentrennzeichen der Quelldaten definieren. Falls Sie eine Formatdatei verwenden, geben Sie den Dateiverbindungs-Manager für den Zugriff auf die Formatdatei an.  
  
-   Geben Sie Aktionen an, die für die Zieltabelle oder -sicht beim Einfügen der Daten durch den Task ausgeführt werden sollen. Beispielsweise, ob Einschränkungen überprüft, IDENTITY INSERT aktiviert, NULL-Werte beibehalten, Trigger ausgelöst werden sollen oder ob die Tabelle gesperrt werden soll.  
  
-   Stellen Sie Informationen zum einzufügenden Datenbatch bereit, wie z. B. die Batchgröße, die erste und letzte Zeile aus der einzufügenden Datei, die Anzahl von INSERT-Fehlern, nach der der Task das Einfügen von Zeilen beendet, sowie die Namen der zu sortierenden Spalten.  
  
 Wenn der Masseneinfügungstask für den Zugriff auf die Quelldatei einen Verbindungs-Manager für Flatfiles verwendet, verwendet der Task nicht das im Verbindungs-Manager für Flatfiles angegebene Format. Stattdessen verwendet der Masseneinfügungstask entweder das in einer Formatdatei angegebene Format oder die Werte der Eigenschaften RowDelimiter und ColumnDelimiter des Tasks.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Masseneinfügungstask-Editor &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/bulk-insert-task-editor-general-page.md)  
  
-   [Masseneinfügungstask-Editor &#40;Seite „Verbindung“&#41;](../../integration-services/control-flow/bulk-insert-task-editor-connection-page.md)  
  
-   [Masseneinfügungstask-Editor &#40;Seite „Optionen“&#41;](../../integration-services/control-flow/bulk-insert-task-editor-options-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
### Programmgesteuerte Konfiguation des Masseneinfügungstasks  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## Verwandte Aufgaben  
 [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Verwandte Inhalte  
  
-   Technischer Artikel [Möglicherweise wird bei UAC-fähigen Systemen der Fehler "Die SSIS-Masseneinfügung kann zum Einfügen von Daten nicht vorbereitet werden" angezeigt](http://go.microsoft.com/fwlink/?LinkId=233693)auf support.microsoft.com.  
  
-   Technischer Artikel [The Data Loading Performance Guide (Leistungsleitfaden für das Laden von Daten)](http://go.microsoft.com/fwlink/?LinkId=233700)auf msdn.microsoft.com  
  
-   Technischer Artikel [Using SQL Server Integration Services to Bulk Load Data](http://go.microsoft.com/fwlink/?LinkId=233701) (Verwenden von SQL Server Integration Services für das Massenladen von Daten) auf simple-talk.com.  
  
  