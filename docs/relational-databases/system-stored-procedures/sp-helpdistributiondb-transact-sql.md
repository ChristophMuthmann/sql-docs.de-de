---
title: Sp_helpdistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 040970c34e8154538135e355744746e3ee1e3cb6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Eigenschaften der angegebenen Verteilungsdatenbank zurück. Diese gespeicherte Prozedur wird auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@database=**] **"***Database_name***"**  
 Der Datenbankname, für den Eigenschaften zurückgegeben werden. *Database_name* ist **Sysname**, hat den Standardwert  **%**  für alle Datenbanken im Zusammenhang mit dem Verteiler bzw. auf dem der Benutzer über Berechtigungen verfügt.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name der Verteilungsdatenbank.|  
|**min_distretention**|**int**|Die Mindestbeibehaltungsdauer in Stunden, bevor Transaktionen gelöscht werden.|  
|**max_distretention**|**int**|Die Höchstbeibehaltungsdauer in Stunden, bevor Transaktionen gelöscht werden.|  
|**verlaufsbeibehaltung**|**int**|Die Anzahl von Stunden, für die der Verlauf erhalten bleibt.|  
|**history_cleanup_agent**|**sysname**|Der Name des Verlaufscleanup-Agents.|  
|**distribution_cleanup_agent**|**sysname**|Der Name des Verteilungscleanup-Agents.|  
|**status**|**int**|Nur interne Verwendung.|  
|**data_folder**|**nvarchar(255)**|Der Name des Verzeichnisses zum Speichern der Datenbankdateien.|  
|**data_file**|**nvarchar(255)**|Der Name der Datenbankdatei.|  
|**data_file_size**|**int**|Die Anfangsgröße der Datendatei in Megabyte.|  
|**log_folder**|**nvarchar(255)**|Der Name des Verzeichnisses für die Datenbankprotokolldatei.|  
|**Log_file**|**nvarchar(255)**|Der Name der Protokolldatei.|  
|**log_file_size**|**int**|Die Anfangsgröße der Protokolldatei in Megabyte.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpdistributiondb** wird für alle Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Mitglieder der **Db_owner** festen Datenbankrolle oder der **Replmonitor** Rolle in einer Verteilungsdatenbank und Benutzer in der veröffentlichungszugriffsliste einer Veröffentlichung mit der Verteilungsdatenbank können ausführen **Sp_helpdistributiondb** um dateibezogene Informationen zurückzugeben. Mitglieder der **öffentlichen** Rolle ausführen kann **Sp_helpdistributiondb** um nicht dateibezogene Daten für Verteilungsdatenbanken zurückzugeben, auf die sie Zugriff haben.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Sp_adddistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [Sp_changedistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [Sp_dropdistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
