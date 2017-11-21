---
title: EVENTDATA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EVENTDATA
- fn_event_data
- EVENTDATA_TSQL
- fn_event_data_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server instance event data [SQL Server]
- event notifications [SQL Server], event status
- events [SQL Server], status infromation
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
caps.latest.revision: 55
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b385ee993ab576307b6609670761deae9a7a1f6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="eventdata-transact-sql"></a>EVENTDATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu Server- oder Datenbankereignissen zurück. EVENTDATA wird beim Auslösen einer Ereignisbenachrichtigung aufgerufen, und die Ergebnisse werden an den angegebenen Service Broker zurückgegeben. EVENTDATA kann auch innerhalb des Texts eines DDL- oder LOGON-Triggers verwendet werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EVENTDATA( )  
```  
  
## <a name="remarks"></a>Hinweise  
 EVENTDATA gibt nur Daten zurück, wenn ein direkter Verweis innerhalb eines DDL- oder LOGON-Triggers vorliegt. Wenn EVENTDATA von anderen Routinen aufgerufen wird, wird auch dann NULL zurückgegeben, wenn diese Routinen von einem DDL- oder LOGON-Trigger aufgerufen wurden.  
  
 Von EVENTDATA zurückgegebene Daten sind nicht gültig, nachdem für eine Transaktion, die EVENTDATA implizit oder explizit aufgerufen hat, ein Commit oder ein Rollback ausgeführt wurde.  
  
> [!CAUTION]  
>  EVENTDATA gibt XML-Daten zurück. Diese Daten werden als Unicode an den Client gesendet; dabei werden 2 Bytes für jedes Zeichen verwendet. Die folgenden Unicode-Codeelemente können in den von EVENTDATA zurückgegebenen XML-Daten dargestellt werden:  
>   
>  `0x0009`  
>   
>  `0x000A`  
>   
>  `0x000D`  
>   
>  `>= 0x0020 && <= 0xD7FF`  
>   
>  `>= 0xE000 && <= 0xFFFD`  
>   
>  Einige Zeichen, die in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Bezeichnern und -Daten enthalten sein können, sind in XML nicht zulässig oder können nicht als XML ausgedrückt werden. Zeichen oder Daten mit Codeelementen, die in der vorhergehenden Liste nicht enthalten sind, weisen ein Fragezeichen auf (?).  
  
 Zum Schutz der Anmeldedaten werden beim Ausführen einer CREATE LOGIN-Anweisung oder ALTER LOGIN-Anweisung keine Kennwörter angezeigt.  
  
## <a name="schemas-returned"></a>Zurückgegebene Schemas  
 EVENTDATA gibt einen Wert vom Typ **Xml**. Standardmäßig wird die Schemadefinition für alle Ereignisse im folgenden Verzeichnis installiert: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd.  
  
 Alternativ können Sie das Ereignisschema an veröffentlicht wird die [Microsoft SQL Server XML-Schemas](http://go.microsoft.com/fwlink/?LinkID=31850) Webseite.  
  
 Um das Schema für ein besonderes Ereignis zu extrahieren, durchsuchen Sie das Schema nach dem komplexen Typ `EVENT_INSTANCE_\<event_type>`. Um beispielsweise das Schema für das DROP_TABLE-Ereignis zu extrahieren, durchsuchen Sie das Schema nach `EVENT_INSTANCE_DROP_TABLE`.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>A. Abfragen von Ereignisdaten in einem DDL-Trigger  
 Im folgenden Beispiel wird ein DDL-Trigger erstellt, der verhindern soll, dass neue Tabellen in der Datenbank erstellt werden. Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, die den Trigger auslöst, wird durch Verwenden eines XQuery-Ausdrucks für die von EVENTDATA generierten XML-Daten erfasst. Weitere Informationen finden Sie unter [XQuery-Sprachreferenz &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md).  
  
> [!NOTE]  
>  Bei einer Abfrage der `\<TSQLCommand>` Element mit **Ergebnisse in Raster** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Zeilenumbrüche im Befehlstext werden nicht angezeigt. Verwendung **Ergebnisse in Text** stattdessen.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value  
        ('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
GO  
--Test the trigger.  
CREATE TABLE NewTable (Column1 int);  
GO  
--Drop the trigger.  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
> [!NOTE]  
>  Wenn Sie Ereignisdaten zurückgeben möchten, wir empfehlen die Verwendung von XQuery **value()** -Methode anstelle der **query()** Methode. Die **query()** Methode zurückgibt XML und Ampersand-Escape Wagenrücklauf und Zeilenvorschub (CR/LF) Instanzen in der Ausgabe während der **value()** Methode rendert ein CR/LF-Instanzen in der Ausgabe nicht sichtbar.  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>B. Erstellen einer Protokolltabelle mit Ereignisdaten in einem DDL-Trigger  
 Im folgenden Beispiel wird eine Tabelle zum Speichern von Informationen zu Ereignissen auf allen Datenbankebenen erstellt und die Tabelle mit einem DDL-Trigger aufgefüllt. Der Ereignistyp und die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung werden mithilfe eines XQuery-Ausdrucks für alle von `EVENTDATA` generierten XML-Daten erfasst.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime datetime, DB_User nvarchar(100), Event nvarchar(100), TSQL nvarchar(2000));  
GO  
CREATE TRIGGER log   
ON DATABASE   
FOR DDL_DATABASE_LEVEL_EVENTS   
AS  
DECLARE @data XML  
SET @data = EVENTDATA()  
INSERT ddl_log   
   (PostTime, DB_User, Event, TSQL)   
   VALUES   
   (GETDATE(),   
   CONVERT(nvarchar(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'nvarchar(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(2000)') ) ;  
GO  
--Test the trigger.  
CREATE TABLE TestTable (a int);  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
--Drop the trigger.  
DROP TRIGGER log  
ON DATABASE;  
GO  
--Drop table ddl_log.  
DROP TABLE ddl_log;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden der EVENTDATA-Funktion](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [DDL-Trigger](../../relational-databases/triggers/ddl-triggers.md)   
 [Ereignisbenachrichtigungen](../../relational-databases/service-broker/event-notifications.md)   
 [Logon-Trigger](../../relational-databases/triggers/logon-triggers.md)  
  
  

