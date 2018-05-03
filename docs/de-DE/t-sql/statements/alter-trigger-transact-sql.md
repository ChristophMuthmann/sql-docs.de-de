---
title: ALTER TRIGGER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER TRIGGER
- ALTER_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, modifying
- triggers [SQL Server], modifying
- modifying triggers
- ALTER TRIGGER statement
- DML triggers, modifying
ms.assetid: 2a99c7c1-ac2f-4637-aa7c-3d1bf514e500
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 22022df96f4ea0093bc5353a8384a54bc79e148e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-trigger-transact-sql"></a>ALTER TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Diese Anweisung ändert die Definition eines DML-, DDL- oder LOGON-Triggers, der zuvor mit der CREATE TRIGGER-Anweisung erstellt wurde. Trigger werden mit CREATE TRIGGER erstellt. Sie können direkt aus [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen oder aus Methoden von Assemblys erstellt werden, die in der Common Language Runtime (CLR) von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] erstellt werden und durch Hochladen an eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] übertragen werden. Weitere Informationen zu den in der ALTER TRIGGER-Anweisung verwendeten Parametern finden Sie unter [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- SQL Server Syntax  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table | view )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
[ NOT FOR REPLICATION ]   
AS { sql_statement [ ; ] [ ...n ] | EXTERNAL NAME <method specifier>   
[ ; ] }   
  
<dml_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table 
-- (DML Trigger on memory-optimized tables)  

ALTER TRIGGER schema_name.trigger_name   
ON  ( table  )   
[ WITH <dml_trigger_option> [ ,...n ] ]  
 ( FOR | AFTER )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [ ...n ] }   
  
<dml_trigger_option> ::=  
    [ NATIVE_COMPILATION ]  
    [ SCHEMABINDING ]  
    [ <EXECUTE AS Clause> ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, 
-- or UPDATE statement (DDL Trigger)  
  
ALTER TRIGGER trigger_name   
ON { DATABASE | ALL SERVER }   
[ WITH <ddl_trigger_option> [ ,...n ] ]  
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement [ ; ] | EXTERNAL NAME <method specifier>   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ <EXECUTE AS Clause> ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
  
-- Trigger on a LOGON event (Logon Trigger)  

ALTER TRIGGER trigger_name   
ON ALL SERVER   
[ WITH <logon_trigger_option> [ ,...n ] ]  
{ FOR| AFTER } LOGON   
AS { sql_statement  [ ; ] [ ,...n ] | EXTERNAL NAME < method specifier >  
  [ ; ] }  
  
<logon_trigger_option> ::=  
    [ ENCRYPTION ]  
    [ EXECUTE AS Clause ]  
  
<method_specifier> ::=  
    assembly_name.class_name.method_name  
```  
  
```  
-- Windows Azure SQL Database Syntax   
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)   
  
ALTER TRIGGER schema_name. trigger_name   
ON (table | view )   
 [ WITH <dml_trigger_option> [ ,...n ] ]   
 ( FOR | AFTER | INSTEAD OF )   
{ [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] }   
AS { sql_statement [ ; ] [...n ] }   
  
<dml_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]   
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE, or UPDATE statement (DDL Trigger)   
  
ALTER TRIGGER trigger_name   
ON { DATABASE }   
 [ WITH <ddl_trigger_option> [ ,...n ] ]   
{ FOR | AFTER } { event_type [ ,...n ] | event_group }   
AS { sql_statement   
[ ; ] }  
}   
  
<ddl_trigger_option> ::=   
    [ <EXECUTE AS Clause> ]  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem ein DML-Trigger gehört. DML-Trigger werden auf das Schema der Tabelle oder der Sicht begrenzt, in denen sie erstellt werden. *schema**_name* ist nur optional, wenn der DML-Trigger und die zugehörige Tabelle oder Sicht zum Standardschema gehören. *schema_name* kann für DDL- oder LOGON-Trigger nicht angegeben werden.  
  
 *trigger_name*  
 Der vorhandene Trigger, der geändert werden soll.  
  
 *table* | *view*  
 Die Tabelle oder Sicht, für die der DML-Trigger ausgeführt wird. Das Angeben des vollqualifizierten Namens einer Tabelle oder Sicht ist optional.  
  
 DATABASE  
 Wendet den Bereich eines DDL-Triggers auf die aktuelle Datenbank an. Wenn angegeben, wird der Trigger jedes Mal ausgelöst, wenn in der aktuellen Datenbank *event_type* oder *event_group* auftritt.  
  
 ALL SERVER  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Wendet den Bereich eines DDL- oder LOGON-Triggers auf den aktuellen Server an. Wenn angegeben, wird der Trigger jedes Mal ausgelöst, wenn auf dem aktuellen Server *event_type* oder *event_group* auftritt.  
  
 WITH ENCRYPTION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Verschlüsselt die sys.syscommentssys.sql_modules-Einträge, die den Text der ALTER TRIGGER-Anweisung enthalten. Durch das Verwenden von WITH ENCRYPTION kann verhindert werden, dass der Trigger als Teil der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Replikation veröffentlicht wird. WITH ENCRYPTION kann nicht für CLR-Trigger angegeben werden.  
  
> [!NOTE]  
>  Wenn ein Trigger mit WITH ENCRYPTION erstellt wird, muss er erneut in der ALTER TRIGGER-Anweisung angegeben werden, damit diese Option aktiviert bleibt.  
  
 EXECUTE AS  
 Gibt den Sicherheitskontext an, unter dem der Trigger ausgeführt wird. Ermöglicht die Steuerung des Benutzerkontos, das die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, um die Berechtigungen für alle Datenbankobjekte zu überprüfen, auf die durch den Trigger verwiesen wird.  
  
 Weitere Informationen finden Sie unter [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 NATIVE_COMPILATION  
 Gibt an, dass die Trigger nativ kompiliert werden.  
  
 Diese Option ist für Trigger in speicheroptimierten Tabellen erforderlich.  
  
 SCHEMABINDING  
 Stellt sicher, dass Tabellen, auf die durch einen Trigger verwiesen wird, nicht gelöscht oder geändert werden können.  
  
 Diese Option ist für Trigger in speicheroptimierten Tabellen erforderlich und wird nicht für Trigger in herkömmlichen Tabellen unterstützt.  
  
 AFTER  
 Gibt an, dass der Trigger erst ausgelöst wird, nachdem die auslösende SQL-Anweisung erfolgreich ausgeführt wurde. Vor dem Auslösen dieses Triggers müssen außerdem alle für die referenzielle Integrität erforderlichen kaskadierenden Aktionen und Einschränkungsüberprüfungen erfolgreich abgeschlossen sein.  
  
 AFTER ist die Standardeinstellung, wenn nur das FOR-Schlüsselwort angegeben ist.  
  
 DML AFTER-Trigger können nur für Tabellen definiert werden.  
  
 INSTEAD OF  
 Gibt an, dass der DML-Trigger anstelle der auslösenden SQL-Anweisung ausgeführt wird, wodurch die Aktionen der auslösenden Anweisungen überschrieben werden. INSTEAD OF kann für DDL- oder LOGON-Trigger nicht angegeben werden.  
  
 Es kann nur maximal ein INSTEAD OF-Trigger pro INSERT-, UPDATE- oder DELETE-Anweisung für eine Tabelle oder Sicht definiert werden. Es ist jedoch möglich, Sichten auf Sichten zu definieren, wobei jede Sicht über einen eigenen INSTEAD OF-Trigger verfügt.  
  
 INSTEAD OF-Trigger sind in Sichten die mit WITH CHECK OPTION erstellt wurden, nicht zulässig. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] löst einen Fehler aus, wenn ein INSTEAD OF-Trigger einer Sicht hinzufügt wird, für die die WITH CHECK OPTION angegeben wurde. Der Benutzer muss die Option mithilfe von ALTER VIEW entfernen, bevor der INSTEAD OF-Trigger definiert wird.  
  
 { [ DELETE ] [ , ] [ INSERT ] [ , ] [ UPDATE ] } | { [INSERT ] [ , ] [ UPDATE ] }   
 Gibt die Datenänderungsanweisungen an, die den DML-Trigger aktivieren, wenn sie auf diese Tabelle oder Sicht angewendet werden. Es muss mindestens eine Option angegeben werden. Die Optionen können in beliebiger Kombination und Reihenfolge in der Triggerdefinition angegeben werden. Wenn Sie mehrere Optionen angeben, trennen Sie diese durch Kommas.  
  
 Für INSTEAD OF-Trigger ist die Option DELETE nicht für Tabellen mit einer referenziellen Beziehung untereinander zulässig, wenn für ON DELETE die Option CASCADE angegeben ist. Ebenso ist die Option UPDATE nicht für Tabellen mit einer referenziellen Beziehung untereinander zulässig, wenn für ON UPDATE die Option CASCADE angegeben ist. Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
 *event_type*  
 Der Name eines [!INCLUDE[tsql](../../includes/tsql-md.md)]-Sprachereignisses, nach dessen Ausführung ein DDL-Trigger ausgelöst wird. Gültige Ereignisse für DDL-Trigger werden unter [DDL-Ereignisse](../../relational-databases/triggers/ddl-events.md) aufgeführt.  
  
 *event_group*  
 Der Name einer vordefinierten Gruppe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Sprachereignissen. Der DDL-Trigger wird nach dem Ausführen eines beliebigen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Sprachereignisses ausgelöst, das zu *event_group* gehört. Gültige Ereignisgruppen für DDL-Trigger werden unter [DDL-Ereignisgruppen](../../relational-databases/triggers/ddl-event-groups.md) aufgeführt. Nach dem Ausführen von ALTER TRIGGER dient *event_group* außerdem als Makro, das der sys.trigger_events-Katalogsicht die verarbeitbaren Ereignistypen hinzufügt.  
  
 NOT FOR REPLICATION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Zeigt an, dass der Trigger nicht ausgeführt werden soll, wenn ein Replikations-Agent die vom Trigger betroffene Tabelle ändert.  
  
 *sql_statement*  
 Die Triggerbedingungen und -aktionen.  
  
 Bei Triggern in speicheroptimierten Tabellen ist auf der obersten Ebene nur ein ATOMIC-Block als *sql_statement* erlaubt. Das im ATOMIC-Block erlaubte T-SQL ist durch das in nativen Prozeduren zulässige T-SQL beschränkt.  
  
 EXTERNAL NAME \<method_specifier>  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Methode an, mit der eine Assembly eine Bindung mit dem Trigger herstellt. Die Methode darf keine Argumente enthalten und muss "void" zurückgeben. *class_name* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner sein und als Klasse mit Assemblysichtbarkeit in der Assembly vorhanden sein. Bei der Klasse darf es sich nicht um eine geschachtelte Klasse handeln.  
  
## <a name="remarks"></a>Remarks  
 Weitere Informationen zu ALTER TRIGGER finden Sie in den Hinweisen unter [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
> [!NOTE]  
>  Die EXTERNAL_NAME- und ON_ALL_SERVER-Optionen sind in einer enthaltenen Datenbank nicht verfügbar.  
  
## <a name="dml-triggers"></a>DML-Trigger  
 ALTER TRIGGER unterstützt manuell aktualisierbare Sichten durch INSTEAD OF-Trigger in Tabellen und Sichten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wendet ALTER TRIGGER analog zu allen anderen Triggern (AFTER, INSTEAD-OF) an.  
  
 Der erste und der letzte AFTER-Trigger, die für eine Tabelle ausgeführt werden sollen, können mithilfe von sp_settriggerorder angegeben werden. Nur der erste und ein letzter AFTER-Trigger können für eine Tabelle angegeben werden. Sind für eine Tabelle weitere AFTER-Trigger vorhanden, werden diese nach dem Zufallsprinzip ausgeführt.  
  
 Wenn eine ALTER TRIGGER-Anweisung den ersten oder den letzten Trigger ändert, wird das erste oder das letzte für den geänderten Trigger festgelegte Attribut gelöscht, und der Reihenfolgewert muss mithilfe von sp_settriggerorder neu festgelegt werden.  
  
 Ein AFTER-Trigger wird nur dann ausgeführt, wenn die den Trigger auslösende SQL-Anweisung erfolgreich ausgeführt wurde. Diese erfolgreiche Ausführung umfasst alle referenziellen kaskadierenden Aktionen und Einschränkungsüberprüfungen, die mit dem aktualisierten oder gelöschten Objekt verknüpft sind. Bei dem AFTER-Triggervorgang werden die Auswirkungen der auslösenden Anweisung sowie alle referenziellen kaskadierenden UPDATE- und DELETE-Aktionen geprüft, die durch die auslösende Anweisung verursacht werden.  
  
 Wenn eine DELETE-Aktion für eine untergeordnete oder verweisende Tabelle das Ergebnis einer CASCADE-Aktion für eine DELETE-Aktion aus der übergeordneten Tabelle ist und wenn für DELETE ein INSTEAD OF-Trigger für diese untergeordnete Tabelle definiert ist, wird der Trigger ignoriert und die DELETE-Aktion ausgeführt.  
  
## <a name="ddl-triggers"></a>DDL-Trigger  
 Im Gegensatz zu DML-Triggern haben DDL-Trigger keinen Schemabereich. Deshalb können OBJECT_ID, OBJECT_NAME, OBJECTPROPERTY und OBJECTPROPERTY(EX) nicht verwendet werden, wenn Metadaten zu DDL-Triggern abgefragt werden. Verwenden Sie stattdessen die Katalogsichten. Weitere Informationen finden Sie unter [Abrufen von Informationen zu DDL-Triggern](../../relational-databases/triggers/get-information-about-ddl-triggers.md).  
  
## <a name="logon-triggers"></a>Logon-Trigger  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] unterstützt keine Trigger für Anmeldeereignisse.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ändern eines DML-Triggers ist eine ALTER-Berechtigung für die Tabelle oder Sicht erforderlich, für die der Trigger definiert ist.  
  
 Zum Ändern eines DDL-Triggers, der mit einem Serverbereich (ON ALL SERVER) definiert ist, oder eines LOGON-Triggers ist die CONTROL SERVER-Berechtigung auf dem Server erforderlich. Zum Ändern eines DDL-Triggers, der mit einem Datenbankbereich (ON DATABASE ANY) definiert ist, ist die ALTER ANY DATABASE DDL TRIGGER-Berechtigung in der aktuellen Datenbank erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird in der AdventureWorks 2012-Datenbank ein DML-Trigger erstellt, der eine benutzerdefinierte Meldung an den Client ausgibt, wenn ein Benutzer versucht, der `SalesPersonQuotaHistory`-Tabelle Daten hinzuzufügen oder sie zu ändern. Der Trigger wird dann mit `ALTER TRIGGER` geändert, damit der Trigger nur für `INSERT`-Aktivitäten angewendet wird. Dieser Trigger ist hilfreich, da er den Benutzer beim Aktualisieren oder Einfügen von Zeilen in die Tabelle daran erinnert, dass auch die Abteilung `Compensation` benachrichtigt werden muss.  
  
```  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  

-- Now, change the trigger.  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [Transaktionen](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [Abrufen von Informationen zu DML-Triggern](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [Abrufen von Informationen zu DDL-Triggern](../../relational-databases/triggers/get-information-about-ddl-triggers.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
