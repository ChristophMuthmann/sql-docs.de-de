---
title: "DDL-Trigger | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-ddl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "DDL-Trigger, Informationen zu DDL-Triggern"
ms.assetid: 1a4a6564-9820-4a14-9305-2c0e9ea37454
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# DDL-Trigger
  DDL-Trigger werden als Reaktion auf verschiedene DDL-Ereignisse (Data Definition Language, Datendefinitionssprache) ausgeführt. Diese Ereignisse entsprechen hauptsächlich [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die mit den Schlüsselwörtern CREATE, ALTER, DROP, GRANT, DENY, REVOKE oder UPDATE STATISTICS beginnen. Bestimmte gespeicherte Systemprozeduren, die DDL-ähnliche Vorgänge ausführen, können ebenfalls DDL-Trigger auslösen.  
  
 Sie können DDL-Trigger für die folgenden Aufgaben verwenden:  
  
-   Verhindern bestimmter Änderungen am Datenbankschema  
  
-   Als Antwort auf eine Änderung im Datenbankschema soll ein bestimmtes Ereignis auftreten.  
  
-   Aufzeichnen von Änderungen oder Ereignissen im Datenbankschema  
  
> [!IMPORTANT]  
>  Testen Sie die DDL-Trigger, um ihre Reaktionen auf ausgeführte, gespeicherte Systemprozeduren zu ermitteln. Beispielsweise wird durch die CREATE TYPE-Anweisung ebenso wie durch die gespeicherte Prozedur **sp_addtype** ein DDL-Trigger ausgelöst, der für ein CREATE_TYPE-Ereignis erstellt wurde.  
  
## DDL-Triggertypen  
 DDL-Trigger für Transact-SQL  
 Ein besonderer Typ der gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur, der mindestens eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung als Reaktion auf ein Ereignis aus dem Bereich des Servers oder der Datenbank ausführt. Beispielsweise wird ein DDL-Trigger möglicherweise ausgelöst, wenn z. B. eine ALTER SERVER CONFIGURATION-Anweisung ausgeführt wird, oder wenn eine Tabelle mit DROP TABLE gelöscht wird.  
  
 CLR-DDL-Trigger  
 Anstatt eine gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur auszuführen, führt ein CLR-Trigger eine oder mehrere Methoden aus, die in verwaltetem Code geschrieben wurden und Elemente einer Assembly sind, die in .NET Framework erstellt und in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hochgeladen werden.  
  
 DDL-Trigger werden nur ausgelöst, nachdem die DDL-Anweisungen ausgeführt werden, die diese Trigger auslösen. DDL-Trigger können nicht als INSTEAD OF-Trigger verwendet werden. DDL-Trigger werden nicht als Antwort auf Ereignisse ausgelöst, die sich auf lokale oder globale temporäre Tabellen und gespeicherte Prozeduren auswirken.  
  
 DDL-Trigger erstellen nicht die speziellen **inserted** - und **deleted** -Tabellen.  
  
 Die Informationen zu einem Ereignis, das einen DDL-Trigger auslöst, sowie zu den nachfolgenden Änderungen, die der Trigger verursacht, werden mit der EVENTDATA-Funktion aufgezeichnet.  
  
 Für jedes DDL-Ereignis sollen mehrere Trigger erstellt werden.  
  
 Im Gegensatz zu DML-Triggern haben DDL-Trigger keinen Schemabereich. Aus diesem Grund können Funktionen wie OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY und OBJECTPROPERTYEX nicht verwendet werden, um Metadaten aus DDL-Triggern abzufragen. Verwenden Sie stattdessen die Katalogsichten.  
  
 DDL-Trigger im Gültigkeitsbereich des Servers werden im Objekt-Explorer von SQL Server Management Studio im Ordner **Trigger** angezeigt. Dieser Ordner befindet sich unter dem Ordner **Serverobjekte** . DDL-Trigger im Gültigkeitsbereich der Datenbanken werden im Ordner **Datenbanktrigger** angezeigt. Dieser Ordner befindet sich unter dem Ordner **Programmierbarkeit** der entsprechenden Datenbank.  
  
> [!IMPORTANT]  
>  Bösartiger Code innerhalb von Triggern kann unter ausgeweiteten Privilegien ausgeführt werden. Weitere Informationen dazu, wie Sie diese Bedrohung minimieren, finden Sie unter [Verwalten der Triggersicherheit](../../relational-databases/triggers/manage-trigger-security.md).  
  
## DDL-Trigger-Bereich  
 DDL-Trigger können als Antwort auf ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -Ereignis ausgelöst werden, das in der aktuellen Datenbank oder auf dem aktuellen Server verarbeitet wird. Der Bereich des Triggers hängt von dem Ereignis ab. Ein DDL-Trigger, der als Antwort auf ein CREATE_TABLE-Ereignis ausgelöst wird, wird z. B. bei jedem Auftreten eines CREATE_TABLE-Ereignisses in der Datenbank oder der Serverinstanz ausgelöst. Ein DDL-Trigger, der als Antwort auf ein CREATE_LOGIN-Ereignis ausgelöst wird, wird nur bei jedem Auftreten eines CREATE_LOGIN-Ereignisses in der Serverinstanz ausgelöst.  
  
 Im folgenden Beispiel wird der DDL-Trigger `safety` immer dann ausgelöst, wenn ein `DROP_TABLE`-Ereignis oder ein `ALTER_TABLE`-Ereignis in der Datenbank auftritt.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
```  
  
 Im nächsten Beispiel wird von einem DDL-Trigger eine Meldung ausgegeben, wenn ein `CREATE_DATABASE` -Ereignis für die aktuelle Serverinstanz auftritt. Für den Trigger wird beispielsweise die `EVENTDATA`-Funktion zum Abrufen des Texts der entsprechenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung verwendet. Weitere Informationen zum Verwenden von EVENTDATA mit DDL-Triggern finden Sie unter [Verwenden der EVENTDATA-Funktion](../../relational-databases/triggers/use-the-eventdata-function.md).  
  
```  
IF EXISTS (SELECT * FROM sys.server_triggers  
    WHERE name = 'ddl_trig_database')  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
  
```  
  
 Die Listen, mit denen die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen den Bereichen zugeordnet werden, die für diese angegeben werden können, stehen über die Links im Abschnitt "Auswählen einer bestimmten DDL-Anweisung für das Auslösen eines DDL-Triggers" weiter unten in diesem Thema zur Verfügung.  
  
 DDL-Trigger im Datenbankbereich werden als Objekte in der Datenbank gespeichert, in der sie erstellt werden. DDL-Trigger können in der **master**-Datenbank erstellt werden und verhalten sich ebenso wie Trigger, die in benutzerdefinierten Datenbanken erstellt wurden. Informationen über DDL-Trigger erhalten Sie, indem Sie die **sys.triggers** -Katalogsicht abfragen. Sie können **sys.triggers** innerhalb des Datenbankkontexts abfragen, in dem sie erstellt werden. Sie können jedoch auch den Datenbanknamen als Bezeichner angeben (z. B. **master.sys.triggers**).  
  
 DDL-Trigger im Gültigkeitsbereich des Servers werden als Objekte in der **master**-Datenbank gespeichert. Informationen zu DDL-Trigger im Gültigkeitsbereich des Servers erhalten Sie durch Abfragen der **sys.server_triggers**-Katalogsicht in jedem beliebigen Datenbankkontext.  
  
## Angeben einer Transact-SQL-Anweisung oder Gruppe von Anweisungen  
  
### Auswählen einer bestimmten DDL-Anweisung für das Auslösen eines DDL-Triggers  
 DDL-Trigger können so entworfen werden, dass ihre Auslösung nach der Ausführung einer oder mehrerer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen erfolgt. Im vorherigen Beispiel wird der Trigger `safety` nach einem `DROP_TABLE`-Ereignis oder einem `ALTER_TABLE`-Ereignis ausgelöst. Listen der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die für das Auslösen eines DDL-Triggers angegeben werden können, sowie den Bereich, in dem sie ausgelöst werden können, finden Sie unter [DDL-Ereignisse](../../relational-databases/triggers/ddl-events.md).  
  
### Auswählen einer vordefinierten Gruppe von DDL-Anweisungen für das Auslösen eines DDL-Triggers  
 Ein DDL-Trigger kann nach der Ausführung eines beliebigen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ereignisses ausgelöst werden, das zu einer vordefinierten Gruppe ähnlicher Ereignisse gehört.  Wenn ein DDL-Trigger z. B. nach jeder Ausführung einer CREATE TABLE-, ALTER TABLE- oder DROP TABLE-Anweisung ausgelöst werden soll, können Sie FOR DDL_TABLE_EVENTS in der CREATE TRIGGER-Anweisung angeben. Nachdem CREATE TRIGGER ausgeführt wurde, werden die von einer Ereignisgruppe abgedeckten Ereignisse der **sys.trigger_events**-Katalogsicht hinzugefügt.  
  
 Wenn in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ein Trigger für eine Ereignisgruppe erstellt wird, enthält **sys.trigger_events** keine Informationen über die Ereignisgruppe. **sys.trigger_events** enthält nur Informationen über die einzelnen von dieser Gruppe abgedeckten Ereignisse. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher speichert **sys.trigger_events** Metadaten über die Ereignisgruppe dauerhaft, für die der Trigger erstellt wird, sowie über die einzelnen Ereignisse, die die Ereignisgruppe abdeckt. Daher gelten Änderungen der von diesen Ereignisgruppen in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher abgedeckten Ereignissen nicht für DDL-Trigger, die für diese Ereignisgruppen in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] erstellt werden.  
  
 Eine Liste der vordefinierten Gruppen von DDL-Anweisungen, die für DDL-Trigger verfügbar sind, die jeweils von den Ereignisgruppen abgedeckten Anweisungen und die Bereiche, für die diese Ereignisgruppen programmiert werden können, finden Sie unter [DDL Event Groups](../../relational-databases/triggers/ddl-event-groups.md).  
  
## Verwandte Aufgaben  
  
|Task|Thema|  
|----------|-----------|  
|Beschreibt, wie DDL-Trigger erstellt, geändert, gelöscht oder deaktiviert werden.|[Implementieren von DDL-Triggern](../../relational-databases/triggers/implement-ddl-triggers.md)|  
|Beschreibt, wie ein CLR-DDL-Trigger erstellt wird.|[Erstellen von CLR-Triggern](../../relational-databases/triggers/create-clr-triggers.md)|  
|Beschreibt, wie Informationen zu DDL-Triggern zurückgegeben werden.|[Abrufen von Informationen zu DDL-Triggern](../../relational-databases/triggers/get-information-about-ddl-triggers.md)|  
|Beschreibt, wie Informationen zu einem Ereignis, das einen DDL-Trigger auslöst, mithilfe der EVENTDATA-Funktion zurückgegeben werden.|[Verwenden der EVENTDATA-Funktion](../../relational-databases/triggers/use-the-eventdata-function.md)|  
|Beschreibt, wie Triggersicherheit verwaltet wird.|[Verwalten der Triggersicherheit](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## Siehe auch  
 [DML-Trigger](../../relational-databases/triggers/dml-triggers.md)   
 [Logon-Trigger](../../relational-databases/triggers/logon-triggers.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  