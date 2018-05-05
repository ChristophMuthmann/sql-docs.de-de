---
title: Sp_wait_for_database_copy_sync (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d63cae17ccc9541a8f14b8dd6ebdd2bccf2817a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="active-geo-replication---spwaitfordatabasecopysync"></a>Aktive geografische Replikation - sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Diese Prozedur ist auf eine [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]-Beziehung zwischen einer primären und sekundären Datenbank beschränkt. Wenn **sp_wait_for_database_copy_sync** aufgerufen wird, wartet die Anwendung, bis alle Transaktionen, für die ein Commit ausgeführt wurde, repliziert und durch die aktive sekundäre Datenbank bestätigt wurden. Führen Sie **sp_wait_for_database_copy_sync** nur in der primären Datenbank aus.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @target_server =] 'Servername'  
 Der Name des SQL-Datenbankservers, der die aktive sekundäre Datenbank hostet. server_name ist vom Datentyp sysname und hat keinen Standardwert.  
  
 [ @target_database =] 'Database_name'  
 Der Name der aktiven sekundären Datenbank. database_name ist vom Datentyp sysname und hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Gibt 0 für Erfolg oder eine Fehlernummer für Fehler zurück.  
  
 Die häufigsten Fehler sind:  
  
-   Der Servername oder der Datenbankname fehlt.  
  
-   Die Verbindung zum angegebenen Servernamen oder der angegebenen Serverdatenbank kann nicht gefunden werden.  
  
-   Interlink-Konnektivität ist unterbrochen. **sp_wait_for_database_copy_sync** wird nach dem Verbindungstimeout zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer in der primären Datenbank kann diese gespeicherte Systemprozedur aufrufen. Die Anmeldung muss einem Benutzer der primären und aktiven sekundären Datenbank entsprechen.  
  
## <a name="remarks"></a>Hinweise  
 Alle Transaktionen, für die vor einem Aufruf von **sp_wait_for_database_copy_sync** ein Commit ausgeführt wurde, werden an die aktive sekundäre Datenbank gesendet.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird **sp_wait_for_database_copy_sync** aufgerufen, um sicherzustellen, dass alle Transaktionen, für die ein Commit in der primären Datenbank db0 ausgeführt wurde, an die jeweilige aktive sekundäre Datenbank auf dem Zielserver ubfyu5ssyt gesendet werden.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. dm_continuous_copy_status &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [Geografische Replikation dynamische Verwaltungssichten und-Funktionen &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)  
  
  
