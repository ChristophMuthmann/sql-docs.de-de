---
title: DROP USER (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_USER_TSQL
- DROP USER
dev_langs:
- TSQL
helpviewer_keywords:
- dropping users
- DROP USER statement
- deleting users
- database user removal [SQL Server]
- removing users
- users [SQL Server], removing
ms.assetid: d6e0e21a-7568-4321-b6d6-bcfba183a719
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7d1af03b517cbef82d0ed1c9f7affb6b7d6eda21
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-user-transact-sql"></a>DROP USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt einen Benutzer aus der aktuellen Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP USER [ IF EXISTS ] user_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP USER user_name  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).  
  
 Bedingt löscht den Benutzer nur dann, wenn sie bereits vorhanden ist.  
  
 *Benutzername*  
 Gibt den Namen an, mit dem der Benutzer innerhalb dieser Datenbank identifiziert wird.  
  
## <a name="remarks"></a>Hinweise  
 Benutzer, die Besitzer sicherungsfähiger Elemente sind, können nicht aus der Datenbank gelöscht werden. Vor dem Löschen eines Datenbankbenutzers, der sicherungsfähige Elemente besitzt, müssen Sie zuerst den Besitz dieser sicherungsfähigen Elemente löschen oder übertragen.  
  
 Der guest-Benutzer kann nicht gelöscht, aber deaktiviert werden. Zu diesem Zweck heben Sie die CONNECT-Berechtigung auf, indem Sie REVOKE CONNECT FROM GUEST in einer beliebigen Datenbank außer master oder tempdb ausführen.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY USER-Berechtigung in der Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Datenbankbenutzer `AbolrousHazem` aus der `AdventureWorks2012`-Datenbank entfernt.  
  
```  
DROP USER AbolrousHazem;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  

