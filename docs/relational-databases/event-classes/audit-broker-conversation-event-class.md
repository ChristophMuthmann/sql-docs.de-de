---
title: "Audit Broker Conversation (Ereignisklasse) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Audit Broker Conversation-Ereignisklasse"
ms.assetid: d58e3577-e297-42e5-b8fe-206665a75d13
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Audit Broker Conversation (Ereignisklasse)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt ein **Audit Broker Conversation** -Ereignis, um Überwachungsmeldungen in Bezug auf die Dialogsicherheit von Service Broker zu melden.  
  
## Datenspalten der Audit Broker Conversation-Ereignisklasse  
  
|Datenspalte|Typ|Beschreibung|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Der Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|**BigintData1**|**bigint**|Die Nachrichtensequenznummer der Nachricht.|52|Nein|  
|**ClientProcessID**|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|**DatabaseID**|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|**Fehler**|**int**|Wenn dieses Ereignis einen Fehler meldet, ist dies die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlernummer.|31|Nein|  
|**EventClass**|**int**|Der Typ der aufgezeichneten Ereignisklasse. Für **Audit Broker Conversation** lautet der Typ immer **158**.|27|Nein|  
|**EventSubClass**|**int**|Der Typ der Ereignisunterklasse, der weitere Informationen zu jeder Ereignisklasse liefert. In der folgenden Tabelle sind die Ereignisunterklassen-Werte für dieses Ereignis aufgeführt.|21|ja|  
|**FileName**|**nvarchar**|Der Grund für den Anmeldefehler. Wenn die Anmeldung erfolgreich war, ist diese Spalte leer.|36|Nein|  
|**GUID**|**uniqueidentifier**|Die Konversations-ID des Dialogs. Dieser Bezeichner wird als Teil der Nachricht übertragen und von beiden Seiten der Konversation gemeinsam verwendet.|54|Nein|  
|**HostName**|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Verwenden Sie die **HOST_NAME**-Funktion, um den Hostnamen zu bestimmen.|8|ja|  
|**IntegerData**|**int**|Die Fragmentnummer der Nachricht.|25|Nein|  
|**NTDomainName**|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|**NTUserName**|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|**ObjectID**|**int**|Die Benutzer-ID des Zieldienstes.|22|Nein|  
|**RoleName**|**nvarchar**|Die Rolle des Konversationshandles. Dabei handelt es sich um **initiator** oder **target**.|38|Nein|  
|**ServerName**|**nvarchar**|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26|Nein|  
|**Severity**|**int**|Wenn dieses Ereignis einen Fehler meldet, ist dies der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Schweregrad.|29|Nein|  
|**SPID**|**int**|Die Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|12|ja|  
|**StartTime**|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar.|14|ja|  
|**Status**|**int**|Gibt den Standort im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quellcode an, der das Ereignis erstellt hat. Jeder Ort, von dem aus dieses Ereignis ggf. erstellt werden kann, besitzt einen anderen Statuscode. Der Microsoft Software Service kann mithilfe dieses Statuscodes herausfinden, wo das Ereignis generiert wurde.|30|Nein|  
|**TextData**|**ntext**|Enthält für Fehler eine Meldung, die den Grund des Fehlers beschreibt. Einer der folgenden Werte:<br /><br /> <br /><br /> **Kein Zertifikat gefunden**. Der für Dialogprotokollsicherheit angegebene Benutzer besitzt kein Zertifikat.<br /><br /> **Ungültige Zeitspanne**. Der für Dialogprotokollsicherheit angegebene Benutzer besitzt ein Zertifikat, das jedoch abgelaufen ist.<br /><br /> **Zertifikat zu groß für Arbeitsspeicher**. Der für Dialogprotokollsicherheit angegebene Benutzer besitzt ein Zertifikat, das jedoch zu groß ist. Die maximale von Service Broker unterstützte Zertifikatgröße beträgt 32.768 Byte.<br /><br /> **Kein privater Schlüssel gefunden**. Der für Dialogprotokollsicherheit angegebene Benutzer besitzt ein Zertifikat, diesem ist jedoch kein privater Schlüssel zugeordnet.<br /><br /> **Die Größe des privaten Zertifikatschlüssels ist nicht mit dem Kryptografieanbieter kompatibel.**. Der private Schlüssel für das Zertifikat besitzt eine Schlüsselgröße, die nicht erfolgreich verarbeitet werden kann. Die Größe des privaten Schlüssels muss ein Vielfaches von 64 Bytes sein.<br /><br /> **Die Größe des öffentlichen Zertifikatschlüssels ist nicht mit dem Kryptografieanbieter kompatibel.**. Der öffentliche Schlüssel für das Zertifikat besitzt eine Schlüsselgröße, die nicht erfolgreich verarbeitet werden kann. Die Größe des öffentlichen Schlüssels muss ein Vielfaches von 64 Bytes sein.<br /><br /> **Die Größe des privaten Zertifikatschlüssels ist nicht mit dem verschlüsselten Schlüsselaustauschschlüssel kompatibel.**. Die im Schlüsselaustauschschlüssel angegebene Schlüsselgröße entspricht nicht der Größe des privaten Schlüssels für das Zertifikat. Dies gibt im Allgemeinen an, dass das Zertifikat auf dem Remotecomputer nicht dem Zertifikat in der Datenbank entspricht.<br /><br /> **Die Größe des öffentlichen Zertifikatschlüssels ist nicht mit der Sicherheitsheadersignatur kompatibel.**. Der Sicherheitsheader enthält eine Signatur, die nicht mit dem öffentlichen Schlüssel des Zertifikats überprüft werden kann. Dies gibt im Allgemeinen an, dass das Zertifikat auf dem Remotecomputer nicht dem Zertifikat in der Datenbank entspricht.|1|ja|  
  
 In der folgenden Tabelle sind die Unterklassenwerte für diese Ereignisklasse aufgelistet.  
  
|ID|Unterklasse|Beschreibung|  
|--------|--------------|-----------------|  
|1|Kein Sicherheitsheader|Während einer sicheren Konversation hat Service Broker eine Nachricht empfangen, die keinen Sitzungsschlüssel enthielt. Nachdem eine sichere Konversation eingerichtet wurde, verlangt das Dialogprotokoll, dass alle Nachrichten in der Konversation einen Sitzungsschlüssel enthalten.|  
|2|Kein Zertifikat|Service Broker konnte kein verwendbares Zertifikat für einen der Teilnehmer der Konversation ermitteln. Um eine Konversation zu sichern, muss die Datenbank ein Zertifikat für den Sender und den Empfänger der Konversation enthalten.|  
|3|Ungültige Signatur|Broker konnte die vom Sender bereitgestellte Nachrichtensignatur mithilfe des öffentlichen Schlüssels im Zertifikat des Senders nicht überprüfen. Dies kann darauf hinweisen, dass die Nachricht beschädigt ist, manipuliert wurde, der Remotedienst und der lokale Dienst nicht mit dem gleichen Zertifikat konfiguriert sind oder das Zertifikat veraltet ist.|  
|4|Ausführung als Zielfehler|Der Zielbenutzer besitzt keine Empfangsberechtigungen für die Zielwarteschlange. Damit verhindert wird, dass nicht autorisierte Benutzer Nachrichten empfangen, speichert Service Broker unabhängig davon, ob der initiierende Benutzer Berechtigungen zum Einreihen von Nachrichten in Warteschlangen besitzt, keine Nachrichten in Warteschlangen, die einen Zielbenutzer aufweisen, der keine Nachrichten aus der Warteschlange empfangen kann.|  
  
## Siehe auch  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  