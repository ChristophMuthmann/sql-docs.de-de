---
title: CREATE EVENT NOTIFICATION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_EVENT_NOTIFICATION_TSQL
- NOTIFICATION_TSQL
- EVENT
- NOTIFICATION
- CREATE EVENT NOTIFICATION
- EVENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EVENT NOTIFICATION statement
- events [SQL Server], notifications
- event notifications [SQL Server], creating
ms.assetid: dbbff0e8-9e25-4f12-a1ba-e12221d16ac2
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2528104adb090ceb67476708cd8470d247e35a3a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-event-notification-transact-sql"></a>CREATE EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt ein Objekt, das Informationen über eine Datenbank oder ein Serverereignis an einen Service Broker-Dienst sendet. Ereignisbenachrichtigungen werden nur mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen erstellt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE EVENT NOTIFICATION event_notification_name   
ON { SERVER | DATABASE | QUEUE queue_name }   
[ WITH FAN_IN ]  
FOR { event_type | event_group } [ ,...n ]  
TO SERVICE 'broker_service' , { 'broker_instance_specifier' | 'current database' }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *event_notification_name*  
 Der Name der Ereignisbenachrichtigung. Der Name der Ereignisbenachrichtigung muss den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen und innerhalb seines Bereichs (SERVER, DATABASE oder *object_name*) eindeutig sein.  
  
 SERVER  
 Wendet den Bereich der Ereignisbenachrichtigung auf die aktuelle Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an. Ist dieser Bereich angegeben, wird die Benachrichtigung jedes Mal ausgelöst, wenn das angegebene Ereignis in der FOR-Klausel irgendwo in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auftritt.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 DATABASE  
 Wendet den Bereich der Ereignisbenachrichtigung auf die aktuelle Datenbank an. Ist dieser Bereich angegeben, wird die Benachrichtigung jedes Mal ausgelöst, wenn das angegebene Ereignis in der FOR-Klausel in der aktuellen Datenbank auftritt.  
  
 QUEUE  
 Wendet den Bereich der Benachrichtigung auf eine bestimmte Warteschlange in der aktuellen Datenbank an. QUEUE kann nur angegeben werden, wenn auch FOR QUEUE_ACTIVATION oder FOR BROKER_QUEUE_DISABLED angegeben ist.  
  
 *queue_name*  
 Der Name der Warteschlange, auf die die Ereignisbenachrichtigung angewendet wird. *queue_name* kann nur angegeben werden, wenn QUEUE angegeben wird.  
  
 WITH FAN_IN  
 Weist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, nur eine Nachricht pro Ereignis an einen beliebigen angegebenen Dienst zu senden, wenn für Ereignisbenachrichtigungen Folgendes gilt:  
  
-   Sie werden für dasselbe Ereignis erstellt.  
  
-   Sie werden vom selben Prinzipal erstellt (erkennbar an der identischen Sicherheits-ID).  
  
-   Geben Sie denselben Dienst und *broker_instance_specifier*-Bezeichner an.  
  
-   Sie geben WITH FAN_IN an.  
  
 Beispielsweise werden drei Ereignisbenachrichtigungen erstellt. Bei allen Ereignisbenachrichtigungen wird FOR ALTER_TABLE, WITH FAN_IN und dieselbe TO SERVICE-Klausel angegeben, und alle werden von derselben SID erstellt. Wenn eine ALTER TABLE-Anweisung ausgeführt wird, werden die durch diese drei Ereignisbenachrichtigungen erstellten Nachrichten in eine Nachricht zusammengeführt. Daher empfängt der Zieldienst nur eine Nachricht bezüglich des Ereignisses.  
  
 *event_type*  
 Der Name eines Ereignistyps, der die Ausführung der Ereignisbenachrichtigung verursacht. *event_type* kann ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-DDL-Ereignistyp, ein SQL-Ablaufverfolgungsereignistyp oder ein [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Ereignistyp sein. Eine Liste aller qualifizierenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-DDL-Ereignistypen finden Sie unter [DDL-Ereignisse](../../relational-databases/triggers/ddl-events.md). [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Ereignistypen sind QUEUE_ACTIVATION und BROKER_QUEUE_DISABLED. Weitere Informationen finden Sie unter [Event Notifications](../../relational-databases/service-broker/event-notifications.md).  
  
 *event_group*  
 Der Name einer vordefinierten Gruppe von [!INCLUDE[tsql](../../includes/tsql-md.md)]- oder SQL-Ablaufverfolgungs-Ereignistypen. Eine Ereignisbenachrichtigung kann nach der Ausführung eines beliebigen Ereignisses ausgelöst werden, das zu einer Ereignisgruppe gehört. Eine Liste der DDL-Ereignisgruppen, der von diesen abgedeckten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ereignisse und der Bereiche, für die sie definiert werden können, finden Sie unter [DDL-Ereignisgruppen](../../relational-databases/triggers/ddl-event-groups.md).  
  
 *event_group* fungiert außerdem als Makro, indem dieser Parameter beim Abschließen der CREATE EVENT NOTIFICATION-Anweisung die betroffenen Ereignistypen der **sys.events**-Katalogsicht hinzufügt.  
  
 **'** *broker_service* **'**  
 Gibt den Zieldienst an, der die Ereignisinstanzdaten empfängt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] öffnet eine oder mehrere Konversationen für den Zieldienst der Ereignisbenachrichtigung. Der Dienst muss denselben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ereignismeldungstyp und Vertrag berücksichtigen, wie sie zum Senden der Nachricht verwendet werden.  
  
 Die Konversationen bleiben geöffnet, bis die Ereignisbenachrichtigung gelöscht wird. Bestimmte Fehler können dazu führen, dass Konversationen früher geschlossen werden. Das explizite Beenden einiger oder aller Konversationen kann verhindern, dass der Zieldienst weitere Nachrichten empfängt.  
  
 {**'***broker_instance_specifier***'** | **'current database'**}  
 Gibt die Service Broker-Instanz an, für die *broker_service* aufgelöst wird. Der Wert für einen bestimmten Service Broker kann durch Abfragen der **service_broker_guid**-Spalte der **sys.databases**-Katalogsicht ermittelt werden. Verwenden Sie **'current database'**, um die Service Broker-Instanz in der aktuellen Datenbank anzugeben. **'current database'** ist ein Zeichenfolgenliteral, das nicht nach Groß-/Kleinschreibung unterscheidet.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] beinhaltet einen speziellen Nachrichtentyp und Vertrag für Ereignisbenachrichtigungen. Es muss also kein initiierender Dienst für Service Broker erstellt werden; dieser ist bereits vorhanden und gibt den folgenden Vertragsnamen an: `http://schemas.microsoft.com/SQL/Notifications/PostEventNotification`  
  
 Der Zieldienst, der Ereignisbenachrichtigungen empfängt, muss diesen bereits vorhandenen Vertrag berücksichtigen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dialogsicherheit sollte für Ereignisbenachrichtigungen konfiguriert werden, die Meldungen an einen Service Broker auf einem Remoteserver senden. Die Dialogsicherheit muss manuell entsprechend dem Modell der vollständigen Sicherheit konfiguriert werden. Weitere Informationen finden Sie unter [Konfigurieren der Dialogsicherheit für Ereignisbenachrichtigungen](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md).  
  
 Wird für eine Ereignistransaktion, die eine Benachrichtigung aktiviert, ein Rollback ausgeführt, wird das Rollback auch für das Senden der Ereignisbenachrichtigung ausgeführt. Benachrichtigungen werden nicht durch eine in einem Trigger definierte Aktion ausgelöst, wenn ein Commit oder Rollback der Transaktion im Trigger ausgeführt wird. Da Ablaufverfolgungsereignisse nicht durch Transaktionen gebunden werden, werden auf Ablaufverfolgungsereignissen basierende Ereignisbenachrichtigungen unabhängig davon gesendet, ob für die Transaktion, durch die sie aktiviert werden, ein Rollback ausgeführt wird.  
  
 Wird die Konversation zwischen Server und Zieldienst nach dem Auslösen einer Ereignisbenachrichtigung unterbrochen, wird ein Fehler gemeldet und die Ereignisbenachrichtigung gelöscht.  
  
 Die Ereignistransaktion, von der die Benachrichtigung ursprünglich gestartet wurde, wird nicht davon betroffen, ob die Ereignisbenachrichtigung erfolgreich gesendet wurde.  
  
 Alle Fehler beim Senden einer Ereignisbenachrichtigung werden protokolliert.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Erstellen einer Ereignisbenachrichtigung mit der Datenbank als Bereich (ON DATABASE) ist die CREATE DATABASE DDL EVENT NOTIFICATION-Berechtigung in der aktuellen Datenbank erforderlich.  
  
 Zum Erstellen einer Ereignisbenachrichtigung für eine DDL-Anweisung mit dem Server als Bereich (ON SERVER) ist die CREATE DDL EVENT NOTIFICATION-Berechtigung auf dem Server erforderlich.  
  
 Zum Erstellen einer Ereignisbenachrichtigung für ein Ablaufverfolgungsereignis ist die CREATE TRACE EVENT NOTIFICATION-Berechtigung auf dem Server erforderlich.  
  
 Zum Erstellen einer Ereignisbenachrichtigung mit einer Warteschlange als Bereich ist die ALTER-Berechtigung für die Warteschlange erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
> [!NOTE]  
>  In den nachfolgenden Beispielen A und B entspricht der GUID in der `TO SERVICE 'NotifyService'`-Klausel ('8140a771-3c4b-4479-8ac0-81008ab17984') dem Computer, auf dem das Beispiel eingerichtet wurde. Für diese Instanz handelt es sich dabei um den GUID für die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank.  
>   
>  Zum Kopieren und Ausführen dieser Beispiele müssen Sie diesen GUID durch einen GUID von Ihrem Computer und Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz ersetzen. Wie im obigen Abschnitt zu den Argumenten erläutert, kann **'***broker_instance_specifier***'** durch Abfragen der Spalte „service_broker_guid“ der Katalogsicht „sys.databases“ ermittelt werden.  
  
### <a name="a-creating-an-event-notification-that-is-server-scoped"></a>A. Erstellen einer Ereignisbenachrichtigung mit dem Server als Bereich  
 Im folgenden Beispiel werden die zum Einrichten eines Zieldiensts mit [!INCLUDE[ssSB](../../includes/sssb-md.md)] erforderlichen Objekte erstellt. Der Zieldienst verweist auf den Nachrichtentyp und den Vertrag des initiierenden Diensts speziell für Ereignisbenachrichtigungen. Dann wird auf dem Zieldienst eine Ereignisbenachrichtigung erstellt, die eine Benachrichtigung sendet, sobald ein `Object_Created`-Ablaufverfolgungsereignis auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorliegt.  
  
```sql  
--Create a queue to receive messages.  
CREATE QUEUE NotifyQueue ;  
GO  
--Create a service on the queue that references  
--the event notifications contract.  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
([http://schemas.microsoft.com/SQL/Notifications/PostEventNotification]);  
GO  
--Create a route on the service to define the address   
--to which Service Broker sends messages for the service.  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
--Create the event notification.  
CREATE EVENT NOTIFICATION log_ddl1   
ON SERVER   
FOR Object_Created   
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
### <a name="b-creating-an-event-notification-that-is-database-scoped"></a>B. Erstellen einer Ereignisbenachrichtigung mit der Datenbank als Bereich  
 Im folgenden Beispiel wird eine Ereignisbenachrichtigung für denselben Zieldienst wie im vorherigen Beispiel erstellt. Die Ereignisbenachrichtigung wird ausgelöst, nachdem ein `ALTER_TABLE`-Ereignis in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Beispieldatenbank aufgetreten ist.  
  
```sql  
CREATE EVENT NOTIFICATION Notify_ALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
### <a name="c-getting-information-about-an-event-notification-that-is-server-scoped"></a>C. Abrufen von Informationen zu einer Ereignisbenachrichtigung mit dem Server als Bereich  
 Im folgenden Beispiel wird die `sys.server_event_notifications`-Katalogsicht für Metadaten zur Ereignisbenachrichtigung `log_ddl1` abgefragt, die mit dem Serverbereich erstellt wurde.  
  
```  
SELECT * FROM sys.server_event_notifications  
WHERE name = 'log_ddl1';  
```  
  
### <a name="d-getting-information-about-an-event-notification-that-is-database-scoped"></a>D. Abrufen von Informationen zu einer Ereignisbenachrichtigung mit der Datenbank als Bereich  
 Im folgenden Beispiel wird die `sys.event_notifications`-Katalogsicht für Metadaten zur Ereignisbenachrichtigung `Notify_ALTER_T1` abgefragt, die mit dem Datenbankbereich erstellt wurde.  
  
```sql  
SELECT * FROM sys.event_notifications  
WHERE name = 'Notify_ALTER_T1';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ereignisbenachrichtigungen](../../relational-databases/service-broker/event-notifications.md)   
 [DROP EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)   
 [sys.events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)   
 [sys.server_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-events-transact-sql.md)  
  
  
