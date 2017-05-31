---
title: 'Progress Report: Online Index Operation-Ereignisklasse | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- 'Progress Report: Online Index Operation event class [SQL Server]'
ms.assetid: 491616c1-f666-4b16-a5ea-1192bf156692
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 74cab49e651efabd8862e4d6ddf78a8fbdf739b8
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="progress-report-online-index-operation-event-class"></a>Progress Report: Online Index Operation-Ereignisklasse
  Die Progress Report: Online Index Operation-Ereignisklasse gibt den Status eines Onlineindexvorgangs während des Erstellungsprozesses an.  
  
## <a name="progress-report-online-index-operation-event-class-data-columns"></a>Datenspalten der Progress Report: Online Index Operation-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|BigintData1|**bigint**|Die Anzahl der eingefügten Zeilen.|52|ja|  
|BigintData2|**bigint**|0 = serieller Plan; andernfalls die Thread-ID während der parallelen Ausführung.|53|ja|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Client die Clientprozess-ID angibt.|9|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die ServerName-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DatabaseName|**nvarchar**|Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|ja|  
|Dauer|**bigint**|Die Zeit (in Mikrosekunden), die für das Ereignis benötigt wurde.|13|Ja|  
|EndTime|**datetime**|Der Zeitpunkt, an dem der Onlineindexvorgang abgeschlossen war.|15|Ja|  
|EventClass|**int**|Ereignistyp = 190.|27|Nein|  
|EventSequence|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|Nein|  
|EventSubClass|**int**|Der Typ der Ereignisunterklasse.<br /><br /> 1 = Start<br /><br /> 2 = Beginn der Ausführung von Phase 1<br /><br /> 3 = Ende der Ausführung von Phase 1<br /><br /> 4 = Beginn der Ausführung von Phase 2<br /><br /> 5 = Ende der Ausführung von Phase 2<br /><br /> 6 = Zählung der eingefügten Zeilen<br /><br /> 7 = Fertig<br /><br /> Phase 1 verweist auf das Basisobjekt (gruppierter Index oder Heap) oder darauf, ob der Indexvorgang nur einen nicht gruppierten Index einschließt. Phase 2 wird verwendet, wenn ein Indexerstellungsvorgang sowohl die ursprüngliche erneute Erstellung als auch zusätzliche nicht gruppierte Indizes einschließt.  Wenn ein Objekt z. B. über einen gruppierten Index und mehrere nicht gruppierte Indizes verfügt, würden bei Verwendung des Befehls "Alle neu erstellen" alle Indizes neu erstellt werden. Das Basisobjekt (der gruppierte Index) wird in Phase 1 neu erstellt, und anschließend werden alle nicht gruppierten Indizes in Phase 2 neu erstellt.|21|ja|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname vom Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|IndexID|**int**|ID für den Index des Objekts, das von dem Ereignis betroffen ist.|24|ja|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|LoginName|**nvarchar**|Der Anmeldename des Benutzers ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsanmeldung oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|LoginSid|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|NTDomainName|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|NTUserName|**nvarchar**|Windows-Benutzername.|6|ja|  
|ObjectID|**int**|Vom System zugewiesene ID des Objekts.|22|Ja|  
|ObjectName|**nvarchar**|Name des Objekts, auf das verwiesen wird|34|ja|  
|PartitionId|**bigint**|Die ID der Partition, die erstellt wird.|65|ja|  
|PartitionNumber|**int**|Die Ordnungszahl der Partition, die erstellt wird.|25|ja|  
|ServerName|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|Nein|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie beispielsweise mithilfe von Login1 eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und eine Anweisung als Login2 ausführen, zeigt SessionLoginName den Wert Login1 an und LoginName den Wert Login2. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|SPID|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|StartTime|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat.|14|Ja|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
