---
title: HAS_DBACCESS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAS_DBACCESS_TSQL
- HAS_DBACCESS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- permissions [SQL Server], user access status
- HAS_DBACCESS
- checking permission status
- verifying permission status
- users [SQL Server], access rights status
- testing permissions
- status information [SQL Server], user access
ms.assetid: 99b43a72-0722-4a7b-a493-bdee1c74c7b9
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: efb5681a5ca390fb2c00033dbbfc70c27ae9544e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="hasdbaccess-transact-sql"></a>HAS_DBACCESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt Informationen über den Zugriff des Benutzers auf die angegebene Datenbank zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
HAS_DBACCESS ( 'database_name' )  
```  
  
## <a name="arguments"></a>Argumente  
 "*Database_name*"  
 Der Name der Datenbank, für die der Benutzer Zugriffsinformationen wünscht. *database_name* ist **sysname**  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 HAS_DBACCESS gibt 1 zurück, wenn der Benutzer Zugriff auf die Datenbank hat, 0, wenn der Benutzer keinen Zugriff auf die Datenbank hat, und NULL, wenn der Datenbankname ungültig ist.  
  
 HAS_DBACCESS gibt 0 zurück, wenn die Datenbank offline oder fehlerverdächtig ist.  
  
 HAS_DBACCESS gibt 0 zurück, wenn sich die Datenbank im Einzelbenutzermodus befindet und die Datenbank von einem anderen Benutzer verwendet wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird getestet, ob der aktuelle Benutzer Zugriff auf die `AdventureWorks2012`-Datenbank hat.  
  
```  
SELECT HAS_DBACCESS('AdventureWorks2012');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel wird getestet, ob der aktuelle Benutzer Zugriff auf die `AdventureWorksPDW2012`-Datenbank hat.  
  
```  
SELECT HAS_DBACCESS('AdventureWorksPDW2012');  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)  
  
  


