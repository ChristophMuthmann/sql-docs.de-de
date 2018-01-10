---
title: SSIS Scale Out-Master (SQL Server Integration Services) | Microsoft-Dokumentation
ms.description: This article describes the Scale Out Master component of SSIS Scale Out
ms.custom: 
ms.date: 12/19/2017
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
ms.openlocfilehash: 2a2405606b0ce974c4067e8f7aa53fe9e9c841bf
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="integration-services-ssis-scale-out-master"></a>Master für horizontales Hochskalieren von Integration Services (SSIS)
Der Scale Out-Master verwaltet das Scale Out-System über den SSISDB-Katalog und den Scale Out-Masterdienst. 

Im SSISDB-Katalog werden alle Informationen für Scale Out-Worker, Pakete und Ausführungen gespeichert. Der Katalog stellt die Schnittstelle bereit, um einen Worker für horizontales Hochskalieren zu aktivieren und Pakete in horizontaler Hochskalierung auszuführen. Weitere Informationen finden Sie unter [Exemplarische Vorgehensweise: Einrichten von Integration Services-Scale Out](walkthrough-set-up-integration-services-scale-out.md) und [Ausführen von Paketen in SSIS Scale Out (SQL Server Integration Services)](run-packages-in-integration-services-ssis-scale-out.md).

Der Scale Out-Masterdienst ist ein Windows-Dienst, über den die Kommunikation mit Scale Out-Workern erfolgt. Der Dienst gibt über HTTPS den Status von Paketausführungen mit Scale Out-Workern zurück und verarbeitet die Daten in SSISDB. 

## <a name="scale-out-views-and-stored-procedures-in-ssisdb"></a>Scale Out-Ansichten und gespeicherte Prozeduren in SSISDB

### <a name="views"></a>Views:
-   [[catalog].[master_properties(../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)
-   [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md).

####<a name="stored-procedures"></a>Gespeicherte Prozeduren:

-   Zum Verwalten von Scale Out-Workern:  
    -   [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)
    -   [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)

- Zum Ausführen von Paketen in Scale Out:   
    -   [[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)
    -   [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)
    -   [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   

## <a name="configure-the-scale-out-master-service"></a>Konfigurieren des Scale Out-Masterdiensts
Konfigurieren Sie den Scale Out-Masterdienst mithilfe der `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`-Datei. Der Dienst muss nach dem Aktualisieren der Konfigurationsdatei neu gestartet werden.


Konfiguration  |Description  |Standardwert  
---------|---------|---------
PortNumber|Die Netzwerkportnummer, die zur Kommunikation mit einem Worker für horizontales Hochskalieren verwendet wird|8391         
SSLCertThumbprint|Der Fingerabdruck des SSL-Zertifikats verwendet, mit dem die Kommunikation mit einem Worker für horizontales Hochskalieren geschützt wird|Der Fingerabdruck des SSL-Zertifikats, das bei der Installation von Worker für horizontales Hochskalieren angegeben wurde         
SqlServerName|Der Name der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz, die den SSISDB-Katalog enthält. Z.B.: Servername\\\\Instanzname.|Der Name der SQL Server-Instanz, mit dem der Scale Out-Master installiert wurde         
CleanupCompletedJobsIntervalInMs|Die Zeitspanne für das Bereinigen von abgeschlossenen Ausführungsaufträgen (in Millisekunden)|43200000         
DealWithExpiredTasksIntervalInMs|Die Zeitspanne für das Verarbeiten von abgelaufenen Ausführungsaufträgen (in Millisekunden)|300000
MasterHeartbeatIntervalInMs|Das Intervall für den Takt von Master für horizontales Hochskalieren (in Millisekunden) Diese Eigenschaft gibt das Intervall an, in dem der Scale Out-Master seinen Onlinestatus im SSISDB-Katalog aktualisiert.|30000
SqlConnectionTimeoutInSecs|Das SQL-Verbindungstimeout in Sekunden, wenn eine Verbindung mit SSISDB hergestellt wird|15    
||||    

## <a name="view-the-scale-out-master-service-log"></a>Anzeigen des Protokolls des Scale Out-Masterdiensts
Die Protokolldatei für den Scale Out-Masterdienst befindet sich im Ordner `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Master`. 

Der Parameter *[Konto]* bezieht sich auf das Konto, unter dem der Scale Out-Masterdienst ausgeführt wird. Standardmäßig lautet das Konto `SSISScaleOutMaster140`.

## <a name="next-steps"></a>Nächste Schritte
[Scale Out-Worker von Integration Services (SSIS)](integration-services-ssis-scale-out-worker.md)
