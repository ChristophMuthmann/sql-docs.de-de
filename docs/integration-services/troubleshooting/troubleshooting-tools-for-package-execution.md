---
title: "Behandlung von Problemen mit Paketausf&#252;hrungstools | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server Integration Services-Pakete, Problembehandlung"
  - "SSIS-Pakete, Problembehandlung"
  - "Integration Services, Problembehandlung"
  - "Fehler [Integration Services], Problembehandlung"
  - "Pakete [Integration Services], Problembehandlung"
ms.assetid: f18d6ff6-e881-444c-a399-730b52130e7c
caps.latest.revision: 59
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 59
---
# Behandlung von Problemen mit Paketausf&#252;hrungstools
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält Funktionen und Tools, die Sie zur Behandlung von Problemen beim Ausführen von Paketen nach deren Fertigstellung und Bereitstellung verwenden können.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] stellt zur Entwurfszeit Breakpoints zum Unterbrechen der Paketausführung, das Statusfenster sowie Daten-Viewer zum Überwachen der Daten beim Durchlaufen des Datenflusses zur Verfügung. Bei der Ausführung von bereitgestellten Paketen sind diese Funktionen jedoch nicht verfügbar. Folgende Haupttechniken zum Behandeln von Problemen mit bereitgestellten Paketen sind verfügbar:  
  
-   Abfangen und Behandeln von Paketfehlern mithilfe von Ereignishandlern  
  
-   Aufzeichnen von fehlerhaften Daten mithilfe von Fehlerausgaben  
  
-   Nachverfolgen der Paketausführungsschritte mithilfe der Protokollierung  
  
 Sie können außerdem die folgenden Tipps und Techniken verwenden, um Probleme mit ausgeführten Paketen zu vermeiden:  
  
-   **Sicherstellen der Datenintegrität mithilfe von Transaktionen**. Weitere Informationen finden Sie unter [Integration Services-Transaktionen](../../integration-services/integration-services-transactions.md).  
  
-   **Erneutes Ausführen von Paketen ab dem Punkt, an dem der Fehler aufgetreten ist, mithilfe von Prüfpunkten**. Weitere Informationen finden Sie unter [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
## Abfangen und Behandeln von Paketfehlern mithilfe von Ereignishandlern  
 Sie können auf viele Ereignisse, die vom Paket und den Objekten im Paket ausgelöst wurden, mit Ereignishandlern reagieren.  
  
-   **Erstellen eines Ereignishandlers für das OnError-Ereignis**. Sie können im Ereignishandler den Task <ui>Mail senden</ui> verwenden, um einen Administrator über den Fehler zu benachrichtigen. Mit einem Skripttask und benutzerdefinierter Logik können Sie Systeminformationen zur Problembehandlung abrufen, oder Sie können einen Cleanup der temporären Ressourcen und unvollständigen Ausgaben durchführen. Weitere Informationen finden Sie unter [Integration Services-Ereignishandler &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
## Behebung von Problemen mit fehlerhaften Daten mithilfe von Fehlerausgaben  
 Sie können die bei vielen Datenflusskomponenten verfügbare Fehlerausgabe verwenden, um Zeilen mit Fehlern an ein anderes Ziel zur späteren Analyse weiterzuleiten. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).  
  
-   **Aufzeichnen von fehlerhaften Daten mithilfe von Fehlerausgaben**. Senden Sie Zeilen, die Fehler enthalten, an eine anderes Ziel, z.B. an eine Fehlertabelle oder eine Textdatei. Die Fehlerausgabe fügt automatisch zwei numerische Spalten mit der Nummer des Fehlers, der zum Abweisen der Zeile führte, und der ID der Spalte, in welcher der Fehler auftrat, hinzu.  
  
-   **Hinzufügen von beschreibenden Informationen zu den Fehlerausgaben**. Fügen Sie zusätzlich zu den beiden von der Fehlerausgabe bereitgestellten numerischen Bezeichnern die Fehlermeldung und den Spaltennamen hinzu, um die Analyse der Fehlerausgabe zu vereinfachen. Ein Beispiel, wie diese beiden zusätzlichen Spalten mithilfe von Skripts hinzugefügt werden, finden Sie unter [Erweitern einer Fehlerausgabe mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
-   **Sie können die Spaltennamen auch abrufen, indem Sie das DiagnosticEx-Ereignis protokollieren**. Dieses Ereignis schreibt eine Herkunftszuordnung für den Datenfluss in das Protokoll. Sie können den Spaltennamen dann in dieser Herkunftszuordnung nachschlagen, und zwar anhand des von einer Fehlerausgabe erfassten Spaltenbezeichners.  Weitere Informationen finden Sie unter [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md).  
  
     Der Wert der Meldungsspalte für **DiagnosticEx** ist XML-Text. Fragen Sie zum Anzeigen des Meldungstexts für eine Paketausführung die Sicht [catalog.operation_messages &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) ab. Beachten Sie, dass Leerraum in der XML-Ausgabe beim **DiagnosticEx** -Ereignis nicht beibehalten wird, um die Größe des Protokolls zu verringern. Kopieren Sie das Protokoll in einen XML-Editor wie z.B. Visual Studio, der XML-Formatierung und Syntaxhervorhebung unterstützt, um die Lesbarkeit zu verbessern.  
  
## Behandlung von Problemen bei der Paketausführung mithilfe von Vorgangsberichten  
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sind Standardvorgangsberichte verfügbar, um Sie zu unterstützen, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete, die im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog bereitgestellt werden, zu überwachen. Sie können die Berichte zu Paketen verwenden, um den Status und Verlauf von Paketen anzuzeigen und ggf. die Ursache von Fehlern zu identifizieren.  
  
 Weitere Informationen finden Sie unter [Behandlung von Problemen in Berichten für die Paketausführung](../../integration-services/troubleshooting/troubleshooting-reports-for-package-execution.md).  
  
## Behebung von Problemen bei der Paketausführung mithilfe von SSISDB-Sichten  
 Sie können eine Reihe von SSISDB-Datenbanksichten abfragen, um die Paketausführung und andere Informationen zu Vorgängen zu überwachen. Weitere Informationen finden Sie unter [Überwachen der Ausführung von Paketen und anderen Vorgängen](../../integration-services/performance/monitor-running-packages-and-other-operations.md).  
  
## Behebung von Problemen bei der Paketausführung mithilfe der Protokollierung  
 Sie können die meisten Vorgänge beim Ausführen von Paketen durch Aktivieren der Protokollierung nachverfolgen. Bei der Protokollierung werden Informationen zu angegebenen Ereignissen zur späteren Analyse aufgezeichnet und in einer Datenbanktabelle, einer Flatfile, einer XML-Datei oder einem anderen unterstützten Ausgabeformat gespeichert.  
  
-   **Aktivieren der Protokollierung**. Sie können die Protokollierungsausgabe optimieren, indem Sie nur die Ereignisse und Informationen auswählen, die Sie aufzeichnen möchten. Weitere Informationen finden Sie unter [Integration Services-Protokollierung (SSIS)](https://msdn.microsoft.com/library/ms140246.aspx).  
  
-   **Wählen Sie das Diagnostic-Ereignis des Pakets aus, um Probleme mit dem Anbieter zu behandeln.** Es sind Meldungen für die Protokollierung enthalten, mit denen Sie Probleme bei der Interaktion eines Pakets mit externen Datenquellen behandeln können. Weitere Informationen finden Sie unter [Troubleshooting Tools Package Connectivity](https://msdn.microsoft.com/library/cc879309.aspx).  
  
-   **Verbessern der Standardprotokollierungsausgabe**. Bei der Protokollierung werden normalerweise bei jeder Paketausführung Zeilen an ein Protokollierungsziel angefügt. Zwar enthält jede Zeile der Protokollierungsausgabe den Namen und eindeutigen Bezeichner des Pakets sowie die eindeutige ExecutionID der Paketausführung, die umfangreiche Protokollierungsausgabe in einer einzigen Liste kann jedoch die Analyse erschweren.  
  
     Die folgende Vorgehensweise stellt eine Möglichkeit zum Verbessern der Standardprotokollierungsausgabe und Vereinfachen der Berichtgenerierung dar.  
  
    1.  **Erstellen einer übergeordneten Tabelle zum Protokollieren aller Paketausführungen**. Diese übergeordnete Tabelle enthält nur eine einzige Zeile pro Paketausführung und verwendet die ExecutionID zur Verlinkung mit den untergeordneten Datensätzen in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Protokollierungstabelle. Zum Erstellen dieser neuen Zeile und Aufzeichnen der Startzeit können Sie am Anfang eines jeden Pakets den Task 'SQL ausführen' verwenden. Anschließend können Sie am Ende des Pakets den Task 'SQL ausführen' erneut verwenden, um die Beendigungszeit, Dauer und den Status in der Zeile zu aktualisieren.  
  
    2.  **Hinzufügen von Überwachungsinformationen zum Datenfluss**. Sie können mit der Überwachungstransformation Informationen zu Zeilen im Datenfluss hinzufügen, die Daten zur Paketausführung enthalten, durch die die betreffende Zeile erstellt oder geändert wurde. Die Überwachungstransformation stellt neun Arten von Informationen bereit, wie z.B. PackageName und ExecutionInstanceGUID. Weitere Informationen finden Sie unter [Audit Transformation](../../integration-services/data-flow/transformations/audit-transformation.md). Wenn Sie zu Überwachungszwecken jede Zeile mit benutzerdefinierten Informationen versehen möchten, können Sie diese Informationen mithilfe einer Transformation für abgeleitete Spalten den Zeilen im Datenfluss hinzufügen. Weitere Informationen finden Sie unter [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
    3.  **Erwägen der Aufzeichnung von Zeilenanzahldaten**. Erwägen Sie, eine separate Tabelle mit Informationen zur Zeilenanzahl zu erstellen, in der jede Paketausführungsinstanz über ihre ExecutionID identifiziert wird. Verwenden Sie die Transformation für Zeilenanzahl, um an wichtigen Stellen im Datenfluss die Zeilenanzahl in einer Reihe von Variablen zu speichern. Verwenden Sie den Task 'SQL ausführen', um nach Beendigung des Datenflusses die Variablenreihe zur späteren Analyse und Berichterstattung in eine Zeile der Tabelle einzufügen.  
  
     Weitere Informationen zu dieser Methode finden Sie im Abschnitt „ETL Auditing and Logging“ im [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Whitepaper [Project REAL: Business Intelligence ETL Design Practices](http://go.microsoft.com/fwlink/?LinkId=96602).  
  
## Behandlung von Problemen bei der Paketausführung mithilfe von Debugdumpdateien  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]können Sie Debugdumpdateien erstellen, die Informationen über die Ausführung eines Pakets enthalten. Weitere Informationen finden Sie unter [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
## Behandlung von Problemen bei der Überprüfung zur Laufzeit  
 Es kann vorkommen, dass Sie keine Verbindung mit den Datenquellen herstellen können oder Teile des Pakets erst nach der Ausführung von vorausgehenden Tasks im Paket zur Laufzeit überprüft werden können. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt die folgenden Funktionen bereit, mit denen Sie die Überprüfungsfehler, die in solchen Fällen ausgelöst werden, vermeiden können:  
  
-   **Konfigurieren der DelayValidation-Eigenschaft für Paketelemente, die beim Laden des Pakets noch nicht gültig sind**. Zum Verhindern von Überprüfungsfehlern beim Laden des Pakets können Sie für Paketelemente, deren Konfigurationen zu diesem Zeitpunkt noch nicht gültig sind, **DelayValidation** auf **True** festlegen. Ein Beispiel hierfür wäre ein Datenflusstask, der eine Zieltabelle verwendet, die erst zur Laufzeit durch einen Task 'SQL ausführen' erstellt wird. Die **DelayValidation**-Eigenschaft kann auf Paketebene oder auf der Ebene der einzelnen, in den Paketen enthaltenen Tasks und Container aktiviert werden.  
  
     Die **DelayValidation** -Eigenschaft kann für einen Datenflusstask, jedoch nicht für einzelne Datenflusskomponenten festgelegt werden. Sie erreichen ein ähnliches Ergebnis, wenn Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A>-Eigenschaft einzelner Datenflusskomponenten auf **FALSE** festlegen. Wenn jedoch der Wert dieser Eigenschaft auf **false** festgelegt ist, erkennt die Komponente keine Änderungen der Metadaten externer Datenquellen. Wenn der Wert auf **true** festgelegt ist, können Sie mithilfe der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A>-Eigenschaft Blockierungsprobleme vermeiden, die durch Sperren in der Datenbank verursacht werden, insbesondere wenn das Paket Transaktionen verwendet.  
  
## Behandlung von Problemen mit Berechtigungen zur Laufzeit  
 Wenn beim Versuch, bereitgestellte Pakete mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents auszuführen, Fehler auftreten, verfügen die vom Agent verwendeten Konten möglicherweise nicht über die erforderlichen Berechtigungen. Informationen zur Fehlerbehebung bei Paketen, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Aufträgen ausgeführt werden, finden Sie unter [Beim Aufrufen aus einem SQL Server-Agentauftragsschritt wird ein SSIS-Paket nicht ausgeführt](http://support.microsoft.com/kb/918760). Weitere Informationen zum Ausführen von Paketen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agentaufträgen finden Sie unter [Aufträge des SQL Server-Agents für Pakete](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).  
  
 Für die Verbindung mit Excel- oder Access-Datenquellen erfordert der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent ein Konto mit entsprechenden Berechtigungen zum Lesen, Schreiben, Erstellen und Löschen temporärer Dateien in dem Ordner, der durch die TEMP- und TMP-Umgebungsvariablen angegeben wird.  
  
## Behandlung von 64-Bit-Problemen  
  
-   **Einige Datenanbieter sind auf der 64-Bit-Plattform nicht verfügbar**. Insbesondere ist keine 64-Bit-Version des [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieters für Jet verfügbar, der zum Herstellen von Verbindungen mit Excel- oder Access-Datenquellen benötigt wird.  
  
## Behandlung von Fehlern ohne Beschreibung  
 Wenn ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Fehler ohne zugehörige Beschreibung auftritt, können Sie die Beschreibung zu dem Fehler anhand seiner Fehlernummer in der Liste unter [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md) nachschlagen. Die Liste enthält zurzeit keine Informationen zur Problembehandlung.  
  
## Verwandte Aufgaben  
 [Konfigurieren einer Fehlerausgabe in einer Datenflusskomponente](../../integration-services/troubleshooting/configure-an-error-output-in-a-data-flow-component.md)  
  
## Verwandte Inhalte  
 Blogeintrag [Adding the error column name to an error output](http://go.microsoft.com/fwlink/?LinkId=261546) (Hinzufügen des Fehlerspaltennamens zu einer Fehlerausgabe) auf dougbert.com.  
  
||  
|-|  
|![Integration Services (kleines Symbol)](../../integration-services/troubleshooting/media/dts-16.png "Integration Services (kleines Symbol)")  **Informieren Sie sich laufend über Integration Services**<br /> Die neuesten Downloads, Artikel, Beispiele und Videos von Microsoft sowie ausgewählte Lösungen aus der Community finden Sie auf MSDN auf der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Seite:<br /><br /> -   [Besuchen Sie die Integration Services-Seite auf MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Abonnieren Sie die auf der Seite verfügbaren RSS-Feeds, um automatische Benachrichtigungen zu diesen Updates zu erhalten.|  
  
  