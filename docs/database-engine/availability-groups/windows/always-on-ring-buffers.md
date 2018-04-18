---
title: Ringpuffer für Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47bb7a1a-c0a5-473c-a7db-d9f4bf3ee650
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 9adc4927435a8502327d42319f428669b2bc87ca
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="always-on-availability-groups-ring-buffers"></a>Ringpuffer für Always On-Verfügbarkeitsgruppen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Sie können Diagnoseinformationen zu Always On-Verfügbarkeitsgruppen über SQL Server-Ringpuffer oder über die dynamische Verwaltungssicht „sys.dm_os_ring_buffers“ abrufen. Ringpuffer werden während des Starts von SQL Server erstellt und melden Warnungen innerhalb des SQL Server-Systems für die interne Diagnose. Sie werden nicht unterstützt, aber Sie können trotzdem während der Problembehandlung nützliche Informationen daraus ziehen. Diese Ringpuffer bieten eine weitere Möglichkeit zum Erhalt von Diagnosedaten, wenn SQL Server nicht mehr reagiert oder abgestürzt ist.  
  
 Die folgende Transact-SQL-Abfrage (T-SQL) ruft alle Ereignisdaten aus dem Ringpuffer der Verfügbarkeitsgruppen ab.  
  
```sql  
SELECT * FROM sys.dm_os_ring_buffers WHERE ring_buffer_type LIKE '%HADR%'  
```  
  
 Filtern Sie die Daten nach Datum und Ringpuffertyp, um sie übersichtlicher zu machen. Die folgende Abfrage ruft Daten aus dem angegebenen Ringpuffer ab, die am selben Tag erfasst wurden.  
  
```sql  
DECLARE @runtime datetime  
SET @runtime = GETDATE()  
SELECT CONVERT (varchar(30), @runtime, 121) as data_collection_runtime,   
DATEADD (ms, -1 * (inf.ms_ticks - ring.[timestamp]), GETDATE()) AS ring_buffer_record_time,   
ring.[timestamp] AS record_timestamp, inf.ms_ticks AS cur_timestamp, ring.*   
FROM sys.dm_os_ring_buffers ring  
CROSS JOIN sys.dm_os_sys_info inf where ring_buffer_type='<RING_BUFFER_TYPE>'  
```  
  
 Die Spalte „Record“ (Datensatz) in jedem Datensatz enthält Diagnosedaten im XML-Format. Die XML-Daten unterscheiden sich je nach Ringpuffertyp. Weitere Informationen zu Ringpuffertypen finden Sie im Abschnitt zu [Ringpuffertypen von Verfügbarkeitsgruppen](#BKMK_RingBufferTypes) weiter unten in diesem Artikel. Sie müssen Ihre T-SQL-Abfrage so anpassen, dass sie die gewünschten XML-Elemente extrahiert, um die XML-Daten lesbarer zu machen. Die folgende Abfrage ruft beispielsweise alle Ereignisse aus dem Ringpuffer RING_BUFFER_HADRDBMGR_API ab und formatiert die XML-Daten in separaten Spalten.  
  
```sql  
WITH hadr(ts, type, record) AS  
(  
  SELECT timestamp AS ts, ring_buffer_type AS type, CAST(record AS XML) AS record   
  FROM sys.dm_os_ring_buffers WHERE ring_buffer_type = 'RING_BUFFER_HADRDBMGR_API'  
)  
SELECT   
  ts,  
  type,  
  record.value('(./Record/@id)[1]','bigint') AS [Record ID],  
  record.value('(./Record/@time)[1]','bigint') AS [Time],  
  record.value('(./Record/HadrDbMgrAPI/dbId)[1]', 'bigint') AS [DBID],  
  record.value('(/Record/HadrDbMgrAPI/API)[1]', 'varchar(50)') AS [API],  
  record.value('(/Record/HadrDbMgrAPI/Action)[1]', 'varchar(50)') AS [Action],  
  record.value('(/Record/HadrDbMgrAPI/role)[1]', 'int') AS [Role],  
  record.value('(/Record/Stack)[1]', 'varchar(100)') AS [Call Stack]  
FROM hadr  
ORDER BY record.value('(./Record/@time)[1]','bigint') DESC  
GO  
```  
  
##  <a name="BKMK_RingBufferTypes"></a> Ringpuffertypen von Verfügbarkeitsgruppen  
 Es gibt in „sys.dm_os_ring_buffers“ vier verschiedene Ringpuffer von Verfügbarkeitsgruppen. Unten werden die Ringpuffertypen beschrieben, und sie sehen einen Beispielausschnitt des Inhalts der Spalte „Record“ für jeden Ringpuffertypen.  
  
 **RING_BUFFER_HADRDBMGR_API**  
  
 Erfasst Statusübergänge, die aufgetreten sind oder gerade auftreten. Wenn Sie sich die Statusübergänge ansehen, achten Sie besonders auf die objectType-Werte.  
  
```xml  
<Record id="11" type="RING_BUFFER_HADRDBMGR_STATE" time="860243">  
  <HadrDbMgrState>  
    <objectType>HadrUsers</objectType>  
    <currentState>HDbMState_Starting</currentState>  
    <proposedState>HDbMState_Started</proposedState>  
    <targetState>HDbMState_Started</targetState>  
    <legalTransition>Y</legalTransition>  
    <role>1</role>  
  </HadrDbMgrState>  
</Record>  
```  
  
 **RING_BUFFER_HADRDBMGR_STATE**  
  
 Erfasst interne Methoden- oder Funktionsaufrufe, die von Always On-Aktivitäten verursacht wurden. Er kann Informationen zum Anhalten, Wiederaufnehmen oder Ändern von Rollen anzeigen, darunter auch Einstiegs- und Ausgangspunkte.  
  
```xml  
<Record id="45" type="RING_BUFFER_HADRDBMGR_STATE" time="1723487912">  
  <HadrDbMgrState>  
    <dbId>5</dbId>  
    <objectType>HadrDbMgr</objectType>  
    <currentState>HDbMState_Starting</currentState>  
    <proposedState>HDbMState_Started</proposedState>  
    <targetState>HDbMState_Started</targetState>  
    <legalTransition>Y</legalTransition>  
    <role>2</role>  
  </HadrDbMgrState>  
</Record>  
```  
  
 **RING_BUFFER_HADRDBMGR_COMMIT**  
  
```xml  
<Record id="0" type="RING_BUFFER_HADRDBMGR_COMMIT" time="1723475368">  
  <HadrDbMgrCommitPolicy>  
    <dbId>5</dbId>  
    <replicaId>883a18f5-97d5-450f-8f8f-9983a4fa5299</replicaId>  
    <dbHardenPolicy>KillAll</dbHardenPolicy>  
    <dbSyncConfig>0x0</dbSyncConfig>  
    <syncPartnerCount>0</syncPartnerCount>  
    <minSyncPartnerConfig>0</minSyncPartnerConfig>  
    <partnerHardenPolicy>KillAll</partnerHardenPolicy>  
    <partnerSyncConfig>0x0</partnerSyncConfig>  
    <logBlock>0x0000000000000000</logBlock>  
    <leaseExpired>Y</leaseExpired>  
    <partnerChange>N</partnerChange>  
    <role>2</role>  
  </HadrDbMgrCommitPolicy>  
</Record>  
```  
  
 **RING_BUFFER_HADR_TRANSPORT_STATE**  
  
```xml  
<Record id="3" type="RING_BUFFER_HADR_TRANSPORT_STATE" time="1723485399">  
  <HadrTransportState>  
    <agId>08264B79-D10B-412F-B38D-CA07B08E9BD8</agId>  
    <localArId>883A18F5-97D5-450F-8F8F-9983A4FA5299</localArId>  
    <targetArId>628D6349-72DD-4D18-A6E1-1272645660BA</targetArId>  
    <currentState>HadrSession_Configuring</currentState>  
    <targetState>HadrSession_Connected</targetState>  
    <legalTransition>Y</legalTransition>  
  </HadrTransportState>  
</Record>  
```  
  
## <a name="parse-xml-data-from-a-ring-buffer"></a>Analysieren von XML-Daten aus einem Ringpuffer  
 Sie können das Feld „Record“ aus dem Ringpuffer analysieren, den Sie untersuchen, indem Sie [value&#40;&#41; Method &#40;xml Data Type&#41;](~/t-sql/xml/value-method-xml-data-type.md) in Ihrer Abfrage verwenden. Dazu müssen Sie zunächst die Spalte „Record“ im Ringpuffer in XML [umwandeln](~/t-sql/functions/cast-and-convert-transact-sql.md) (verwenden Sie dazu CAST). Die Abfrage unten veranschaulicht, wie Sie RING_BUFFER_HADRDBMGR_API mit dieser Methode in ein lesbares Format umwandeln.  
  
```sql 
WITH hadr(ts, type, record) AS  
   (SELECT timestamp AS ts, ring_buffer_type AS type, CAST(record AS XML) AS record   
FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_HADRDBMGR_API')  
SELECT ts,  
type,  
record.value('(./Record/@id)[1]','bigint') AS [Record id],  
record.value('(./Record/@time)[1]','bigint') AS [Time],  
record.value('(./Record/HadrDbMgrAPI/dbId)[1]', 'bigint') AS [dbid],  
record.value('(/Record/HadrDbMgrAPI/API)[1]', 'varchar(50)') AS [API],  
record.value('(/Record/HadrDbMgrAPI/Action)[1]', 'varchar(50)') AS [Action],  
record.value('(/Record/HadrDbMgrAPI/role)[1]', 'int') AS [Role],  
record.value('(/Record/Stack)[1]', 'varchar(100)') AS [Call Stack]  
FROM hadr  
ORDER BY record.value('(./Record/@time)[1]','bigint') DESC  
GO  
```  
  
  