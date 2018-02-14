---
title: Showplan All for Query Compile-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Showplan All for Query Compile event class
ms.assetid: bb1dc446-5e6c-43d6-9db8-78c76cc2e01f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72cff9b0f6567430b31b7ac70523d3b50f55f4ab
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="showplan-all-for-query-compile-event-class"></a>Showplan All for Query Compile-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Showplan All for Query Compile-Ereignisklasse tritt auf, wenn [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine SQL-Anweisung kompiliert. Schließen Sie diese Ereignisklasse ein, um die Showplan-Operatoren zu identifizieren. Die enthaltenen Informationen sind eine Teilmenge der in der Showplan XML For Query Compile-Ereignisklasse verfügbaren Informationen.  
  
 Die Showplan All for Query Compile-Ereignisklasse zeigt vollständige Kompilierungszeitdaten an. Bei Ablaufverfolgungen, die „Showplan All for Query Compile“ enthalten, kann ein erheblicher Verwaltungsaufwand anfallen. Um dieses Problem zu minimieren, beschränken Sie die Verwendung dieser Ereignisklasse auf Ablaufverfolgungen, die bestimmte Probleme nur für einen kurzen Zeitraum überwachen.  
  
 Wenn die Showplan All for Query Compile-Ereignisklasse in eine Ablaufverfolgung eingeschlossen ist, muss die BinaryData-Datenspalte ausgewählt sein. Ist dies nicht der Fall, werden Informationen zu dieser Ereignisklasse nicht in der Ablaufverfolgung angezeigt.  
  
## <a name="showplan-all-for-query-compile-event-class-data-columns"></a>Datenspalten der Showplan All for Query Compile-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|BinaryData|**image**|Die geschätzten Kosten der Abfrage.|2|nein|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DatabaseName|**nvarchar**|Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|ja|  
|EventClass|**int**|Ereignistyp = 169.|27|nein|  
|EventSequence|**int**|Die Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|IntegerData|**int**|Geschätzte Anzahl der zurückgegebenen Zeilen.|25|ja|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|LineNumber|**int**|Zeigt die Nummer der Zeile an, die den Fehler enthält|5|ja|  
|LoginName|**nvarchar**|Anmeldename des Benutzers (Anmeldung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheit oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|LoginSID|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|nein|  
|NestLevel|**int**|Ganze Zahl, die die von @@NESTLEVEL zurückgegebenen Daten darstellt.|29|ja|  
|NTDomainName|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|NTUserName|**nvarchar**|Windows-Benutzername.|6|ja|  
|ObjectID|**int**|Vom System zugewiesene ID des Objekts.|22|ja|  
|ObjectName|**nvarchar**|Name des Objekts, auf das verwiesen wird|34|ja|  
|ObjectType|**int**|Der Wert, der den Typ des am Ereignis beteiligten Objekts darstellt. Dieser Wert entspricht der type-Spalte in sys.objects. Weitere Werte finden Sie unter [ObjectType (Spalte für Ablaufverfolgungsereignisse)](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|ja|  
|RequestID|**int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|ServerName|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|SPID|**int**|Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist|12|ja|  
|StartTime|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar).|14|ja|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
|XactSequence|**bigint**|Token zur Beschreibung der aktuellen Transaktion.|50|ja|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Referenz zu logischen und physischen Showplanoperatoren](../../relational-databases/showplan-logical-and-physical-operators-reference.md)  
  
  
