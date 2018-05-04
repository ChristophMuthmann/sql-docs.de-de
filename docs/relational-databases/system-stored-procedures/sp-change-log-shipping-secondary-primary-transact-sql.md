---
title: Sp_change_log_shipping_secondary_primary (Transact-SQL) | Microsoft Docs
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
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bd9a1c1cfcdc85443e0084fe0d7a4b173859bc8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spchangelogshippingsecondaryprimary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert Einstellungen sekundärer Datenbanken.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@primary_server** =] '*Primary_server*"  
 Der Name der primären Instanz von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in der Protokollversandkonfiguration. *primary_server* ist vom Datentyp **sysname** und darf nicht NULL sein.  
  
 [ **@primary_database** =] '*Primary_database*"  
 Der Name der Datenbank auf dem primären Server. *primary_database* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 [ **@backup_source_directory** =] '*Backup_source_directory*"  
 Das Verzeichnis, in dem die Dateien der Transaktionsprotokollsicherung gespeichert werden. *backup_source_directory* ist vom Datentyp **nvarchar(500)** und darf nicht NULL sein.  
  
 [ **@backup_destination_directory** =] '*Backup_destination_directory*"  
 Das Verzeichnis auf dem sekundären Server, in das Sicherungsdateien kopiert werden *backup_destination_directory* ist vom Datentyp **nvarchar(500)** und darf nicht NULL sein.  
  
 [ **@file_retention_period** =] '*File_retention_period*"  
 Der Zeitraum (in Minuten), für den der Verlauf beibehalten wird. *history_retention_period* ist vom Datentyp **int**. Der Standardwert ist NULL. Der Wert 14420 wird verwendet, falls kein anderer Wert angegeben wird.  
  
 [ **@monitor_server_security_mode** =] '*Monitor_server_security_mode*"  
 Der Sicherheitsmodus, der zum Herstellen einer Verbindung mit dem Überwachungsserver verwendet wird.  
  
 1 = Windows-Authentifizierung;  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. *monitor_server_security_mode* ist vom Datentyp **bit** und darf nicht NULL sein.  
  
 [ **@monitor_server_login** =] '*Monitor_server_login*"  
 Der Benutzername für das Konto, das zum Zugreifen auf den Überwachungsserver verwendet wird.  
  
 [ **@monitor_server_password** =] '*Monitor_server_password*"  
 Das Kennwort des Kontos, das zum Zugreifen auf den Überwachungsserver verwendet wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **sp_change_log_shipping_secondary_primary** muss von der **master** -Datenbank aus auf dem sekundären Server ausgeführt werden. Diese gespeicherte Prozedur führt folgende Aktionen aus:  
  
1.  Änderung von Einstellungen in den **log_shipping_secondary** -Datensätzen, sofern dies notwendig ist.  
  
2.  Sofern notwendig, eine Änderung des Überwachungsdatensatzes in **log_shipping_monitor_secondary** auf dem Überwachungsserver mithilfe angegebener Parameter, falls der Überwachungsserver nicht mit dem sekundären Server identisch ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
