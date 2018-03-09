---
title: Sp_ivindexhasnullcols (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dbdbe2a627eb49dbd2ab71bef5bc102f1b157d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Überprüft, ob der gruppierte Index der indizierten Sicht eindeutig ist und keine Spalten enthält, die NULL-Werte zulassen, wenn die indizierte Sicht verwendet wird, um eine Transaktionsveröffentlichung zu erstellen. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@viewname** =] **"***View_name***"**  
 Der Name der Sicht, die überprüft werden soll. *View_name* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@fhasnullcols** =] *Field_has_null_columns* Ausgabe  
 Das Flag, das angibt, ob der Sichtindex Spalten enthält, die NULL zulassen. *View_name* ist **Sysname**, hat keinen Standardwert. Gibt einen Wert von **1** , wenn der Sichtindex über Spalten verfügt, die NULL zulassen. Gibt einen Wert von **0** , wenn die Sicht keine Spalten enthält, die NULL-Werte zulassen.  
  
> [!NOTE]  
>  Wenn die gespeicherte Prozedur selbst einen Rückgabecode von zurückgibt **1**, d. h. die Ausführung der gespeicherten Prozedur einen Fehler aufgetreten ist, dieser Wert ist **0** und sollte ignoriert werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_ivindexhasnullcols** wird von der Transaktionsreplikation verwendet.  
  
 Standardmäßig werden Artikel für indizierte Sichten in einer Veröffentlichung als Tabellen bei den Abonnenten erstellt. Wenn die indizierte Spalte jedoch NULL-Werte zulässt, wird die indizierte Sicht auf dem Abonnenten als indizierte Sicht erstellt und nicht als Tabelle. Durch die Ausführung dieser gespeicherten Prozedur kann der Benutzer gewarnt werden, wenn dieses Problem mit der aktuellen indizierten Sicht besteht.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_ivindexhasnullcols**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
