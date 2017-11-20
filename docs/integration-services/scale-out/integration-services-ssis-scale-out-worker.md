---
title: SQL Serverintegration Services (SSIS) Dezentrales Skalieren Worker | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 77cf90268938bada458aa159a5f18f885491b407
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out-worker"></a>Worker für horizontales Hochskalieren von Integration Services (SSIS)

Scale-Out-Worker ausgeführt werden wird eine [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] Scale-Out-Worker-Dienst zur Ausführung von Pull aus Scale-Out-Master Aufgaben und führt die Pakete mit ISServerExec.exe lokal.

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>Konfigurieren des Worker für horizontales Hochskalieren von SQL Server Integration Services-Diensts
Der Worker für horizontales Hochskalieren-Dienst kann mit der Datei „ \<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config“ konfiguriert werden. Der Dienst muss neu gestartet werden, nachdem die Konfigurationsdatei aktualisiert wurde.

Konfiguration  |Description  |Standardwert  
---------|---------|---------
DisplayName|Der Anzeigename des Workers für horizontales Hochskalieren. **NICHT in Gebrauch in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017.**|Computername         
Description|Die Beschreibung des Workers für horizontales Hochskalieren. **NICHT in Gebrauch in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017.**|Empty         
MasterEndpoint|Der Endpunkt zum Herstellen einer Verbindung mit Master für horizontales Hochskalieren|Der Endpunkt, der während der Installation des Workers für horizontales Hochskalieren festgelegt wurde         
MasterHttpsCertThumbprint|Der Fingerabdruck des Client-SSL-Zertifikats, mit dem Master für horizontales Hochskalieren authentifiziert wird|Der Fingerabdruck des Clientzertifikats, das bei der Installation von Worker für horizontales Hochskalieren angegeben wurde          
WorkerHttpsCertThumbprint|Der Fingerabdruck des Zertifikats, das für den Master für horizontales Hochskalieren verwendet wird, um den Worker für horizontales Hochskalieren zu authentifizieren|Der Fingerabdruck eines Zertifikats, das bei der Installation von Worker für horizontales Hochskalieren automatisch erstellt und installiert wurde          
StoreLocation|Der Speicherort des Workerzertifikats|LocalMachine       
StoreName|Der Name des Speichers, in dem sich das Workerzertifikat befindet|My         
AgentHeartbeatInterval|Das Zeitintervall für den Takt für Worker für horizontales Hochskalieren|00:01:00         
TaskHeartbeatInterval|Das Zeitintervall für den Status des Berichtstasks für Worker für horizontales Hochskalieren|00:00:10         
HeartbeatErrorTollerance|Nach diesem Zeitraum ab dem letzten erfolgreichen Tasktakt wird der Task beendet, wenn eine Fehlerantwort des Takts empfangen wird.|00:10:00      
TaskRequestMaxCPU|Die Obergrenze bezüglich CPU für Worker für horizontales Hochskalieren, um Tasks anzufordern. **NICHT in Gebrauch in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017.**|70.0         
TaskRequestMinMemory|Die Mindestmenge von Arbeitsspeicher in MB für Worker für horizontales Hochskalieren, um Tasks anzufordern. **NICHT in Gebrauch in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017.**|100.0         
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
ExecutionLogRetryTimeout|Das wiederholungstimeout, wenn die Protokollierung der Ausführung ein Fehler auftritt. ExecutionLogRetryCount wird ignoriert, wenn ExecutionLogRetryTimeout erreicht wird.|7.00:00:00 (7 Tage)        
AgentId|Worker-Agent-ID für den Worker für horizontales Hochskalieren|Wird automatisch generiert        

## <a name="view-scale-out-worker-log"></a>Anzeigen des Protokolls für Worker für horizontales Hochskalieren
Die Protokolldatei des Scale-Out-Worker-Dienst befindet sich in der \<Treiber\>: \Users\\*[Account]*\AppData\Local\SSIS\ScaleOut\Agent Ordnerpfad.

Der Protokollspeicherort jedes einzelnen Tasks ist in der Datei „WorkerSettings.config“ durch „TasksRootFolder“ konfiguriert. Wenn sie nicht angegeben ist, wird das Protokoll der \<Treiber\>: \Users\\*[Account]*\AppData\Local\SSIS\ScaleOut\Tasks Ordnerpfad. 

Die *[Account]* ist das Konto, das Scale-Out-Worker-Dienst ausgeführt wird. Standardmäßig ist dies das Konto SSISScaleOutWorker140.

