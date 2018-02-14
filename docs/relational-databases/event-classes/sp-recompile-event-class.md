---
title: SP:Recompile (Ereignisklasse) | Microsoft-Dokumentation
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
- SP:Recompile event class
ms.assetid: 526c8eae-a07b-4d0e-b91e-8e537835d77d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f56543d46915673c51e1626d669f473416aed01f
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="sprecompile-event-class"></a>SP:Recompile (Ereignisklasse)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die SP:Recompile-Ereignisklasse gibt an, dass eine gespeicherte Prozedur, ein Trigger oder eine benutzerdefinierte Funktion neu kompiliert wurde. Die von dieser Ereignisklasse gemeldeten Neukompilierungen finden auf der Anweisungsebene statt.  
  
 Die SQL:StmtRecompile-Ereignisklasse stellt die bevorzugte Methode für die Ablaufverfolgung von Neukompilierungen auf Anweisungsebene dar. Die SP:Recompile-Ereignisklasse ist als veraltet markiert. Weitere Informationen finden Sie unter [SQL:StmtRecompile Event Class](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md).  
  
## <a name="sprecompile-event-class-data-columns"></a>Datenspalten der SP:Recompile-Ereignisklasse  
  
|Datenspaltenname|**Data type**|Description|Column ID|Filterbar|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Prozess-ID durch den Client bereitgestellt wird.|9|ja|  
|DatabaseID|**int**|ID der Datenbank, in der die gespeicherte Prozedur ausgeführt wird. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DatabaseName|**nvarchar**|Name der Datenbank, in der die gespeicherte Prozedur ausgeführt wird.|35|ja|  
|EventClass|**int**|Ereignistyp = 37.|27|nein|  
|EventSequence|**int**|Die Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse. Gibt den Grund für die Neukompilierung an.<br /><br /> 1 = Schema geändert<br /><br /> 2 = Statistiken geändert<br /><br /> 3 = DNR neu kompilieren<br /><br /> 4 = Festgelegte Option geändert<br /><br /> 5 = Temp. Tabelle geändert<br /><br /> 6 = Remoterowset geändert<br /><br /> 7 = FOR BROWSE-Berechtigung geändert<br /><br /> 8 = Abfragebenachrichtigungsumgebung geändert<br /><br /> 9 = MPI-Sicht geändert<br /><br /> 10 = Cursoroptionen geändert<br /><br /> 11 = WITH RECOMPILE-Option|21|ja|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname vom Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|IntegerData2|**int**|Endoffset der Anweisung innerhalb der gespeicherten Prozedur oder des Batches, die bzw. der die Neukompilierung verursacht hat. Der Endoffset ist -1, falls die Anweisung die letzte Anweisung im Batch ist.|55|ja|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|LoginName|**nvarchar**|Der Anmeldename des Benutzers ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsanmeldung oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|LoginSid|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|NestLevel|**int**|Die Schachtelungsebene der gespeicherten Prozedur.|29|ja|  
|NTDomainName|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|NTUserName|**nvarchar**|Windows-Benutzername.|6|ja|  
|ObjectID|**int**|Vom System zugewiesene ID der gespeicherten Prozedur.|22|ja|  
|ObjectName|**nvarchar**|Der Name des Objekts, das die Neukompilierung ausgelöst hat.|34|ja|  
|ObjectType|**int**|Der Wert, der den Typ des am Ereignis beteiligten Objekts darstellt. Weitere Informationen finden Sie unter [ObjectType Trace Event Column](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|ja|  
|Offset|**int**|Startoffset der Anweisung innerhalb der gespeicherten Prozedur oder des Batches, die bzw. der die Neukompilierung verursacht hat.|61|ja|  
|RequestID|**int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|ServerName|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|SqlHandle|**varbinary**|64-Bit-Hash, der auf dem Text einer Ad-hoc-Abfrage oder der Datenbank- und Objekt-ID eines SQL-Objekts basiert. Dieser Wert kann an sys.dm_exec_sql_text übergeben werden, um den zugehörigen SQL-Text abzurufen.|63|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**ntext**|Der Text der Transact-SQL-Anweisung, die eine Neukompilierung auf Anweisungsebene verursacht hat.|1|ja|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
|XactSequence|**bigint**|Token zur Beschreibung der aktuellen Transaktion.|50|ja|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL:StmtRecompile (Ereignisklasse)](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md)  
  
  
