---
title: SQL Serverintegration Services (SSIS) Dezentrales Skalieren Master | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1672c015186998065b5d6dc95897147aa11d14ec
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out-master"></a>Master für horizontales Hochskalieren von Integration Services (SSIS)
Master für horizontales Hochskalieren verwaltet das System für horizontale Hochskalierung über den SSISDB-Katalog und den Dienst für Master für horizontales Hochskalieren. 

Im SSISDB-Katalog werden alle Informationen für Worker für horizontales Hochskalieren, Pakete und Ausführungen gespeichert. Der Katalog stellt die Schnittstelle bereit, um einen Worker für horizontales Hochskalieren zu aktivieren und Pakete in horizontaler Hochskalierung auszuführen. Weitere Informationen finden Sie unter [Exemplarische Vorgehensweise: Einrichten von horizontaler Hochskalierung für Integration Services](walkthrough-set-up-integration-services-scale-out.md), [Ausführen von Paketen in horizontaler Hochskalierung für Integration Services (SSIS)](run-packages-in-integration-services-ssis-scale-out.md).

Der Dienst für Master für horizontales Hochskalieren ist ein Windows-Dienst, über den die Kommunikation mit Workern für horizontales Hochskalieren erfolgt. Der Dienst tauscht über HTTPS den Status von Paketausführungen mit Workern für horizontales Hochskalieren aus und verarbeitet die Daten in SSISDB. 

## <a name="scale-out-related-sql-views-and-stored-procedures-in-ssisdb"></a>Horizontales Skalieren verknüpfte SQL-Ansichten und gespeicherten Prozeduren in der SSISDB

#### <a name="views"></a>Views:
[[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md), [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md).

#### <a name="stored-procedures"></a>Gespeicherte Prozeduren:

- Für die Verwaltung von Worker für horizontales Hochskalieren:  
 [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md), [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md).
- Zum Ausführen von Paketen in horizontaler Hochskalierung:   
[[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md), [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).   

## <a name="configure-sql-server-integration-services-scale-out-master-service"></a>Konfigurieren des Master für horizontales Hochskalieren von SQL Server Integration Services-Diensts
Der Dienst für Master für horizontales Hochskalieren kann mit der Datei „ \<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config“ konfiguriert werden. Der Dienst muss neu gestartet werden, nachdem die Konfigurationsdatei aktualisiert wurde.


Konfiguration  |Description  |Standardwert  
---------|---------|---------
PortNumber|Die Netzwerkportnummer, die zur Kommunikation mit einem Worker für horizontales Hochskalieren verwendet wird|8391         
SSLCertThumbprint|Der Fingerabdruck des SSL-Zertifikats verwendet, mit dem die Kommunikation mit einem Worker für horizontales Hochskalieren geschützt wird|Der Fingerabdruck des SSL-Zertifikats, das bei der Installation von Worker für horizontales Hochskalieren angegeben wurde         
SQL Server-Name|Der Name des der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , die den SSISDB-Katalog enthält. Beispiel: ServerName\\\\InstanceName.|Der Name des SQL-Servers, der mit dem Scale-Out-Master installiert ist.         
CleanupCompletedJobsIntervalInMs|Die Zeitspanne für das Bereinigen von abgeschlossenen Ausführungsaufträgen (in Millisekunden)|43200000         
DealWithExpiredTasksIntervalInMs|Die Zeitspanne für das Verarbeiten von abgelaufenen Ausführungsaufträgen (in Millisekunden)|300000
MasterHeartbeatIntervalInMs|Das Intervall für den Takt von Master für horizontales Hochskalieren (in Millisekunden) Dieser Wert gibt das Intervall an, in dem der Master für horizontales Hochskalieren seinen Onlinestatus im SSISDB-Katalog aktualisiert.|30000
SqlConnectionTimeoutInSecs|Das SQL-Verbindungstimeout in Sekunden beim Herstellen von SSISDB.|15        

## <a name="view-scale-out-master-service-log"></a>Anzeigen des Protokolls des Diensts für Master für horizontales Hochskalieren
Das Scale-Out-Master-Dienstprotokolldatei befindet sich der \<Treiber\>: \Users\\*[Account]*\AppData\Local\SSIS\ScaleOut\Master Ordnerpfad. 

Die *[Account]* bezieht sich auf das Konto, das Scale-Out-Master-Dienst ausgeführt wird. Standardmäßig ist dies das Konto „SSISScaleOutMaster140“.

