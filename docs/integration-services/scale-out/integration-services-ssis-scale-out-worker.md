---
title: SSIS Scale Out-Worker (SQL Server Integration Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb36dc89fbe8fbedc96e426d00f6982213d7d4c9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-scale-out-worker"></a>Worker für horizontales Hochskalieren von Integration Services (SSIS)

Ein Scale Out-Worker führt einen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] Scale Out-Workerdienst aus, um Ausführungstasks aus dem Scale Out-Master abzurufen, und führt die Pakete lokal mit „ISServerExec.exe“ aus.

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>Konfigurieren des Worker für horizontales Hochskalieren von SQL Server Integration Services-Diensts
Der Worker für horizontales Hochskalieren-Dienst kann mit der Datei „ \<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config“ konfiguriert werden. Der Dienst muss neu gestartet werden, nachdem die Konfigurationsdatei aktualisiert wurde.

Konfiguration  |Description  |Standardwert  
---------|---------|---------
DisplayName|Der Anzeigename des Workers für horizontales Hochskalieren. **Wird NICHT in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 verwendet.**|Computername         
Description|Die Beschreibung des Workers für horizontales Hochskalieren. **Wird NICHT in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 verwendet.**|Empty         
MasterEndpoint|Der Endpunkt zum Herstellen einer Verbindung mit Master für horizontales Hochskalieren|Der Endpunkt, der während der Installation des Workers für horizontales Hochskalieren festgelegt wurde         
MasterHttpsCertThumbprint|Der Fingerabdruck des Client-SSL-Zertifikats, mit dem Master für horizontales Hochskalieren authentifiziert wird|Der Fingerabdruck des Clientzertifikats, das bei der Installation von Worker für horizontales Hochskalieren angegeben wurde          
WorkerHttpsCertThumbprint|Der Fingerabdruck des Zertifikats, das für den Master für horizontales Hochskalieren verwendet wird, um den Worker für horizontales Hochskalieren zu authentifizieren|Der Fingerabdruck eines Zertifikats, das bei der Installation von Worker für horizontales Hochskalieren automatisch erstellt und installiert wurde          
StoreLocation|Der Speicherort des Workerzertifikats|LocalMachine       
StoreName|Der Name des Speichers, in dem sich das Workerzertifikat befindet|My         
AgentHeartbeatInterval|Das Zeitintervall für den Takt für Worker für horizontales Hochskalieren|00:01:00         
TaskHeartbeatInterval|Das Zeitintervall für den Status des Berichtstasks für Worker für horizontales Hochskalieren|00:00:10         
HeartbeatErrorTollerance|Nach diesem Zeitraum ab dem letzten erfolgreichen Tasktakt wird der Task beendet, wenn eine Fehlerantwort des Takts empfangen wird.|00:10:00      
TaskRequestMaxCPU|Die Obergrenze bezüglich CPU für Worker für horizontales Hochskalieren, um Tasks anzufordern. **Wird NICHT in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 verwendet.**|70.0         
TaskRequestMinMemory|Die Mindestmenge von Arbeitsspeicher in MB für Worker für horizontales Hochskalieren, um Tasks anzufordern. **Wird NICHT in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 verwendet.**|100.0         
MaxTaskCount|Die maximale Anzahl von Tasks, die der Worker für horizontales Hochskalieren aufnehmen kann|10         
LeaseInternval|Das Leaseintervall einer Taskaufbewahrung durch den Worker für horizontales Hochskalieren|00:01:00         
TasksRootFolder|Der Ordner für die Taskprotokolle. Es wird der Ordnerpfad „ \<Treiber\>:\Benutzer\\*[Konto]*\AppData\Local\SSIS\Cluster\Tasks“ verwendet, wenn der Wert leer ist. [Konto] ist das Konto, unter dem der Dienst für Worker für horizontales Hochskalieren ausgeführt wird. Standardmäßig ist dies das Konto SSISScaleOutWorker140.|Empty         
TaskLogLevel|Die Taskprotokollebene für den Worker für horizontales Hochskalieren. (Ausführlich 0x01, Informationen 0x02, Warnung 0x04, Fehler 0x08, Status 0x10, schwerwiegender Fehler 0x20, Überwachung 0x40)|126 (Informationen, Warnung, Fehler, Status, schwerwiegender Fehler, Überwachung)     
TaskLogSegment|Die Zeitspanne einer Taskprotokolldatei|00:00:00         
TaskLogEnabled|Gibt an, ob das Taskprotokoll aktiviert ist.|true         
ExecutionLogCacheFolder|Der Ordner, in dem das Paketausführungsprotokoll zwischengespeichert wird. Es wird der Ordnerpfad „ \<Treiber\>:\Benutzer\\*[Konto]*\AppData\Local\SSIS\Cluster\Agent\ELogCache“ verwendet, wenn der Wert leer ist. [Konto] ist das Konto, unter dem der Dienst für Worker für horizontales Hochskalieren ausgeführt wird. Standardmäßig ist dies das Konto SSISScaleOutWorker140.|Empty         
ExecutionLogMaxBufferLogCount|Die maximale Anzahl von Ausführungsprotokollen, die in einem Ausführungsprotokollpuffer im Arbeitsspeicher zwischengespeichert werden|10000        
ExecutionLogMaxInMemoryBufferCount|Die maximale Anzahl von Ausführungsprotokollpuffern im Arbeitsspeicher für Ausführungsprotokolle|10         
ExecutionLogRetryCount|Die Anzahl von Wiederholungsversuchen, wenn bei der Ausführungsprotokollierung ein Fehler auftritt|3
ExecutionLogRetryTimeout|Die Anzahl von Wiederholungsversuchen, wenn bei der Ausführungsprotokollierung ein Fehler auftritt. ExecutionLogRetryCount wird ignoriert, wenn ExecutionLogRetryTimeout erreicht wird.|7.00:00:00 (7 Tage)        
AgentId|Worker-Agent-ID für den Worker für horizontales Hochskalieren|Wird automatisch generiert        

## <a name="view-scale-out-worker-log"></a>Anzeigen des Protokolls für Worker für horizontales Hochskalieren
Die Protokolldatei des Scale Out-Workerdiensts befindet sich unter dem Ordnerpfad „\<Laufwerk\>:\Benutzer\\*[Konto]*\AppData\Local\SSIS\Cluster\Agent“.

Der Protokollspeicherort jedes einzelnen Tasks ist in der Datei „WorkerSettings.config“ durch „TasksRootFolder“ konfiguriert. Ist kein Speicherort angegeben, befindet sich das Protokoll unter dem Ordnerpfad „\<Laufwerk\>:\Benutzer\\*[Konto]*\AppData\Local\SSIS\Cluster\Tasks“. 

Das *[Konto]* ist das Konto, unter dem der Scale Out-Workerdienst ausgeführt wird. Standardmäßig ist dies das Konto SSISScaleOutWorker140.
