---
title: Sp_addextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs: TSQL
helpviewer_keywords: sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf0fa69b0704ba7ad3a4f433415298e3706d98bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spaddextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registriert den Namen einer neuen erweiterten gespeicherten Prozedur in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen die [CLR-Integration](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@functname =** ] **"***Prozedur***"**  
 Der Name der aufzurufenden Funktion innerhalb der DLL (Dynamic Link Library). *Prozedur* ist **nvarchar(517)**, hat keinen Standardwert. *Prozedur* optional den Namen des Besitzers im Format einschließen können *owner.function*.  
  
 [  **@dllname =** ] **"***Dll***"**  
 Der Name der DLL, die die Funktion enthält. *DLL* ist **varchar(255)**, hat keinen Standardwert. Es ist empfehlenswert, den vollständigen Pfad der DLL anzugeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Nachdem eine erweiterte gespeicherte Prozedur erstellt wurde, es muss hinzugefügt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit **Sp_addextendedproc**. Weitere Informationen finden Sie unter [Hinzufügen einer erweiterten gespeicherten Prozedur zu SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md).  
  
 Diese Prozedur kann nur in ausgeführt werden die **master** Datenbank. So führen Sie eine erweiterte gespeicherte Prozedur in einer Datenbank außer aus **master**, qualifizieren Sie den Namen der erweiterten gespeicherten Prozedur mit **master**.  
  
 **Sp_addextendedproc** Einträge hinzugefügt der [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) -Katalogsicht, registrieren den Namen der neuen erweiterten gespeicherten Prozedur mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es wird auch ein Eintrag in der [extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) -Katalogsicht angezeigt.  
  
> [!IMPORTANT]  
>  Vorhandene DLLs, die nicht mit einem vollständigen Pfad registriert wurden, sind nach dem Upgrade auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nicht mehr funktionsfähig. Verwenden Sie zum Beheben des Problems **Sp_dropextendedproc** zum Aufheben der Registrierung der DLL, und registrieren Sie ihn mit **Sp_addextendedproc**, Angabe des vollständigen Pfades.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_addextendedproc**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die **Xp_hello** der erweiterten gespeicherten Prozedur.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Sp_dropextendedproc &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [Sp_helpextendedproc &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
