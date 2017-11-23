---
title: SUSER_SID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs: TSQL
helpviewer_keywords:
- logins [SQL Server], users
- SIDs [SQL Server]
- security identifiers [SQL Server]
- users [SQL Server], logins
- 15401 (Database Engine error)
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- SUSER_SID function
ms.assetid: 57b42a74-94e1-4326-85f1-701b9de53c7d
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 77c7ab84b6fe936722f0b0c18ca889922485f1fd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="susersid-transact-sql"></a>SUSER_SID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die SID (Sicherheits-ID) für den angegebenen Anmeldenamen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SUSER_SID ( [ 'login' ] [ , Param2 ] )   
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Anmeldung* **"**  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Der Anmeldename des Benutzers. *Anmeldung* ist **Sysname**. *Anmeldung*, ist optional und kann einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Benutzer oder Gruppe. Wenn *Anmeldung* ist nicht angegeben wird, werden Informationen zu den aktuellen Sicherheitskontext zurückgegeben. Wenn der Parameter das Wort NULL enthalten ist, wird NULL zurückgegeben.  
  
 *Param2*  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt an, ob der Anmeldename validiert wird. *Param2* ist vom Typ **Int** und ist optional. Wenn *Param2* gleich 0 ist, der Anmeldename nicht überprüft. Wenn *Param2* nicht angegeben als 0 (null) der Windows-Anmeldename überprüft wird, mit dem Anmeldenamen identisch sein, die in gespeicherten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-types"></a>Rückgabetypen  
 **varbinary (85)**  
  
## <a name="remarks"></a>Hinweise  
 SUSER_SID kann als DEFAULT-Einschränkung in ALTER TABLE oder CREATE TABLE verwendet werden. SUSER_SID kann in der SELECT-Liste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist. Auf SUSER_SID müssen immer Klammern folgen, selbst wenn kein Parameter angegeben wird.  
  
 Bei einem Aufruf ohne Argument gibt SUSER_SID die SID des aktuellen Sicherheitskontexts zurück. Bei einem Aufruf ohne Argument innerhalb eines Batches, bei dem der Kontext mithilfe von EXECUTE AS gewechselt wurde, gibt SUSER_SID die SID des Kontexts an, dessen Identität angenommen wurde. Wenn SUSER_SID(ORIGINAL_LOGIN()) aus einem Kontext aufgerufen wird, dessen Identität angenommen wurde, wird die SID des ursprünglichen Kontexts zurückgegeben.  
  
 Unterscheiden sich die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierung und die Windows-Sortierung, kann SUSER_SID fehlschlagen, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Windows die Anmeldung in einem unterschiedlichen Format speichern. Falls der Windows-Computer "TestComputer" z. B. über den Anmeldenamen "User" verfügt und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anmeldung als TESTCOMPUTER\User speichert, kann die Suche nach der Anmeldung "TestComputer\User" den Anmeldenamen ggf. nicht richtig auflösen. Um diese Überprüfung des Anmeldenamens zu überspringen, verwenden Sie *Param2*. Abweichende Sortierungen sind häufig die Ursache für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehler 15401:  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-susersid"></a>A. Verwenden von SUSER_SID  
 Im folgenden Beispiel wird die Sicherheits-ID (SID) für den aktuellen Sicherheitskontext zurückgegeben.  
  
```  
SELECT SUSER_SID('sa');  
```  
  
### <a name="b-using-susersid-with-a-specific-login"></a>B. Verwenden von SUSER_SID mit bestimmten Anmeldedaten  
 Im folgende Beispiel gibt die Sicherheits-ID für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa` Anmeldung.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-susersid-with-a-windows-user-name"></a>C. Verwenden von SUSER_SID mit einem Windows-Benutzernamen  
 Im folgenden Beispiel wird die Sicherheits-ID für den Windows-Benutzer `London\Workstation1` zurückgegeben.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('London\Workstation1');  
GO  
```  
  
### <a name="d-using-susersid-as-a-default-constraint"></a>D. Verwenden von SUSER_SID als DEFAULT-Einschränkung  
 Im folgenden Beispiel wird `SUSER_SID` als `DEFAULT`-Einschränkung in einer `CREATE TABLE`-Anweisung verwendet.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sid_example  
(  
login_sid   varbinary(85) DEFAULT SUSER_SID(),  
login_name  varchar(30) DEFAULT SYSTEM_USER,  
login_dept  varchar(10) DEFAULT 'SALES',  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sid_example DEFAULT VALUES;  
GO  
```  
  
### <a name="e-comparing-the-windows-login-name-to-the-login-name-stored-in-sql-server"></a>E. Vergleichen des Windows-Anmeldenamens mit dem in SQL Server gespeicherten Anmeldenamen  
 Das folgende Beispiel zeigt, wie Sie *Param2* zum Abrufen der SID von Windows und verwendet diese SID als Eingabe für die `SUSER_SNAME` Funktion. Im Beispiel wird die Anmeldung in dem Format verwendet, in dem sie unter Windows gespeichert ist (`TestComputer\User`). Die Anmeldung wird dann in dem Format zurückgegeben, in dem sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert ist (`TESTCOMPUTER\User`).  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ORIGINAL_LOGIN &#40; Transact-SQL &#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Binary und Varbinary &#40; Transact-SQL &#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [Systemfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
