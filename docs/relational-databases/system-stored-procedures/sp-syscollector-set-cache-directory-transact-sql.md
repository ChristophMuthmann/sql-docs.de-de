---
title: Sp_syscollector_set_cache_directory (Transact-SQL) | Microsoft Docs
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
- sp_syscollector_set_cache_directory_TSQL
- sp_syscollector_set_cache_directory
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_cache_directory stored procedure
ms.assetid: df56d5a5-8961-494f-a745-d752ca63805a
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9cceecfcd2c738ad95c035a2d50b2e44c52ce692
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spsyscollectorsetcachedirectory-transact-sql"></a>sp_syscollector_set_cache_directory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt das Verzeichnis an, in dem die aufgelisteten Daten gespeichert werden, bevor sie in das Verwaltungs-Data Warehouse hochgeladen werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@cache_directory =** ] **'***cache_directory***'**  
 Das Verzeichnis im Dateisystem, in dem aufgelistete Daten vorübergehend gespeichert werden. *Cache_directory* ist **nvarchar(255)**, hat den Standardwert NULL. Wenn kein Wert angegeben ist, wird das temporäre Verzeichnis [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sie müssen den Datensammler deaktivieren, bevor Sie die Konfiguration für das Cacheverzeichnis ändern. Bei dieser gespeicherten Prozedur tritt ein Fehler auf, wenn der Datensammler aktiviert ist. Weitere Informationen finden Sie unter [aktivieren oder Deaktivieren der Datensammlung](../../relational-databases/data-collection/enable-or-disable-data-collection.md), und [Verwalten von Datensammlungen](../../relational-databases/data-collection/manage-data-collection.md).  
  
 Das angegebene Verzeichnis muss zum Zeitpunkt der Ausführung von sp_syscollector_set_cache_directory nicht vorhanden sein. Daten können jedoch erst erfolgreich zwischengespeichert und hochgeladen werden, wenn das Verzeichnis erstellt wurde. Sie sollten das Verzeichnis erstellen, bevor Sie diese gespeicherte Prozedur ausführen.  
  
## <a name="permissions"></a>Berechtigungen  
 Damit diese Prozedur ausgeführt werden kann, ist die Mitgliedschaft in der festen Datenbankrolle dc_admin (mit EXECUTE-Berechtigung) erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Datensammler deaktiviert, das Cacheverzeichnis für den Datensammler auf `D:\tempdata`, und der Datensammler anschließend aktiviert.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXEC dbo.sp_syscollector_set_cache_directory N'D:\tempdata';  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
