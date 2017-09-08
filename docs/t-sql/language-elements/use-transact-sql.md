---
title: Nutzung (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/28/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USE_TSQL
- USE
dev_langs:
- TSQL
helpviewer_keywords:
- USE statement
- database context [SQL Server]
- context changes [SQL Server]
- modifying database context
ms.assetid: c05acac8-c063-4770-8e36-d7f71d500b10
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d6274293bd4caedc9cad00ad4532952e63e3e989
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="use-transact-sql"></a>USE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Ändert den Datenbankkontext in die angegebene Datenbank oder die angegebene Datenbank-Momentaufnahme in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
USE { database_name }   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank oder der Datenbankmomentaufnahme, in die der Benutzerkontext geändert wird. Datenbank und die Namen von datenbankmomentaufnahmen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] kann der Datenbankparameter nur auf die aktuelle Datenbank verweisen. Wenn eine andere Datenbank als der aktuellen Datenbank angegeben ist, wird die `USE` -Anweisung nicht zwischen Datenbanken gewechselt und der Fehlercode 40508 zurückgegeben. Um die Datenbank zu wechseln, müssen Sie eine direkte Verbindung herstellen. Die USE-Anweisung wird als gilt nicht für SQL-Datenbank am oberen Rand dieser Seite gekennzeichnet, da können, obwohl Sie verwenden die `USE` Anweisung in einem Batch nicht alles.
  
## <a name="remarks"></a>Hinweise  
 Wenn von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt wird, wird die Anmeldung automatisch mit ihrer Standarddatenbank verbunden und bekommt den Sicherheitskontext eines Datenbankbenutzers zugewiesen. Falls kein Datenbankbenutzer für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung erstellt wurde, wird die Verbindung als guest hergestellt. Verfügt der Datenbankbenutzer nicht über die CONNECT-Berechtigung für die Datenbank, meldet die USE-Anweisung einen Fehler. Falls der Anmeldung keine Standarddatenbank zugewiesen wurde, wird ihre Standarddatenbank auf master festgelegt.  
  
 USE wird zur Kompilierungszeit und zur Ausführungszeit ausgeführt und ist sofort wirksam. Deshalb werden Anweisungen, die in einem Batch nach der USE-Anweisung auftreten, in der angegebenen Datenbank ausgeführt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONNECT-Berechtigung für die Zieldatenbank.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Datenbankkontext in die `AdventureWorks2012`-Datenbank geändert.  
  
```  
USE AdventureWorks2012;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel wird der Datenbankkontext in die `AccountingDB`-Datenbank geändert.  
  
```  
USE AccountingDB;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
  



