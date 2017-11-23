---
title: Sp_resync_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- sp_resync_targetserver
- sp_resync_targetserver_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_resync_targetserver
ms.assetid: 40e44df7-d3e3-44ee-b149-08aba629a21f
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 893b053fc258eda26db679530a2a6c67f4fbc27b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spresynctargetserver-transact-sql"></a>sp_resync_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Synchronisiert alle Multiserveraufträge auf dem angegebenen Zielserver neu.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_resync_targetserver  
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@server_name =**] **"***Server***"**  
 Der Name des erneut zu synchronisierenden Serverobjekts. *server* ist vom Datentyp **sysname**und hat keinen Standardwert. Mit **ALL** werden alle Zielserver neu synchronisiert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Meldet das Ergebnis von **sp_post_msx_operation** -Aktionen.  
  
## <a name="remarks"></a>Hinweise  
 **sp_resync_targetserver** löscht die aktuellen Anweisungen für den Zielserver und stellt neue Anweisungen für den Zielserver zum Herunterladen bereit. Die neuen Anweisungen bestehen aus einer Anweisung zum Löschen aller Multiserveraufträge, gefolgt von einem Eintrag für jeden Auftrag, der an diesen Server gerichtet ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig verfügen Mitglieder der festen Serverrolle **sysadmin** über die Berechtigungen zum Ausführen dieser Prozedur.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Zielserver `SEATTLE1` neu synchronisiert.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_resync_targetserver  
    N'SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_help_downloadlist &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)   
 [Sp_post_msx_operation &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
