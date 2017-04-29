---
title: Broker:Conversation-Ereignisklasse | Microsoft-Dokumentation
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
- Broker:Conversation event class
ms.assetid: 784707b5-cc67-46a3-8ae6-8f8ecf4b27c0
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e7161ab04ec24504b6ba0a5f6e7cd304166b7b1
ms.lasthandoff: 04/11/2017

---
# <a name="brokerconversation-event-class"></a>Broker:Conversation-Ereignisklasse
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **Broker:Conversation** -Ereignis, um den Fortschritt einer Service Broker-Konversation anzugeben.  
  
## <a name="brokerconversation-event-class-data-columns"></a>Datenspalten der Broker:Conversation-Ereignisklasse  
  
|Datenspalte|Typ|Beschreibung|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|**ClientProcessID**|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|**DatabaseID**|**int**|Die ID der Datenbank, die mithilfe der USE *database* -Anweisung angegeben wird. Die ID der Standarddatenbank, wenn keine USE *database*-Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Bestimmen Sie den Wert für eine Datenbank mithilfe der **DB_ID** -Funktion.|3|ja|  
|**EventClass**|**int**|Der Typ der aufgezeichneten Ereignisklasse. Immer **124** für **Broker:Conversation**.|27|Nein|  
|**EventSequence**|**int**|Die Sequenznummer für dieses Ereignis.|51|Nein|  
|**EventSubClass**|**nvarchar**|Der Typ der Ereignisunterklasse Dieser stellt weitere Informationen zu jeder Ereignisklasse bereit.|21|ja|  
|**GUID**|**uniqueidentifier**|Die Konversations-ID des Dialogs. Dieser Bezeichner wird als Teil der Nachricht übertragen und von beiden Seiten der Konversation gemeinsam verwendet.|54|Nein|  
|**HostName**|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Verwenden Sie die **HOST_NAME** -Funktion, um den Hostnamen zu bestimmen.|8|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist.<br /><br /> 0 = Benutzer<br /><br /> 1 = System|60|Nein|  
|**LoginSid**|**image**|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|**MethodName**|**nvarchar**|Die Konversationsgruppe, zu der die Konversation gehört.|47|Nein|  
|**NTDomainName**|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|**NTUserName**|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|**ObjectName**|**nvarchar**|Das Konversationshandle des Dialogs.|34|Nein|  
|**Priority**|**int**|Die Prioritätsstufe der Konversation|5|ja|  
|**RoleName**|**nvarchar**|Die Rolle des Konversationshandles. Dabei handelt es sich um **initiator** oder **target**.|38|Nein|  
|**ServerName**|**nvarchar**|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung erfolgt.|26|Nein|  
|**Severity**|**int**|Wenn dieses Ereignis einen Fehler meldet, ist dies der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Schweregrad.|29|Nein|  
|**SPID**|**int**|Die Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|12|ja|  
|**StartTime**|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar).|14|Ja|  
|**TextData**|**ntext**|Der aktuelle Status der Konversation. Kann einen der folgenden Werte aufweisen:|1|ja|  
|||**SO**. Started Outbound (Ausgehend gestartet). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat eine BEGIN CONVERSATION-Anweisung für diese Konversation verarbeitet, es wurden jedoch keine Nachrichten gesendet.|||  
|||**SI**. Started Inbound (Eingehend gestartet). Eine andere Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] hat eine neue Konversation mit der aktuellen Instanz begonnen, die aktuelle Instanz hat den Empfang der ersten Nachricht jedoch noch nicht beendet. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann die Konversation in diesem Status starten, wenn die erste Meldung fragmentiert ist oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Nachrichten in falscher Reihenfolge empfängt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] könnte die Konversation jedoch im Status CO erstellen, wenn die erste empfangene Übertragung für die Konversation die erste Nachricht vollständig enthält.|||  
|||**CO**. Conversing (Konversation begonnen). Die Konversation ist eingerichtet, und beide Seiten der Konversation können Meldungen senden. Der Großteil der Kommunikation für einen typischen Dienst findet statt, wenn sich die Konversation in diesem Status befindet.|||  
|||**DI**. Disconnected Inbound (Eingehend getrennt). Die Remoteseite der Konversation hat eine END CONVERSATION-Anweisung ausgegeben. Die Konversation verbleibt in diesem Status, bis die lokale Seite der Konversation eine END CONVERSATION-Anweisung ausgibt. Eine Anwendung kann weiter Nachrichten für die Konversation empfangen. Da die Remoteseite der Konversation die Konversation beendet hat, kann eine Anwendung in dieser Konversation keine Nachrichten mehr senden. Wenn eine Anwendung eine END CONVERSATION-Anweisung ausgibt, geht die Konversation in den CD-Status (Geschlossen) über.|||  
|||**DO**. Disconnected Outbound (Ausgehend getrennt). Die lokale Seite der Konversation hat eine END CONVERSATION-Anweisung ausgegeben. Die Konversation bleibt so lange in diesem Status, bis die Remoteseite der Konversation END CONVERSATION anerkennt. Eine Anwendung kann keine Nachrichten für die Konversation senden oder empfangen. Wenn die Remoteseite der Konversation die END CONVERSATION-Anweisung bestätigt, geht die Konversation in den CD-Status (Geschlossen) über.|||  
|||**ER**. Error (Fehler). An diesem Endpunkt ist ein Fehler aufgetreten. Die Error-, Severity- und State-Spalten enthalten Informationen zu dem aufgetretenen Fehler.|||  
|||**CD**. Closed (Geschlossen). Der Konversationsendpunkt wird nicht mehr verwendet.|||  
|**Transaction ID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|Nein|  
  
 In der folgenden Tabelle sind die Unterklassenwerte für diese Ereignisklasse aufgeführt.  
  
|ID|Unterklasse|Beschreibung|  
|--------|--------------|-----------------|  
|1|SEND Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **SEND Message** -Ereignis, wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine SEND-Anweisung ausführt.|  
|2|END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **END CONVERSATION** -Ereignis, wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine END CONVERSATION-Anweisung ausführt, die keine WITH ERROR-Klausel enthält.|  
|3|END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **END CONVERSATION WITH ERROR** -Ereignis, wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine END CONVERSATION-Anweisung ausführt, die eine WITH ERROR-Klausel enthält.|  
|4|Broker Initiated Error|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert jedes Mal ein **Broker Initiated Error** -Ereignis, wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Fehlermeldung erstellt. Wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] z. B. eine Nachricht für einen Dialog nicht erfolgreich weiterleiten kann, erstellt der Broker eine Fehlermeldung für den Dialog und generiert dieses Ereignis. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert dieses Ereignis nicht, wenn eine Anwendung eine Konversation mit einem Fehler beendet.|  
|5|Terminate Dialog|[!INCLUDE[ssSB](../../includes/sssb-md.md)] hat den Dialog beendet. [!INCLUDE[ssSB](../../includes/sssb-md.md)] beendet Dialoge als Reaktion auf Bedingungen, die verhindern, dass der Dialog fortgesetzt wird, die jedoch keine Fehler oder das normale Ende einer Konversation darstellen. So führt z. B. das Löschen eines Dienstes dazu, dass [!INCLUDE[ssSB](../../includes/sssb-md.md)] alle Dialoge für diesen Dienst beendet.|  
|6|Received Sequenced Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert eine **Received Sequenced Message** -Ereignisklasse, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Nachricht empfängt, die eine Nachrichtensequenznummer enthält. Alle benutzerdefinierten Nachrichtentypen sind sequenzierte Nachrichten. [!INCLUDE[ssSB](../../includes/sssb-md.md)] generiert in zwei Fällen eine nicht sequenzierte Nachricht:<br /><br /> Von [!INCLUDE[ssSB](../../includes/sssb-md.md)] generierte Fehlermeldungen sind nicht sequenziert.<br /><br /> Nachrichtenbestätigungen sind möglicherweise nicht sequenziert. Aus Effizienzgründen schließt [!INCLUDE[ssSB](../../includes/sssb-md.md)] alle verfügbaren Nachrichtenbestätigungen als Teil einer sequenzierten Nachricht ein. Wenn eine Anwendung jedoch innerhalb eines bestimmten Zeitraums keine sequenzierte Nachricht an den Remoteendpunkt sendet, erstellt [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine nicht sequenzierte Nachricht für die Nachrichtenbestätigung.|  
|7|Received END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein Received END CONVERSATION-Ereignis, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine End Dialog-Nachricht von der anderen Seite der Konversation empfängt.|  
|8|Received END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **Received END CONVERSATION WITH ERROR** -Ereignis, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen benutzerdefinierten Fehler von der anderen Seite der Konversation empfängt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert dieses Ereignis nicht, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen vom Broker definierten Fehler empfängt.|  
|9|Received Broker Error Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **Received Broker Error Message** -Ereignis, wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine vom Broker definierte Fehlermeldung von der anderen Seite der Konversation empfängt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert dieses Ereignis nicht, wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Fehlermeldung empfängt, die von einer Anwendung generiert wurde.<br /><br /> Wenn z. B. die aktuelle Datenbank eine Standardroute zu einer Weiterleitungsdatenbank enthält, leitet [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Nachricht mit einem unbekannten Dienstnamen zur Weiterleitungsdatenbank weiter. Wenn diese Datenbank die Nachricht nicht weiterleiten kann, erstellt der Broker in dieser Datenbank eine Fehlermeldung und gibt diese Fehlermeldung an die aktuelle Datenbank zurück. Wenn die aktuelle Datenbank die vom Broker generierte Fehlermeldung von der Weiterleitungsdatenbank empfängt, generiert die aktuelle Datenbank ein **Received Broker Error Message** -Ereignis.|  
|10|Received END CONVERSATION Ack|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **Received END CONVERSATION Ack** -Ereignis, wenn die andere Seite einer Konversation eine von dieser Seite der Konversation gesendete End Dialog-Nachricht oder eine Fehlermeldung empfängt.|  
|11|BEGIN DIALOG|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **BEGIN DIALOG** -Ereignis, wenn das Datenbankmodul einen BEGIN DIALOG-Befehl ausführt.|  
|12|Dialog Created|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein **Dialogfeld Created** -Ereignis, wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] einen Endpunkt für einen Dialog erstellt. [!INCLUDE[ssSB](../../includes/sssb-md.md)] erstellt jedes Mal einen Endpunkt, wenn ein neuer Dialog eingerichtet wird, unabhängig davon, ob die aktuelle Datenbank der Initiator oder das Ziel des Dialogs ist.|  
|13|END CONVERSATION WITH CLEANUP|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert ein END CONVERSATION WITH CLEANUP-Ereignis, wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine END CONVERSATION-Anweisung ausführt, die eine WITH CLEANUP-Klausel enthält.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
