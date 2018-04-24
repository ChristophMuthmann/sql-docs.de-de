---
title: DROP AGGREGATE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
caps.latest.revision: 31
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d06dcd7a23455a658dd3771457e315dcbdaca24b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt eine benutzerdefinierte Aggregatfunktion aus der aktuellen Datenbank. Benutzerdefinierte Aggregatfunktionen werden mithilfe von [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md) erstellt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>Argumente  
 *IF EXISTS*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Löscht das Aggregat nur, wenn diese bereits vorhanden ist.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die benutzerdefinierte Aggregatfunktion gehört.  
  
 *aggregate_name*  
 Der Name der benutzerdefinierten Aggregatfunktion, die Sie löschen möchten.  
  
## <a name="remarks"></a>Remarks  
 DROP AGGREGATE wird nicht ausgeführt, wenn mit einer Schemabindung erstellte Sichten, Funktionen oder gespeicherte Prozeduren vorhanden sind, die auf die benutzerdefinierte Aggregatfunktion verweisen, die Sie löschen möchten.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen von DROP AGGREGATE benötigt der Benutzer mindestens die ALTER-Berechtigung für das Schema, zu dem das benutzerdefinierte Aggregat gehört, oder die CONTROL-Berechtigung für das Aggregat.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das `Concatenate`-Aggregat gelöscht.  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [Erstellen benutzerdefinierter Aggregate](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  
