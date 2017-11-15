---
title: Broker:Conversation Group-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Broker:Conversation Group event class
ms.assetid: 6595bef6-9d40-42eb-a934-735622dd23fb
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 91ef8c1e01a0e7cb730e81be1b8d9406b31b94cb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="brokerconversation-group-event-class"></a>Broker:Conversation Group-Ereignisklasse
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **Broker:Conversation Group** -Ereignis, wenn Service Broker eine neue Konversationsgruppe erstellt oder eine vorhandene Konversationsgruppe löscht.  
  
## <a name="brokerconversation-group-event-class-data-columns"></a>Datenspalten der Broker:Conversation Group-Ereignisklasse  
  
|Datenspalte|Typ|Beschreibung|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|**ClientProcessID**|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|**DatabaseID**|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|Ja|  
|**EventClass**|**int**|Der Typ der aufgezeichneten Ereignisklasse. Immer **136** für **Broker:Conversation Group**.|27|Nein|  
|**EventSequence**|**int**|Die Sequenznummer für dieses Ereignis.|51|Nein|  
|**EventSubClass**|**nvarchar**|Der Typ der Ereignisunterklasse, der weitere Informationen zu jeder Ereignisklasse liefert. Diese Spalte kann die folgenden Werte enthalten:<br /><br /> **Erstellen**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat eine neue Konversationsgruppe erstellt.<br /><br /> **Drop**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat eine Konversationsgruppe gelöscht.|21|ja|  
|**GUID**|**uniqueidentifier**|Der Konversationsgruppenbezeichner der Konversationsgruppe, die dieses Ereignis beschreibt.|54|Nein|  
|**HostName**|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|Nein|  
|**LoginSid**|**image**|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|**NTDomainName**|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|**NTUserName**|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|**ServerName**|**nvarchar**|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26|Nein|  
|**SPID**|**int**|Die Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|12|ja|  
|**StartTime**|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar.|14|ja|  
|**TransactionID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|Nein|  
  
  
