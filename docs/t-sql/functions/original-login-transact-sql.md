---
title: ORIGINAL_LOGIN (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c49c887b85ae6c5314420f8ba93e6b1f11604818
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Anmeldenamen zurück, der eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt hat. Mit dieser Funktion können Sie die Identität des ursprünglichen Anmeldenamens in Sitzungen zurückgeben, in denen zahlreiche explizite oder implizite Kontextwechsel vorkommen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **sysname**  
  
## <a name="remarks"></a>Remarks  
 Diese Funktion kann sich bei der Überwachung der Identität des ursprünglichen Verbindungskontexts als nützlich erweisen. Während Funktionen wie [SESSION_USER](../../t-sql/functions/session-user-transact-sql.md) und [CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md) den aktuellen Ausführungskontext zurückgeben, gibt ORIGINAL_LOGIN die Identität des Anmeldenamens zurück, mit dem die erste Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der Sitzung hergestellt wurde.  
  
 Gibt NULL für [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] zurück.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wechselt der Ausführungskontext der aktuellen Sitzung vom Aufrufer der Anweisungen zu `login1`. Die Funktionen `SUSER_SNAME` und `ORIGINAL_LOGIN` werden verwendet, um den aktuellen Sitzungsbenutzer (der Benutzer, zu dem der Kontext gewechselt hat) und das ursprüngliche Anmeldekonto zurückzugeben.  
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  
