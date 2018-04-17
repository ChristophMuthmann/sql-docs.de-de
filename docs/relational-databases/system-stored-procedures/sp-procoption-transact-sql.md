---
title: Sp_procoption (Transact-SQL) | Microsoft Docs
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
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49f2d1c4bf0e446b7c1577afbae138027a1a5745
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spprocoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Legt die automatische Ausführung einer gespeicherten Prozedur fest oder löscht diese. Eine gespeicherte Prozedur, die auf automatische Ausführung ausgeführt wird jedes Mal eine Instanz der Entitätenmenge wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@ProcName =** ] **"***Prozedur***"**  
 Ist der Name der Prozedur für die eine Option festgelegt. *Prozedur* ist **nvarchar(776)**, hat keinen Standardwert.  
  
 [  **@OptionName =** ] **"***Option***"**  
 Der Name der festzulegenden Option. Der einzige Wert für *Option* ist **Start**.  
  
 [  **@OptionValue =** ] **"***Wert***"**  
 Gibt an, ob die Option auf ON gesetzt (**"true"** oder **auf**) oder off (**"false"** oder **deaktiviert**). *Wert* ist **varchar(12)**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder eine Fehlernummer (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Autostartprozeduren muss der **master** Datenbank und darf keine Eingabe-oder Ausgabe enthalten. Die Ausführung der gespeicherten Prozeduren beginnt, wenn alle Datenbanken wiederhergestellt sind und beim Start die Meldung "Die Wiederherstellung ist abgeschlossen" protokolliert wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird für eine Prozedur die automatische Ausführung festgelegt.  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = ] 'startup'   
    , @OptionValue = 'on';   
```  
  
 Im folgenden Beispiel wird die automatische Ausführung einer Prozedur verhindert.  
  
```  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
