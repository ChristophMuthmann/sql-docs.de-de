---
title: Sp_bindsession (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_bindsession
- sp_bindsession_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c426c9ecca2c67dd1892d3d09a800fd229291598
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spbindsession-transact-sql"></a>sp_bindsession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Bindet oder hebt die Bindung einer Sitzungs mit anderen Sitzungen in derselben Instanz von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Bei Sitzungsbindungen können zwei oder mehr Sitzungen an derselben Transaktion teilnehmen und freigegebene Sperren verwenden, bis eine ROLLBACK TRANSACTION- oder COMMIT TRANSACTION-Anweisung ausgegeben wird.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen Multiple Active Results Sets (MARS) oder verteilte Transaktionen. Weitere Informationen finden Sie unter [mithilfe von Multiple Active Result Sets &#40; MARS &#41; ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Bind_token* **"**  
 Wird das Token, das die Transaktion identifiziert ursprünglich über erzielt **Sp_getbindtoken** oder der Open Data Services **Srv_getbindtoken** Funktion. *Bind_token*ist **varchar(255)**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Zwei gebundene Sitzungen verwenden nur eine Transaktion und Sperren gemeinsam. Jede Sitzung behält ihre eigene Isolationsstufe. Das Festlegen einer neuen Isolationsstufe für eine Sitzung hat keine Auswirkungen auf die Isolationsstufe der anderen Sitzung. Jede Sitzung wird weiterhin über ihr Sicherheitskonto identifiziert und kann nur auf die Datenbankressourcen zugreifen, für die dem Konto Berechtigungen erteilt wurden.  
  
 **Sp_bindsession** ein Bindungstoken verwendet, um zwei oder mehr vorhandene Clientsitzungen zu binden. Diese Clientsitzungen müssen zu derselben Instanz vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] gehören, von der der Bindungstoken erhalten wurde. Eine Sitzung ist ein Client, der einen Befehl ausführt. Gebundene Datenbanksitzungen verwenden einen Transaktions- und Sperrbereich gemeinsam.  
  
 Ein von einer Instanz vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] ausgegebenes Bindungstoken kann nicht für eine Clientsitzung mit einer anderen Instanz verwendet werden, auch nicht bei DTC-Transaktionen. Ein Bindungstoken ist nur lokal innerhalb einer Instanz gültig und kann nicht auf mehreren Instanzen freigegeben werden. Um Clientsitzungen auf einer anderen Instanz binden der [!INCLUDE[ssDE](../../includes/ssde-md.md)], Sie müssen ein anderes Bindungstoken abrufen, indem Sie die Ausführung **Sp_getbindtoken**.  
  
 **Sp_bindsession** schlägt mit einem Fehler fehl, wenn er ein Token verwendet, die nicht aktiv ist.  
  
 Heben Sie die Bindung aus einer Sitzung, die entweder mit **Sp_bindsession** ohne *Bind_token* oder übergeben Sie NULL in *Bind_token*.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das angegebene Bindungstoken an die aktuelle Sitzung gebunden.  
  
> [!NOTE]  
>  Das Bindungstoken im Beispiel durch Ausführen abgerufen wurde **Sp_getbindtoken** vor der Ausführung **Sp_bindsession**.  
  
```  
USE master;  
GO  
EXEC sp_bindsession 'BP9---5---->KB?-V'<>1E:H-7U-]ANZ';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_getbindtoken &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [Srv_getbindtoken &#40; Erweiterte gespeicherte Prozedur API &#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
