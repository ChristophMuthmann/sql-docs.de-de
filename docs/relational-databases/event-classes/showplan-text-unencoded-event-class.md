---
title: Showplan Text-Ereignisklasse (Unencoded)| Microsoft-Dokumentation
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
- Showplan Text (Unencoded) event class
ms.assetid: 0aad4563-8caf-4971-92af-55992bc5ff2c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 68cce941d242102c6818e00d3ce28023d5aef21b
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="showplan-text-unencoded-event-class"></a>Showplan Text (Unencoded)-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Showplan Text (Unencoded)-Ereignisklasse tritt auf, wenn in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine SQL-Anweisung ausgeführt wird. Diese Ereignisklasse ist mit der Showplan Text-Ereignisklasse bis auf den Unterschied identisch, dass die Informationen hier nicht als binäre Daten, sondern als Zeichenfolge formatiert sind.  
  
 Bei den eingeschlossenen Informationen handelt es sich um eine Teilmenge der Informationen, die in den Ereignisklassen „Showplan All“, „Showplan XML“ und „Showplan XML Statistics Profile“ verfügbar sind.  
  
 Wenn die Showplan Text (Unencoded)-Ereignisklasse in eine Ablaufverfolgung eingeschlossen ist, kann die Gesamtleistung durch den Verarbeitungsaufwand erheblich beeinträchtigt werden. Der durch Showplan Text (Unencoded) verursachte Verarbeitungsaufwand ist jedoch geringer als bei anderen Showplan-Ereignisklassen. Um den Verarbeitungsaufwand zu minimieren, sollten Sie die Verwendung dieser Ereignisklasse auf Ablaufverfolgungen beschränken, durch die ganz bestimmte Probleme über einen kurzen Zeitraum überwacht werden.  
  
## <a name="showplan-text-unencoded-event-class-data-columns"></a>Showplan Text (Unencoded)-Ereignisklasse (Datenspalten)  
  
|Datenspaltenname|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|BinaryData|**image**|Binärer Wert, der von der Ereignisklasse abhängt, die in der Ablaufverfolgung aufgezeichnet wird.|2|ja|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Client die Clientprozess-ID angibt.|9|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DatabaseName|**nvarchar**|Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|ja|  
|EventClass|**int**|Ereignistyp = 68.|27|nein|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|nein|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname vom Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|IntegerData|**int**|Wert für eine ganze Zahl, der von der in der Ablaufverfolgung erfassten Ereignisklasse abhängt.|25|ja|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|LineNumber|**int**|Zeigt die Nummer der Zeile an, die den Fehler enthält|5|ja|  
|LoginName|**nvarchar**|Der Anmeldename des Benutzers ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsanmeldung oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|LoginSid|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|NestLevel|**int**|Ganze Zahl, die die von @@NESTLEVEL zurückgegebenen Daten darstellt.|29|ja|  
|NTDomainName|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|NTUserName|**nvarchar**|Windows-Benutzername.|6|ja|  
|ObjectID|**int**|Vom System zugewiesene ID des Objekts.|22|ja|  
|ObjectName|**nvarchar**|Name des Objekts, auf das verwiesen wird|34|ja|  
|ObjectType|**int**|Der Wert, der den Typ des am Ereignis beteiligten Objekts darstellt. Dieser Wert entspricht der type-Spalte in der sys.objects-Katalogsicht. Weitere Werte finden Sie unter [ObjectType (Spalte für Ablaufverfolgungsereignisse)](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|ja|  
|RequestID|**int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|ServerName|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**ntext**|Textwert, der von der Ereignisklasse abhängt, die in der Ablaufverfolgung aufgezeichnet wurde.|1|ja|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
|XactSequence|**bigint**|Das Token, das die aktuelle Transaktion beschreibt.|50|ja|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Referenz zu logischen und physischen Showplanoperatoren](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [Showplan All (Ereignisklasse)](../../relational-databases/event-classes/showplan-all-event-class.md)   
 [Showplan XML (Ereignisklasse)](../../relational-databases/event-classes/showplan-xml-event-class.md)   
 [Showplan XML Statistics Profile-Ereignisklasse](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)  
  
  
