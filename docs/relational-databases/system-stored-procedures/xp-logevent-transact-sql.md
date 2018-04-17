---
title: Xp_logevent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 18f3cf3516eee810aca57c4be2b2521df15c9b45
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="xplogevent-transact-sql"></a>xp_logevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Protokolliert eine benutzerdefinierte Nachricht in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Protokolldatei und in der Windows-Ereignisanzeige. Xp_logevent kann eine Warnung gesendet, ohne das Senden einer Nachricht an den Client verwendet werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>Argumente  
 *error_number*  
 Eine benutzerdefinierte Fehlernummer, die größer als 50.000 ist. Der Maximalwert ist 2147483647 (2^31 - 1).  
  
 **"** *Nachricht* **"**  
 Eine Zeichenfolge mit maximal 2048 Zeichen.  
  
 **"** *Schweregrad* **"**  
 Eine der drei folgenden Zeichenfolgen: INFORMATIONAL, WARNING oder ERROR. *Schweregrad* ist optional, Standardwert ist Informational.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 xp_logevent gibt für das Codebeispiel die folgende Fehlermeldung zurück:  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>Hinweise  
 Beim Senden von Nachrichten aus [!INCLUDE[tsql](../../includes/tsql-md.md)] Prozeduren, Trigger, Batches und So weiter, verwenden Sie die RAISERROR-Anweisung statt Xp_logevent. Xp_logevent nicht Nachrichtenhandler eines Clients oder set @@ERROR. Führen Sie die RAISERROR-Anweisung aus, um Nachrichten in die Windows-Ereignisanzeige und in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokolldatei in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu schreiben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle db_owner in der master-Datenbank oder Mitgliedschaft in der festen Serverrolle sysadmin.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Nachricht (mit den an sie übergebenen Variablen) in der Windows-Ereignisanzeige protokolliert.  
  
```  
DECLARE @@TABNAME varchar(30, @@USERNAME varchar(30),DECLARE @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte allgemeine erweiterte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
