---
title: Ereignisbenachrichtigungen | Microsoft-Dokumentation
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
- event notifications, about
- events [SQL Server], notifications
ms.assetid: 4da73ca1-6c06-4e96-8ab8-2ecba30b6c86
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 01d42e113fabb39353971749462c144374e470fe
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="event-notifications"></a>Ereignisbenachrichtigungen
  Mit Ereignisbenachrichtigungen werden Informationen zu Ereignissen an einen [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dienst gesendet. Ereignisbenachrichtigungen werden als Antwort auf eine Vielzahl von [!INCLUDE[tsql](../../includes/tsql-md.md)] -DDL-Anweisungen (Data Definition Language, Datendefinitionssprache) und Ereignissen der SQL-Ablaufverfolgung ausgeführt, indem Informationen zu diesen Ereignissen an einen [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dienst gesendet werden.  
  
 Ereignisbenachrichtigungen können für die folgenden Aufgaben verwendet werden:  
  
-   Protokollieren und Prüfen von Änderungen oder Aktivitäten, die für die Datenbank auftreten.  
  
-   Ausführen einer Aktion als Antwort auf ein Ereignis auf asynchrone statt auf synchrone Weise.  
  
 Ereignisbenachrichtigungen können eine Programmieralternative zu DDL-Triggern und zur SQL-Ablaufverfolgung bieten.  
  
## <a name="event-notifications-benefits"></a>Vorteile von Ereignisbenachrichtigungen  
 Ereignisbenachrichtigungen werden asynchron außerhalb des Bereichs einer Transaktion ausgeführt. Im Gegensatz zu DDL-Triggern können Ereignisbenachrichtigungen deshalb in einer Datenbankanwendung als Reaktion auf Ereignisse verwendet werden, ohne Ressourcen zu belegen, die von der unmittelbaren Transaktion definiert werden.  
  
 Im Gegensatz zur SQL-Ablaufverfolgung kann mithilfe von Ereignisbenachrichtigungen eine Aktion innerhalb einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz als Antwort auf ein Ereignis der SQL-Ablaufverfolgung ausgeführt werden.  
  
 Ereignisdaten können von Anwendungen, die zusammen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt werden, zum Nachverfolgen des Fortschritts sowie zum Treffen von Entscheidungen verwendet werden. Die folgende Ereignisbenachrichtigung sendet z. B. bei jeder Ausgabe einer `ALTER TABLE` -Anweisung in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank eine Benachrichtigung an einen bestimmten Dienst:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE '//Adventure-Works.com/ArchiveService' ,  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
## <a name="event-notifications-concepts"></a>Konzepte der Ereignisbenachrichtigungen  
 Wenn eine Ereignisbenachrichtigung erstellt wird, werden eine oder mehrere [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Konversationen zwischen einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und dem von Ihnen angegebenen Zieldienst geöffnet. Die Konversationen bleiben in der Regel geöffnet, so lange die Ereignisbenachrichtigung als Objekt für die Serverinstanz vorhanden ist. In einigen Fehlerfällen können die Konversationen geschlossen werden, bevor die Ereignisbenachrichtigung gelöscht wird. Diese Konversationen werden niemals für Ereignisbenachrichtigungen freigegeben. Jede Ereignisbenachrichtigung besitzt ihre eigenen, exklusiven Konversationen. Das explizite Beenden einer Konversation verhindert, dass der Zieldienst weitere Nachrichten empfängt, und die Konversation wird bei der nächsten Auslösung der Ereignisbenachrichtigung nicht erneut geöffnet.  
  
 Ereignisinformationen werden an den [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dienst als Variable des Typs **xml** übermittelt; diese Variable stellt Informationen zum Zeitpunkt des Auftretens eines Ereignisses, zum betroffenen Datenbankobjekt, zur beteiligten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Batchanweisung sowie weitere Informationen bereit. Weitere Informationen zum XML-Schema, das von Ereignisbenachrichtigungen erstellt wird, finden Sie unter [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md).  
  
### <a name="event-notifications-vs-triggers"></a>Ereignisbenachrichtigungen im Vergleich zur Trigger  
 In der folgenden Tabelle werden Trigger und Ereignisbenachrichtigungen verglichen und Unterschiede aufgezeigt.  
  
|Trigger|Ereignisbenachrichtigungen|  
|--------------|-------------------------|  
|DML-Trigger reagieren auf DML-Ereignisse. DDL-Trigger reagieren auf DDL-Ereignisse (Data Definition Language, Datendefinitionssprache).|Ereignisbenachrichtigungen reagieren auf DDL-Ereignisse und eine Teilmenge von SQL-Ablaufverfolgungsereignissen.|  
|Trigger können verwalteten Transact-SQL- oder CLR-Code (Common Language Runtime) ausführen.|Ereignisbenachrichtigungen führen keinen Code aus. Sie senden **xml** -Nachrichten an einen Service Broker-Dienst.|  
|Trigger werden synchron innerhalb des Bereichs der Transaktionen verarbeitet, die ihre Auslösung bewirken.|Ereignisbenachrichtigungen können asynchron verarbeitet werden und werden nicht innerhalb des Bereichs der Transaktionen ausgeführt, die ihre Auslösung bewirken.|  
|Der Consumer eines Triggers ist eng mit dem Ereignis verkoppelt, das seine Auslösung bewirkt.|Der Consumer einer Ereignisbenachrichtigung ist von dem Ereignis entkoppelt, das seine Auslösung bewirkt.|  
|Trigger müssen auf dem lokalen Server verarbeitet werden.|Ereignisbenachrichtigungen können auf einem Remoteserver verarbeitet werden.|  
|Für Trigger kann ein Rollback durchgeführt werden.|Für Ereignisbenachrichtigungen kann kein Rollback durchgeführt werden.|  
|Die Namen von DML-Triggern stammen aus dem Bereich des Schemas. Die Namen von DDL-Triggern stammen aus dem Bereich der Datenbank oder des Servers.|Die Namen von Ereignisbenachrichtigungen stammen aus dem Bereich des Servers oder der Datenbank. Ereignisbenachrichtigungen für ein QUEUE_ACTIVATION-Ereignis stammen aus dem Bereich einer bestimmten Warteschlange.|  
|DML-Trigger weisen den gleichen Besitzer wie die Tabellen auf, auf die sie angewendet werden.|Der Besitzer einer Ereignisbenachrichtigung für eine Warteschlange kann einen anderen Besitzer als das Objekt aufweisen, auf das diese angewendet wird.|  
|Trigger unterstützen die EXECUTE AS-Klausel.|Ereignisbenachrichtigungen unterstützen die EXECUTE AS-Klausel nicht.|  
|Die Ereignisinformationen von DDL-Triggern können mit der EVENTDATA-Funktion aufgezeichnet werden, die einen **xml** -Datentyp zurückgibt.|Ereignisbenachrichtigungen senden **xml** -Ereignisinformationen an einen Service Broker-Dienst. Die Informationen werden für das gleiche Schema formatiert, das auch die EVENTDATA-Funktion verwendet.|  
|Metadaten zu Triggern sind in den **sys.triggers** - und **sys.server_triggers** -Katalogsichten enthalten.|Metadaten zu Ereignisbenachrichtigungen sind in den **sys.event_notifications**- und **sys.server_event_notifications**-Katalogsichten enthalten.|  
  
### <a name="event-notifications-vs-sql-trace"></a>Ereignisbenachrichtigungen im Vergleich zur SQL-Ablaufverfolgung  
 Die folgende Tabelle vergleicht das Verwenden von Ereignisbenachrichtigungen mit der SQL-Ablaufverfolgung zum Überwachen von Serverereignissen und führt die jeweiligen Merkmale auf.  
  
|SQL-Ablaufverfolgung|Ereignisbenachrichtigungen|  
|---------------|-------------------------|  
|Die SQL-Ablaufverfolgung bewirkt keinen zusätzlichen Verwaltungsaufwand, der auf Transaktionen zurückzuführen ist. Die Verpackung der Daten ist effizient.|Durch das Erstellen der als XML formatierten Ereignisdaten und Senden der Ereignisbenachrichtigung entsteht zusätzlicher Verwaltungsaufwand.|  
|Die SQL-Ablaufverfolgung kann beliebige Ablaufverfolgungs-Ereignisklassen überwachen.|Ereignisbenachrichtigungen können Untergruppen von Ablaufverfolgungs-Ereignisklassen und außerdem alle DDL-Ereignisse (Data Definition Language) überwachen.|  
|Sie können anpassen, welche Datenspalten in einem Ablaufverfolgungsereignis generiert werden sollen.|Das Schema der durch Ereignisbenachrichtigungen zurückgegebenen Ereignisdaten im XML-Format ist fest.|  
|Durch DDL generierte Ablaufverfolgungsereignisse werden unabhängig davon generiert, ob für die DDL-Anweisung ein Rollback durchgeführt wird.|Ereignisbenachrichtigungen werden nicht ausgelöst, wenn für das Ereignis in der zugehörigen DDL-Anweisung ein Rollback durchgeführt wird.|  
|Das Verwalten des Zwischenflusses der Daten der Ablaufverfolgungsereignisse beinhaltet das Auffüllen und Verwalten von Ablaufverfolgungsdateien oder -tabellen.|Die Zwischenverwaltung der Ereignisbenachrichtigungsdaten erfolgt automatisch über Service Broker-Warteschlangen.|  
|Die Ablaufverfolgung muss bei jedem Neustart des Servers ebenfalls neu gestartet werden.|Nach ihrer Registrierung sind Ereignisbenachrichtigungen serverzyklenübergreifend persistent und transaktiv.|  
|Nach der Initiierung kann das Auslösen von Ablaufverfolgungen nicht mehr gesteuert werden. Beendigungszeiten und Filterzeiten können für das Angeben des Zeitpunkts ihrer Initiierung verwendet werden. Auf Ablaufverfolgungen wird durch Abrufen der entsprechenden Ablaufverfolgungsdatei zugegriffen.|Ereignisbenachrichtigungen können mithilfe der WAITFOR-Anweisung für die Warteschlange gesteuert werden, die die Nachricht empfängt, die von der Ereignisbenachrichtigung generiert wurde. Auf diese kann durch Abrufen der Warteschlange zugegriffen werden.|  
|ALTER TRACE ist die Mindestberechtigung, die zum Erstellen einer Ablaufverfolgung erforderlich ist. Außerdem ist die Berechtigung zum Erstellen einer Ablaufverfolgungsdatei auf dem entsprechenden Computer erforderlich.|Die Mindestberechtigung hängt vom Typ der erstellten Ereignisbenachrichtigung ab. Die RECEIVE-Berechtigung wird auch für die entsprechende Warteschlange benötigt.|  
|Ablaufverfolgungen können remote empfangen werden.|Ereignisbenachrichtigungen können remote empfangen werden.|  
|Ablaufverfolgungsereignisse werden mithilfe gespeicherter Systemprozeduren implementiert.|Ereignisbenachrichtigungen werden mithilfe einer Kombination aus [!INCLUDE[ssDE](../../includes/ssde-md.md)] - und [!INCLUDE[ssSB](../../includes/sssb-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen implementiert.|  
|Auf Ablaufverfolgungsdaten kann über Programmcode durch Abfragen der entsprechenden Ablaufverfolgungstabelle, durch Analysieren der Ablaufverfolgungsdatei oder mithilfe der TraceReader-Klasse von SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) zugegriffen werden.|Auf Ereignisdaten wird über Programmcode durch Ausgeben von XQuery für die als XML formatierten Ereignisdaten oder mithilfe der SMO-Ereignisklassen zugegriffen.|  
  
## <a name="event-notification-tasks"></a>Tasks der Ereignisbenachrichtigung  
  
|Task|Thema|  
|----------|-----------|  
|Beschreibt, wie Ereignisbenachrichtigungen erstellt und implementiert werden.|[Implementieren von Ereignisbenachrichtigungen](../../relational-databases/service-broker/implement-event-notifications.md)|  
|Beschreibt, wie für Ereignisbenachrichtigungen, die Nachrichten an eine Service Broker-Instanz auf einem Remoteserver senden, die Dialogsicherheit von [!INCLUDE[ssSB](../../includes/sssb-md.md)] konfiguriert wird.|[Konfigurieren der Dialogsicherheit für Ereignisbenachrichtigungen](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)|  
|Beschreibt, wie Informationen zu Ereignisbenachrichtigungen zurückgegeben werden.|[Abrufen von Informationen zu Ereignisbenachrichtigungen](../../relational-databases/service-broker/get-information-about-event-notifications.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [DDL-Trigger](../../relational-databases/triggers/ddl-triggers.md)   
 [DML-Trigger](../../relational-databases/triggers/dml-triggers.md)   
 [SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md)  
  
  
