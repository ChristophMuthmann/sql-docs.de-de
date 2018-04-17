---
title: Sp_cursorclose (Transact-SQL) | Microsoft Docs
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
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1053cf5b483f2bce87c103bd1ad44fee3bae0455
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Schließt den Cursor, hebt, sowie alle zugeordneten Ressourcen frei; d. h. es zur Unterstützung KEYSET oder STATIC verwendete temporäre Tabelle löscht **Cursor**. Sp_cursorclose wird aufgerufen, indem ID = 9 in einem tabular Data Stream (TDS)-Paket.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>Argumente  
 *Cursor*  
 Ist ein Cursor *behandeln* generierter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , und von der Prozedur Sp_cursoropen zurückgegeben. *Cursor* ist ein erforderlicher Parameter, der erfordert eine **Int** Eingabewert.  
  
> [!NOTE]  
>  Der Eingabewert -1 gilt für alle Cursor der aktuellen Verbindung.  
  
## <a name="remarks"></a>Hinweise  
 *Cursor* zurück Fehlermeldungen, wenn die Prozedur ausgeführt wurde, nachdem der Cursor geschlossen wurde, oder wenn ein ungültiges Handle angegeben wird.  
  
 Der RPC-Status gibt an, ob der Vorgang erfolgreich oder fehlerhaft war.  
  
 Die DONE-Zeilenanzahl beträgt immer 0.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
