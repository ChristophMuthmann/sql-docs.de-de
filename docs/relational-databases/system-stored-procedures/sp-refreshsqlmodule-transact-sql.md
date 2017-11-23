---
title: Sp_refreshsqlmodule (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_refreshsqlmodule_TSQL
- sp_refreshsqlmodule
dev_langs: TSQL
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- metadata [SQL Server], triggers
- metadata [SQL Server], views
- triggers [SQL Server], refreshing metadata
- views [SQL Server], refreshing metadata
- sp_refreshsqlmodule
- metadata [SQL Server], functions
- stored procedures [SQL Server], refreshing metadata
- user-defined functions [SQL Server], refreshing metadata
ms.assetid: f0022a05-50dd-4620-961d-361b1681d375
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 671088e5f0fd1a0a86af688b0c00e8cfa277831f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sprefreshsqlmodule-transact-sql"></a>sp_refreshsqlmodule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Aktualisiert die Metadaten für die angegebene nicht schemagebundene gespeicherte Prozedur, benutzerdefinierte Funktion oder Sicht, den DML-Trigger, DDL-Trigger auf Datenbankebene oder DDL-Trigger auf Serverebene in der aktuellen Datenbank. Persistente Metadaten für diese Objekte, z. B. Datentypen von Parametern, können aufgrund von Änderungen an den zugrunde liegenden Objekten veraltet sein.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_refreshsqlmodule [ @name = ] 'module_name'   
    [ , [ @namespace = ] ' <class> ' ]  
  
<class> ::=  
{  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@name=** ] **"***Modulname***"**  
 Der Name der gespeicherten Prozedur, der benutzerdefinierten Funktion, der Sicht, des DML-Triggers, des DDL-Triggers auf Datenbankebene oder des DDL-Triggers auf Serverebene. *Modulname* nicht mit eine common Language Runtime (CLR) gespeicherte Prozedur oder eine CLR-Funktion. *Modulname* darf nicht schemagebunden sein. *Modulname* ist **Nvarchar**, hat keinen Standardwert. *Modulname* kann ein mehrteiliger Bezeichner sein, aber nur auf Objekte in der aktuellen Datenbank verweisen.  
  
 [ **,** @**Namespace** =] **"** \<Klasse > **"**  
 Klasse des angegebenen Moduls. Wenn *Modulname* wird ein DDL-Trigger \<Klasse > ist erforderlich. *\<Klasse >* ist **Nvarchar**(20). Gültige Eingaben sind:  
  
|||  
|-|-|  
|DATABASE_DDL_TRIGGER||  
|SERVER_DDL_TRIGGER|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder eine Zahl ungleich Null (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_refreshsqlmodule** sollte ausgeführt werden, wenn Änderungen an den Objekten, die dem Modul zugrunde liegen vorgenommen werden, die zugehörige Definition auswirkt. Andernfalls kann das Modul bei einer Abfrage oder einem Aufruf unerwartete Ergebnisse generieren. Um eine Ansicht zu aktualisieren, verwenden Sie entweder **Sp_refreshsqlmodule** oder **Sp_refreshview** mit den gleichen Ergebnissen.  
  
 **Sp_refreshsqlmodule** wirkt sich keine Berechtigungen, erweiterte Eigenschaften oder SET-Optionen, die dem Objekt zugeordnet sind.  
  
 Um einen DDL-Trigger auf Serverebene zu aktualisieren, führen Sie diese gespeicherte Prozedur aus dem Kontext einer beliebigen Datenbank aus.  
  
> [!NOTE]  
>  Alle Signaturen, die dem Objekt zugeordnet sind werden gelöscht, wenn Sie ausführen **Sp_refreshsqlmodule**.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für das Modul und die REFERENCES-Berechtigung für alle CLR-benutzerdefinierten Typen und XML-Schemaauflistungen, auf die durch das Objekt verwiesen wird. Erfordert eine ALTER ANY DATABASE DDL TRIGGER-Berechtigung in der aktuellen Datenbank, wenn es sich beim angegebenen Modul um einen DDL-Trigger auf Datenbankebene handelt. Erfordert eine CONTROL SERVER-Berechtigung, wenn es sich beim angegebenen Modul um einen DDL-Trigger auf Serverebene handelt.  
  
 Zusätzlich ist für Module, die mit der EXECUTE AS-Klausel definiert wurden, die IMPERSONATE-Berechtigung für den angegebenen Prinzipal erforderlich. Im Allgemeinen wird beim Aktualisieren eines Objekts dessen EXECUTE AS-Prinzipal nicht geändert, es sei denn, das Modul wurde mit EXECUTE AS USER definiert und der Benutzername des Prinzipals wird jetzt zu einem anderen Benutzer aufgelöst als zur Erstellungszeit des Moduls.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-refreshing-a-user-defined-function"></a>A. Aktualisieren einer benutzerdefinierten Funktion  
 Im folgenden Beispiel wird eine benutzerdefinierte Funktion aktualisiert. In dem Beispiel werden der Aliasdatentyp `mytype` und die benutzerdefinierte Funktion `to_upper`, die `mytype` verwendet, erstellt. Anschließend wird `mytype` in `myoldtype` umbenannt, und ein neuer `mytype` wird mit einer anderen Definition erstellt. Die `dbo.to_upper`-Funktion wird aktualisiert, sodass sie auf die neue Implementierung von `mytype` verweist und nicht auf die alte.  
  
```  
-- Create an alias type.  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT 'mytype' FROM sys.types WHERE name = 'mytype')  
DROP TYPE mytype;  
GO  
  
CREATE TYPE mytype FROM nvarchar(5);  
GO  
  
IF OBJECT_ID ('dbo.to_upper', 'FN') IS NOT NULL  
DROP FUNCTION dbo.to_upper;  
GO  
  
CREATE FUNCTION dbo.to_upper (@a mytype)  
RETURNS mytype  
WITH ENCRYPTION  
AS  
BEGIN  
RETURN upper(@a)  
END;  
GO  
  
SELECT dbo.to_upper('abcde');  
GO  
  
-- Increase the length of the alias type.  
sp_rename 'mytype', 'myoldtype', 'userdatatype';  
GO  
  
CREATE TYPE mytype FROM nvarchar(10);  
GO  
  
-- The function parameter still uses the old type.  
SELECT name, type_name(user_type_id)   
FROM sys.parameters   
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh'); -- Fails because of truncation  
GO  
  
-- Refresh the function to bind to the renamed type.  
EXEC sys.sp_refreshsqlmodule 'dbo.to_upper';  
  
-- The function parameters are now bound to the correct type and the statement works correctly.  
SELECT name, type_name(user_type_id) FROM sys.parameters  
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh');  
GO  
```  
  
### <a name="b-refreshing-a-database-level-ddl-trigger"></a>B. Aktualisieren eines DDL-Triggers auf Datenbankebene  
 Im folgenden Beispiel wird ein DDL-Trigger auf Datenbankebene aktualisiert.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddlDatabaseTriggerLog' , @namespace = 'DATABASE_DDL_TRIGGER';  
GO  
```  
  
### <a name="c-refreshing-a-server-level-ddl-trigger"></a>C. Aktualisieren eines DDL-Triggers auf Serverebene  
 Im folgenden Beispiel wird ein DDL-Trigger auf Serverebene aktualisiert.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
```  
USE master;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddl_trig_database' , @namespace = 'SERVER_DDL_TRIGGER';  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_refreshview &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
