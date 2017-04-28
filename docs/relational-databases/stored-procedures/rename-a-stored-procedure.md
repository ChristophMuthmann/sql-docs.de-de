---
title: Umbenennen einer gespeicherten Prozedur | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8082b0cdf5788bd4b96c14ff60dbd9103c27bd74
ms.lasthandoff: 04/11/2017

---
# <a name="rename-a-stored-procedure"></a>Umbenennen einer gespeicherten Prozedur
  In diesem Thema wird beschrieben, wie Sie eine gespeicherte Prozedur in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]umbenennen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **Umbenennen einer gespeicherten Prozedur mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Prozedurnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md)entsprechen.  
  
-   Beim Umbenennen einer gespeicherten Prozedur wird der Name des entsprechenden Objekts in der Definitionsspalte der **sys.sql_modules** -Katalogsicht nicht geändert. Daher empfiehlt es sich, diesen Objekttyp nicht umzubenennen. Löschen Sie die gespeicherte Prozedur stattdessen, und erstellen Sie sie unter dem neuen Namen neu.  
  
-   Das Ändern des Namens oder der Definition einer Prozedur kann dazu führen, dass abhängige Objekte fehlschlagen, wenn sie nicht entsprechend den Änderungen an der Prozedur aktualisiert werden. Weitere Informationen finden Sie unter [Anzeigen der Abhängigkeiten einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 CREATE PROCEDURE  
 Erfordert die CREATE PROCEDURE-Berechtigung für die Datenbank und die ALTER-Berechtigung für das Schema, in dem die Prozedur erstellt wird, oder die Mitgliedschaft in der festen Datenbankrolle **db_ddladmin** .  
  
 ALTER PROCEDURE  
 Erfordert die ALTER-Berechtigung für die Prozedur oder die Mitgliedschaft in der festen Datenbankrolle **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-rename-a-stored-procedure"></a>So benennen Sie eine gespeicherte Prozedur um  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, erweitern Sie die Datenbank, zu der die Prozedur gehört, und erweitern Sie dann **Programmierbarkeit**.  
  
3.  [Anzeigen der Abhängigkeiten einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
4.  Erweitern Sie **Gespeicherte Prozeduren**, klicken Sie mit der rechten Maustaste auf die umzubenennende Prozedur, und klicken Sie dann auf **Umbenennen**.  
  
5.  Ändern Sie den Namen der Prozedur.  
  
6.  Ändern Sie den Namen der Prozedur in abhängigen Objekten oder Skripts, in denen auf den Namen verwiesen wird.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-rename-a-stored-procedure"></a>So benennen Sie eine gespeicherte Prozedur um  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie eine Prozedur umbenannt wird, indem sie gelöscht und mit einem neuen Namen neu erstellt wird. Im ersten Beispiel wird die gespeicherte Prozedur `'HumanResources.uspGetAllEmployeesTest`erstellt. Im zweiten Beispiel wird die gespeicherte Prozedur in `HumanResources.uspEveryEmployeeTest`umbenannt.  
  
```tsql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspEveryEmployeeTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Ändern einer gespeicherten Prozedur](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Löschen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [Anzeigen der Definition einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Anzeigen der Abhängigkeiten einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
  
