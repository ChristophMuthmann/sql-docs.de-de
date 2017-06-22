---
title: "Ändern oder Umbenennen von DML-Triggern | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- renaming triggers
- modifying triggers
- DML triggers, modifying
ms.assetid: c7317eec-c0e9-479e-a4a7-83b6b6c58d59
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2ac7956829213d52669a3408a9a64c597cafa03d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="modify-or-rename-dml-triggers"></a>Ändern oder Umbenennen von DML-Triggern
  In diesem Thema wird beschrieben, wie Sie einen DML-Trigger in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]umbenennen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **Ändern oder Umbenennen eines DML-Triggers mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie einen Trigger umbenennen, muss der Trigger in der aktuellen Datenbank vorhanden sein, und der neue Name muss den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md)entsprechen.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Es wird davon abgeraten, die gespeicherte Prozedur [sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md) zum Umbenennen eines Triggers zu verwenden. Wenn Sie Teile eines Objektnamens ändern, können Skripts und gespeicherte Prozeduren funktionsunfähig werden. Durch das Umbenennen eines Triggers wird der entsprechende Objektname in der definition-Spalte der [sys.sql_modules-Katalogsicht](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) nicht geändert. Es wird empfohlen, den Trigger stattdessen zu löschen und neu zu erstellen.  
  
-   Wenn Sie den Namen eines Objekts ändern, auf das ein DML-Trigger verweist, müssen Sie den Trigger so ändern, dass sein Text den neuen Namen widerspiegelt. Bevor Sie ein Objekt umbenennen, sollten Sie daher erst die Abhängigkeiten des Objekts anzeigen, um feststellen zu können, ob Trigger von der beabsichtigten Änderung betroffen sind.  
  
-   Sie können einen DML-Trigger auch ändern, um seine Definition zu verschlüsseln.  
  
-   Sie können die Abhängigkeiten eines Triggers mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder mit der folgenden Funktion und den Katalogsichten anzeigen:  
  
    -   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
    -   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
    -   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Zum Ändern eines DML-Triggers ist eine ALTER-Berechtigung für die Tabelle oder Sicht erforderlich, für die der Trigger definiert ist.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-modify-a-dml-trigger"></a>So ändern Sie einen DML-Trigger  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie die gewünschte Datenbank, **Tabellen**und dann die Tabelle, die den zu ändernden Trigger enthält.  
  
3.  Erweitern Sie **Trigger**, klicken Sie mit der rechten Maustaste auf den zu ändernden Trigger, und klicken Sie anschließend auf **Ändern**.  
  
4.  Ändern Sie den Trigger, und klicken Sie dann auf **Ausführen**.  
  
#### <a name="to-rename-a-dml-trigger"></a>So benennen Sie einen DML-Trigger um  
  
1.  [Löschen Sie den Trigger](../../relational-databases/triggers/delete-or-disable-dml-triggers.md) , den Sie umbenennen möchten.  
  
2.  [Erstellen Sie den Trigger neu](../../relational-databases/triggers/create-dml-triggers.md), und geben Sie dabei den neuen Namen an.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-modify-a-trigger-using-alter-trigger"></a>So ändern Sie einen Trigger mit ALTER TRIGGER  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie die folgenden Beispiele, und fügen Sie sie in das Abfragefenster ein. Führen Sie das erste Beispiel aus, um einen DML-Trigger zu erstellen, der eine benutzerdefinierte Meldung an den Client ausgibt, wenn ein Benutzer versucht, Daten in der `SalesPersonQuotaHistory` -Tabelle hinzuzufügen oder zu ändern. Führen Sie die [ALTER TRIGGER](../../t-sql/statements/alter-trigger-transact-sql.md) -Anweisung aus, um den Trigger so zu ändern, dass er nur bei `INSERT` -Aktivitäten ausgelöst wird. Dieser Trigger ist hilfreich, da er den Benutzer beim Aktualisieren oder Einfügen von Zeilen in die Tabelle daran erinnert, dass auch die Abteilung `Compensation` benachrichtigt werden muss.  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;  
GO  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
#### <a name="to-rename-a-trigger-using-drop-trigger-and-alter-trigger"></a>So benennen Sie einen Trigger mit DROP TRIGGER und ALTER TRIGGER um  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel werden die [DROP TRIGGER](../../t-sql/statements/drop-trigger-transact-sql.md) - und [ALTER TRIGGER](../../t-sql/statements/alter-trigger-transact-sql.md) -Anweisungen verwendet, um den `Sales.bonus_reminder` -Trigger in `Sales.bonus_reminder_2`umzubenennen.  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder_2  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Abrufen von Informationen zu DML-Triggern](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  
