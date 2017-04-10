---
title: "Worker f&#252;r horizontales Hochskalieren von Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 480a3f3d-9a79-4a02-81e5-7d27afd756c4
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Worker f&#252;r horizontales Hochskalieren von Integration Services (SSIS)
Ein Worker für horizontales Hochskalieren führt einen Worker für horizontales Hochskalieren von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)]-Dienst aus, um Ausführungsaufgaben aus dem Master für horizontales Hochskalieren abzurufen, und führt die Pakete lokal mit „ISServerExec.exe“ aus.

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>Konfigurieren des Worker für horizontales Hochskalieren von SQL Server Integration Services-Diensts
Der Worker für horizontales Hochskalieren-Dienst kann mit der Datei „\<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config“ konfiguriert werden. Der Dienst muss neu gestartet werden, nachdem die Konfigurationsdatei aktualisiert wurde.
    


Konfiguration  |Description  |Standardwert  
---------|---------|---------
DisplayName|Der Anzeigename des Workers für horizontales Hochskalieren. **Wird in [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1 nicht verwendet.**|Computername         
Description|Die Beschreibung des Workers für horizontales Hochskalieren. **Wird in [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1 nicht verwendet.**|Empty         
MasterEndpoint|Der Endpunkt zum Herstellen einer Verbindung mit Master für horizontales Hochskalieren|Der Endpunkt, der während der Installation des Workers für horizontales Hochskalieren festgelegt wurde         
MasterHttpsCertThumbprint|Der Fingerabdruck des Client-SSL-Zertifikats, mit dem Master für horizontales Hochskalieren authentifiziert wird|Der Fingerabdruck des Clientzertifikats, das bei der Installation von Worker für horizontales Hochskalieren angegeben wurde          
WorkerHttpsCertThumbprint|Der Fingerabdruck des Zertifikats, das für den Master für horizontales Hochskalieren verwendet wird, um den Worker für horizontales Hochskalieren zu authentifizieren|Der Fingerabdruck eines Zertifikats, das bei der Installation von Worker für horizontales Hochskalieren automatisch erstellt und installiert wurde          
StoreLocation|Der Speicherort des Workerzertifikats|LocalMachine       
StoreName|Der Name des Speichers, in dem sich das Workerzertifikat befindet|My         
AgentHeartbeatInterval|Das Zeitintervall für den Takt für Worker für horizontales Hochskalieren|00:01:00         
TaskHeartbeatInterval|Das Zeitintervall für den Status des Berichtstasks für Worker für horizontales Hochskalieren|00:00:10         
HeartbeatErrorTollerance|Nach diesem Zeitraum ab dem letzten erfolgreichen Tasktakt wird der Task beendet, wenn eine Fehlerantwort des Takts empfangen wird.|00:10:00      
TaskRequestMaxCPU|Die Obergrenze bezüglich CPU für Worker für horizontales Hochskalieren, um Tasks anzufordern. **Wird in [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1 nicht verwendet.**|70.0         
TaskRequestMinMemory|Die Mindestmenge von Arbeitsspeicher in MB für Worker für horizontales Hochskalieren, um Tasks anzufordern. **Wird in [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1 nicht verwendet.**|100.0         
MaxTaskCount|Die maximale Anzahl von Tasks, die der Worker für horizontales Hochskalieren aufnehmen kann|10         
LeaseInternval|Das Leaseintervall einer Taskaufbewahrung durch den Worker für horizontales Hochskalieren|00:01:00         
TasksRootFolder|Der Ordner für die Taskprotokolle. Es wird der Ordnerpfad „\<Treiber\>:\Benutzer\\*[Konto]*\AppData\Local\SSIS\Cluster\Tasks“ verwendet, wenn der Wert leer ist. [Konto] ist das Konto, unter dem der Dienst für Worker für horizontales Hochskalieren ausgeführt wird. Standardmäßig ist dies das Konto SSISScaleOutWorker140.|Empty         
TaskLogLevel|Die Taskprotokollebene für den Worker für horizontales Hochskalieren. (Ausführlich 0x01, Informationen 0x02, Warnung 0x04, Fehler 0x08, Status 0x10, schwerwiegender Fehler 0x20, Überwachung 0x40)|126 (Informationen, Warnung, Fehler, Status, schwerwiegender Fehler, Überwachung)     
TaskLogSegment|Die Zeitspanne einer Taskprotokolldatei|00:00:00         
TaskLogEnabled|Gibt an, ob das Taskprotokoll aktiviert ist.|true         
ExecutionLogCacheFolder|Der Ordner, in dem das Paketausführungsprotokoll zwischengespeichert wird. Es wird der Ordnerpfad „\<Treiber\>:\Benutzer\\*[Konto]*\AppData\Local\SSIS\Cluster\Agent\ELogCache“ verwendet, wenn der Wert leer ist. [Konto] ist das Konto, unter dem der Dienst für Worker für horizontales Hochskalieren ausgeführt wird. Standardmäßig ist dies das Konto SSISScaleOutWorker140.|Empty         
ExecutionLogMaxBufferLogCount|Die maximale Anzahl von Ausführungsprotokollen, die in einem Ausführungsprotokollpuffer im Arbeitsspeicher zwischengespeichert werden|10000        
ExecutionLogMaxInMemoryBufferCount|Die maximale Anzahl von Ausführungsprotokollpuffern im Arbeitsspeicher für Ausführungsprotokolle|10         
ExecutionLogRetryCount|Die Anzahl von Wiederholungsversuchen, wenn bei der Ausführungsprotokollierung ein Fehler auftritt|3         
AgentId|Worker-Agent-ID für den Worker für horizontales Hochskalieren|Wird automatisch generiert        



## <a name="view-scale-out-worker-log"></a>Anzeigen des Protokolls für Worker für horizontales Hochskalieren
Die Protokolldatei des Diensts für Worker für horizontales Hochskalieren befindet sich im Ordnerpfad „\<Treiber\>:\Benutzer\\*[Konto]*\AppData\Local\SSIS\Cluster\Agent“.

Der Protokollspeicherort jedes einzelnen Tasks ist in der Datei „WorkerSettings.config“ durch „TasksRootFolder“ konfiguriert. Ist kein Speicherort angegeben, befindet sich das Protokoll im Ordnerpfad „\<Treiber\>:\Benutzer\\*[Konto]*\AppData\Local\SSIS\Cluster\Tasks“. 

Der Ordner *[Konto]* ist das Konto, unter dem der Dienst für Worker für horizontales Hochskalieren ausgeführt wird. Standardmäßig ist dies das Konto SSISScaleOutWorker140.
    