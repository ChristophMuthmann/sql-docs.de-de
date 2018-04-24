---
title: Implementieren von Ereignisbenachrichtigungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: service-broker
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], target service
- target service [SQL Server]
- event notifications [SQL Server], creating
ms.assetid: 29ac8f68-a28a-4a77-b67b-a8663001308c
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 21038b9922fe335e2cdd127160cf70dd37688da7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="implement-event-notifications"></a>Implementieren von Ereignisbenachrichtigungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Zum Implementieren einer Ereignisbenachrichtigung müssen Sie zuerst einen Zieldienst erstellen, der Ereignisbenachrichtigungen empfängt, und dann die Ereignisbenachrichtigung erstellen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dialogsicherheit sollte für Ereignisbenachrichtigungen konfiguriert werden, die Meldungen an einen Service Broker auf einem Remoteserver senden. Die Dialogsicherheit muss manuell entsprechend dem Modell der vollständigen Sicherheit konfiguriert werden.  
  
## <a name="creating-the-target-service"></a>Erstellen des Zieldiensts  
 Sie müssen keinen Dienst zum Initiieren von [!INCLUDE[ssSB](../../includes/sssb-md.md)]erstellen, da [!INCLUDE[ssSB](../../includes/sssb-md.md)] den folgenden speziellen Meldungstyp und Vertrag für Ereignisbenachrichtigungen enthält:  
  
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
  
## <a name="creating-the-event-notification"></a>Erstellen der Ereignisbenachrichtigung  
 Ereignisbenachrichtigungen werden mithilfe der [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE EVENT NOTIFICATION-Anweisung erstellt und mithilfe von DROP EVENT NOTIFICATION gelöscht. Wenn Sie eine Ereignisbenachrichtigung ändern möchten, müssen Sie sie löschen und dann neu erstellen.  
  
 Im folgenden Beispiel wird die Ereignisbenachrichtigung mit dem Namen `CreateDatabaseNotification`erstellt. Diese Ereignisbenachrichtigung sendet eine Meldung zu jedem `CREATE_DATABASE`-Ereignis, das auf dem Server auftritt, an den `NotifyService`-Dienst, der zuvor erstellt wurde.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Abrufen von Informationen zu Ereignisbenachrichtigungen](../../relational-databases/service-broker/get-information-about-event-notifications.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
