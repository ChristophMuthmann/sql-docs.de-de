---
title: "Benutzerdefinierte Meldungen f&#252;r die Protokollierung | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Protokolle [Integration Services], benutzerdefinierte"
  - "Schreiben von Protokolleinträgen"
  - "SSIS-Pakete, Protokolle"
  - "benutzerdefinierte Meldungen zur Protokollierung [Integration Services]"
ms.assetid: 3c74bba9-02b7-4bf5-bad5-19278b680730
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Benutzerdefinierte Meldungen f&#252;r die Protokollierung
SQL Server Integration Services stellt einen umfangreichen Satz an benutzerdefinierten Ereignissen zum Schreiben von Protokolleinträgen für Pakete und für mehrere Tasks bereit. Sie können diese Einträge verwenden, um detaillierte Informationen zum Fortschritt sowie über die Ergebnisse und Probleme der Ausführung zu speichern, indem Sie vordefinierte Ereignisse bzw. benutzerdefinierte Meldungen für die spätere Analyse erfassen. Sie können beispielsweise Beginn und Ende eines Masseneinfügungsvorgangs erfassen, um Leistungsprobleme beim Ausführen des Pakets zu identifizieren.  
  
 Die benutzerdefinierten Protokolleinträge unterscheiden sich von den für Pakete und alle Container und Tasks verfügbaren Standardprotokollierungsereignissen. Die benutzerdefinierten Protokolleinträge dienen zum Erfassen nützlicher Informationen zu einem bestimmten Task eines Pakets. Beispielsweise zeichnet einer der benutzerdefinierten Protokolleinträge für den Task SQL ausführen die von dem Task ausgeführte SQL-Anweisung im Protokoll auf.  
  
 In allen Protokolleinträgen sind jeweils das Datum und die Uhrzeit enthalten, einschließlich der beim Beginnen und Beenden eines Pakets automatisch geschriebenen Protokolleinträge. Bei vielen Protokollereignissen werden mehrere Einträge in das Protokoll geschrieben. In der Regel tritt dies dann auf, wenn ein Ereignis verschiedene Phasen aufweist. Beispielsweise schreibt das **ExecuteSQLExecutingQuery** -Protokollereignis drei Einträge: einen Eintrag, nachdem der Task eine Verbindung mit der Datenbank erhalten hat; einen weiteren, nachdem der Task begonnen hat, die SQL-Anweisung vorzubereiten; und noch einen, nachdem die Ausführung der SQL-Anweisung abgeschlossen wurde.  
  
 Die folgenden [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objekte verfügen über benutzerdefinierte Protokolleinträge:  
  
 [Paket](#Package)  
  
 [Masseneinfügungstask](#BulkInsert)  
  
 [Datenflusstask](#DataFlow)  
  
 [DTS 2000 ausführen (Task)](#ExecuteDTS200)  
  
 [Prozess ausführen (Task)](#ExecuteProcess)  
  
 [SQL ausführen (Task)](#ExecuteSQL)  
  
 [Task Dateisystem](#FileSystem)  
  
 [FTP-Task](#FTP)  
  
 [Nachrichtenwarteschlange (Task)](#MessageQueue)  
  
 [Skripttask](#Script)  
  
 [Mail senden (Task)](#SendMail)  
  
 [Datenbanken übertragen (Task)](#TransferDatabase)  
  
 [Fehlermeldungen übertragen (Task)](#TransferErrorMessages)  
  
 [Aufträge übertragen (Task)](#TransferJobs)  
  
 [Task "Anmeldungen übertragen"](#TransferLogins)  
  
 [In master gespeicherte Prozeduren übertragen (Task)](#TransferMasterStoredProcedures)  
  
 [SQL Server-Objekte kopieren (Task)](#TransferSQLServerObjects)  
  
 [Webdienste (Task)](#WebServices)  
  
 [WMI-Datenleser (Task)](#WMIDataReader)  
  
 [WMI-Ereignisüberwachung (Task)](#WMIEventWatcher)  
  
 [XML-Task](#XML)  
  
## Protokolleinträge  
  
###  <a name="Package"></a> Paket  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für Pakete aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**PackageStart**|Zeigt den Beginn der Paketausführung an. Dieser Protokolleintrag wird automatisch in das Protokoll geschrieben. Dieser Eintrag kann nicht ausgeschlossen werden.|  
|**PackageEnd**|Zeigt den Abschluss der Paketausführung an. Dieser Protokolleintrag wird automatisch in das Protokoll geschrieben. Dieser Eintrag kann nicht ausgeschlossen werden.|  
|**Diagnostic**|Enthält Informationen zur Systemkonfiguration, die sich auf die Paketausführung auswirken, wie z. B. die Anzahl ausführbarer Dateien, die gleichzeitig ausgeführt werden können.<br /><br /> Der Protokolleintrag **Diagnostic** enthält auch vorherige und nachfolgende Einträge für Aufrufe von externen Datenanbietern.|  
  
###  <a name="BulkInsert"></a> Masseneinfügungstask  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Masseneinfügungstask aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**DTSBulkInsertTaskBegin**|Zeigt den Beginn der Masseneinfügung an.|  
|**DTSBulkInsertTaskEnd**|Zeigt die Fertigstellung der Masseneinfügung an.|  
|**DTSBulkInsertTaskInfos**|Enthält beschreibende Informationen zum Task.|  
  
###  <a name="DataFlow"></a> Datenflusstask  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Datenflusstask aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**BufferSizeTuning**|Zeigt an, dass der Datenflusstask die Größe des Puffers geändert hat. Der Protokolleintrag beschreibt die Gründe für die Größenänderung und listet die temporäre neue Puffergröße auf.|  
|**OnPipelinePostEndOfRowset**|Gibt an, dass eine Komponente das Signal für das Ende des Rowsets erhalten hat. Dieses Signal wird durch den letzten Aufruf der **ProcessInput**-Methode festgelegt. Für jede Komponente im Datenfluss, die eine Eingabe verarbeitet, wird ein Eintrag geschrieben. Der Eintrag schließt den Namen der Komponente ein.|  
|**OnPipelinePostPrimeOutput**|Zeigt an, dass die Komponente ihren letzten Aufruf der **PrimeOutput** -Methode abgeschlossen hat. Je nach Datenfluss werden möglicherweise mehrere Protokolleinträge geschrieben. Wenn es sich bei der Komponente um eine Quelle handelt, bedeutet das, dass die von der Komponente durchgeführte Zeilenverarbeitung fertig gestellt wurde.|  
|**OnPipelinePreEndOfRowset**|Zeigt an, dass eine Komponente das Signal für das Ende des Rowsets erhalten soll. Dieses Signal wird durch den letzten Aufruf der **ProcessInput**-Methode festgelegt. Für jede Komponente im Datenfluss, die eine Eingabe verarbeitet, wird ein Eintrag geschrieben. Der Eintrag schließt den Namen der Komponente ein.|  
|**OnPipelinePrePrimeOutput**|Zeigt an, dass die Komponente einen Aufruf aus der **PrimeOutput** -Methode erhalten soll. Je nach Datenfluss werden möglicherweise mehrere Protokolleinträge geschrieben.|  
|**OnPipelineRowsSent**|Berichtet die Anzahl von Zeilen, die einer Komponenteneingabe durch einen Aufruf der **ProcessInput** -Methode bereitgestellt wurden. Der Protokolleintrag enthält den Komponentennamen.|  
|**PipelineBufferLeak**|Stellt Informationen zu Komponenten bereit, die Puffer aufrechterhalten haben, nachdem der Puffer-Manager beendet wurde. Das bedeutet, dass Pufferressourcen nicht freigegeben wurden, was zu Speicherverlusten führen kann. Der Protokolleintrag stellt den Namen der Komponente und die ID des Puffers bereit.|  
|**PipelineExecutionPlan**|Berichtet den Ausführungsplan des Datenflusses. Es werden Informationen darüber bereitgestellt, wie Puffer an Komponenten gesendet werden. Diese Informationen in Verbindung mit dem PipelineExecutionTrees-Eintrag beschreiben, was in dem Task geschieht.|  
|**PipelineExecutionTrees**|Berichtet die Ausführungsstrukturen des Layouts im Datenfluss. Der Planer des Datenflussmoduls verwendet die Strukturen zum Erstellen des Datenflussplans.|  
|**PipelineInitialization**|Bietet Initialisierungsinformationen zu dem Task. Zu diesen Informationen gehören die Verzeichnisse für die temporäre Speicherung von BLOB-Daten, die Standardpuffergröße und die Zeilenanzahl in einem Puffer. Je nach der Konfiguration des Datenflusstasks werden möglicherweise mehrere Protokolleinträge geschrieben.|  
  
###  <a name="ExecuteDTS200"></a> DTS 2000 ausführen (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task DTS 2000 ausführen aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**ExecuteDTS80PackageTaskBegin**|Zeigt an, dass die Ausführung eines DTS 2000-Pakets über den Task gestartet wurde.|  
|**ExecuteDTS80PackageTaskEnd**|Zeigt an, dass die Ausführung über den Task beendet wurde.<br /><br /> Hinweis: Das DTS 2000-Paket kann nach Beendigung des Tasks mit der Ausführung fortfahren.|  
|**ExecuteDTS80PackageTaskTaskInfo**|Enthält beschreibende Informationen zum Task.|  
|**ExecuteDTS80PackageTaskTaskResult**|Berichtet das Ausführungsergebnis des durch den Task ausgeführten DTS 2000-Pakets.|  
  
###  <a name="ExecuteProcess"></a> Prozess ausführen (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task Prozess ausführen aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|Enthält Informationen zum Ausführprozess der zur Ausführung konfigurierten ausführbaren Datei.<br /><br /> Es werden zwei Protokolleinträge geschrieben. Der eine Protokolleintrag enthält Informationen über den Namen und Speicherort der vom Task ausgeführten ausführbaren Datei, im anderen Eintrag wird das Beenden der ausführbaren Datei erfasst.|  
|**ExecuteProcessVariableRouting**|Enthält Informationen darüber, welche Variablen an die Eingabe und an die Ausgaben der ausführbaren Datei geleitet werden. Es werden Protokolleinträge für stdin (für die Eingabe), für stdout (für die Ausgabe) und für stderr (für die Fehlerausgabe) geschrieben.|  
  
###  <a name="ExecuteSQL"></a> SQL ausführen (Task)  
 In der folgenden Tabelle wird der benutzerdefinierte Protokolleintrag für den Task <legacyBold>SQL ausführen</legacyBold> beschrieben.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|Enthält Informationen zu den Ausführungsphasen der SQL-Anweisung. Protokolleinträge werden geschrieben, wenn der Task eine Verbindung mit der Datenbank erhält, wenn der Task beginnt, die SQL-Anweisung vorzubereiten, und nachdem die Ausführung der SQL-Anweisung abgeschlossen wurde. Der Protokolleintrag für die Vorbereitungsphase schließt die vom Task verwendete SQL-Anweisung ein.|  
  
###  <a name="FileSystem"></a> Task Dateisystem  
 In der folgenden Tabelle wird der benutzerdefinierte Protokolleintrag für den Task "Dateisystem" beschrieben.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**FileSystemOperation**|Berichtet den vom Task durchgeführten Vorgang. Der Protokolleintrag wird geschrieben, wenn der Dateisystemvorgang begonnen wird, und schließt Informationen über die Quelle und das Ziel ein.|  
  
###  <a name="FTP"></a> FTP-Task  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den FTP-Task aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**FTPConnectingToServer**|Zeigt an, dass mit dem Task eine Verbindung zum FTP-Server initiiert wurde.|  
|**FTPOperation**|Berichtet den Beginn und Typ des vom Task ausgeführten FTP-Vorgangs.|  
  
###  <a name="MessageQueue"></a> Nachrichtenwarteschlange (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task Nachrichtenwarteschlange aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**MSMQAfterOpen**|Zeigt an, dass das Öffnen der Warteschlange beendet wurde.|  
|**MSMQBeforeOpen**|Zeigt an, dass das Öffnen der Warteschlange begonnen wurde.|  
|**MSMQBeginReceive**|Zeigt an, dass das Empfangen einer Meldung begonnen wurde.|  
|**MSMQBeginSend**|Zeigt an, dass das Senden einer Meldung begonnen wurde.|  
|**MSMQEndReceive**|Zeigt an, dass das Empfangen einer Meldung beendet wurde.|  
|**MSMQEndSend**|Zeigt an, dass das Senden einer Meldung beendet wurde.|  
|**MSMQTaskInfo**|Enthält beschreibende Informationen zum Task.|  
|**MSMQTaskTimeOut**|Zeigt an, dass beim Task ein Timeout eingetreten ist.|  
  
###  <a name="Script"></a> Skripttask  
 In der folgenden Tabelle wird der benutzerdefinierte Protokolleintrag für den Skripttask beschrieben.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|Gibt die Ergebnisse des Implementierens der Protokollierung innerhalb des Skripts an. Für jeden Aufruf der **Log** -Methode des **Dts** -Objekts wird jeweils ein Protokolleintrag geschrieben. Der Eintrag wird beim Ausführen des Codes geschrieben. Weitere Informationen finden Sie unter [Logging in the Script Task](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md).|  
  
###  <a name="SendMail"></a> Mail senden (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task 'Mail senden' aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**SendMailTaskBegin**|Zeigt an, dass das Senden einer E-Mail-Nachricht begonnen wurde.|  
|**SendMailTaskEnd**|Zeigt an, dass das Senden einer E-Mail-Nachricht beendet wurde.|  
|**SendMailTaskInfo**|Enthält beschreibende Informationen zum Task.|  
  
###  <a name="TransferDatabase"></a> Datenbanken übertragen (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task Datenbanken übertragen aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**SourceDB**|Gibt die vom Task kopierte Datenbank an.|  
|**SourceSQLServer**|Gibt den Computer an, von dem die Datenbank kopiert wurde.|  
  
###  <a name="TransferErrorMessages"></a> Fehlermeldungen übertragen (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task Fehlermeldungen übertragen aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**TransferErrorMessagesTaskFinishedTransferringObjects**|Zeigt an, dass das Übertragen von Fehlermeldungen beendet wurde.|  
|**TransferErrorMessagesTaskStartTransferringObjects**|Zeigt an, dass das Übertragen von Fehlermeldungen gestartet wurde.|  
  
###  <a name="TransferJobs"></a> Aufträge übertragen (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task Aufträge übertragen aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**TransferJobsTaskFinishedTransferringObjects**|Zeigt an, dass das Übertragen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Aufträgen beendet wurde.|  
|**TransferJobsTaskStartTransferringObjects**|Zeigt an, dass das Übertragen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Aufträgen gestartet wurde.|  
  
###  <a name="TransferLogins"></a> Task "Anmeldungen übertragen"  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task Anmeldungen übertragen aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**TransferLoginsTaskFinishedTransferringObjects**|Zeigt an, dass das Übertragen von Anmeldungen beendet wurde.|  
|**TransferLoginsTaskStartTransferringObjects**|Zeigt an, dass das Übertragen von Anmeldungen gestartet wurde.|  
  
###  <a name="TransferMasterStoredProcedures"></a> In master gespeicherte Prozeduren übertragen (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task In master gespeicherte Prozeduren übertragen aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**TransferStoredProceduresTaskFinishedTransferringObjects**|Zeigt an, dass das Übertragen von benutzerdefinierten gespeicherten Prozeduren, die in der **master**-Datenbank gespeichert sind, beendet wurde.|  
|**TransferStoredProceduresTaskStartTransferringObjects**|Zeigt an, dass das Übertragen von benutzerdefinierten gespeicherten Prozeduren, die in der **master**-Datenbank gespeichert sind, gestartet wurde.|  
  
###  <a name="TransferSQLServerObjects"></a> SQL Server-Objekte kopieren (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte kopieren aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**TransferSqlServerObjectsTaskFinishedTransferringObjects**|Zeigt an, dass das Übertragen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankobjekten beendet wurde.|  
|**TransferSqlServerObjectsTaskStartTransferringObjects**|Zeigt an, dass das Übertragen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankobjekten gestartet wurde.|  
  
###  <a name="WebServices"></a> Webdienste (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge aufgelistet, die für den Task Webdienste aktiviert werden können.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|Der Zugriff auf einen Webdienst wurde begonnen.|  
|**WSTaskEnd**|Eine Webdienstmethode wurde beendet.|  
|**WSTaskInfo**|Beschreibende Informationen zum Task.|  
  
###  <a name="WMIDataReader"></a> WMI-Datenleser (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task WMI-Datenleser aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|Zeigt an, dass das Lesen der WMI-Daten begonnen wurde.|  
|**WMIDataReaderOperation**|Berichtet die vom Task ausgeführte WQL-Abfrage.|  
  
###  <a name="WMIEventWatcher"></a> WMI-Ereignisüberwachung (Task)  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task WMI-Ereignisüberwachung aufgelistet.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|Zeigt an, dass das vom Task überwachte Ereignis aufgetreten ist.|  
|**WMIEventWatcherTimedout**|Zeigt an, dass beim Task ein Timeout eingetreten ist.|  
|**WMIEventWatcherWatchingForWMIEvents**|Zeigt an, dass die Ausführung der WQL-Abfrage begonnen wurde. Der Eintrag schließt die Abfrage ein.|  
  
###  <a name="XML"></a> XML-Task  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den XML-Task beschrieben.  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**XMLOperation**|Stellt Informationen über den vom Task durchgeführten Vorgang bereit.|  
  
## Verwandte Aufgaben  
  
## Verwandte Inhalte  
 Blog-Artikel, [Logging custom events for Integration Services tasks](http://go.microsoft.com/fwlink/?LinkId=150580)(Protokollieren von benutzerdefinierten Ereignissen für Integration Services-Tasks), auf dougbert.com  
  
## Siehe auch  
 [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  