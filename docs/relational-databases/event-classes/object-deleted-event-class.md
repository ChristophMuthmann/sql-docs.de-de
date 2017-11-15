---
title: Object:Deleted-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Object:Deleted event class
ms.assetid: d4db32bc-972d-4429-809a-a62047c33e79
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c43e82f21e7b29d84ad7b758992b47e38af98ecf
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="objectdeleted-event-class"></a>Object:Deleted-Ereignisklasse
  Die Object:Deleted-Ereignisklasse zeigt an, dass ein Objekt gelöscht wurde. Beispielsweise mit den Anweisungen DROP INDEX oder DROP TABLE. Mit dieser Ereignisklasse kann ermittelt werden, ob Objekte gelöscht werden, die häufig temporäre gespeicherte Prozeduren erstellen, z. B. durch ODBC-Anwendungen.  
  
 Durch Überwachen der Standarddatenspalten LoginName und NTUserName zusätzlich zu den Objects-Ereignisklassen können Sie den Namen des Benutzers ermitteln, der die Objekte erstellt, löscht oder darauf zugreift.  
  
## <a name="objectdeleted-event-class-data-columns"></a>Datenspalten der Object:Deleted-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DatabaseName|**nvarchar**|Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|ja|  
|EventClass|**int**|Ereignistyp = 47.|27|Nein|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|Nein|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 0 = Begin<br /><br /> 1 = Commit<br /><br /> 2 = Rollback|21|ja|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|IndexID|**int**|ID für den Index des Objekts, das von dem Ereignis betroffen ist. Um die Index-ID für ein Objekt zu ermitteln, verwenden Sie die index_id-Spalte der Katalogsicht sys.indexes.|24|ja|  
|IntegerData|**int**|Wert für eine ganze Zahl, der von der in der Ablaufverfolgung erfassten Ereignisklasse abhängt.|25|Ja|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|LoginName|**nvarchar**|Der Anmeldename des Benutzers ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsanmeldung oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|LoginSid|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|NTDomainName|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|NTUserName|**nvarchar**|Windows-Benutzername.|6|ja|  
|ObjectID|**int**|Vom System zugewiesene ID des Objekts.|22|ja|  
|ObjectID2|**bigint**|Die ID des verbundenen Objekts oder der verbundenen Entität.|56|ja|  
|ObjectName|**nvarchar**|Name des Objekts, auf das verwiesen wird|34|Ja|  
|ObjectType|**int**|Der Wert, der den Typ des am Ereignis beteiligten Objekts darstellt. Dieser Wert entspricht der type-Spalte in sys.objects. Weitere Werte finden Sie unter [ObjectType (Spalte für Ablaufverfolgungsereignisse)](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|Ja|  
|RequestID|**int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|ServerName|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|Nein|  
|SessionLoginName|**nvarchar**|Anmeldename des Benutzers, der die Sitzung geöffnet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|Ja|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
|XactSequence|**bigint**|Token zur Beschreibung der aktuellen Transaktion.|50|ja|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
