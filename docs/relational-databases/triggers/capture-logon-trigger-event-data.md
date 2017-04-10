---
title: "Erfassen von Ereignisdaten f&#252;r Logon-Trigger | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
caps.latest.revision: 5
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 5
---
# Erfassen von Ereignisdaten f&#252;r Logon-Trigger
  Wenn Sie XML-Daten zu LOGON-Ereignissen für die Verwendung in Logon-Triggern erfassen möchten, verwenden Sie die [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md) -Funktion. Mit dem LOGON-Ereignis wird das folgende Ereignisdatenschema zurückgegeben:  
  
 `<EVENT_INSTANCE>`  
  
 `<EventType>event_type</EventType>`  
  
 `<PostTime>post_time</PostTime>`  
  
 `<SPID>spid</SPID>`  
  
 `<ServerName>server_name</ServerName>`  
  
 `<LoginName>login_name</LoginName>`  
  
 `<LoginType>login_type</LoginType>`  
  
 `<SID>sid</SID>`  
  
 `<ClientHost>client_host</ClientHost>`  
  
 `<IsPooled>is_pooled</IsPooled>`  
  
 `</EVENT_INSTANCE>`  
  
 `<EventType>`  
 Enthält `LOGON`.  
  
 `<PostTime>`  
 Enthält die Uhrzeit, zu der eine Anforderung zum Erstellen einer Sitzung ausgegeben wird.  
  
 `<SID>`  
 Enthält den base64-verschlüsselten binären Datenstrom der Sicherheits-ID (SID) für den angegebenen Anmeldenamen.  
  
 `<ClientHost>`  
 Enthält den Hostnamen des Clients, von dem aus die Verbindung hergestellt wird. Der Wert lautet '`<local_machine>`', wenn der Name des Clients und des Servers identisch sind. Andernfalls entspricht der Wert der IP-Adresse des Clients.  
  
 `<IsPooled>`  
 Lautet `1` , wenn die Verbindung durch Verbindungspooling wiederverwendet wird. Andernfalls lautet der Wert `0`.  
  
  