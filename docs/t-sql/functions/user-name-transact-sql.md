---
title: USER_NAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USER_NAME
- USER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- IDs [SQL Server], databases
- USER_NAME function
- users [SQL Server], database username
- names [SQL Server], database users
- identification numbers [SQL Server], databases
- database usernames [SQL Server]
ms.assetid: ab32d644-4228-449a-9ef0-5a975c305775
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 74040ef26d016301cb861c1f1b8e395fe897196d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="username-transact-sql"></a>USER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen Datenbank-Benutzernamen über eine angegebene ID zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
USER_NAME ( [ id ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *id*  
 Die ID, die einem Datenbankbenutzer zugeordnet ist. *id* ist vom Datentyp **int**. Die Klammern sind erforderlich.  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar(256)**  
  
## <a name="remarks"></a>Remarks  
 Wenn *id* nicht angegeben ist, wird der aktuelle Benutzer im aktuellen Kontext vermutet. Wenn der Parameter das Wort NULL enthalten ist, wird NULL zurückgegeben. Wenn USER_NAME aufgerufen wird, ohne nach einer EXECUTE AS-Anweisung eine *d* anzugeben, gibt USER_NAME den Namen des Benutzers zurück, dessen Identität angenommen wurde. Falls ein Windows-Prinzipal über eine Mitgliedschaft in einer Gruppe auf die Datenbank zugreift, gibt USER_NAME den Namen des Windows-Prinzipals anstelle der Gruppe zurück.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-username"></a>A. Verwenden von USER_NAME  
 Im folgenden Beispiel wird der Benutzername für die Benutzer-ID `13` zurückgegeben.  
  
```  
SELECT USER_NAME(13);  
GO  
```  
  
### <a name="b-using-username-without-an-id"></a>B. Verwenden von USER_NAME ohne ID  
 Das folgende Beispiel sucht nach dem Namen des aktuellen Benutzers, ohne eine ID anzugeben.  
  
```  
SELECT USER_NAME();  
GO  
```  
  
 Im Folgenden wird das Resultset für einen Benutzer aufgeführt, der Mitglied der festen sysadmin-Serverrolle ist:  
  
 ```
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="c-using-username-in-the-where-clause"></a>C. Verwenden von USER_NAME in der WHERE-Klausel  
 Das folgende Beispiel findet in der `sysusers`-Tabelle diejenige Zeile, in der der Name mit dem Ergebnis der `USER_NAME`-Systemfunktion (angewendet auf Benutzer-ID `1`) übereinstimmt.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
name  
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="d-calling-username-during-impersonation-with-execute-as"></a>D. Aufrufen von USER_NAME während des Identitätswechsels mit EXECUTE AS  
 Das folgende Beispiel zeigt, wie sich `USER_NAME` während des Identitätswechsels verhält.  
  
```  
SELECT USER_NAME();  
GO  
EXECUTE AS USER = 'Zelig';  
GO  
SELECT USER_NAME();  
GO  
REVERT;  
GO  
SELECT USER_NAME();  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
DBO  
Zelig  
DBO
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="e-using-username-without-an-id"></a>E. Verwenden von USER_NAME ohne ID  
 Das folgende Beispiel sucht nach dem Namen des aktuellen Benutzers, ohne eine ID anzugeben.  
  
```  
SELECT USER_NAME();  
```  
  
 Nachfolgend finden Sie das Resultset für einen zum aktuellen Zeitpunkt angemeldeten Benutzer.  
  
```  
------------------------------   
User7                              
```  
  
### <a name="f-using-username-in-the-where-clause"></a>F. Verwenden von USER_NAME in der WHERE-Klausel  
 Das folgende Beispiel findet in der `sysusers`-Tabelle diejenige Zeile, in der der Name mit dem Ergebnis der `USER_NAME`-Systemfunktion (angewendet auf Benutzer-ID `1`) übereinstimmt.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
name                             
------------------------------   
User7                              
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact-SQL&#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40;Transact-SQL&#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)  
  
  

