---
title: Lock:Escalation-Ereignisklasse | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Escalation event class
- lock escalation [SQL Server], event class
ms.assetid: d253b44c-7600-4afa-a3a7-03cc937c6a4b
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 399af418d43ec95ab6335c7bc76f677525f4db97
ms.sourcegitcommit: beaad940c348ab22d4b4a279ced3137ad30c658a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/20/2018
---
# <a name="lockescalation-event-class"></a>Lock:Escalation-Ereignisklasse
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die **Lock:Escalation** -Ereignisklasse zeigt an, dass eine differenziertere Sperre in eine gröbere Sperre konvertiert wurde (z.B. eine Zeilensperre, die in Objektsperre konvertiert wurde). Die Ausweitungsereignisklasse hat die Ereignis-ID 60.  
  
## <a name="lockescalation-event-class-data-columns"></a>Datenspalten der Lock:Escalation-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|**ClientProcessID**|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Client die Clientprozess-ID angibt.|9|ja|  
|**DatabaseID**|**int**|Die ID der Datenbank, in der die Sperre eingerichtet wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|**DatabaseName**|**nvarchar**|Der Name der Datenbank, in der die Sperrenausweitung auftrat.|35|ja|  
|**EventClass**|**int**|Ereignistyp = 60.|27|nein|  
|**EventSubClass**|**int**|Die Ursache der Sperrenausweitung:<br /><br /> **0 - LOCK_THRESHOLD** zeigt an, dass die Anweisung den Sperrengrenzwert überschritten hat.<br /><br /> **1 - MEMORY_THRESHOLD** zeigt an, dass die Anweisung den Grenzwert für den Arbeitsspeicher überschritten hat.|21|ja|  
|**EventSequence**|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|**GroupID**|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
|**HostName**|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname vom Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|**IntegerData**|**int**|Die Anzahl der Heap- oder B-Struktursperren. Die Anzahl der Sperren für die Heap- oder B-Struktur zum Zeitpunkt der Sperrenausweitung.|25|ja|  
|**IntegerData2**|**int**|Die Anzahl der ausgeweiteten Sperren. Die Gesamtanzahl von konvertierten Sperren. Für diese Sperrenstrukturen wird die Zuweisung aufgehoben, da sie bereits durch die ausgeweitete Sperre abgedeckt sind.|55|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|**LineNumber**|**int**|Die Zeilennummer der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung.|5|ja|  
|**LoginName**|**nvarchar**|Der Anmeldename des Benutzers ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsanmeldung oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|**LoginSid**|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der **sys.server_principals** -Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|**Mode**|**int**|Der Sperrmodus nach der Ausweitung.<br /><br /> 0 = NULL - Kompatibel mit allen anderen Sperrmodi (LCK_M_NL)<br /><br /> 1 = Schemastabilitätssperre (LCK_M_SCH_S)<br /><br /> 2 = Schemaänderungssperre (LCK_M_SCH_M)<br /><br /> 3 = Freigegebene Sperre (LCK_M_S)<br /><br /> 4 = Updatesperre (LCK_M_U)<br /><br /> 5 = Exklusive Sperre (LCK_M_X)<br /><br /> 6 = Beabsichtigte freigegebene Sperre (LCK_M_IS)<br /><br /> 7 = Beabsichtigte Updatesperre (LCK_M_IU)<br /><br /> 8 = Beabsichtigte exklusive Sperre (LCK_M_IX)<br /><br /> 9 = Freigegebene Sperre mit beabsichtigter Updatesperre (LCK_M_SIU)<br /><br /> 10 = Freigegebene Sperre mit beabsichtigter exklusiver Sperre (LCK_M_SIX)<br /><br /> 11 = Updatesperre mit beabsichtigter exklusiver Sperre (LCK_M_UIX)<br /><br /> 12 = Massenupdatesperre (LCK_M_BU)<br /><br /> 13 = Freigegebene Sperren für Schlüsselbereich und Ressource (LCK_M_RS_S)<br /><br /> 14 = Freigegebene Sperre für Schlüsselbereich und Updatesperre für Ressource (LCK_M_RS_U)<br /><br /> 15 = Einfügungssperre für Schlüsselbereich und NULL-Sperre für Ressource (LCK_M_RI_NL)<br /><br /> 16 = Einfügungssperre für Schlüsselbereich und freigegebene Ressourcensperre (LCK_M_RI_S)<br /><br /> 17 = Einfügungssperre für Schlüsselbereich und Updatesperre (LCK_M_RI_U)<br /><br /> 18 = Einfügungssperre für Schlüsselbereich und exklusive Ressourcensperre (LCK_M_RI_X)<br /><br /> 19 = Exklusive Sperren für Schlüsselbereich und freigegebene Ressource (LCK_M_RX_S)<br /><br /> 20 = Exklusive Sperren für Schlüsselbereich und Update (LCK_M_RX_U)<br /><br /> 21 = Exklusive Sperren für Schlüsselbereich und Ressource (LCK_M_RX_X)|32|ja|  
|**NTDomainName**|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|**NTUserName**|**nvarchar**|Windows-Benutzername.|6|ja|  
|**ObjectID**|**int**|Die vom System zugewiesene ID der Tabelle, für die die Sperrenausweitung ausgelöst wurde.|22|ja|  
|**ObjectID2**|**bigint**|Die ID des verbundenen Objekts oder der verbundenen Entität. (Die Heap- oder B-Struktur-ID, für die die Sperrenausweitung ausgelöst wurde.)|56|ja|  
|**Offset**|**int**|Der Startoffset der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung.|61|ja|  
|**OwnerID**|**int**|1 = TRANSACTION<br /><br /> 2 = CURSOR<br /><br /> 3 = SESSION<br /><br /> 4 = SHARED_TRANSACTION_WORKSPACE<br /><br /> 5 = EXCLUSIVE_TRANSACTION_WORKSPACE<br /><br /> 6 = WAITFOR_QUERY|58|ja|  
|**RequestID**|**int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|**ServerName**|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|**SessionLoginName**|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie z. B. mit Login1 eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und mit Login2 eine Anweisung ausführen, zeigt **SessionLoginName** Login1 an, und **LoginName** zeigt Login2 an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|**SPID**|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|**StartTime**|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|**TextData**|**ntext**|Der Text der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung, die die Sperrenausweitung ausgelöst hat.|1|ja|  
|**TransactionID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
|**Typ**|**int**|Granularität der Sperrenausweitung:<br /><br /> 1 = NULL_RESOURCE<br /><br /> 2 = DATABASE<br /><br /> 3 = FILE<br /><br /> 5 = OBJECT (Tabellenebene)<br /><br /> 6 = PAGE<br /><br /> 7 = KEY<br /><br /> 8 = EXTENT<br /><br /> 9 = RID<br /><br /> 10 = APPLICATION<br /><br /> 11 = METADATA<br /><br /> 12 = HOBT<br /><br /> 13 = ALLOCATION_UNIT|57|ja|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird mit der `sp_trace_create` -Prozedur eine Ablaufverfolgung erstellt, mit `sp_trace_setevent` werden der Ablaufverfolgung Spalten für die Sperrenausweitung hinzugefügt, und mit `sp_trace_setstatus` wird die Ablaufverfolgung gestartet. In Anweisungen wie `EXEC sp_trace_setevent @TraceID, 60, 22, 1`zeigt die Zahl `60` die Ausweitungsereignisklasse und die Zahl `22` die **ObjectID** -Spalte an. Durch `1` wird das Ablaufverfolgungsereignis auf ON festgelegt.  
  
```  
DECLARE @RC int, @TraceID int;  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\TraceResults';  
-- Set the events and data columns you need to capture.  
EXEC sp_trace_setevent @TraceID, 60,  1, 1; --  1 = TextData  
EXEC sp_trace_setevent @TraceID, 60, 12, 1; -- 12 = SPID  
EXEC sp_trace_setevent @TraceID, 60, 21, 1; -- 21 = EventSubClass  
EXEC sp_trace_setevent @TraceID, 60, 22, 1; -- 22 = ObjectID  
EXEC sp_trace_setevent @TraceID, 60, 25, 1; -- 25 = IntegerData  
EXEC sp_trace_setevent @TraceID, 60, 55, 1; -- 25 = IntegerData2  
EXEC sp_trace_setevent @TraceID, 60, 57, 1; -- 57 = Type  
-- Set any filter  byusing sp_trace_setfilter.  
-- Start the trace.  
EXEC sp_trace_setstatus @TraceID, 1;  
GO  
```  
  
 Sobald die Ablaufverfolgung läuft, können Sie die zu verfolgenden Anweisungen ausführen. Nach Abschluss der Anweisungen führen Sie den folgenden Code aus, um die Ablaufverfolgung zu beenden und zu schließen. In diesem Beispiel wird mit der `fn_trace_getinfo` -Funktion die in den `traceid` -Anweisungen zu verwendende `sp_trace_setstatus` abgerufen.  
  
```  
-- After the trace is complete.  
DECLARE @TraceID int;  
-- Find the traceid of the current trace.  
SELECT @TraceID = traceid   
FROM ::fn_trace_getinfo(default)   
WHERE value = N'C:\TraceResults.trc';  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0;  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
