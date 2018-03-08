---
title: sp_rda_reconcile_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac447329552758ad6070cf4a22489c9d1ed44e64
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="syssprdareconcilecolumns-transact-sql"></a>sys.sp_rda_reconcile_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gleicht die Spalten in der Azure-Remotetabelle den Spalten in der Stretch-aktivierten SQL Server-Tabelle.  
    
  **Sp_rda_reconcile_columns** fügt Spalten hinzu, an die Remotetabelle, die in der Stretch-aktivierten SQL Server-Tabelle jedoch nicht in der Remotetabelle vorhanden sind. Diese Spalten sind möglicherweise Spalten, die Sie versehentlich aus der Remotetabelle gelöscht. Allerdings **Sp_rda_reconcile_columns** löscht keine Spalten aus der Remotetabelle, die in der Remotetabelle, aber nicht in der SQL Server-Tabelle vorhanden sind.
  
  > [!IMPORTANT]
  > Wenn **sp_rda_reconcile_columns** Spalten neu erstellt, die Sie versehentlich aus der Remotetabelle gelöscht haben, dann werden nicht die zuvor in den gelöschten Spalten enthaltenen Daten wiederhergestellt.
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>Syntax  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>Argumente  
 @objname = '*@objname*'  
 Der Name der SQL Server Stretch-aktivierte Tabelle.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder >0 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert Db_owner-Berechtigungen.  
   
## <a name="remarks"></a>Hinweise  
 Wenn Spalten in der Azure-Remotetabelle enthalten sind, die in der Stretch-aktivierten SQL Server-Tabelle nicht mehr vorhanden sind, dann verhindern diese zusätzlichen Spalten nicht, dass Stretch Database ordnungsgemäß arbeitet. Sie können die zusätzlichen Spalten optional manuell entfernen.  
  
## <a name="example"></a>Beispiel  
 Abstimmen der Spalten in der Azure-Remotetabelle, führen Sie die folgende Anweisung.  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
