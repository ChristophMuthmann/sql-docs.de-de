---
title: Database Mirroring:Connection-Ereignisklasse | Microsoft-Dokumentation
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
ms.assetid: b59dccc9-f40d-4c82-aa35-ac40acea86ff
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d26accbe02ac42a01dbb4c8bf832facec5b1b99e
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="database-mirroring-connection-event-class"></a>Database Mirroring:Connection-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **Database Mirroring:Connection** -Ereignis, um den Status einer Transportverbindung zu melden, die von der Datenbankspiegelung verwaltet wird.  
  
## <a name="database-mirroringconnection-event-class-data-columns"></a>Datenspalten der Database Mirroring:Connection-Ereignisklasse  
  
|Datenspalte|Typ|Description|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|**ClientProcessID**|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|**DatabaseID**|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database*-Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Bestimmen Sie den Wert für eine Datenbank mithilfe der **DB_ID** -Funktion.|3|ja|  
|**Fehler**|**int**|Die Nachrichten-ID-Nummer in **sys.messages** für den Text des Ereignisses. Wenn dieses Ereignis einen Fehler meldet, ist dies die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlernummer.|31|nein|  
|**EventClass**|**int**|Der Typ der aufgezeichneten Ereignisklasse. Immer **151** für **Database Mirroring:Connection**.|27|nein|  
|**EventSequence**|**int**|Die Sequenznummer für dieses Ereignis.|51|nein|  
|**EventSubClass**|**nvarchar**|Der Verbindungsstatus dieser Verbindung. Für dieses Ereignis hat die Unterklasse einen der folgenden Werte.<br /><br /> **Verbindungsherstellung**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] initiiert eine Transportverbindung.<br /><br /> **Verbunden**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat eine Transportverbindung hergestellt.<br /><br /> **Verbindung ist fehlgeschlagen**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] konnte keine Transportverbindung herstellen.<br /><br /> **Schließt**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schließt die Transportverbindung.<br /><br /> **Geschlossen**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat die Transportverbindung geschlossen.<br /><br /> **Annehmen**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat eine Transportverbindung von einer anderen Instanz akzeptiert.<br /><br /> **IO-Fehler gesendet**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist beim Senden einer Nachricht ein Transportfehler aufgetreten.<br /><br /> **IO-Fehler empfangen**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist beim Empfangen einer Nachricht ein Transportfehler aufgetreten.|21|ja|  
|**GUID**|**uniqueidentifier**|Die Endpunkt-ID dieser Verbindung.|54|nein|  
|**HostName**|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Verwenden Sie die **HOST_NAME** -Funktion, um den Hostnamen zu bestimmen.|8|ja|  
|**IntegerData**|**int**|Die Angabe, wie oft diese Verbindung geschlossen wurde.|25|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist.<br /><br /> 0 = Benutzer<br /><br /> 1 = System|60|nein|  
|**LoginSid**|**image**|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|**NTDomainName**|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|**NTUserName**|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|**ObjectName**|**nvarchar**|Das Konversationshandle des Dialogs.|34|nein|  
|**ServerName**|**nvarchar**|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|**SPID**|**int**|Die Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|12|ja|  
|**StartTime**|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar.|14|ja|  
|**TextData**|**ntext**|Der Text der Fehlermeldung, die sich auf dieses Ereignis bezieht. Bei Ereignissen, die keine Fehler melden, ist dieses Feld leer. Die Fehlermeldung kann eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlermeldung oder eine Windows-Fehlermeldung sein.|1|ja|  
|**TransactionID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|nein|  
  
  
