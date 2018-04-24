---
title: SUSER_SNAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SUSER_SNAME_TSQL
- SUSER_SNAME
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- SIDs [SQL Server]
- SUSER_SNAME function
- users [SQL Server], logins
- logins [SQL Server], names
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- names [SQL Server], logins
ms.assetid: 11ec7d86-d429-4004-a436-da25df9f8761
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 974c880a2d8d99c1a8f37d3b2af0b13b41efebc3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="susersname-transact-sql"></a>SUSER_SNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den einer Sicherheits-ID (SID) zugeordneten Anmeldenamen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
## <a name="arguments"></a>Argumente  
 *server_user_sid*  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Entspricht der optionalen Anmeldesicherheits-ID. *server_user_sid* ist **varbinary(85)**. *server_user_sid* kann der Sicherheits-ID einer beliebigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung oder eines [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Windows-Benutzers bzw. einer -Gruppe entsprechen. Wenn *server_user_sid* nicht angegeben ist, werden Informationen zum aktuellen Benutzer zurückgegeben. Wenn der Parameter das Wort NULL enthalten ist, wird NULL zurückgegeben.  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
 SUSER_SNAME kann als DEFAULT-Einschränkung in ALTER TABLE oder CREATE TABLE verwendet werden. SUSER_SNAME kann in einer Auswahlliste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist. SUSER_SNAME muss immer von Klammern gefolgt sein, selbst wenn kein Parameter angegeben wird.  
  
 Wenn SUSER_SNAME ohne Argument aufgerufen wird, wird der Name des aktuellen Sicherheitskontexts zurückgegeben. Wenn SUSER_SNAME ohne Argument innerhalb eines Batches aufgerufen wird, der den Kontext mithilfe von EXECUTE AS gewechselt hat, wird der Name des Kontexts zurückgegeben, dessen Identität angenommen wurde. Wenn ORIGINAL_LOGIN aus einem Kontext aufgerufen wird, dessen Identität angenommen wurde, wird der Name des ursprünglichen Kontexts zurückgegeben.  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-remarks"></a>Hinweise zu [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 SUSER_NAME gibt stets den Anmeldenamen für den aktuellen Sicherheitskontext zurück.  
  
 Die SUSER_SNAME-Anweisung unterstützt nicht die Ausführung mit einem Sicherheitskontext, dessen Identität angenommen wird, durch EXECUTE AS.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-susersname"></a>A. Verwenden von SUSER_SNAME  
 Im folgenden Beispiel wird der Anmeldename für den aktuellen Sicherheitskontext zurückgegeben.  
  
```  
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-susersname-with-a-windows-user-security-id"></a>B. Verwenden von SUSER_SNAME mit der Sicherheits-ID eines Windows-Benutzers  
 Im folgenden Beispiel wird der einer Windows-Sicherheits-ID zugeordnete Anmeldename zurückgegeben.  
  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-susersname-as-a-default-constraint"></a>C. Verwenden von SUSER_SNAME als DEFAULT-Einschränkung  
 Im folgenden Beispiel wird `SUSER_SNAME` als `DEFAULT`-Einschränkung in einer `CREATE TABLE`-Anweisung verwendet.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sname_example  
(  
login_sname sysname DEFAULT SUSER_SNAME(),  
employee_id uniqueidentifier DEFAULT NEWID(),  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sname_example DEFAULT VALUES;  
GO  
```  
  
### <a name="d-calling-susersname-in-combination-with-execute-as"></a>D. Aufrufen von SUSER_SNAME in Verbindung mit EXECUTE AS  
 Dieses Beispiel zeigt das Verhalten von SUSER_SNAME beim Aufrufen aus einem Kontext, dessen Identität angenommen wurde.  
  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME();  
GO  
EXECUTE AS LOGIN = 'WanidaBenShoof';  
SELECT SUSER_SNAME();  
REVERT;  
GO  
SELECT SUSER_SNAME();  
GO  
  
```  
  
 Im Folgenden wird das Ergebnis aufgeführt:  
  
 ```
sa  
WanidaBenShoof  
sa
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="e-using-susersname"></a>E. Verwenden von SUSER_SNAME  
 Im folgenden Beispiel wird der Anmeldename für die Sicherheits-ID mit einem Wert von `0x01` zurückgegeben.  
  
```  
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>F. Zurückgeben der aktuellen Anmeldung  
 Das folgende Beispiel gibt den Anmeldenamen der aktuellen Anmeldung zurück.  
  
```  
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  

