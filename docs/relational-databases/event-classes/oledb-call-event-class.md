---
title: OLE DB Call-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: OLEDB Call event class
ms.assetid: e1be1e90-98cc-47a3-addd-59d4aeca6547
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 52b44fe50eac1dfbab29aeeebe9cc5f82107bcd5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="oledb-call-event-class"></a>OLE DB Call-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Die **OLEDB Call**-Ereignisklasse tritt auf, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen OLE DB-Anbieter für verteilte Abfragen und remote gespeicherte Prozeduren aufruft.  
  
 Schließen Sie die **OLEDB Call** -Ereignisklasse in Ablaufverfolgungen ein, um nur jene Aufrufe zu überwachen, die keine Daten anfordern, oder jene Aufrufe, die nicht für die **QueryInterface** -Methode ausgeführt werden. Wenn die **OLEDB Call** -Ereignisklasse in eine Ablaufverfolgung eingeschlossen wird, ist der Mehraufwand davon abhängig, wie häufig OLE DB-Aufrufe für die Datenbank während der Ablaufverfolgung auftreten. Wenn Aufrufe häufig auftreten, kann die Ablaufverfolgung die Leistung bedeutend beeinträchtigen.  
  
## <a name="oledb-call-event-class-data-columns"></a>OLEDB Call (Ereignisklassen-Datenspalten)  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|ClientProcessID|**Int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Client die Clientprozess-ID angibt.|9|ja|  
|DatabaseID|**Int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DatabaseName|**nvarchar**|Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|ja|  
|Dauer|**Bigint**|Zeit, die zum Abschließen des OLE DB-Aufrufereignisses erforderlich ist|13|Nein|  
|EndTime|**Datetime**|Zeitpunkt, zu dem das Ereignis beendet wurde|15|ja|  
|Fehler|**int**|Fehlernummer eines bestimmten Ereignisses. Dies ist häufig die in der sys.messages-Katalogsicht gespeicherte Fehlernummer.|31|ja|  
|EventClass|**Int**|Ereignistyp = 119.|27|Nein|  
|EventSequence|**Int**|Sequenz der OLE DB-Ereignisklasse im Batch|51|Nein|  
|EventSubClass|**Int**|0=Wird gestartet<br /><br /> 1 = Abgeschlossen|21|Nein|  
|GroupID|**int**|ID der Arbeitsauslastungsgruppe, in der das SQL-Ablaufverfolgungsereignis ausgelöst wird.|66|ja|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname vom Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|LinkedServerName|**nvarchar**|Name des Verbindungsservers|45|ja|  
|LoginName|**nvarchar**|Anmeldename des Benutzers (Anmeldung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheit oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|LoginSid|**Bild**|Die Sicherheits-ID (Security Identifier, SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|MethodName|**nvarchar**|Der Name der OLE DB-Methode.|47|ja|  
|NTDomainName|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|NTUserName|**nvarchar**|Windows-Benutzername.|6|ja|  
|ProviderName|**nvarchar**|Name des OLE DB-Anbieters.|46|ja|  
|RequestID|**Int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|SessionLoginName|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie z. B. mit Login1 eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und mit Login2 eine Anweisung ausführen, zeigt **SessionLoginName** Login1 an, und **LoginName** zeigt Login2 an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|SPID|**Int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|TextData|**nvarchar**|Während des OLE DB-Aufrufs gesendete und empfangene Parameter|1|Nein|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|Ja|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [OLE-Automatisierungsobjekte in Transact-SQL](../../relational-databases/stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
