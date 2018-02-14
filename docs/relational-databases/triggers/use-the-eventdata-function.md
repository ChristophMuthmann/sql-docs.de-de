---
title: Verwenden der EVENTDATA-Funktion | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: triggers
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EVENTDATA function
- DDL triggers, EVENTDATA function
ms.assetid: 675b8320-9c73-4526-bd2f-91ba42c1b604
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 049d6eb85ebd1fcbbfecb1d64ec507979a0026f1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="use-the-eventdata-function"></a>Verwenden der EVENTDATA-Funktion
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
Informationen zu einem Ereignis, das einen DDL-Trigger auslöst, werden mit der EVENTDATA-Funktion erfasst. Diese Funktion gibt einen **xml** -Wert zurück. Das XML-Schema schließt Informationen zu folgenden Punkten ein:  
  
-   Zeitpunkt des Ereignisses.  
  
-   Die SPID (System Process ID) der Verbindung, als der Trigger ausgeführt wurde.  
  
-   Der Typ des Ereignisses, die den Trigger ausgelöst haben.  
  
 Abhängig vom Ereignistyp schließt das Schema dann weitere Informationen ein, z. B. die Datenbank, in der das Ereignis aufgetreten ist, das Objekt, für das das Ereignis erfolgte, und die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung des Ereignisses. Weitere Informationen finden Sie unter [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md).  
  
 Der folgende DDL-Trigger wird z. B. in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank erstellt:  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
```  
  
 Anschließend wird die folgende `CREATE TABLE` -Anweisung ausgeführt:  
  
 `CREATE TABLE NewTable (Column1 int);`  
  
 Die `EVENTDATA()` -Anweisung im DDL-Trigger erfasst den Text der `CREATE TABLE` -Anweisung, die nicht zulässig ist. Dies erfolgt mithilfe einer XQuery-Anweisung für die von EVENTDATA generierten **xml**-Daten und durch Abrufen des \<CommandText>-Elements. Weitere Informationen finden Sie unter [XQuery-Sprachreferenz &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md).  
  
> [!CAUTION]  
>  EVENTDATA erfasst die Daten von CREATE_SCHEMA-Ereignissen sowie den <schema_element>-Text der entsprechenden CREATE SCHEMA-Definition, sofern vorhanden. Darüber hinaus erkennt EVENTDATA die <schema_element>-Definition als ein gesondertes Ereignis. Deshalb ist es möglich, dass ein DDL-Trigger erstellt wurde, der für ein CREATE_SCHEMA-Ereignis sowie für ein Ereignis, das durch den <schema_element>-Text der CREATE SCHEMA-Definition dargestellt wird, möglicherweise dieselben Ereignisdaten doppelt zurückgibt, wie z. B. die `TSQLCommand`-Daten. Angenommen, ein DDL-Trigger wird für die Ereignisse CREATE_SCHEMA und CREATE_TABLE erstellt, und der folgende Batch wird ausgeführt:  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  Ruft die Anwendung die `TSQLCommand` -Daten des CREATE_TABLE-Ereignisses ab, sollten Sie beachten, dass diese Daten möglicherweise doppelt angezeigt werden: einmal, wenn das CREATE_SCHEMA-Ereignis stattfindet, und ein zweites Mal, wenn das CREATE_TABLE-Ereignis stattfindet. Vermeiden Sie das Erstellen von DDL-Triggern sowohl für die CREATE_SCHEMA-Ereignisse als auch für die <schema_element>-Texte entsprechender CREATE SCHEMA-Definitionen, oder integrieren Sie eine Logik in die Anwendung, damit dasselbe Ereignis nicht doppelt verarbeitet wird.  
  
## <a name="alter-table-and-alter-database-events"></a>ALTER TABLE-Ereignis und ALTER DATABASE-Ereignis  
 Die Ereignisdaten für das ALTER_TABLE-Ereignis und das ALTER DATABASE-Ereignis umfassen auch die Namen und Typen anderer Objekte, die durch die DDL-Anweisung betroffen sind, sowie die Aktionen, die für diese Objekte ausgeführt werden. Die Daten für das ALTER_TABLE-Ereignis umfassen die Namen der Spalten, Einschränkungen oder Trigger, die durch die ALTER TABLE-Anweisung betroffen sind, sowie die Aktion (Erstellen, Ändern, Löschen, Aktivieren oder Deaktivieren), die für die betroffenen Objekte ausgeführt wurde. Die Daten für das ALTER_DATABASE-Ereignis umfassen die Namen aller Dateien oder Dateigruppen, die durch die ALTER_DATABASE-Anweisung betroffen sind, sowie die Aktion (Erstellen, Ändern oder Löschen), die für die betroffenen Objekte ausgeführt wurde.  
  
 Der folgende DDL-Trigger wird beispielsweise in der AdventureWorks-Beispieldatenbank erstellt:  
  
```  
CREATE TRIGGER ColumnChanges  
ON DATABASE   
FOR ALTER_TABLE  
AS  
-- Detect whether a column was created/altered/dropped.  
SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]', 'nvarchar(max)')  
RAISERROR ('Table schema cannot be modified in this database.', 16, 1);  
ROLLBACK;  
```  
  
 Führen Sie dann die folgende ALTER TABLE-Anweisung aus, die gegen eine Einschränkung verstößt:  
  
```  
ALTER TABLE Person.Address ALTER COLUMN ModifiedDate date;   
```  
  
 Die EVENTDATA()-Anweisung im DDL-Trigger erfasst den Text der `ALTER TABLE` -Anweisung, der nicht zulässig ist.  
  
## <a name="example"></a>Beispiel  
 Mithilfe der EVENTDATA-Funktion können Sie ein Ereignisprotokoll erstellen. Im folgenden Beispiel wird eine Tabelle zum Speichern von Ereignisinformationen erstellt. Anschließend wird ein DDL-Trigger für die aktuelle Datenbank erstellt, die bei jedem Auftreten eines DDL-Ereignisses auf Datenbankebene die Tabelle mit den folgenden Informationen auffüllt:  
  
-   Zeitpunkt des Ereignisses (mithilfe der GETDATE-Funktion)  
  
-   Datenbankbenutzer, für dessen Sitzung das Ereignis aufgetreten ist (mithilfe der CURRENT_USER-Funktion)  
  
-   Typ des Ereignisses  
  
-   Die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung, die das Ereignis enthalten hat.  
  
 Die beiden letzten Elemente werden wiederum erfasst, indem XQuery für die von EVENTDATA generierten **xml** -Daten verwendet wird.  
  
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
--Test the trigger  
CREATE TABLE TestTable (a int)  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
```  
  
> [!NOTE]  
>  Zum Zurückgeben von Ereignisdaten wird die Verwendung der XQuery **value()** -Methode anstelle der **query()** -Methode empfohlen. Bei der **query()** -Methode werden XML-Daten und durch das kaufmännische Und-Zeichen geschützte CR/LF-Instanzen (Wagenrücklauf/Zeilenvorschub) in der Ausgabe zurückgegeben, während bei der **value()** -Methode CR/LF-Instanzen zurückgegeben werden, die in der Ausgabe nicht sichtbar sind.  
  
 Ein ähnliches Beispiel für einen DDL-Trigger wird mit der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank bereitgestellt. Auf das Beispiel können Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Ordner "Datenbanktrigger" zugreifen. Dieser Ordner befindet sich unter dem Ordner **Programmierbarkeit** der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Datenbank. Klicken Sie mit der rechten Maustaste auf **ddlDatabseTriggerLog** , und wählen Sie **Skript für Datenbanktrigger als**aus. Standardmäßig ist der DDL-Trigger **ddlDatabseTriggerLog** deaktiviert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DDL-Ereignisse](../../relational-databases/triggers/ddl-events.md)   
 [DDL-Ereignisgruppen](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
