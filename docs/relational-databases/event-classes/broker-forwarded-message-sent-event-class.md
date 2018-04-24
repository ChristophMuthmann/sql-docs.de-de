---
title: Broker:Forwarded Message Sent-Ereignisklasse | Microsoft-Dokumentation
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
- Broker:Forwarded Message Sent event class
ms.assetid: d0ef74d9-a4ef-4918-aa21-6b267e85569f
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6c886ae4f70caf05aa63777571cb0afa73f4a771
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="brokerforwarded-message-sent-event-class"></a>Broker:Forwarded Message Sent-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein Broker:Forwarded Message Sent-Ereignis, wenn Service Broker eine Nachricht weiterleitet.  
  
## <a name="brokerforwarded-message-sent-event-class-data-columns"></a>Datenspalten der Broker:Forwarded Message Sent-Ereignisklasse  
  
|Datenspalte|Typ|Description|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|BigintData1|**bigint**|Nachrichtensequenznummer.|52|nein|  
|ClientProcessID|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|DatabaseID|**int**|Die ID der Datenbank, die durch die USE *Datenbank* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *Datenbank*-Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die Server Name-Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|DBUserName|**nvarchar**|Die Brokerinstanz-ID für den Dienst, vom dem die Nachricht stammt.|40|nein|  
|EventClass|**int**|Der Typ der aufgezeichneten Ereignisklasse. Immer 139 für Broker:Forwarded Message Sent.|27|nein|  
|EventSequence|**int**|Die Sequenznummer für dieses Ereignis.|51|nein|  
|FileName|**nvarchar**|Name des Diensts, an den die Nachricht gerichtet ist.|36|nein|  
|GUID|**uniqueidentifier**|Die Konversations-ID des Dialogs. Dieser Bezeichner wird als Teil der Nachricht übertragen und von beiden Seiten der Konversation gemeinsam verwendet.|54|nein|  
|HostName|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|IndexID|**int**|Die Anzahl der für die weitergeleitete Nachricht verbleibenden Hops.|24|nein|  
|IntegerData|**int**|Die Fragmentnummer der weitergeleiteten Nachricht.|25|nein|  
|IsSystem|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|nein|  
|LoginSid|**image**|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|NTDomainName|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|NTUserName|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|ObjectID|**int**|Der Gültigkeitsdauerwert für die weitergeleitete Nachricht, als die Nachricht weitergeleitet wurde.|22|nein|  
|ObjectName|**nvarchar**|Nachrichten-ID der weitergeleiteten Nachricht.|34|nein|  
|OwnerName|**nvarchar**|Der Brokerbezeichner, an den die Nachricht weitergeleitet wird.|37|nein|  
|RoleName|**nvarchar**|Die Rolle des Konversationshandles. Gültige Werte sind:<br /><br /> Initiator. Dieser Broker hat die Konversation initiiert.<br /><br /> Ziel. Der Broker ist das Ziel der Konversation.|38|nein|  
|ServerName|**nvarchar**|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|SPID|**int**|Die Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|12|ja|  
|StartTime|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar.|14|ja|  
|Success|**int**|Die Zeitspanne, die für den Weiterleitungsvorgang benötigt wurde.|23|nein|  
|TargetLoginName|**nvarchar**|Die Netzwerkadresse, an die diese Instanz die Nachricht gesendet hat. Beachten Sie, dass sich diese Adresse vom endgültigen Ziel der Nachricht unterscheiden kann.|42|nein|  
|TargetUserName|**nvarchar**|Der Name des initiierenden Diensts für die Nachricht.|39|nein|  
|TransactionID|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|nein|  
  
  
