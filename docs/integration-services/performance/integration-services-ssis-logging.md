---
title: "Integration Services-Protokollierung (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Container [Integration Services], Protokolle"
  - "Windows-Ereignisprotokollanbieter [Integration Services]"
  - "XML-Dateiprotokollanbieter [Integration Services]"
  - "SQL Server Profiler, Protokollanbieter"
  - "SQL Server Integration Services-Pakete, Protokolle"
  - "SSIS-Pakete, Protokolle"
  - "Tasks [Integration Services], Protokolle"
  - "Protokolle [Integration Services], Protokollanbieter"
  - "Integration Services-Pakete, Protokolle"
  - "Protokollanbieter [Integration Services]"
  - "Pakete [Integration Services], Protokolle"
  - "Textdatei-Protokollanbieter"
  - "SQL Server-Protokollanbieter"
ms.assetid: 65e17889-371f-4951-9a7e-9932b2d0dcde
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 69
---
# Integration Services-Protokollierung (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält Protokollanbieter, mit denen Sie die Protokollierung in Paketen, Containern und Tasks implementieren können. Mit der Protokollierung können Sie Laufzeitinformationen zu einem Paket aufzeichnen, damit Sie ein Paket bei jeder Ausführung überwachen und Probleme behandeln können. Beispielsweise können in einem Protokoll der Name des Operators, der das Paket ausgeführt hat, und der Zeitpunkt, zu dem die Paketausführung begann und endete, aufgezeichnet werden.  
  
 Sie können den Protokollierungsbereich konfigurieren, der während einer Paketausführung auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server auftritt. Weitere Informationen finden Sie unter [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/enable-logging-for-package-execution-on-the-ssis-server.md).  
  
 Sie können die Protokollierung auch einschließen, wenn Sie ein Paket mit dem Eingabeaufforderungs-Hilfsprogramm **dtecex** ausführen. Weitere Informationen zu den Befehlszeilenargumenten, die die Protokollierung unterstützen, finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
## Konfigurieren der Protokollierung in SQL Server Data Tools  
 Protokolle werden Paketen zugeordnet und auf Paketebene konfiguriert. Jeder Task oder Container in einem Paket kann Informationen in einem Paketprotokoll protokollieren. Die Tasks und Container in einem Paket können für die Protokollierung auch dann aktiviert werden, wenn das Paket selbst nicht aktiviert ist. Sie können z. B. die Protokollierung für den Task "SQL ausführen" aktivieren, ohne die Protokollierung für das übergeordnete Paket zu aktivieren. Ein Paket, ein Container oder ein Task kann in mehrere Protokolle schreiben. Sie haben die Möglichkeit, die Protokollierung nur für das Paket bzw. für einen beliebigen im Paket enthaltenen Task oder Container zu aktivieren.  
  
 Wenn Sie das Protokoll einem Paket hinzufügen, wählen Sie den Protokollanbieter und den Speicherort des Protokolls aus. Der Protokollanbieter gibt das Format für die Protokolldaten an, z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank oder eine Textdatei.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält die folgenden Protokollanbieter:  
  
-   Den Textdatei-Protokollanbieter, der Protokolleinträge in ASCII-Textdateien durch Trennzeichen getrennt im CSV-Format schreibt. Die standardmäßige Dateinamenerweiterung für diesen Anbieter ist LOG.  
  
-   Den [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -Protokollanbieter, der Ablaufverfolgungen schreibt, die Sie mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler anzeigen können. Die standardmäßige Dateinamenerweiterung für diesen Anbieter ist TRC.  
  
    > [!NOTE]  
    >  Der [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]-Protokollanbieter kann nicht in einem Paket verwendet werden, das im 64-Bit-Modus ausgeführt wird.  
  
-   Den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Protokollanbieter, der Protokolleinträge in die **sysssislog** -Tabelle in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank schreibt.  
  
-   Den Windows-Ereignisprotokollanbieter, der Einträge in das Anwendungsprotokoll im Windows-Ereignisprotokoll auf dem lokalen Computer schreibt.  
  
-   Den XML-Dateiprotokollanbieter, der Protokolldateien in eine XML-Datei schreibt. Die standardmäßige Dateinamenerweiterung für diesen Anbieter ist XML.  
  
 Wenn Sie einem Paket einen Protokollanbieter hinzufügen oder die Protokollierung programmgesteuert konfigurieren, können Sie eine ProgID oder ClassID zum Identifizieren des Protokollanbieters verwenden, statt die vom [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer im Dialogfeld **SSIS-Protokolle konfigurieren** angezeigten Namen zu verwenden.  
  
 In der folgenden Tabelle sind die ProgID und die ClassID für die Protokollanbieter von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aufgeführt, sowie der Speicherort der Protokolle, in die Protokollanbieter schreiben.  
  
|Protokollanbieter|ProgID|ClassID|Speicherort|  
|------------------|------------|-------------|--------------|  
|Textdatei|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|Der vom Protokollanbieter verwendete Dateiverbindungs-Manager gibt den Pfad der Textdatei an.|  
|SQL Server Profiler|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|Der vom Protokollanbieter verwendete Dateiverbindungs-Manager gibt den Pfad der von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]verwendeten Textdatei an.|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|Der vom Protokollanbieter verwendete OLE DB-Verbindungs-Manager gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank an, die die sysssislog-Tabelle mit den Protokolleinträgen enthält.|  
|Windows-Ereignisprotokoll|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Das Anwendungsprotokoll der Windows-Ereignisanzeige enthält die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Protokollinformationen.|  
|XML-Datei|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|Der vom Protokollanbieter verwendete Dateiverbindungs-Manager gibt den Pfad der XML-Datei an.|  
  
 Außerdem können Sie benutzerdefinierte Protokollanbieter erstellen. Weitere Informationen finden Sie unter [Creating a Custom Log Provider](../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md).  
  
 Die Protokollanbieter in einem Paket sind Elemente der Protokollanbieterauflistung des Pakets. Wenn Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer ein Paket erstellen und die Protokollierung implementieren, können Sie eine Liste der Sammelelemente im Ordner **Protokollanbieter** auf der Registerkarte **Paket-Explorer** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers anzeigen.  
  
 Zum Konfigurieren eines Protokollanbieters stellen Sie einen Namen und eine Beschreibung für den Protokollanbieter bereit und geben den Verbindungs-Manager an, den der Protokollanbieter verwendet. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Protokollanbieter verwendet einen OLE DB-Verbindungs-Manager. Für die Textdatei-, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]- und XML-Datei-Protokollanbieter werden Dateiverbindungs-Manager verwendet. Für den Windows-Ereignisprotokollanbieter wird kein Verbindungs-Manager verwendet, da direkt in das Windows-Ereignisprotokoll geschrieben wird. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md) und [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
### Protokollierungsanpassung  
 Zum Anpassen der Protokollierung eines Ereignisses oder einer benutzerdefinierten Meldung wird in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ein Schema häufig protokollierter Informationen bereitgestellt, die in Protokolleinträgen aufgenommen werden. Das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Protokollschema definiert die Informationen, die Sie protokollieren können. Für jeden Protokolleintrag können Sie Elemente aus dem Protokollschema auswählen.  
  
 Ein Paket und seine Container und Tasks protokollieren nicht dieselben Informationen, und Tasks innerhalb desselben Pakets oder Containers können verschiedene Informationen protokollieren. Ein Paket kann z. B. Operatorinformationen protokollieren, wenn das Paket gestartet wird, ein Task kann die Fehlerquelle des Tasks protokollieren, und ein weiterer Task kann Informationen protokollieren, wenn Fehler auftreten. Wenn ein Paket und seine Container mehrere Protokolle verwenden, werden dieselben Informationen in alle Protokolle geschrieben.  
  
 Sie können einen Protokolliergrad auswählen, der Ihren Anforderungen entspricht, indem Sie die zu protokollierenden Ereignisse und die für jedes Ereignis zu protokollierenden Informationen festlegen. Eventuell enthalten Ihrer Meinung nach einige Ereignisse nützlichere Informationen als andere. Vielleicht möchten Sie z. B. nur die Computer- und Operatornamen für das **PreExecute** -Ereignis protokollieren, für das **Error** -Ereignis jedoch alle verfügbaren Informationen.  
  
 Damit die Protokolldateien keine großen Speichermengen belegen oder um eine zu umfangreiche Protokollierung zu vermeiden, was zu einer Leistungsverschlechterung führen könnte, können Sie die Protokollierung einschränken, indem Sie bestimmte zu protokollierende Ereignisse und Informationen auswählen. So können Sie z. B. ein Protokoll konfigurieren, das nur das Datum und den Computernamen für einen Fehler erfasst.  
  
 In [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer legen Sie die Protokollierungsoptionen im Dialogfeld **SSIS-Protokolle konfigurieren** fest.  
  
#### Protokollschema  
 In der folgenden Tabelle werden die Elemente im Protokollschema beschrieben.  
  
|Element|Description|  
|-------------|-----------------|  
|Computer|Der Name des Computers, auf dem das Protokollereignis auftrat.|  
|Operator|Die Identität des Benutzers, der das Paket gestartet hat.|  
|SourceName|Der Name des Containers oder des Tasks, für den das Protokollereignis auftrat.|  
|SourceID|Der eindeutige Bezeichner des Pakets; der For-Schleifen-, Foreach-Schleifen- oder Sequenz-Container; oder der Task, für den das Protokollereignis auftrat.|  
|ExecutionID|Die GUID der Paketausführungsinstanz.<br /><br /> Hinweis: Beim Ausführen eines einzelnen Pakets werden möglicherweise Protokolleinträge mit anderen Werten für das ExecutionID-Element erstellt. Wenn Sie ein Paket beispielsweise in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]ausführen, werden in der Überprüfungsphase möglicherweise Protokolleinträge mit einem ExecutionID-Element erstellt, das [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]entspricht. In der Ausführungsphase werden jedoch unter Umständen Protokolleinträge mit einem ExecutionID-Element erstellt, das dtshost.exe entspricht. Um ein weiteres Beispiel zu geben, können Sie ein Paket ausführen, das Tasks vom Typ "Paket ausführen" enthält, wobei von jedem dieser Tasks ein untergeordnetes Paket ausgeführt wird. Diese untergeordneten Pakete erstellen möglicherweise Protokolleinträge mit einem anderen ExecutionID-Element als in den vom übergeordneten Paket erstellten Protokolleinträgen.|  
|MessageText|Eine dem Protokolleintrag zugeordnete Meldung.|  
|DataBytes|Ein für den Protokolleintrag spezifisches Bytearray. Die Bedeutung dieses Felds variiert je nach Protokolleintrag.|  
  
 Die folgende Tabelle beschreibt drei zusätzliche Elemente des Protokollschemas, die auf der Registerkarte **Details** des Dialogfensters **SSIS-Protokolle konfigurieren** nicht verfügbar sind.  
  
|Element|Description|  
|-------------|-----------------|  
|StartTime|Der Zeitpunkt, zu dem der Container oder der Task die Ausführung beginnt.|  
|EndTime|Der Zeitpunkt, zu dem der Container oder der Task die Ausführung beendet.|  
|DataCode|Ein optionaler ganzzahliger Wert, der typischerweise einen Wert aus der <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>-Enumeration enthält, der das Ergebnis des aktuell ausgeführten Containers oder Tasks angibt:<br /><br /> 0 – Erfolg<br /><br /> 1 – Fehlschlag<br /><br /> 2 – Abgeschlossen<br /><br /> 3 – Abgebrochen|  
  
#### Protokolleinträge  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt Protokolleinträge für vordefinierte Ereignisse und stellt für viele [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objekte benutzerdefinierte Protokolleinträge bereit. Im Dialogfeld **SSIS-Protokolle konfigurieren** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers werden diese Ereignisse und benutzerdefinierten Protokolleinträge aufgelistet.  
  
 In der folgenden Tabelle werden die vordefinierten Ereignisse beschrieben, die beim Auftreten von Laufzeitereignissen zum Schreiben von Protokolleinträgen aktiviert werden können. Diese Protokolleinträge gelten für ausführbare Dateien, das Paket sowie die im Paket enthaltenen Tasks und Container. Der Name des Protokolleintrags entspricht dem Namen des ausgelösten Laufzeitereignisses, mit dem das Schreiben des Protokolleintrags verursacht wurde.  
  
|Ereignisse|Description|  
|------------|-----------------|  
|**OnError**|Schreibt einen Protokolleintrag, wenn ein Fehler auftritt.|  
|**OnExecStatusChanged**|Schreibt einen Protokolleintrag, wenn ein Task (nicht ein Container) während des Debuggens angehalten oder wieder aufgenommen wurde.|  
|**OnInformation**|Schreibt einen Protokolleintrag während der Prüfung und Ausführung einer ausführbaren Datei, um Informationen zu melden.|  
|**OnPostExecute**|Schreibt einen Protokolleintrag unmittelbar nach Beendigung der Ausführung der ausführbaren Datei.|  
|**OnPostValidate**|Schreibt einen Protokolleintrag, wenn die Überprüfung der ausführbaren Datei beendet ist.|  
|**OnPreExecute**|Schreibt einen Protokolleintrag unmittelbar vor Ausführung der ausführbaren Datei.|  
|**OnPreValidate**|Schreibt einen Protokolleintrag, wenn die Überprüfung der ausführbaren Datei beginnt.|  
|**OnProgress**|Schreibt einen Protokolleintrag, wenn die ausführbare Datei einen messbaren Fortschritt gemacht hat.|  
|**OnQueryCancel**|Schreibt einen Protokolleintrag für jeden Punkt in der Taskverarbeitung, an dem ein Abbruch der Ausführung sinnvoll ist.|  
|**OnTaskFailed**|Schreibt einen Protokolleintrag, wenn ein Task fehlschlägt.|  
|**OnVariableValueChanged**|Schreibt einen Protokolleintrag, wenn sich der Wert einer Variablen ändert.|  
|**OnWarning**|Schreibt einen Protokolleintrag, wenn eine Warnung auftritt.|  
|**PipelineComponentTime**|Schreibt für jede Datenflusskomponente einen Protokolleintrag für jede Phase der Überprüfung und der Ausführung. Der Protokolleintrag gibt die Verarbeitungszeit für jede Phase an.|  
|**Diagnostic**<br /><br /> **DiagnosticEx**|Schreibt einen Protokolleintrag, der Diagnoseinformationen enthält.<br /><br /> Sie können zum Beispiel vor und nach jedem Aufruf eines externen Datenanbieters eine Meldung protokollieren. Weitere Informationen finden Sie unter [Behandlung von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).<br /><br /> Protokollieren Sie das **DiagnosticEx** -Ereignis, wenn Sie die Spaltennamen für Spalten im Datenfluss finden möchten, die Fehler enthalten. Dieses Ereignis schreibt eine Herkunftszuordnung für den Datenfluss in das Protokoll. Sie können den Spaltennamen dann in dieser Herkunftszuordnung nachschlagen, und zwar anhand des von einer Fehlerausgabe erfassten Spaltenbezeichners. Weitere Informationen finden Sie unter [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> Beachten Sie, dass Leerraum in der XML-Ausgabe beim **DiagnosticEx** -Ereignis nicht beibehalten wird, um die Größe des Protokolls zu verringern. Kopieren Sie das Protokoll in einen XML-Editor wie z.B. Visual Studio, der XML-Formatierung und Syntaxhervorhebung unterstützt, um die Lesbarkeit zu verbessern.<br /><br /> Hinweis: Wenn Sie das **DiagnosticEx** -Ereignis mit dem SQL Server-Protokollanbieter protokollieren, wird die Ausgabe möglicherweise abgeschnitten. Das **message**-Feld des SQL Server-Protokollanbieters ist vom Typ „nvarchar(2048)“. Verwenden Sie beim Protokollieren des **DiagnosticEx** -Ereignisses einen anderen Protokollanbieter, um eine abgeschnittene Ausgabe zu vermeiden.|  
  
 Das Paket und viele Tasks verfügen über benutzerdefinierte Protokolleinträge, die für die Protokollierung aktiviert werden können. Der Task „Mail senden“ stellt z.B. den benutzerdefinierten Protokolleintrag **SendMailTaskBegin** bereit, mit dem im Zeitraum zwischen dem Beginn der Ausführung des Tasks „Mail senden“ und dem Senden einer E-Mail-Nachricht Informationen protokolliert werden. Weitere Informationen finden Sie unter [Custom Messages for Logging](../../integration-services/performance/custom-messages-for-logging.md).  
  
### Unterscheiden von Paketkopien  
 Protokolldaten schließen den Namen und den GUID des Pakets ein, zu dem die Protokolleinträge gehören. Beim Erstellen eines neuen Pakets durch Kopieren eines vorhandenen Pakets werden Name und GUID des vorhandenen Pakets ebenfalls kopiert. Folglich können GUID und Name zweier Pakete identisch sein, sodass die Pakete in den Protokolldaten schwer voneinander zu unterscheiden sind.  
  
 Sie sollten den Namen und GUID der neuen Pakete ändern, um diese Mehrdeutigkeit zu umgehen. Sie können in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mithilfe des Eigenschaftenfensters die GUID in der **ID**-Eigenschaft neu generieren und den Wert der **Name**-Eigenschaft aktualisieren. Sie haben auch die Möglichkeit, den GUID und Namen programmgesteuert oder mit dem Hilfsprogramm **dtutil** zu ändern. Weitere Informationen finden Sie unter [Festlegen von Paketeigenschaften](../../integration-services/set-package-properties.md) und [dtutil (Hilfsprogramm)](../../integration-services/dtutil-utility.md).  
  
### Übergeordnete Protokollierungsoptionen  
 Häufig entsprechen die Protokollierungsoptionen von Tasks und For-Schleifen-, Foreach-Schleifen- und Sequenz-Containern denen des Paketcontainers oder eines übergeordneten Containers. In diesem Fall können Sie diese so konfigurieren, dass sie die Protokollierungsoptionen von ihrem übergeordneten Container erben. In einem For-Schleifen-Container, der den Task "SQL ausführen" enthält, kann z. B. der Task "SQL ausführen" die Protokollierungsoptionen verwenden, die für den For-Schleifen-Container festgelegt werden. Legen Sie zum Verwenden der übergeordneten Protokollierungsoptionen die LoggingMode-Eigenschaft des Containers auf **UseParentSetting** fest. Sie können diese Eigenschaft im Fenster **Eigenschaften** von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder im Dialogfeld **SSIS-Protokolle konfigurieren** in [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen.  
  
### Protokollierungsvorlagen  
 Im Dialogfeld **SSIS-Protokolle konfigurieren** können Sie auch häufig verwendete Protokollierungskonfigurationen als Vorlagen erstellen und speichern und die Vorlagen dann in mehreren Paketen verwenden. So ist es einfach, eine konsequente Protokollierungsstrategie für mehrere Pakete anzuwenden und Protokolleinstellungen für Pakete zu ändern, indem die Vorlagen aktualisiert und dann angewendet werden. Die Vorlagen werden als XML-Dateien gespeichert.  
  
 **So konfigurieren Sie die Protokollierung im Dialogfeld "SSIS-Protokolle konfigurieren"**  
  
1.  Aktivieren Sie das Paket und seine Tasks für die Protokollierung. Die Protokollierung kann auf Paket-, Container- und Taskebene stattfinden. Sie können verschiedene Protokolle für Pakete, Container und Tasks angeben.  
  
2.  Wählen Sie einen Protokollanbieter aus, und fügen Sie ein Protokoll für das Paket hinzu. Protokolle können nur auf Paketebene erstellt werden, und ein Task oder Container muss eines der für das Paket erstellten Protokolle verwenden. Jedes Protokoll ist einem der folgenden Protokollanbieter zugeordnet: Textdatei, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Windows-Ereignisprotokoll oder XML-Datei. Weitere Informationen finden Sie unter [Aktivieren der Paketprotokollierung in SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md).  
  
3.  Wählen Sie die Ereignisse und die Protokollschemainformationen zu jedem Ereignis aus, das Sie im Protokoll erfassen möchten. Weitere Informationen finden Sie unter [Konfigurieren der Protokollierung mithilfe einer gespeicherten Konfigurationsdatei](../../integration-services/performance/configure-logging-by-using-a-saved-configuration-file.md).  
  
### Konfiguration des Protokollanbieters  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Ein Protokollanbieter wird als ein Schritt beim Implementieren der Protokollierung in einem Paket erstellt und konfiguriert.  
  
 Nachdem Sie einen Protokollanbieter erstellt haben, können Sie dessen Eigenschaften im Eigenschaftenfenster von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]anzeigen und ändern.  
  
 Weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften finden Sie in der Dokumentation zur <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider>-Klasse.  
  
### Protokollierung von Datenflusstasks  
 Der Datenflusstask stellt eine Reihe von benutzerdefinierten Protokolleinträge bereit, die zum Überwachen und Anpassen der Leistung verwendet werden können. Sie können beispielsweise Komponenten überwachen, die möglicherweise Arbeitsspeicherverluste verursachen, oder nachverfolgen, wie lange das Ausführen einer bestimmten Komponente dauert. Eine Liste dieser benutzerdefinierten Protokolleinträge sowie Beispiele für Protokollausgaben finden Sie unter [Data Flow Task](../../integration-services/control-flow/data-flow-task.md).  
  
#### Erfassen der Namen fehlerhafter Spalten  
 Die Fehlerausgabe im Datenfluss ist standardmäßig so konfiguriert, dass sie nur den numerischen Bezeichner der Spalte bereitstellt, in der der Fehler aufgetreten ist. Weitere Informationen finden Sie unter [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md).  
  
 Sie finden die Spaltennamen, indem Sie die Protokollierung aktivieren und das **DiagnosticEx** -Ereignis auswählen. Dieses Ereignis schreibt eine Herkunftszuordnung für den Datenfluss in das Protokoll. Anschließend können Sie den Namen der Spalte anhand ihres Bezeichners in dieser Herkunftszuordnung nachschlagen. Beachten Sie, dass Leerraum in der XML-Ausgabe beim **DiagnosticEx** -Ereignis nicht beibehalten wird, um die Größe des Protokolls zu verringern. Kopieren Sie das Protokoll in einen XML-Editor wie z.B. Visual Studio, der XML-Formatierung und Syntaxhervorhebung unterstützt, um die Lesbarkeit zu verbessern.  
  
#### Verwenden des PipelineComponentTime-Ereignisses  
 Das PipelineComponentTime-Ereignis stellt möglicherweise den nützlichsten benutzerdefinierten Protokolleintrag dar. Dieser Protokolleintrag meldet den Zeitaufwand in Millisekunden, den jede Komponente im Datenfluss für die fünf Hauptverarbeitungsschritte jeweils aufbringt. In der folgenden Tabelle werden diese Verarbeitungsschritte beschrieben. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Entwickler kennen diese Schritte als Hauptmethoden einer <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
|Schritt|Description|  
|----------|-----------------|  
|Überprüfen|Die Komponente überprüft Eigenschaftswerte und Konfigurationseinstellungen auf ihre Gültigkeit.|  
|PreExecute|Die Komponente führt eine einmalige Verarbeitung aus, bevor sie mit der Verarbeitung von Datenzeilen beginnt.|  
|PostExecute|Die Komponente führt eine einmalige Verarbeitung aus, nachdem alle Datenzeilen verarbeitet wurden.|  
|ProcessInput|Die Transformations- oder Zielkomponente verarbeitet die eingehenden Datenzeilen, die von einer Upstreamquelle oder einer Transformation an sie übergeben wurden.|  
|PrimeOutput|Die Quell- oder Transformationskomponente füllt die Puffer von Daten auf, die an eine Downstreamtransformation oder eine Zielkomponente übergeben werden sollen.|  
  
 Wenn Sie das PipelineComponentTime-Ereignis aktivieren, protokolliert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Meldung für jeden der von den einzelnen Komponenten ausgeführten Verarbeitungsschritt. Die folgenden Protokolleinträge zeigen eine Teilmenge der Meldungen, die vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CalculatedColumns-Paketbeispiel protokolliert werden:  
  
 `The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`  
  
 `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`  
  
 `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`  
  
 `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`  
  
 `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`  
  
 `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`  
  
 Diese Protokolleinträge zeigen, dass der Datenflusstask den größten Zeitaufwand für die folgenden, hier in absteigender Reihenfolge gezeigten Schritte benötigt hat:  
  
-   Die OLE DB-Quelle mit dem Namen "Extract Data" hat 688 Millisekunden für das Laden von Daten benötigt.  
  
-   Die Transformation für abgeleitete Spalten mit dem Namen "Calculate LineItemTotalCost" hat 356 Millisekunden für das Durchführen von Berechnungen für eingehende Zeilen benötigt.  
  
-   Die Transformation für das Aggregieren mit dem Namen "Sum Quantity and LineItemTotalCost" hat insgesamt 220 Millisekunden &ndash; 141 für den PrimeOutput- und 79 für den ProcessInput-Schritt &ndash; benötigt, um Berechnungen durchzuführen und die Daten an die nächste Transformation zu übergeben.  
  
## Verwandte Aufgaben  
 Die folgende Liste enthält Links zu Themen, die die Ausführung von Tasks in Verbindung mit der Protokollierungsfunktion beschreiben.  
  
-   [SSIS-Protokolle konfigurieren (Dialogfeld)](../../integration-services/performance/configure-ssis-logs-dialog-box.md)  
  
-   [Aktivieren der Paketprotokollierung in SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)  
  
-   [Aktivieren der Protokollierung für die Paketausführung auf dem SSIS-Server](../../integration-services/performance/enable-logging-for-package-execution-on-the-ssis-server.md)  
  
-   [Anzeigen der Protokolleinträge im Fenster 'Protokollereignisse'](../../integration-services/performance/view-log-entries-in-the-log-events-window.md)  
  
## Verwandte Inhalte  
 [DTLoggedExec-Tool für vollständige und Detailprotokollierung (CodePlex-Projekt)](http://go.microsoft.com/fwlink/?LinkId=150579)  
  
## Siehe auch  
 [Anzeigen der Protokolleinträge im Fenster 'Protokollereignisse'](../../integration-services/performance/view-log-entries-in-the-log-events-window.md)  
  
  