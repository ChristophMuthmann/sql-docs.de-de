---
title: USE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8c20661fce74b89b41760ef8da7c4b41e7a95049
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="use-transact-sql"></a>USE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Ändert den Datenbankkontext in die angegebene Datenbank oder die angegebene Datenbank-Momentaufnahme in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
USE { database_name }   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank oder der Datenbankmomentaufnahme, in die der Benutzerkontext geändert wird. Datenbanknamen und Namen von Datenbankmomentaufnahmen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] kann der Datenbankparameter nur auf die aktuelle Datenbank verweisen. Wenn eine andere Datenbank als die aktuelle angegeben ist, wechselt die `USE`-Anweisung nicht zwischen den Datenbanken, und der Fehlercode 40508 wird zurückgegeben. Um die Datenbank zu wechseln, müssen Sie eine direkte Verbindung herstellen. Die USE-Anweisung ist am Anfang dieser Seite als nicht zutreffend für SQL-Datenbank markiert, da nichts passiert, selbst wenn Sie die `USE`-Anweisung in einem Batch verwenden.
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
  


