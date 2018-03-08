---
title: Sp_syscollector_set_warehouse_database_name (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_warehouse_database_name
- sp_syscollector_set_warehouse_database_name_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_set_warehouse_database_name
- data collector [SQL Server], stored procedures
ms.assetid: a85aca1b-8135-4c81-9a05-da5aec76f1ed
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e82f8bd3d88cfb2e12ef9fb7c5d6fadb287ca10d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spsyscollectorsetwarehousedatabasename-transact-sql"></a>sp_syscollector_set_warehouse_database_name (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den in der Verbindungszeichenfolge definierten Datenbanknamen an, mit dem die Verbindung zum Verwaltungs-Data Warehouse hergestellt wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_set_warehouse_database_name [ @database_name = ] 'database_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @database_name = ] '*database_name*'  
 Ist der Name des Verwaltungs-Datawarehouse. *Database_name* ist **Sysname** hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie müssen den Datensammler deaktivieren, bevor Sie die Konfiguration für den gesamten Datensammler ändern. Dieser Vorgang schlägt fehl, wenn der Datensammler aktiviert ist.  
  
 Um den aktuellen Datenbanknamen anzuzeigen, Fragen Sie die [Syscollector_config_store](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md) -Systemsicht.  
  
## <a name="permissions"></a>Berechtigungen  
 Damit diese Prozedur ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle dc_admin (mit EXECUTE-Berechtigung) erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Name des Verwaltungs-Data Warehouse auf `RemoteMDW` festgelegt.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_set_warehouse_database_name N'RemoteMDW';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
