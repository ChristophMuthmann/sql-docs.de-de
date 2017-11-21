---
title: DATABASE_PRINCIPAL_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_PRINCIPAL_ID_TSQL
- DATABASE_PRINCIPAL_ID
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], principals
- principal ID numbers [SQL Server]
- DATABASE_PRINCIPAL_ID function
- IDs [SQL Server], principals
ms.assetid: 908c7dd8-c10b-4658-92f6-0224f9835dd9
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a26dcac49e19f9a0dda738e58042c83cb8e46b8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="databaseprincipalid-transact-sql"></a>DATABASE_PRINCIPAL_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die ID-Nummer eines Prinzipals in der aktuellen Datenbank zurück. Weitere Informationen zu Prinzipalen finden Sie unter [Prinzipale &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>Argumente  
*principal_name*  
Ist ein Ausdruck vom Typ **Sysname** , den Prinzipal darstellt.  
Wenn *Principal_name* wird weggelassen wird, wird die ID des aktuellen Benutzers zurückgegeben. Die Klammern sind erforderlich.
  
## <a name="return-types"></a>Rückgabetypen
**int**  
NULL, wenn der Datenbankprinzipal nicht vorhanden ist.
  
## <a name="remarks"></a>Hinweise  
DATABASE_PRINCIPAL_ID kann in einer Auswahlliste, einer WHERE-Klausel oder überall sonst verwendet werden, wo ein Ausdruck zulässig ist. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-retrieving-the-id-of-the-current-user"></a>A. Abrufen der ID des aktuellen Benutzers  
Das folgende Beispiel gibt die Datenbankprinzipal-ID des aktuellen Benutzers zurück.
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### <a name="b-retrieving-the-id-of-a-specified-database-principal"></a>B. Abrufen der ID eines angegebenen Datenbankprinzipals  
Das folgende Beispiel gibt die Datenbankprinzipal-ID für die Datenbankrolle `db_owner` zurück.
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[Berechtigungshierarchie &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  

