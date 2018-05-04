---
title: Sp_dropserver (Transact-SQL) | Microsoft Docs
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
- sp_dropserver_TSQL
- sp_dropserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropserver
ms.assetid: 0fc83e35-0caa-49a3-a4b6-a1890d4f46ef
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4d106722ed5777ca5ceb00c93c7c5edbc2a9f20d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdropserver-transact-sql"></a>sp_dropserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Entfernt einen Server aus der Liste der bekannten Remote- und Verbindungsserver auf der lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.  
  
[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@server =** ] **'***server***'**  
 Der Server, der entfernt werden soll. *server* ist vom Datentyp **sysname**und hat keinen Standardwert. *server* muss vorhanden sein.  
  
 [  **@droplogins =** ] **"Droplogins"** | NULL  
 Gibt an, dass die zugehörigen Remote- und Verbindungsserver-Anmeldenamen für *server* ebenfalls entfernt werden müssen, wenn **droplogins** angegeben wird. **@droplogins** ist **char(10)**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wird **sp_dropserver** auf einem Server ausgeführt, dem Einträge für Remote- und Verbindungsserver-Anmeldenamen zugeordnet sind oder der als Replikationsverleger konfiguriert ist, wird eine Fehlermeldung zurückgegeben. Verwenden Sie das **droplogins** -Argument, um beim Entfernen eines Servers alle Remote- und Verbindungsserver-Anmeldenamen für den Server zu entfernen.  
  
 **sp_dropserver** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert ALTER ANY LINKED SERVER-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel werden der Remoteserver `ACCOUNTS` und alle zugehörigen Remoteanmeldenamen von der lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz entfernt.  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Security Stored Procedures &#40;Transact-SQL&#41; (Gespeicherte Sicherheitsprozeduren (Transact-SQL))](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [Sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
