---
title: "Implementieren von Ereignisbenachrichtigungen | Microsoft Docs"
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
  - "Ereignisbenachrichtigungen [SQL Server], Zieldienst"
  - "Zieldienst [SQL Server]"
  - "Ereignisbenachrichtigungen [SQL Server], erstellen"
ms.assetid: 29ac8f68-a28a-4a77-b67b-a8663001308c
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Implementieren von Ereignisbenachrichtigungen
  Zum Implementieren einer Ereignisbenachrichtigung müssen Sie zuerst einen Zieldienst erstellen, der Ereignisbenachrichtigungen empfängt, und dann die Ereignisbenachrichtigung erstellen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dialogsicherheit sollte für Ereignisbenachrichtigungen konfiguriert werden, die Meldungen an einen Service Broker auf einem Remoteserver senden. Die Dialogsicherheit muss manuell entsprechend dem Modell der vollständigen Sicherheit konfiguriert werden.  
  
## Erstellen des Zieldiensts  
 Sie müssen keinen Dienst zum Initiieren von [!INCLUDE[ssSB](../../includes/sssb-md.md)] erstellen, da [!INCLUDE[ssSB](../../includes/sssb-md.md)] den folgenden speziellen Meldungstyp und Vertrag für Ereignisbenachrichtigungen enthält:  
  
```  
http://schemas.microsoft.com/SQL/Notifications/PostEventNotification  
```  
  
 Der Zieldienst, der Ereignisbenachrichtigungen empfängt, muss diesen bereits vorhandenen Vertrag berücksichtigen.  
  
 **So erstellen Sie einen Zieldienst**:  
  
1.  Erstellen Sie eine Warteschlange, in der Meldungen gespeichert werden.  
  
    > [!NOTE]  
    >  Die Warteschlange empfängt den folgenden Meldungstyp: `http://schemas.microsoft.com/SQL/Notifications/QueryNotification`.  
  
2.  Erstellen Sie einen Dienst für die Warteschlange, der auf den Ereignisbenachrichtigungsvertrag verweist.  
  
3.  Erstellen Sie eine Route für den Dienst, um die Adresse zu definieren, an die [!INCLUDE[ssSB](../../includes/sssb-md.md)] Meldungen für den Dienst sendet. Für Ereignisbenachrichtigungen, die an einen Dienst in der gleichen Datenbank gerichtet sind, geben Sie `ADDRESS = 'LOCAL'`an.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Routing bestimmt den Dienst, der die Benachrichtigungsmeldungen empfängt. Wenn die Ereignisbenachrichtigung an einen Dienst auf einem Remoteserver gerichtet ist, müssen für den Quellserver und den Zielserver Routen definiert sein, damit sichergestellt ist, dass eine bidirektionale Kommunikation stattfindet.  
  
 Das folgende Beispiel erstellt eine Warteschlange, einen Dienst für die Warteschlange und eine Route für den Dienst, um Meldungen aus dem Ereignisbenachrichtigungsvertrag zu verarbeiten:  
  
```  
CREATE QUEUE NotifyQueue ;  
GO  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
(  
[http://schemas.microsoft.com/SQL/Notifications/PostEventNotification]  
);  
GO  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
```  
  
## Erstellen der Ereignisbenachrichtigung  
 Ereignisbenachrichtigungen werden mithilfe der [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE EVENT NOTIFICATION-Anweisung erstellt und mithilfe von DROP EVENT NOTIFICATION gelöscht. Wenn Sie eine Ereignisbenachrichtigung ändern möchten, müssen Sie sie löschen und dann neu erstellen.  
  
 Im folgenden Beispiel wird die Ereignisbenachrichtigung mit dem Namen `CreateDatabaseNotification` erstellt. Diese Ereignisbenachrichtigung sendet eine Meldung zu jedem `CREATE_DATABASE`-Ereignis, das auf dem Server auftritt, an den `NotifyService`-Dienst, der zuvor erstellt wurde.  
  
```  
CREATE EVENT NOTIFICATION CreateDatabaseNotification  
ON SERVER  
FOR CREATE_DATABASE  
TO SERVICE 'NotifyService', '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
> [!CAUTION]  
>  Ereignisbenachrichtigungen erkennen CREATE_SCHEMA-Ereignisse und die <schema_element>-Definitionen von CREATE SCHEMA-Anweisungen als separate Ereignisse. Angenommen, eine Ereignisbenachrichtigung wird für die Ereignisse CREATE_SCHEMA und CREATE_TABLE erstellt, und Sie führen den folgenden Batch aus.  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  In diesem Fall wird die Ereignisbenachrichtigung zweimal ausgegeben: Einmal beim Auftreten des CREATE_SCHEMA-Ereignisses, und ein zweites Mal beim Auftreten des CREATE_TABLE-Ereignisses. Es wird empfohlen, entweder keine Ereignisbenachrichtigungen für die CREATE_SCHEMA-Ereignisse und gleichzeitig für die <schema_element>-Texte von entsprechenden CREATE SCHEMA-Definitionen zu erstellen, oder Ihre Anwendung so zu programmieren, dass keine nicht erwünschten Ereignisdaten erfasst werden.  
  
 **So erstellen Sie eine Ereignisbenachrichtigung**  
  
-   [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
 **So löschen Sie eine Ereignisbenachrichtigung**  
  
-   [DROP EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-notification-transact-sql.md)  
  
## Siehe auch  
 [Abrufen von Informationen zu Ereignisbenachrichtigungen](../../relational-databases/service-broker/get-information-about-event-notifications.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  