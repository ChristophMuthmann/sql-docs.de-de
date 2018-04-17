---
title: Sp_can_tlog_be_applied (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_can_tlog_be_applied_TSQL
- sp_can_tlog_be_applied
dev_langs:
- TSQL
helpviewer_keywords:
- sp_can_tlog_be_applied
ms.assetid: 9c143b6c-27ac-4ab7-98d1-3b7b265f3963
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc1afae648ab14db8aca25b9730de2e5cb916f1f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spcantlogbeapplied-transact-sql"></a>sp_can_tlog_be_applied (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Überprüft, ob eine Sicherung des Transaktionsprotokolls kann, um angewendet werden eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank. **sp_can_tlog_be_applied** setzt voraus, dass sich die Datenbank im Wiederherstellungsstatus befindet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_can_tlog_be_applied [ @backup_file_name = ] 'backup_file_name'   
        , [ @database_name = ] 'database_name'   
        , [ @result = ] result OUTPUT  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@backup_file_name=** ] **"***Backup_file_name***"**  
 Der Name einer Sicherungsdatei. *backup_file_name* ist **nvarchar(128)**  
  
 [ **@database_name=** ] **'***database_name***'**  
 Der Name der Datenbank. *database_name* ist **sysname**  
  
 [  **@result=** ] *Ergebnis* **Ausgabe**  
 Gibt an, ob das Transaktionsprotokoll auf die Datenbank angewendet werden kann. *result* ist **bit**  
  
 1 = Das Protokoll kann angewendet werden.  
  
 0 = Das Protokoll kann nicht angewendet werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können **sp_can_tlog_be_applied**ausführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine lokale Variable, `@MyBitVar`, zum Speichern des Ergebnisses deklariert.  
  
```  
USE master;  
GO  
DECLARE @MyBitVar BIT;  
EXEC sp_can_tlog_be_applied  
     @backup_file_name =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\AdventureWorks2012.bak',  
     @database_name = N'AdventureWorks2012',  
     @result = @MyBitVar OUTPUT;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
