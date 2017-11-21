---
title: DROP PROCEDURE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP PROCEDURE
- DROP_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing stored procedures
- dropping procedure groups
- deleting stored procedures
- deleting procedure groups
- DROP PROCEDURE statement
- dropping stored procedures
- stored procedures [SQL Server], removing
- removing procedure groups
ms.assetid: 1c2d7235-7b9b-4336-8f17-429e7d82c2c3
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b386dfca28622eb95eec500d909aa7190d081493
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt eine oder mehrere gespeicherte Prozeduren oder Prozedurgruppen aus der aktuellen Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Bedingt löscht die Prozedur nur, wenn sie bereits vorhanden ist.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Prozedur gehört. Ein Servername oder Datenbankname kann nicht angegeben werden.  
  
 *Prozedur*  
 Der Name der gespeicherten Prozedur bzw. der gespeicherten Prozedurgruppe, die entfernt werden soll. Einzelne Prozeduren innerhalb einer nummerierten Prozedurgruppe können nicht gelöscht werden. Es wird die gesamte Prozedurgruppe gelöscht.  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Überprüfen Sie abhängige Objekte, und ändern Sie diese Objekte entsprechend, bevor Sie eine gespeicherte Prozedur löschen. Das Löschen einer gespeicherten Prozedur kann Fehler bei abhängigen Objekten und Skripts verursachen, wenn diese Objekte nicht aktualisiert werden. Weitere Informationen finden Sie unter [Anzeigen der Abhängigkeiten einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
## <a name="metadata"></a>Metadaten  
 Um eine Liste der vorhandenen Prozeduren anzuzeigen, Fragen Sie die **sys.objects** -Katalogsicht angezeigt. Um die Definition der Prozedur anzuzeigen, Fragen Sie die **sql_modules** -Katalogsicht angezeigt.  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert **Steuerelement** Berechtigung für die Prozedur oder **ALTER** -Berechtigung für das Schema, zu dem die Prozedur gehört, oder die Mitgliedschaft in der **Db_ddladmin** festen Serverrolle "" .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die gespeicherte Prozedur `dbo.uspMyProc` aus der aktuellen Datenbank entfernt.  
  
```  
DROP PROCEDURE dbo.uspMyProc;  
GO  
```  
  
 Im folgenden Beispiel werden mehrere gespeicherte Prozeduren aus der aktuellen Datenbank entfernt.  
  
```  
DROP PROCEDURE dbo.uspGetSalesbyMonth, dbo.uspUpdateSalesQuotes, dbo.uspGetSalesByYear;  
```  
  
 Im folgenden Beispiel wird die `dbo.uspMyProc` gespeicherte Prozedur aus, wenn er vorhanden ist, aber bewirkt keinen Fehler aus, wenn die Prozedur nicht vorhanden ist. Diese Syntax ist neu in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Löschen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  



