---
title: EXECUTE AS-Klausel (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AS
- AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permission sets [SQL Server]
- queues [SQL Server]
- stored procedures [SQL Server], executing
- user-defined functions [SQL Server], execution context
- EXECUTE AS
- triggers [SQL Server], execution context
- execution context [SQL Server]
- switching execution context
- functions [SQL Server], execution context
ms.assetid: bd517aa3-f06e-4356-87d8-70de5df4494a
caps.latest.revision: 70
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b96757281a5b36755422346ef444136ad8702726
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="execute-as-clause-transact-sql"></a>EXECUTE AS-Klausel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Sie den Ausführungskontext der folgenden benutzerdefinierten Module definieren: Funktionen (außer Inline-Tabellenwertfunktionen), Prozeduren, Warteschlangen und Trigger.  
  
 Durch Angeben des Kontexts, in dem das Modul ausgeführt wird, können Sie steuern, mit welchem Benutzerkonto [!INCLUDE[ssDE](../../includes/ssde-md.md)] Berechtigungen für Objekte, auf die im Modul verwiesen wird, überprüft. Dies bietet zusätzliche Flexibilität und Kontrolle bei der Verwaltung von Berechtigungen für die Objektkette, die zwischen benutzerdefinierten Modulen und den Objekten vorhanden ist, auf die von diesen Modulen verwiesen wird. Berechtigungen müssen nur Benutzern für das Modul selbst erteilt werden, ohne dass ihnen explizite Berechtigungen für die Objekte, auf die verwiesen wird, erteilt werden müssen. Nur das Benutzerkonto, unter dem das Modul ausgeführt wird, benötigt Berechtigungen für die Objekte, auf die das Modul zugreift.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- SQL Server Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }   
  
DDL Triggers with Server Scope and logon triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'login_name' }   
  
Queues  
{ EXEC | EXECUTE } AS { SELF | OWNER | 'user_name' }   
```  
  
```  
  
-- Windows Azure SQL Database Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }  
  
```  
  
## <a name="arguments"></a>Argumente  
 **AUFRUFER**  
 Gibt an, dass die Anweisungen innerhalb des Moduls im Kontext des Aufrufers des Moduls ausgeführt werden. Der Benutzer, der das Modul ausführt, benötigt die entsprechenden Berechtigungen nicht nur für das Modul selbst, sondern auch für alle Datenbankobjekte, auf die das Modul verweist.  
  
 CALLER ist der Standardwert für alle Module außer Warteschlangen, was dem Verhalten von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] entspricht.  
  
 CALLER kann in einer CREATE QUEUE- oder ALTER QUEUE-Anweisung nicht angegeben werden.  
  
 **SELF-SERVICE**  
 EXECUTE AS SELF ist gleichbedeutend mit EXECUTE AS *User_name*, wobei der angegebene Benutzer die Person, die das Modul erstellt oder ändert. Befindet sich die tatsächlichen Benutzer-ID der Person erstellen oder ändern die Module in der **Execute_as_principal_id** Spalte in der **sql_modules** oder **Sys. service_queues** -Katalogsicht.  
  
 SELF ist der Standardwert für Warteschlangen.  
  
> [!NOTE]  
>  So ändern Sie die Benutzer-ID, der die **Execute_as_principal_id** in der **Sys. service_queues** Katalogsicht, müssen Sie explizit die EXECUTE AS-Einstellung in der ALTER QUEUE-Anweisung angeben.  
  
 OWNER  
 Gibt an, dass die Anweisungen innerhalb des Moduls im Kontext des aktuellen Besitzers des Moduls ausgeführt werden. Falls für das Modul kein Besitzer angegeben ist, wird der Besitzer des Modulschemas verwendet. OWNER kann für DDL- oder LOGON-Trigger nicht angegeben werden.  
  
> [!IMPORTANT]  
>  OWNER muss einem Singleton-Konto zugeordnet werden und darf keine Rolle oder Gruppe sein.  
  
 **"** *User_name* **"**  
 Gibt an, führen Sie die Anweisungen innerhalb des Moduls im Kontext des Benutzers im angegebenen *User_name*. Berechtigungen für Objekte innerhalb des Moduls werden gegen überprüft *User_name*. *USER_NAME* kann nicht für DDL-Trigger mit Serverbereich oder Logon-Trigger angegeben werden. Verwendung *Login_name* stattdessen.  
  
 *USER_NAME* muss in der aktuellen Datenbank vorhanden sein und muss ein Singleton-Konto sein. *USER_NAME* nicht mit einer Gruppe, Rolle, Zertifikat, Schlüssel oder integriertes Konto, z. B. NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService oder NT AUTHORITY\LocalSystem.  
  
 Die Benutzer-ID des Ausführungskontexts wird in den Metadaten gespeichert und angezeigt werden können, der **Execute_as_principal_id** Spalte in der **sql_modules** oder **Sys. assembly_modules** -Katalogsicht.  
  
 **"** *Login_name* **"**  
 Gibt an, führen Sie die Anweisungen innerhalb des Moduls im Rahmen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angegebenen Benutzernamen *Login_name*. Berechtigungen für Objekte innerhalb des Moduls werden gegen überprüft *Login_name*. *Login_name* können nur für DDL-Trigger mit Serverbereich oder Logon-Trigger auf Serverebene angegeben werden.  
  
 *Login_name* nicht mit einer Gruppe, Rolle, Zertifikat, Schlüssel oder integriertes Konto, z. B. NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService oder NT AUTHORITY\LocalSystem.  
  
## <a name="remarks"></a>Hinweise  
 Wie [!INCLUDE[ssDE](../../includes/ssde-md.md)] Berechtigungen für Objekte auswertet, auf die im Modul verwiesen wird, hängt von der Besitzkette ab, die zwischen den aufrufenden Objekten und den Objekten vorhanden ist, auf die verwiesen wird. In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] war die Besitzverkettung die einzig verfügbare Methode, um zu vermeiden, dass dem aufrufenden Benutzer der Zugriff für alle Objekte, auf die verwiesen wird, erteilt werden muss.  
  
 Für die Besitzverkettung gelten die folgenden Einschränkungen:  
  
-   Gilt nur für DML-Anweisungen: SELECT, INSERT, UPDATE und DELETE.  
  
-   Die Besitzer der aufrufenden Objekte und der aufgerufenen Objekte, müssen identisch sein.  
  
-   Gilt nicht für dynamische Abfragen innerhalb des Moduls.  
  
 Die folgenden Aktionen werden immer angewendet, unabhängig vom Ausführungskontext, der im Modul angegeben ist:  
  
-   Wenn das Modul ausgeführt wird, überprüft [!INCLUDE[ssDE](../../includes/ssde-md.md)] zunächst, ob der Benutzer, der das Modul ausführt, die EXECUTE-Berechtigung für das Modul besitzt.  
  
-   Besitzverkettungsregeln werden weiterhin angewendet. Das heißt, wenn die Besitzer der aufrufenden und der aufgerufenen Objekte identisch sind, werden keine Berechtigungen der zugrunde liegenden Objekte überprüft.  
  
 Wenn ein Benutzer ein Modul ausführt, für das die Ausführung in einem anderen Kontext als CALLER definiert wurde, wird die Berechtigung des Benutzers zum Ausführen des Moduls überprüft. Zusätzliche Berechtigungsüberprüfungen für Objekte, auf die das Modul zugreift, werden jedoch für das Benutzerkonto ausgeführt, das in der EXECUTE AS-Klausel angegeben ist. Der Benutzer, der das Modul ausführt, nimmt die Identität des angegebenen Benutzers an.  
  
 Der in der EXECUTE AS-Klausel des Moduls angegebene Kontext ist nur während der Ausführung des Moduls gültig. Der Kontext des Aufrufers wird wiederhergestellt, wenn die Ausführung des Moduls abgeschlossen ist.  
  
## <a name="specifying-a-user-or-login-name"></a>Angeben eines Benutzer- oder Anmeldenamens  
 Ein Datenbankbenutzer oder Serveranmeldename, der in der EXECUTE AS-Klausel eines Moduls angegeben ist, kann erst gelöscht werden, wenn das Modul zur Ausführung unter einem anderen Kontext geändert wird.  
  
 In EXECUTE AS-Klausel angegebene Name Benutzer- oder Anmeldename muss vorhanden sein, als Prinzipal in **Sys. database_principals** oder **Sys. server_principals**, bzw. oder anderen erstellen oder Ändern der Modul-Vorgang fehl . Darüber hinaus benötigt der Benutzer, der das Modul erstellt oder ändert, IMPERSONATE-Berechtigungen für den Prinzipal.  
  
 Falls der Benutzer impliziten Zugriff auf die Datenbank oder Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] über eine Windows-Gruppenmitgliedschaft hat, wird der in der EXECUTE AS-Klausel angegebene Benutzer beim Erstellen des Moduls implizit erstellt. Dazu muss eine der folgenden Anforderungen erfüllt sein:  
  
-   Der angegebene Benutzer oder Anmeldename ist ein Mitglied der **Sysadmin** festen Serverrolle "".  
  
-   Der Benutzer, der das Modul erstellt, hat die Berechtigung zum Erstellen von Prinzipalen.  
  
 Wenn keine dieser Anforderungen erfüllt ist, wird für den Vorgang zum Erstellen des Moduls ein Fehler gemeldet.  
  
> [!IMPORTANT]  
>  Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)-Dienst als lokales Konto (lokaler Dienst oder lokales Benutzerkonto) ausgeführt wird, hat er keine Privilegien zum Erhalten der Gruppenmitgliedschaften eines Windows-Domänenkontos, das in der EXECUTE AS-Klausel angegeben ist. Deshalb wird die Ausführung des Moduls fehlschlagen.  
  
 Stellen Sie sich z. B. folgende Bedingungen vor:  
  
-   **Die CompanyDomain\SQLUsers** -Gruppe hat Zugriff auf die **Sales** Datenbank.  
  
-   **CompanyDomain\SqlUser1** Mitglied **SQLUsers** und aus diesem Grund hat Zugriff auf die **Sales** Datenbank.  
  
-   Der Benutzer, der das Modul erstellt oder ändert, hat Berechtigungen zum Erstellen von Prinzipalen.  
  
 Wenn die folgende `CREATE PROCEDURE`-Anweisung ausgeführt wird, wird `CompanyDomain\SqlUser1` implizit als Datenbankprinzipal in der `Sales`-Datenbank erstellt.  
  
```  
USE Sales;  
GO  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'CompanyDomain\SqlUser1'  
AS  
SELECT user_name();  
GO  
```  
  
## <a name="using-execute-as-caller-stand-alone-statement"></a>Verwenden der eigenständigen EXECUTE AS CALLER-Anweisung  
 Verwenden Sie die eigenständige EXECUTE AS CALLER-Anweisung innerhalb eines Moduls, um den Ausführungskontext auf den Aufrufer des Moduls festzulegen.  
  
 Angenommen, die folgende gespeicherte Prozedur wird von `SqlUser2` aufgerufen.  
  
```  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'SqlUser1'  
AS  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
EXECUTE AS CALLER;  
SELECT user_name(); -- Shows execution context is set to SqlUser2, the caller of the module.  
REVERT;  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
GO  
```  
  
## <a name="using-execute-as-to-define-custom-permission-sets"></a>Verwenden von EXECUTE AS zum Definieren benutzerdefinierter Berechtigungssätze  
 Das Angeben eines Ausführungskontexts für ein Modul kann äußerst hilfreich sein, wenn Sie benutzerdefinierte Berechtigungssätze definieren möchten. Beispielsweise weisen bestimmte Aktionen wie etwa TRUNCATE TABLE keine erteilbaren Berechtigungen auf. Sie können die TRUNCATE TABLE-Anweisung innerhalb eines Moduls integrieren und angeben, dass dieses Modul als Benutzer mit Berechtigungen zum Ändern der Tabelle ausgeführt wird. Dadurch können Sie die Berechtigungen zum Abschneiden der Tabelle auf den Benutzer erweitern, dem Sie EXECUTE-Berechtigungen für das Modul erteilen.  
  
 Verwenden Sie zum Anzeigen der Definition des Moduls mit dem angegebenen Ausführungskontext der [Sys. sql_modules &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) -Katalogsicht angezeigt.  
  
## <a name="best-practice"></a>Bewährte Methoden  
 Geben Sie einen Anmeldenamen oder einen Benutzer an, der die mindestens erforderlichen Privilegien zum Ausführen der im Modul definierten Vorgänge aufweist. Geben Sie z. B. kein Datenbankbesitzer-Konto an, außer diese Berechtigungen sind erforderlich.  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Ausführung eines mit EXECUTE AS angegebenen Moduls benötigt der Aufrufer EXECUTE-Berechtigungen für das Modul.  
  
 Für die Ausführung eines mit EXECUTE AS angegebenen CLR-Moduls, das auf Ressourcen in einer anderen Datenbank oder auf einem anderen Server zugreift, muss die Zieldatenbank oder der Server dem Authentifikator der Datenbank vertrauen, aus der das Modul stammt (die Quelldatenbank).  
  
 Zum Angeben der EXECUTE AS-Klausel beim Erstellen oder Ändern eines Moduls benötigen Sie IMPERSONATE-Berechtigungen für den angegebenen Prinzipal sowie Berechtigungen zum Erstellen des Moduls. Sie können immer Ihre eigene Identität annehmen. Wenn kein Ausführungskontext angegeben ist, oder EXECUTE AS CALLER angegeben ist, sind keine IMPERSONATE-Berechtigungen erforderlich.  
  
 Angeben einer *Login_name* oder *User_name* , der impliziten Zugriff auf die Datenbank über eine Windows-Gruppenmitgliedschaft hat, benötigen Sie CONTROL-Berechtigungen für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine gespeicherte Prozedur in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank erstellt und der Ausführungskontext `OWNER` zugewiesen.  
  
```  
CREATE PROCEDURE HumanResources.uspEmployeesInDepartment   
@DeptValue int  
WITH EXECUTE AS OWNER  
AS  
    SET NOCOUNT ON;  
    SELECT e.BusinessEntityID, c.LastName, c.FirstName, e.JobTitle  
    FROM Person.Person AS c   
    INNER JOIN HumanResources.Employee AS e  
        ON c.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS edh  
        ON e.BusinessEntityID = edh.BusinessEntityID  
    WHERE edh.DepartmentID = @DeptValue  
    ORDER BY c.LastName, c.FirstName;  
GO  
  
-- Execute the stored procedure by specifying department 5.  
EXECUTE HumanResources.uspEmployeesInDepartment 5;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Sys. service_queues &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-service-queues-transact-sql.md)   
 [Wiederherstellen &#40; Transact-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [Führen Sie AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  

