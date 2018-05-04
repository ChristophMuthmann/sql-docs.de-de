---
title: Xp_sqlmaint (Transact-SQL) | Microsoft Docs
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
- xp_sqlmaint
- xp_sqlmaint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sqlmaint
ms.assetid: bda66e1b-6bbd-49be-b86e-37efc920e912
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c127d8cf7e27872d946a350c3e5d53e900145805
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xpsqlmaint-transact-sql"></a>xp_sqlmaint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft die **Sqlmaint** -Hilfsprogramm mit eine Zeichenfolge, enthält **Sqlmaint**Switches. Die **Sqlmaint** -Hilfsprogramm führt eine Reihe von Wartungsvorgänge für eine oder mehrere Datenbanken.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
xp_sqlmaint 'switch_string'     
```  
  
## <a name="arguments"></a>Argumente  
 **'** *switch_string* **'**  
 Eine Zeichenfolge, enthält die **Sqlmaint** Optionen des Hilfsprogramms. Die Optionen und ihre Werte müssen durch ein Leerzeichen getrennt werden.  
  
 Die **-?** Switch ist nicht gültig für **Xp_sqlmaint**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine. Gibt einen Fehler zurück, wenn die **Sqlmaint** Hilfsprogramm ein Fehler auftritt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn diese Prozedur von einem Benutzer, die mit SQL Server-Authentifizierung angemeldet aufgerufen, wird die **- U "***Anmelde-ID***"** und **-P "***Kennwort***"** Switches vorangestellt *Switch_string* vor der Ausführung. Wenn der Benutzer in Windows-Authentifizierung angemeldet ist, auf *Switch_string* übergeben wird, ohne Änderung **Sqlmaint**.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel ruft `xp_sqlmaint` das Hilfsprogramm `sqlmaint` auf, um Integritätsprüfungen auszuführen, eine Berichtsdatei zu erstellen und `msdb.dbo.sysdbmaintplan_history` zu aktualisieren.  
  
```  
EXEC xp_sqlmaint '-D AdventureWorks2012 -PlanID 02A52657-D546-11D1-9D8A-00A0C9054212   
   -Rpt "C:\Program Files\Microsoft SQL Server\MSSQL\LOG\DBMaintPlan2.txt" -WriteHistory  -CkDB -CkAl';   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The command(s) executed successfully.  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sqlmaint (Hilfsprogramm)](../../tools/sqlmaint-utility.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
