---
title: Broker:Forwarded Message Dropped-Ereignisklasse | Microsoft-Dokumentation
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
- Broker:Forwarded Message Dropped event class
ms.assetid: ec242d0b-77b0-45f5-8b12-186a14b173a8
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b64db8b03faa5a21cc0644d58cac76df13483511
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="brokerforwarded-message-dropped-event-class"></a>Broker:Forwarded Message Dropped-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein Broker:Forwarded Message Dropped-Ereignis, wenn Service Broker eine Nachricht löscht, die eigentlich weitergeleitet werden sollte.  
  
## <a name="brokerforwarded-message-dropped-event-class-data-columns"></a>Datenspalten der Broker:Forwarded Message Dropped-Ereignisklasse  
  
|Datenspalte|Typ|Description|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|BigintData1|**bigint**|Nachrichtensequenznummer.|52|nein|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *Datenbank* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *Datenbank*-Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die Server Name-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DatabaseName|**nvarchar**|Der Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|ja|  
|DBUserName|**nvarchar**|Der Brokerinstanzbezeichner, vom dem diese Nachricht stammt.|40|nein|  
|Fehler|**int**|Die Nachrichten-ID-Nummer in sys.messages für den Text des Ereignisses.|31|nein|  
|EventClass|**int**|Der Typ der aufgezeichneten Ereignisklasse. Für Broker:Forwarded Message Dropped lautet der Typ immer 191.|27|nein|  
|EventSequence|**int**|Die Sequenznummer für dieses Ereignis.|51|nein|  
|FileName|**nvarchar**|Name des Diensts, an den die Nachricht gerichtet ist.|36|nein|  
|GUID|**uniqueidentifier**|Die Konversations-ID des Dialogs. Dieser Bezeichner wird als Teil der Nachricht übertragen und von beiden Seiten der Konversation gemeinsam verwendet.|54|nein|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|IndexID|**int**|Die Anzahl der für die weitergeleitete Nachricht verbleibenden Hops.|24|nein|  
|IntegerData|**int**|Die Fragmentnummer der weitergeleiteten Nachricht.|25|nein|  
|LoginSid|**image**|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|NTDomainName|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|NTUserName|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|ObjectID|**int**|Der Gültigkeitsdauerwert der weitergeleiteten Nachricht.|22|nein|  
|ObjectName|**nvarchar**|Nachrichten-ID der weitergeleiteten Nachricht.|34|nein|  
|OwnerName|**nvarchar**|Der Brokerinstanzbezeichner für das Ziel der Nachricht.|37|nein|  
|RoleName|**nvarchar**|Die Rolle des Konversationshandles. Folgende Angaben sind möglich:<br /><br /> -Initiator. Dieser Broker hat die Konversation initiiert.<br /><br /> -Target. Der Broker ist das Ziel der Konversation.|38|nein|  
|ServerName|**nvarchar**|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|Schweregrad|**int**|Schweregradnummer für den Text im Ereignis.|29|nein|  
|SPID|**int**|Die Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|12|ja|  
|StartTime|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar.|14|ja|  
|Status|**int**|Gibt den Standort im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quellcode an, der das Ereignis erstellt hat. Jeder Ort, von dem aus dieses Ereignis ggf. erstellt werden kann, besitzt einen anderen Statuscode. Der Microsoft Software Service kann mithilfe dieses Statuscodes herausfinden, wo das Ereignis generiert wurde.|30|nein|  
|Success|**int**|Die Zeitdauer, für die die Nachricht gültig war. Wenn dieser Wert größer oder gleich der Gültigkeitsdauer ist, wird die Nachricht gelöscht.|23|nein|  
|TargetLoginName|**nvarchar**|Die Netzwerkadresse, an die die Nachricht weitergeleitet werden soll.|42|nein|  
|TargetUserName|**nvarchar**|Der Name des initiierenden Diensts für die Nachricht.|39|nein|  
|TextData|**ntext**|Beschreibung des Grundes, aus dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Nachricht gelöscht hat.|1|ja|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|nein|  
  
 Die TextData-Spalte dieses Ereignisses enthält eine Beschreibung des Grundes, aus dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Nachricht gelöscht hat.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
