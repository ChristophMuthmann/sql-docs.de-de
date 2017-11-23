---
title: Sp_delete_targetserver (Transact-SQL) | Microsoft Docs
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
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9fbe2a49724fd45ac8c635fc758323b5d34b8eb9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spdeletetargetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt den angegebenen Server aus der Liste der verfügbaren Zielserver.  
   
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@server_name=** ] **"***Server***"**  
 Der Name des Servers, der als verfügbarer Zielserver entfernt werden soll. *Server* ist **nvarchar(30)**, hat keinen Standardwert.  
  
 [  **@clear_downloadlist=** ] *Clear_downloadlist*  
 Gibt an, ob die Downloadliste für den Zielserver gelöscht werden soll. *Clear_downloadlist* Typ **Bit**, hat den Standardwert **1**. Wenn *Clear_downloadlist* ist **1**, die Prozedur löscht die Downloadliste für den Server, bevor der Server gelöscht. Wenn *Clear_downloadlist* ist **0**, die Downloadliste nicht deaktiviert ist.  
  
 [  **@post_defection=** ] *Post_defection*  
 Gibt an, ob eine Austrittsanweisung auf dem Zielserver bereitgestellt werden soll. *Post_defection* Typ **Bit**, hat den Standardwert 1. Wenn *Post_defection* ist **1**, die Prozedur sendet eine austrittsanweisung auf dem Zielserver sein, bevor der Server gelöscht. Wenn *Post_defection* ist **0**, bucht die Prozedur eine austrittsanweisung auf dem Zielserver nicht.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Die normale Methode zum Löschen eines Zielservers ist das Aufrufen **Sp_msx_defect** auf dem Zielserver. Verwendung **Sp_delete_targetserver** nur ab, wenn ein manueller Austritt erforderlich ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Um diese gespeicherte Prozedur auszuführen, müssen Benutzer gewährt werden die **Sysadmin** festen Serverrolle "".  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Server `LONDON1` aus der Liste der verfügbaren Auftragsserver entfernt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_help_targetserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [Sp_msx_defect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
