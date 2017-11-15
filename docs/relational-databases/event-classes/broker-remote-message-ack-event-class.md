---
title: Broker:Remote Message Ack-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Broker:Remote Message Ack event class
ms.assetid: 3d67efe1-74b4-4633-b029-c6e05b19f4dc
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a0733f3ec4a8b13a698bf07251f109fcd346392
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="brokerremote-message-ack-event-class"></a>Broker:Remote Message Ack (Ereignisklasse)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **Broker:Remote Message Ack** -Ereignis, wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Nachrichtenbestätigung sendet oder empfängt.  
  
## <a name="brokerremote-message-ack-event-class-data-columns"></a>Datenspalten der Broker:Remote Message Ack-Ereignisklasse  
  
|Datenspalte|Typ|Beschreibung|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|**BigintData1**|**bigint**|Enthält die Sequenznummer der Nachricht, die die Bestätigung enthält.|52|Nein|  
|**BigintData2**|**bigint**|Enthält die Sequenznummer der bestätigten Nachricht.|53|Nein|  
|**ClientProcessID**|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|**DatabaseID**|**int**|Die ID der Datenbank, die mithilfe der USE *database* -Anweisung angegeben wird. Die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *Datenbank* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|Ja|  
|**EventClass**|**int**|Der Typ der aufgezeichneten Ereignisklasse. Für **Broker:Message Ack** lautet der Typ immer **149**.|27|Nein|  
|**EventSequence**|**int**|Die Sequenznummer für dieses Ereignis.|51|Nein|  
|**EventSubClass**|**nvarchar**|Der Typ der Ereignisunterklasse, der weitere Informationen zu jeder Ereignisklasse bereitstellt. Diese Spalte kann die folgenden Werte enthalten:<br /><br /> **Message With Acknowledgement Sent**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] hat eine Bestätigung als Teil einer normalen Sequenznachricht gesendet.<br /><br /> **Acknowledgement Sent**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] hat eine Bestätigung außerhalb einer normalen Sequenznachricht gesendet.<br /><br /> **Message With Acknowledgement Received**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] hat eine Bestätigung als Teil einer normalen Sequenznachricht empfangen.<br /><br /> **Acknowledgement Received**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] hat eine Bestätigung außerhalb einer Sequenznachricht empfangen.|21|ja|  
|**GUID**|**uniqueidentifier**|Die Konversations-ID des Dialogs. Dieser Bezeichner wird als Teil der Nachricht übertragen und von beiden Seiten der Konversation gemeinsam verwendet.|54|Nein|  
|**HonorBrokerPriority**|**Int**|Der aktuelle Wert der HONOR_BROKER_PRIORITY-Datenbankoption: 0 = OFF, 1 = ON.|32|ja|  
|**HostName**|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|**IntegerData**|**int**|Die Fragmentnummer der Nachricht, die die Bestätigung enthält.|25|Nein|  
|**IntegerData2**|**int**|Die Fragmentnummer der Nachricht, die bestätigt wird.|55|Nein|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist.<br /><br /> 0 = Benutzer<br /><br /> 1 = System|60|Nein|  
|**LoginSid**|**image**|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|**NTDomainName**|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|**NTUserName**|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|**Priority**|**int**|Die Prioritätsstufe der Konversation.|5|ja|  
|**RoleName**|**nvarchar**|Die Rolle der Instanz, die die Nachricht bestätigt. Dabei handelt es sich um **initiator** oder **target**.|38|Nein|  
|**ServerName**|**nvarchar**|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung erfolgt.|26|Nein|  
|**SPID**|**int**|Die Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|12|ja|  
|**StartTime**|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar.|14|ja|  
|**StarvationElevation**|**int**|Die Nachricht wurde mit einer höheren Priorität gesendet als die Priorität, die für die Konversation konfiguriert wurde: 0 = false, 1 = true.|33|ja|  
|**TransactionID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|Nein|  
  
  
