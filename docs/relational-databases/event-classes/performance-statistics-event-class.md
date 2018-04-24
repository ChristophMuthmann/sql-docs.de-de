---
title: Performance Statistics-Ereignisklasse | Microsoft-Dokumentation
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
- Performance Statistics event class
ms.assetid: da9cd2c4-6fdd-4ada-b74f-105e3541393c
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 02db411f94695499fa0fdc3ad061ff8e0e5effe4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="performance-statistics-event-class"></a>Performance Statistics-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Die Performance Statistics-Ereignisklasse kann zur Leistungsüberwachung der ausgeführten Abfragen, gespeicherten Prozeduren und Trigger verwendet werden. Jede der sechs Ereignisunterklassen zeigt ein Ereignis für die Lebensdauer von Abfragen, gespeicherten Prozeduren und Triggern innerhalb des Systems an. Mithilfe einer Kombination aus diesen Ereignisunterklassen und den zugehörigen dynamischen Verwaltungssichten sys.dm_exec_query_stats, sys.dm_exec_procedure_stats und sys.dm_exec_trigger_stats können Sie den Leistungsverlauf einer bestimmten Abfrage, gespeicherten Prozedur oder eines Triggers nachvollziehen.  
  
## <a name="performance-statistics-event-class-data-columns"></a>Datenspalten der Performance Statistics-Ereignisklasse  
 In den folgenden Tabellen werden die Ereignisklassen-Datenspalten beschrieben, die jeweils den folgenden Ereignisunterklassen zugeordnet sind: EventSubClass 0, EventSubClass 1, EventSubClass 2, EventSubClass 3, EventSubClass 4 und EventSubClass 5.  
  
### <a name="eventsubclass-0"></a>EventSubClass 0  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|ja|  
|BinaryData|**image**|NULL|2|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 0 = Neuer SQL-Text des Batches, der zurzeit nicht im Cache vorhanden ist.<br /><br /> Die folgenden EventSubClass-Typen werden in der Ablaufverfolgung für Ad-hoc-Batches generiert.<br /><br /> Für Ad-hoc-Batches mit *n* Abfragen:<br /><br /> 1 vom Typ 0|21|ja|  
|IntegerData2|**int**|NULL|55|ja|  
|ObjectID|**int**|NULL|22|ja|  
|Offset|**int**|NULL|61|ja|  
|PlanHandle|**Image**|NULL|65|ja|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|SqlHandle|**image**|SQL-Handle, das zum Abrufen des SQL-Texts des Batchs mithilfe der dynamischen Verwaltungssicht sys.dm_exec_sql_text verwendet werden kann.|63|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**ntext**|SQL-Text des Batches.|1|ja|  
  
### <a name="eventsubclass-1"></a>EventSubClass 1  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|Die Gesamtanzahl der Neukompilierungen dieses Plans.|52|ja|  
|BinaryData|**image**|Binary XML des kompilierten Plans.|2|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 1 = Abfragen innerhalb einer gespeicherten Prozedur wurden kompiliert.<br /><br /> Die folgenden EventSubClass-Typen werden in der Ablaufverfolgung für gespeicherte Prozeduren generiert.<br /><br /> Für gespeicherte Prozeduren mit *n* Abfragen:<br /><br /> *n* vom Typ 1|21|ja|  
|IntegerData2|**int**|Ende der Anweisung in der gespeicherten Prozedur.<br /><br /> -1 für das Ende der gespeicherten Prozedur.|55|ja|  
|ObjectID|**int**|Vom System zugewiesene ID des Objekts.|22|ja|  
|Offset|**int**|Der Startoffset der Anweisung in der gespeicherten Prozedur oder im Batch.|61|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|SqlHandle|**image**|SQL-Handle, das zum Abrufen des SQL-Texts der gespeicherten Prozedur mithilfe der dynamischen Verwaltungssicht dm_exec_sql_text verwendet werden kann.|63|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**ntext**|NULL|1|ja|  
|PlanHandle|**image**|Das Planhandle des kompilierten Plans für die gespeicherte Prozedur. Hiermit kann der XML-Plan abgerufen werden, indem die dynamische Verwaltungssicht sys.dm_exec_query_plan verwendet wird.|65|ja|  
|ObjectType|**int**|Ein Wert, der den Typ des am Ereignis beteiligten Objekts darstellt.<br /><br /> 8272 = gespeicherte Prozedur|28|ja|  
|BigintData2|**bigint**|Für die Kompilierung verwendeter Arbeitsspeicher insgesamt (in KB).|53|ja|  
|CPU|**int**|Die CPU-Gesamtzeit in Millisekunden, die für die Kompilierung erforderlich war.|18|ja|  
|Duration|**int**|Gesamtzeit für die Kompilierung in Mikrosekunden.|13|ja|  
|IntegerData|**int**|Die Größe des kompilierten Plans (in KB).|25|ja|  
  
### <a name="eventsubclass-2"></a>EventSubClass 2  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|Die Gesamtanzahl der Neukompilierungen dieses Plans.|52|ja|  
|BinaryData|**image**|Binary XML des kompilierten Plans.|2|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 2 = Abfragen innerhalb einer Ad-hoc-SQL-Anweisung wurden kompiliert.<br /><br /> Die folgenden EventSubClass-Typen werden in der Ablaufverfolgung für Ad-hoc-Batches generiert.<br /><br /> Für Ad-hoc-Batches mit *n* Abfragen:<br /><br /> *n* vom Typ 2|21|ja|  
|IntegerData2|**int**|Ende der Anweisung im Batch.<br /><br /> -1 für das Ende des Batches.|55|ja|  
|ObjectID|**int**|–|22|ja|  
|Offset|**int**|Startoffset der Anweisung im Batch.<br /><br /> 0 für den Anfang des Batches.|61|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|SqlHandle|**image**|SQL-Handle Hiermit kann der SQL-Text des Batchs abgerufen werden, indem die dynamische Verwaltungssicht dm_exec_sql_text verwendet wird.|63|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**ntext**|NULL|1|ja|  
|PlanHandle|**image**|Das Planhandle des kompilierten Plans für den Batch. Hiermit kann der Batch-XML-Plan abgerufen werden, indem die dynamische Verwaltungssicht dm_exec_query_plan verwendet wird.|65|ja|  
|BigintData2|**bigint**|Für die Kompilierung verwendeter Arbeitsspeicher insgesamt (in KB).|53|ja|  
|CPU|**int**|Die CPU-Gesamtzeit in Mikrosekunden, die für die Kompilierung erforderlich war.|18|ja|  
|Duration|**int**|Gesamtzeit für die Kompilierung in Millisekunden.|13|ja|  
|IntegerData|**int**|Die Größe des kompilierten Plans (in KB).|25|ja|  
  
### <a name="eventsubclass-3"></a>EventSubClass 3  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|Die Gesamtanzahl der Neukompilierungen dieses Plans.|52|ja|  
|BinaryData|**image**|NULL|2|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 3 = Eine zwischengespeicherte Abfrage wurde gelöscht, und die Leistungsverlaufsdaten dieses Plans werden nun gelöscht.<br /><br /> Die folgenden EventSubClass-Typen werden in der Ablaufverfolgung generiert.<br /><br /> Für Ad-hoc-Batches mit *n* Abfragen:<br /><br /> 1 vom Typ 3, wenn die Abfrage aus dem Cache geleert wird<br /><br /> Für gespeicherte Prozeduren mit *n* Abfragen:<br /><br /> 1 vom Typ 3, wenn die Abfrage aus dem Cache geleert wird.|21|ja|  
|IntegerData2|**int**|Ende der Anweisung in der gespeicherten Prozedur oder dem Batch.<br /><br /> -1 für das Ende der gespeicherten Prozedur oder des Batches.|55|ja|  
|ObjectID|**int**|NULL|22|ja|  
|Offset|**int**|Der Startoffset der Anweisung in der gespeicherten Prozedur oder im Batch.<br /><br /> 0 für den Anfang der gespeicherten Prozedur oder des Batches.|61|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|SqlHandle|**image**|SQL-Handle, das zum Abrufen des SQL-Texts der gespeicherten Prozedur oder des Batchs mithilfe der dynamischen Verwaltungssicht dm_exec_sql_text verwendet werden kann.|63|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**ntext**|QueryExecutionStats|1|ja|  
|PlanHandle|**image**|Das Planhandle des kompilierten Plans für die gespeicherte Prozedur oder den Batch. Hiermit kann der XML-Plan abgerufen werden, indem die dynamische Verwaltungssicht dm_exec_query_plan verwendet wird.|65|ja|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
  
### <a name="eventsubclass-4"></a>EventSubClass 4  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|ja|  
|BinaryData|**image**|NULL|2|ja|  
|DatabaseID|**int**|ID der Datenbank, in der sich die angegebene gespeicherte Prozedur befindet.|3|ja|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 4 = Eine zwischengespeicherte gespeicherte Prozedur wurde aus dem Cache gelöscht, und die verknüpften Leistungsverlaufsdaten werden nun gelöscht.|21|ja|  
|IntegerData2|**int**|NULL|55|ja|  
|ObjectID|**int**|ID der gespeicherten Prozedur. Entspricht der object_id-Spalte in sys.procedures.|22|ja|  
|Offset|**int**|NULL|61|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|SqlHandle|**image**|SQL-Handle, das zum Abrufen des SQL-Texts der ausgeführten gespeicherten Prozedur mithilfe der dynamischen Verwaltungssicht dm_exec_sql_text verwendet werden kann.|63|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**ntext**|ProcedureExecutionStats|1|ja|  
|PlanHandle|**image**|Das Planhandle des kompilierten Plans für die gespeicherte Prozedur. Hiermit kann der XML-Plan abgerufen werden, indem die dynamische Verwaltungssicht dm_exec_query_plan verwendet wird.|65|ja|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
  
### <a name="eventsubclass-5"></a>EventSubClass 5  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|ja|  
|BinaryData|**image**|NULL|2|ja|  
|DatabaseID|**int**|ID der Datenbank, in der sich der angegebene Trigger befindet.|3|ja|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 5 = Ein zwischengespeicherter Trigger wurde aus dem Cache gelöscht, und die verknüpften Leistungsverlaufsdaten werden nun gelöscht.|21|ja|  
|IntegerData2|**int**|NULL|55|ja|  
|ObjectID|**int**|ID des Triggers. Entspricht der object_id-Spalte in den Katalogsichten sys.triggers und sys.server_triggers.|22|ja|  
|Offset|**int**|NULL|61|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|SqlHandle|**image**|SQL-Handle, das zum Abrufen des SQL-Texts des Triggers mithilfe der dynamischen Verwaltungssicht dm_exec_sql_text verwendet werden kann.|63|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**ntext**|TriggerExecutionStats|1|ja|  
|PlanHandle|**image**|Das Planhandle des kompilierten Plans für den Trigger. Hiermit kann der XML-Plan abgerufen werden, indem die dynamische Verwaltungssicht dm_exec_query_plan verwendet wird.|65|ja|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Showplan XML for Query Compile (Ereignisklasse)](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
